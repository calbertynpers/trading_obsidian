# [binance-position-tools] Reduce `get_income_history` payload size

**Type:** Enhancement
**Priority:** Medium
**Component:** `binance-position-tools` MCP server
**Tool:** `get_income_history`
**Created:** 2026-04-22

---

## Summary

The `get_income_history` tool returns the full raw record set grouped by symbol. For a 24h unfiltered call this currently returns ~300KB (~900 records across ~90 symbols), which overflows LLM context windows and inflates token usage significantly. Add response-shaping parameters so callers can get what they need without the full dump.

## Problem

Observed behaviour on `get_income_history(hours=24)` with no filters:

- **904 records** returned, grouped by symbol
- **~298KB** response size
- Breakdown: 468 `FUNDING_FEE` + 245 `COMMISSION` + 191 `REALIZED_PNL`
- Only **4 symbols** had realized PnL activity (closed round-trips) — the signal
- **86 symbols** had only funding accrual on open positions — mostly near-zero noise from an analysis perspective

The useful information for PnL review is concentrated in:
- The `summary` block (~1KB)
- The `REALIZED_PNL` records (~20% of records)
- The `round_trip_symbols` list

The remaining ~80% of the payload (funding dust on open positions, per-record commission detail) is rarely needed for the default use case and forces token-expensive offloading to file storage.

## Proposed changes

Add the following optional parameters to `get_income_history`:

### 1. `summary_only: bool = False`
When `True`, return only the `summary` block and `round_trip_symbols` list. Omit `records_by_symbol` entirely. Expected payload reduction: ~95%+.

### 2. `top_n_per_symbol: int | None = None`
When set, cap the number of records returned per symbol (most recent first). Useful for symbols like `NAORISUSDT` that had 125 fills in 24h.

### 3. `min_abs_amount: float | None = None`
When set, exclude records with `abs(amount) < min_abs_amount`. Filters funding dust (e.g. values like `0.00013924 BNFCR`) without losing meaningful entries.

### 4. `exclude_open_positions: bool = False`
When `True`, exclude symbols that have no `REALIZED_PNL` records in the window (i.e. open positions accruing only funding). Focuses the response on actually-closed trading activity.

## Proposed default behaviour change

Consider making `summary_only=True` the default, with an `include_records=True` opt-in. The summary + round-trip list answers most "how did I do today" questions without the raw record dump. This is a **breaking change** — flag accordingly if adopted.

## Acceptance criteria

- [ ] All four new parameters accepted and documented in the tool schema
- [ ] `summary_only=True` response is under 5KB for a 24h unfiltered call with typical activity
- [ ] `top_n_per_symbol=10` correctly returns the 10 most recent records per symbol
- [ ] Existing callers (no new params) see identical behaviour — backward compatible
- [ ] Parameter combinations work (e.g. `income_type="REALIZED_PNL"` + `exclude_open_positions=True`)

## Workarounds until shipped

Callers can approximate this today by:
- Always passing `income_type="REALIZED_PNL"` (cuts ~80% of records)
- Scoping to specific `symbol` once target symbols are known from a broader scan
- Keeping `hours` as tight as the analysis requires

## References

- Discovered during 24h PnL review session, 2026-04-22
- Related: may want to apply similar shaping to `get_order_history` if it exhibits the same payload bloat on high-fill symbols
