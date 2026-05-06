# Telegram MCP Server

Standalone MCP server wrapping the Telegram Bot API. Lets any MCP client (agent, IDE, CLI) send and edit Telegram messages and read incoming ones without embedding Telegram-specific code.

- **Repo:** `~/Documents/repos/telegram-mcp-server/`
- **Package:** `telegram_mcp_server`
- **Run:** `python -m telegram_mcp_server` or `uvx telegram-mcp-server`
- **Transport:** FastMCP + stdio
- **Python:** ≥3.12

## Purpose

Thin, stateless wrapper — no business logic, no deduplication, no rate limiting, no filtering. Callers retain full control over cadence and formatting. Intended for reuse across multiple agents with different reliability/spam tolerance needs.

## Tools exposed

| Tool | Purpose | Bot API endpoint |
|---|---|---|
| `send_message` | Plain text or HTML message | `sendMessage` |
| `send_alert` | Structured HTML alert — severity emoji + bold title + body + details + "→ action" | `sendMessage` (formatted HTML) |
| `get_updates` | Pull new messages; auto-tracks offset | `getUpdates` |
| `edit_message` | Update a previously sent message | `editMessageText` |
| `send_photo` | Send an image URL with optional caption | `sendPhoto` |

All send tools accept an optional `chat_id` override (default from env).

## Severity → emoji

| Severity | Emoji |
|---|---|
| CRITICAL | 🔴 |
| WARNING | ⚠️ |
| INFO | ℹ️ |

## Configuration

Required env vars (validated at startup — missing → `ValidationError` → `sys.exit(1)`):

- `TELEGRAM_BOT_TOKEN`
- `TELEGRAM_CHAT_ID`

No config files. No secrets in the repo.

## Source of truth

Specs live in the repo under `.kiro/specs/telegram-mcp-server/`:

- `requirements.md` — EARS-format acceptance criteria
- `design.md` — architecture, data models, correctness properties
- `tasks.md` — implementation task list (10 tasks, bottom-up)

If this Obsidian page conflicts with the spec, the spec wins.

## Tickets

- [[TMS-001]] — initial implementation (open)
- See [[Trading/Tickets/Ticket Index|Ticket Index]] for the rolling list.

## Related pages

- [[Trading/telegram-mcp-server/Technical Notes|Technical Notes]] — rolling architectural log and gotchas.
