# Telegram MCP Server — Technical Notes

Rolling log of non-obvious implementation details, architectural decisions, and gotchas. Ticket-specific resolution notes live on the ticket; cross-cutting context lives here.

## Stack

- Python ≥3.12 (repo runs 3.14).
- `httpx.AsyncClient` for HTTP — 10s timeout across all Bot API calls.
- `pydantic` v2 + `pydantic-settings` for config + models.
- `mcp` (FastMCP) with stdio transport.
- Test: `pytest`, `pytest-asyncio` (auto mode), `hypothesis`, `respx`.

## Module layout

| Module | Role |
|---|---|
| `config.py` | `TelegramSettings(BaseSettings)` — env-driven, validates at import. |
| `models.py` | `Severity`, `SEVERITY_EMOJI`, `AlertInput`, `TelegramUpdate`, `SendResult`, `ErrorResult`. |
| `formatter.py` | Pure `format_alert` / `parse_alert`. HTML-escaped, round-trip safe. No I/O. |
| `client.py` | `TelegramClient` — thin async httpx wrapper, one method per Bot API endpoint. |
| `server.py` | FastMCP instance, 5 tool defs, module-level settings/client/offset. |
| `__main__.py` | Entry point — catches `ValidationError` around `server.mcp` import, else `mcp.run()`. |

## Key design decisions

### No business logic in the server
Per Requirement 7 (explicit in the spec). No dedup, no rate-limit, no filter, no transformation beyond structuring raw Bot API updates into `TelegramUpdate`. Same content sent twice = two Bot API calls.

**Why:** callers own formatting + cadence. This server is intended to be reused by multiple agents with different reliability / spam tolerance needs.

### Only state is the getUpdates offset
Module-level `_last_update_offset: int = 0` in `server.py`. Resets on restart (stateless design).

**Invariant (Property 2):** after each batch, offset == `max(update_ids) + 1`.

### Alert formatting is a pure function, not a method
Pattern: `{emoji} <b>{SEVERITY}</b> | {title}\n{body}\n{key}: {value}\n→ {suggested_action}`.

All user-provided strings go through `html.escape()` before concatenation to prevent Telegram HTML parse errors on `<`, `>`, `&`. Structural tags (`<b>`, `</b>`) and the emoji/arrow prefixes are not escaped.

**Invariant (Property 1):** `parse_alert(format_alert(...))` recovers the original severity / title / body / details / suggested_action. Verified via Hypothesis across 100+ iterations with Unicode and HTML specials in inputs.

### Error handling
- Bot API non-200 → `{"error": "Bot API error", "status_code": N, "description": "..."}` (description pulled from response JSON; raw text if JSON parse fails).
- `httpx.HTTPError` (ConnectError, TimeoutException, etc.) → error dict, server process does **not** crash — MCP connection stays open for subsequent calls.
- Config `ValidationError` at startup → printed to stderr → `sys.exit(1)` before any tool calls accepted.

### Update parsing
`get_updates` skips updates without a `message` field (callback queries, edits, etc.). Missing `text` defaults to `""`. All other fields come straight from the Bot API response.

**Invariant (Property 3):** every valid Bot API update → `TelegramUpdate` populated with `update_id`, `chat_id`, `sender_name`, `text`, `date`.

## Testing notes

- `respx` mocks httpx for `test_client.py` — no real Bot API hits.
- Hypothesis property tests cover the 3 correctness properties; minimum 100 iterations each.
- `asyncio_mode = "auto"` in `pyproject.toml` so tests don't need explicit `@pytest.mark.asyncio`.
- Property test inputs exclude newlines (formatter is line-delimited) but include HTML specials and Unicode.

## Open questions / deferred

*(none yet — fill in as implementation surfaces surprises)*

## Changelog

- **2026-04-23** — Project kicked off. [[TMS-001]] opened covering tasks 1–10 of `.kiro/specs/telegram-mcp-server/tasks.md`. Scaffolding next.


## Open questions / deferred


- **Formatter round-trip input constraints.** The spec pattern `{key}: {value}` / `→ {suggested_action}` is not invertible for arbitrary inputs. `parse_alert` can't unambiguously recover (a) detail keys containing `": "` or (b) detail keys starting with `"→ "`. Resolved pragmatically: documented as input preconditions in `format_alert`'s docstring; Property 1 test generator respects them. Real-world alert keys (`symbol`, `entry_price`, `pnl`, etc.) never hit either case. If the constraints become a problem, revisit the delimiter / add an escaping scheme (would require a spec update).


## Changelog


- **2026-04-23** — All 10 tasks of [[TMS-001]] implemented. 39/39 tests passing (5 formatter + 21 client + 13 server). Hypothesis covers the 3 documented correctness properties at 100 iterations each. Refactor: parsing logic for `get_updates` factored into pure `_parse_updates` / `_advance_offset` helpers in `server.py` so Properties 2 and 3 test without mocks. Flagged and resolved the formatter round-trip ambiguity (see Open questions). No commits yet.
