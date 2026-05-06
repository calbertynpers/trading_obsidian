# telegram-mcp-server — Daily Log

Per-project rolling log. Newest entries at the top. End-of-session summaries, live-verification notes, and decisions made in-session go here instead of the global `daily/YYYY-MM-DD.md`.

Related: [[Overview]], [[Technical Notes]], [[../Tickets/telegram-mcp-server/TMS-001|TMS-001]], [[../Tickets/telegram-mcp-server/TMS-002|TMS-002]]

---

## 2026-04-23 — TMS-001 closed, TMS-002 opened

### Accomplished
- **Live verification** of the Telegram MCP server against the real bot (chat_id `2141629529`):
  - `send_message` → message_id 9 ✅
  - `send_alert` (INFO) → message_id 10 ✅
  - `edit_message` on message 10 ✅
  - `get_updates` picked up reply "Be careful" (update_id `578174315`) ✅
  - `send_photo` not exercised — low-risk, same code path.
- **Secrets hygiene:** `.mcp.json` (contains live Telegram bot token + Binance + CoinGecko keys) added to `.gitignore` before first commit. `.vscode/` also gitignored.
- **[[../Tickets/telegram-mcp-server/TMS-001|TMS-001]]** → 🟢 Done. Acceptance criteria all met; ticket updated with live-verification section.
- **[[../Tickets/telegram-mcp-server/TMS-002|TMS-002]]** opened: *Reply poller + agent responder*. Motivated directly by today's `get_updates` round-trip — the MCP server surfaces replies on demand, but nothing consumes them asynchronously.

### Decisions
- **Reply-handling architecture (high-level, TMS-002 design to confirm):** separate long-running worker process does the polling; each new reply is dispatched to a Claude Agent SDK call with the Telegram MCP tools attached. Worker becomes the *sole* consumer of `get_updates` to avoid the in-process offset being stolen.
- **Polling over webhooks for v1.** Webhooks need public HTTPS + infra; polling fits the current shape. Revisit if latency becomes an issue.
- **Per-project daily log over global daily note** — user preference captured mid-session. This file is the canonical log for this project going forward.

### Open Questions (carried into TMS-002)
- Offset ownership — does the MCP server keep owning `_last_update_offset` (and then the worker *is* the MCP server's only caller of `get_updates`), or do we move the offset to shared storage?
- Safety controls for the responder: chat allowlist, per-chat rate limit, system-prompt scoping, agent-user-id echo prevention.
- Cost ceiling per day — every reply = one Agent SDK call. Needs a back-of-envelope estimate in the design.

### Next up
- Write `.kiro/specs/telegram-reply-agent/` (requirements → design → tasks) for TMS-002.
- Decide offset ownership before touching code.
