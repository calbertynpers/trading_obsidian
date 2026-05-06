# Ticket Index

Central tracker for all service tickets. Agents should check this before starting work and update status when tickets are resolved.

## Status Legend

| Status | Meaning |
|--------|---------|
| 🔴 Open | Not started |
| 🟡 In Progress | Being worked on |
| 🟢 Done | Implemented and verified |
| ⚪ Blocked | Waiting on dependency |

---

## Binance Position Tools (`position_mcp_server`)

| Ticket | Title | Priority | Status | Depends On |
|--------|-------|----------|--------|------------|
| [[BDS-001]] | Fix limit order price + stop order endpoint | High | 🟢 Done | — |
| [[BDS-002]] | Add take-profit order tool | High | 🟢 Done | BDS-001 |
| [[BDS-003]] | Add get open orders tool | High | 🟢 Done | — |
| [[BDS-004]] | Include algo/conditional orders in get_open_orders | High | 🟢 Done | BDS-001, BDS-003 |
| [[BDS-005]] | Cancel algo/conditional orders | High | 🟢 Done | BDS-001, BDS-004 |
| [[BDS-006]] | Add trailing stop order tool | High | 🔴 Open | BDS-001 |
| [[BDS-007]] | Add modify/amend order tool | High | 🔴 Open | — |
| [[BDS-008]] | Add order history tool | High | 🟢 Done | — |
| [[BDS-009]] | Add income history tool (cross-symbol P&L, funding, commissions) | High | 🟢 Done | — |
| [[BDS-010]] | Add account balance history tool | High | 🔴 Open | — |
| [[BDS-011]] | Add countdown cancel-all (dead man's switch) | Medium | 🔴 Open | — |
| [[BDS-012]] | Add batch orders tool | Medium | 🔴 Open | — |
| [[BDS-013]] | Reduce get_income_history payload size | Medium | 🔴 Open | BDS-009 |
| [[BDS-014]] | Add funding rate & open interest snapshot tool | High | 🔴 Open | — |
| [[BDS-015]] | Dynamic watchlist sync from active positions | Medium | 🔴 Open | — |
| [[BDS-016]] | Fix estimated_8h_funding_cost sign for SHORT positions | Medium | 🔴 Open | BDS-014 |
| ~~[[BDS-017]]~~ | ~~Trigger ingestion system~~ → Moved to [[TIS-001]] | — | — | — |
| [[BDS-018]] | MySQL migration for trigger ingestion system | Low | 🔴 Open | TIS-006 |
| [[BDS-019]] | Add-to-watchlist MCP tool for data collector | Medium | 🟢 Done | — |
| [[BDS-020]] | PostgreSQL database adapter (asyncpg migration) | High | 🔴 Open | — |

---

## Trigger Ingestion System (`trigger_ingestion_system`)

| Ticket | Title | Priority | Status | Depends On |
|--------|-------|----------|--------|------------|
| [[TIS-001]] | Master spec — trigger ingestion system architecture | High | 🟡 In Progress | — |
| [[TIS-002]] | Core pipeline (schemas, config, price fetcher, conditions) | High | 🟢 Done | BDS-019 ✅ |
| [[TIS-003]] | External triggers + enrichment (webhooks, BDS) | High | 🟢 Done | TIS-002 ✅ |
| [[TIS-004]] | SQS publisher — generic event publishing client | High | 🔴 Open | TIS-003 ✅, ADF-008 |
| [[TIS-005]] | Agent integration — Bedrock Claude for event evaluation (Phase 2) | High | 🔴 Open | TIS-011, ADF-009, ADF-011 |
| [[TIS-006]] | Confirmation handler + agent execution (Phase 2) | High | 🔴 Open | TIS-005, ADF-009 |
| [[TIS-007]] | Pine Script alert integration — chart-driven trigger source | Medium | 🔴 Open | TIS-004 |
| [[TIS-008]] | Telegram synchronous wait-for-reply tool | Medium | 🔴 Open | TMS-005 |
| [[TIS-009]] | Price monitor producer — independent source process | High | 🔴 Open | TIS-004 |
| [[TIS-010]] | Webhook receiver producer — independent source process | High | 🔴 Open | TIS-004 |
| [[TIS-011]] | Lambda event consumer — notification service (Phase 1) | High | 🔴 Open | TIS-004, ADF-008, TMS-005 |

### Execution Order (Phase 1 — End-to-End Notifications)

```
TIS-004 (SQS publisher)
    ├── TIS-009 (price monitor producer) ──┐
    ├── TIS-010 (webhook receiver producer)│── TIS-011 (Lambda consumer) → Telegram
    └── (future sources)───────────────────┘
```

**Minimum viable chain**: TIS-004 → TIS-009 → TIS-011 = trigger fires → Telegram notification

1. **TIS-004** — SQS publisher (generic client + config extension). No external deps beyond ADF-008.
2. **TIS-009** — Price monitor producer. First source to complete the chain.
3. **TIS-011** — Lambda event consumer. Reads from SQS, sends Telegram notifications.
4. **TIS-010** — Webhook receiver producer. Second source (can come later).

**Phase 2 — Agent Evaluation:**
5. **TIS-005** — Upgrade Lambda consumer to invoke Bedrock Claude.
6. **TIS-006** — Confirmation handler + agent execution.

**Infrastructure (parallel):**
- **ADF-008** — SQS queues (needed by TIS-004)
- **TMS-005** — Telegram client refactor (needed by TIS-011)
- **ADF-009** — Lambda + DynamoDB + API Gateway (needed by TIS-005/006)
- **ADF-011** — EFS One Zone (needed by TIS-005)
- **ADF-012** — Deploy source processes to EC2 (production)

---

## Telegram MCP Server (`telegram-mcp-server`)

| Ticket | Title | Priority | Status | Depends On |
|--------|-------|----------|--------|------------|
| [[TMS-001]] | Initial implementation — Telegram MCP server | High | 🟢 Done | — |
| [[TMS-002]] | Reply poller + agent responder | Medium | 🔴 Open | TMS-001 |
| [[TMS-003]] | Document macOS hidden-flag workaround for Python 3.14 + uv venvs | Medium | 🟢 Done | — |
| [[TMS-004]] | Self-healing launcher script for MCP server cold starts | Medium | 🟢 Done | TMS-003 |
| [[TMS-005]] | Refactor into service client + MCP wrapper | High | 🔴 Open | TMS-001 ✅ |

---

## Alpha Scanner (`alpha_scanner`)

| Ticket | Title | Priority | Status | Depends On |
|--------|-------|----------|--------|------------|
| [[ALS-001]] | Alpha Scanner — placeholder | Medium | 🔴 Open | TIS-009 |

---

## Idea Discovery Service (`idea_discovery_service`)

| Ticket | Title | Priority | Status | Depends On |
|--------|-------|----------|--------|------------|
| [[IDS-001]] | TradingView community ideas — access research spike | Medium | 🔴 Open | TIS-004 |
| [[IDS-002]] | Pine Script generation POC — chart drawing + alert pipeline demo | Medium | 🟢 Done | TIS-003 (soft) |
| [[IDS-003]] | RSI Extreme Scanner | Medium | 🔴 Open | IDS-004, IDS-005 |
| [[IDS-004]] | Marimo Setup Notebook Generator | High | 🔴 Open | IDS-002, IDS-005 |
| [[IDS-005]] | Live MCP Data Provider for Pine Generator | High | 🟡 In Progress | IDS-002 |

---

## AWS Deployment Framework (`aws-deployment-framework`)

| Ticket | Title | Priority | Status | Depends On |
|--------|-------|----------|--------|------------|
| [[ADF-001]] | Import SSH key pair to AWS | High | 🟢 Done | — |
| [[ADF-002]] | Provision and harden EC2 instance | High | 🟢 Done | ADF-001 |
| [[ADF-003]] | Store Binance API credentials in Secrets Manager | High | 🟢 Done | ADF-002 |
| [[ADF-004]] | Provision RDS PostgreSQL | High | 🟢 Done | ADF-002 |
| [[ADF-005]] | Deploy Binance Data Collector to EC2 | High | 🔴 Open | ADF-002, ADF-003, ADF-004, BDS-020 |
| [[ADF-006]] | CI/CD pipeline (CodeBuild + CodeDeploy) | Medium | 🔴 Open | ADF-005 |
| [[ADF-007]] | Position monitoring dashboard hosting | Medium | 🔴 Open | ADF-004, ADF-005 |
| [[ADF-008]] | SQS queues for Trigger Ingestion System | High | 🔴 Open | ADF-002 ✅ |
| [[ADF-009]] | Lambda + DynamoDB + API Gateway for TIS agent layer | High | 🔴 Open | ADF-008 |
| [[ADF-010]] | POC — FastAPI on ECS Fargate with API Gateway | Medium | 🔴 Open | ADF-002 ✅ |
| [[ADF-011]] | EFS One Zone for Trading Knowledge Base (shared vault) | High | 🔴 Open | ADF-002 ✅ |
| [[ADF-012]] | Deploy TIS source processes to EC2 | High | 🔴 Open | ADF-005, ADF-008, TIS-009 |

### Execution Order
1. ~~**ADF-001–004**~~ — ✅ Done.
2. **ADF-005** — Deploy BDS to EC2. Blocked on BDS-020.
3. **ADF-008** — SQS queues. Unblocked. Can start now.
4. **ADF-011** — EFS One Zone. Unblocked. Can start now.
5. **ADF-009** — Lambda + DynamoDB. Needs ADF-008.
6. **ADF-012** — Deploy TIS to EC2. Needs ADF-005 + ADF-008 + TIS-009.

---

## Adding New Tickets

- Create ticket in `Tickets/<service-folder>/` (e.g., `Tickets/trigger-ingestion-system/TIS-012.md`)
- Update this index with the new row

### Service Prefixes

| Prefix | Service |
|--------|---------|
| ADF | AWS Deployment Framework |
| ALS | Alpha Scanner |
| BDS | Binance Data Collector / Position Tools |
| CGS | CoinGecko Scanner |
| FTP | FTP Agent (Monitor/Executor) |
| IDS | Idea Discovery Service |
| TIS | Trigger Ingestion System |
| TMS | Telegram MCP Server |
