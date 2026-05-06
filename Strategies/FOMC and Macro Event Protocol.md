---
wing: strategies
type: strategy
status: active
regime:
  - all
tunnels:
  - Strategies/Overnight Risk Protocol
  - Trade Log
created: 2026-04-30
trigger_trades: "Trades 017, 018, 019 (SKYAIUSDT -$114, NAORISUSDT -$136, GRIFFAINUSDT -$57 — all FOMC 2026-04-29)"
---

# FOMC and Macro Event Protocol

**One-line rule:** *If a scheduled macro event is on the calendar, all stop-exposed positions must be closed, hedged, or widened at least 1 hour before the announcement — no exceptions.*

Generated after three simultaneous stop-outs on 2026-04-29 during the FOMC announcement window: SKYAIUSDT (-$114), GRIFFAINUSDT (-$57), and NAORISUSDT (-$136 partial, fired at 01:40 UTC post-announcement). Total avoidable loss: **-$307**. The event was known in advance. Nothing about the losses was unforeseeable — it was a calendar failure, not a market failure.

---

## Why Macro Events Are Different

Macro announcements (FOMC, CPI, NFP, Fed speeches) create **non-directional volatility spikes** within a predictable time window. Unlike overnight risk (which is probabilistic), these events are:

1. **Scheduled and known days in advance** — there is no excuse for being caught off-guard
2. **Magnitude-unpredictable but occurrence-certain** — you don't know which way it moves, but you know it *will* move sharply
3. **Stop-hunting by design** — algos target stop clusters in both directions before the real move begins; even a "correct" directional trade gets stopped before it recovers
4. **Followed by continuation** — post-FOMC follow-through can last 24–48 hours, not just minutes (NAORI stop at 01:40 UTC = 8 hours after the announcement)

---

## The Mandatory Pre-Event Checklist

Run this **every time a macro event appears in the calendar within the next 24 hours.**

| # | Check | Action if yes |
|---|-------|---------------|
| 1 | Is there a stop-loss order currently live on any position? | → **Remove or widen the stop** before the event window |
| 2 | Is any stop within 5% of current price on a leveraged position? | → **Must act** — tight stops will be hunted |
| 3 | Is there a limit entry order that could fill during the event window? | → **Cancel and re-place after the dust settles** |
| 4 | Is any position at a leveraged loss currently? | → **Close or fully hedge before the event** |
| 5 | Are any new positions being considered in the 2 hours pre-event? | → **Do not open** — see "What NOT to Do" below |

---

## The Rule: 1 Hour Before / 30 Minutes After

```
T-60 min: Complete the checklist. All flagged positions resolved.
T-0:       Announcement fires.
T+30 min:  Initial volatility spike usually resolved. Review market structure.
T+24h:     Post-announcement continuation risk window ends for most assets.
```

**Before re-entering any closed position:** wait for the first 30 minutes to pass and a clear directional candle to print on the 15m chart. Don't re-enter into the spike itself.

---

## Tiered Response by Position Type

| Position type | Action |
|---|---|
| **Tight stop (<5% away), leveraged** | Close or move stop outside 2× ADR before T-60 |
| **Wide stop (>10% away), leveraged** | Widen further to outside 3× ADR, or close |
| **Profitable position with unrealised gain** | Consider banking partial profit at T-60; let remainder ride with wider stop |
| **Losing position already in drawdown** | Close before T-60 — don't let FOMC volatility decide |
| **Limit entry order pending** | Cancel at T-60; re-evaluate and re-place after T+30 |
| **No stop, large position** | This is the most dangerous case — close or set emergency stop at T-60 |

---

## Scheduled Macro Events Calendar (recurring)

Mark these in your calendar at the start of each month. Times are approximate UTC:

| Event | Frequency | Typical UTC time | Volatility window |
|-------|-----------|-----------------|------------------|
| **FOMC rate decision** | 8× per year (every ~6 weeks) | ~18:00–19:00 UTC | ±4h, follow-through 24–48h |
| **FOMC minutes release** | 3 weeks after each meeting | ~18:00 UTC | ±2h |
| **US CPI** | Monthly (2nd week) | ~12:30 UTC | ±2h |
| **US NFP (non-farm payrolls)** | Monthly (1st Friday) | ~12:30 UTC | ±2h |
| **Fed Chair speech / Jackson Hole** | Ad hoc | varies | ±4h |
| **US GDP release** | Quarterly | ~12:30 UTC | ±1h |
| **ECB rate decision** | 8× per year | ~12:15 UTC | ±2h |

**FOMC dates for 2026 (approximate):**
- Jan 28–29 ✓ (past)
- Mar 18–19 ✓ (past)
- Apr 29–30 ← **This session's event**
- Jun 17–18
- Jul 29–30
- Sep 16–17
- Nov 4–5
- Dec 16–17

---

## What NOT to Do

- ❌ Open a new leveraged position within 2 hours of a known macro event
- ❌ Leave tight stops live during the event window — they will be hunted
- ❌ Re-enter a stopped-out position immediately after the spike — wait for structure to reform
- ❌ Assume a "correct" trade thesis protects you — stops get taken regardless of direction before the real move starts
- ❌ Treat the announcement itself as the end of volatility — post-FOMC follow-through lasted 8+ hours on 2026-04-29

---

## What TO Do

- ✅ Check the macro calendar every Sunday for the coming week
- ✅ Set a phone reminder at T-90 min for every scheduled event
- ✅ Document the decision (close / widen / hold) in the daily note before the event fires
- ✅ Re-enter with conviction *after* the directional move is confirmed — the post-FOMC setup is often a better entry than the pre-FOMC one
- ✅ If you believe strongly in a directional trade through the event, express it via options or a minimal size with an ultra-wide stop — don't hold a full-size futures position into the spike

---

## Interaction with Overnight Risk Protocol

This protocol and [[Strategies/Overnight Risk Protocol]] address different risk windows:

| Protocol | Risk window | Trigger | Mechanism |
|---|---|---|---|
| Overnight Risk Protocol | 22:00–07:00 local (sleep) | New listing / extreme RSI / low float | 6-point checklist before placing any limit |
| **This protocol** | Scheduled macro event ±2h | FOMC / CPI / NFP / Fed speech | Calendar check → position resolution before T-60 |

They can overlap (e.g. FOMC decision followed by a sleep window = both protocols apply). When both fire, apply the stricter constraint.

---

## Origin

Three stop-outs on 2026-04-29 during the FOMC announcement:

| Trade | Symbol | Loss | Timing |
|-------|--------|------|--------|
| 017 | SKYAIUSDT | -$114 | 16:05 UTC (FOMC window) |
| 019 | GRIFFAINUSDT | -$57 | 16:00 UTC (FOMC window) |
| 018 | NAORISUSDT | -$136 | 01:40 UTC (post-FOMC follow-through) |
| **Total** | | **-$307** | |

All three were avoidable. The FOMC date (Apr 29–30, 2026) was published weeks in advance. A 1-hour pre-announcement window to resolve stop exposure would have preserved the entire $307.

The same session produced +$1,960 net from the BSB full-cycle trade. That doesn't offset the fact that $307 was donated unnecessarily.

**Rule: from 2026-04-30 forward, macro event dates go in the calendar the moment they are published, and the pre-event checklist runs at T-90 min without exception.**

---

## Links

- [[Trade Log]] — Trades 017, 018, 019 (origin cases)
- [[2026-04-29]] — session where this was created
- [[Strategies/Overnight Risk Protocol]] — sibling protocol for sleep-window risk
- [[Strategies/Account Configuration]] — cross-margin context
