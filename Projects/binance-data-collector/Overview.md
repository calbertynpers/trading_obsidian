# Binance Data Collector — Service Overview

> **For agents building against this service.** This document describes the architecture, MCP tools, data model, and integration patterns for the Binance Data Collector. If you're building a service that consumes market data or manages positions on Binance Futures, start here.

---

## What It Is

The Binance Data Collector is a standalone Python project that serves as the market data backbone and position management layer for the FTP trading system. It replaces the defunct Orion Terminal REST API. The project lives at `~/binance_data_service/` and exposes two independently-runnable MCP servers:

1. **Data Collector MCP** (`binance-data-collector`) — read-only market data: snapshots, history, metrics
2. **Position Tools MCP** (`binance-position-tools`) — authenticated position management: orders, positions, income, funding

Both servers communicate through a shared SQLite database (`data/market_data.db`) in WAL mode.

---

## Architecture

```
┌─────────────────────────────────────────────────────────┐
│                   Binance Public API                     │
│  /fapi/v1/ticker/24hr    /fapi/v1/premiumIndex          │
└──────────────┬──────────────────────┬───────────────────┘
               │                      │
       ┌───────▼──────────────────────▼───────┐
       │        Collector Service              │
       │  (polls every 60s, writes to SQLite)  │
       │  python -m binance_data_collector     │
       └───────────────┬──────────────────────┘
                       │ writes
               ┌───────▼───────┐
               │  SQLite (WAL) │
               │ market_data.db│
               └───┬───────┬───┘
            reads  │       │  reads
       ┌───────────▼─┐ ┌──▼──────────────┐
       │ Data MCP     │ │ Position MCP     │
       │ (read-only)  │ │ (authenticated)  │
       │ get_snapshot  │ │ get_positions    │
       │ get_history   │ │ get_open_orders  │
       │ get_metrics   │ │ place_*_order    │
       │ collector_    │ │ get_order_history│
       │   status      │ │ get_income_      │
       └──────┬────────┘ │   history        │
              │           │ get_funding_info │
              │           └────────┬─────────┘
              │                    │
       ┌──────▼────────────────────▼──────┐
       │         Claude / Kiro / TIS       │
       │        (MCP tool consumers)       │
       └──────────────────────────────────┘
```

---

## Two MCP Servers

### 1. Data Collector MCP (`binance-data-collector`)

**Purpose:** Read-only market data queries against the SQLite database.

**Process:** `python -m binance_data_collector.mcp_server`

**Tools:**

| Tool | Parameters | Returns |
|------|-----------|---------|
| `get_snapshot` | `symbols: list[str] \| None` | Latest price, volume, funding rate, mark price per symbol. None = all tracked symbols. |
| `get_history` | `symbol: str`, `hours: int = 24` | Time-series snapshot rows for a symbol within the time window. |
| `get_metrics` | `symbol: str`, `windows: list[int] \| None` | Computed metrics: price velocity, volume spike, funding trend, relative strength vs BTC, momentum score. Default windows: [5, 15, 60] minutes. |
| `collector_status` | — | Last update time, symbol count, history row count, DB size, data age. |
| `add_to_watchlist` | `symbols: list[str]`, `added_by: str = "mcp_client"` | **(BDS-019, pending)** Dynamically add symbols to the collector's tracked set at runtime. |

**Data source:** The Collector Service polls two Binance public endpoints every 60 seconds:
- `GET /fapi/v1/ticker/24hr` — price, volume, 24h change
- `GET /fapi/v1/premiumIndex` — mark price, funding rate, next funding time

Data is merged by symbol, filtered to the watchlist, and written to SQLite.

**Watchlist:** Configured in `config/collector_config.yml`. Empty = track all Binance Futures pairs. BDS-019 will add runtime mutation via `add_to_watchlist`.

### 2. Position Tools MCP (`binance-position-tools`)

**Purpose:** Authenticated Binance Futures account operations — positions, orders, income, funding.

**Process:** `python -m binance_data_collector.position_mcp_server`

**Requires:** `BINANCE_API_KEY` and `BINANCE_SECRET_KEY` environment variables.

**Read Tools** (with retry — safe for auto-approval):

| Tool | Parameters | Returns |
|------|-----------|---------|
| `get_positions` | — | All active positions with PnL, margin, leverage, liquidation risk, recommendations. |
| `get_trading_readiness` | — | Available margin, utilization %, position count, can-open-new flag. |
| `get_open_orders` | `symbol: str \| None` | Open orders (standard + algo/conditional) grouped by symbol with summary. |
| `get_order_history` | `symbol: str`, `hours: int = 24`, `status: str \| None` | Historical orders (filled, cancelled, expired) merging standard + algo endpoints. |
| `get_income_history` | `symbol: str \| None`, `hours: int = 24`, `income_type: str \| None` | Realized PnL, commissions, funding fees across all symbols. Round-trip trade detection. |
| `get_funding_info` | `symbols: list[str] \| None`, `include_open_interest: bool = True`, `include_history: bool = False` | **(BDS-014, pending)** Live funding rates, OI, historical settlements. Defaults to active position symbols. |

**Write Tools** (no retry — require confirmation):

| Tool | Parameters | Notes |
|------|-----------|-------|
| `place_market_order` | symbol, side, quantity, position_side | Immediate execution |
| `place_limit_order` | symbol, price, side, position_side, leverage, margin | Auto-calculates quantity from margin × leverage |
| `place_stop_order` | symbol, side, stop_price, quantity, position_side | STOP_MARKET via algo endpoint |
| `place_take_profit_order` | symbol, side, tp_price, quantity, position_side | TAKE_PROFIT_MARKET via algo endpoint |
| `cancel_order` | symbol, order_id | Tries standard then algo cancel |
| `cancel_all_orders` | symbol | Cancels standard + algo orders |
| `close_position` | symbol, position_side | Market close of full position |
| `set_leverage` | symbol, leverage | Changes leverage for a symbol |

---

## SQLite Database Schema

**File:** `data/market_data.db` (WAL mode for concurrent reads)

```sql
-- Current state: one row per symbol
CREATE TABLE latest_snapshots (
    symbol TEXT PRIMARY KEY,
    last_price REAL, price_change_pct_24h REAL,
    high_24h REAL, low_24h REAL,
    quote_volume_24h REAL, num_trades_24h INTEGER,
    mark_price REAL, funding_rate REAL, next_funding_time INTEGER,
    collected_at TEXT  -- ISO 8601 UTC
);

-- Time series: one row per symbol per poll cycle
CREATE TABLE snapshot_history (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    symbol TEXT, last_price REAL, price_change_pct_24h REAL,
    high_24h REAL, low_24h REAL,
    quote_volume_24h REAL, num_trades_24h INTEGER,
    mark_price REAL, funding_rate REAL, next_funding_time INTEGER,
    collected_at TEXT
);
CREATE INDEX idx_history_symbol_time ON snapshot_history (symbol, collected_at);

-- BDS-019 (pending): runtime watchlist additions
CREATE TABLE dynamic_watchlist (
    symbol TEXT PRIMARY KEY,
    added_at TEXT NOT NULL,
    added_by TEXT NOT NULL
);
```

---

## Key Integration Patterns

### For services that need market data (e.g., TIS)

1. Call `get_snapshot()` to get current prices for tracked symbols
2. If your symbol isn't tracked, call `add_to_watchlist(["XYZUSDT"])` first (BDS-019)
3. Call `get_history(symbol, hours)` for time-series analysis
4. Call `get_metrics(symbol)` for computed indicators (velocity, volume spike, momentum)

### For services that need position context

1. Call `get_positions()` for current portfolio state
2. Call `get_open_orders(symbol)` to see pending orders
3. Call `get_income_history(hours=24)` for daily P&L summary
4. Call `get_funding_info()` (BDS-014) for funding rate analysis across positions

### For services that execute trades

1. Call `get_trading_readiness()` to check margin availability
2. Call `place_limit_order(...)` or `place_market_order(...)` to execute
3. Call `place_stop_order(...)` and `place_take_profit_order(...)` for risk management
4. Call `get_order_history(symbol, hours=1)` to verify execution

---

## Configuration

**Collector config:** `config/collector_config.yml`

```yaml
watchlist:
  - BTCUSDT
  - ETHUSDT
  # empty = track all Binance Futures pairs

poll_interval_seconds: 60
retention_hours: 168        # 7 days of history
database_path: "data/market_data.db"
binance_base_url: "https://fapi.binance.com"
request_timeout_seconds: 10
```

**Position tools config:** Environment variables only

```
BINANCE_API_KEY=...
BINANCE_SECRET_KEY=...
BINANCE_TESTNET=false       # optional
BINANCE_MAX_POSITIONS=10    # optional constraint overrides
```

---

## Tech Stack

- **Python 3.14**
- **httpx** — async HTTP client for Binance public API
- **binance-futures-connector** — official Binance SDK for authenticated endpoints
- **aiosqlite** — async SQLite access
- **pydantic** — config validation and data models
- **mcp[cli]** — FastMCP server framework
- **tenacity** — retry logic for authenticated API calls
- **hypothesis** — property-based testing

---

## Ticket Tracker

All tickets use the **BDS** prefix and live in `Tickets/binance-position-tools/`. See [[Ticket Index]] for the full list.

**Completed:** BDS-001 through BDS-005, BDS-008, BDS-009
**In progress / specced:** BDS-013 (payload reduction), BDS-014 (funding & OI), BDS-019 (add-to-watchlist)
**Open:** BDS-006 (trailing stop), BDS-007 (modify order), BDS-010 (balance history), BDS-011 (dead man's switch), BDS-012 (batch orders), BDS-015 (dynamic watchlist sync), BDS-016 (funding cost sign fix)

---

## Related

- [[TIS-001]] — Trigger Ingestion System (primary consumer of `get_snapshot` and `add_to_watchlist`)
- [[Ticket Index]] — Full ticket tracker across all services
