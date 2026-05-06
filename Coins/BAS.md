---
wing: coins
type: coin-profile
symbol: BAS
status: active
narrative:
  - L1-L2 Infrastructure
strategy:
  - Directional Probe (50/50 re-hedge)
  - FTP Strategies
  - Squeeze Environment Playbook
position: hedged (100k long / 85k short), asymmetric directional stops + short TP ladder
leverage: long 10x · short 10x
last_reviewed: 2026-04-24
tunnels:
  - Narratives/L1-L2 Infrastructure
  - Strategies/FTP Strategies
  - Strategies/Squeeze Environment Playbook
  - Trade Log
tags:
  - bnb-chain
  - post-launch
  - re-hedged
  - directional-probe
  - asymmetric-stops
  - post-pivot
---

# BAS — BNB Attestation Service

> **Status (2026-04-24, 06:53 UTC):** Re-hedged from naked short into an asymmetric directional probe with a full short TP ladder now placed. Book is 100k long / 85k short — 50/50 view on direction. Hard stops let either direction confirm without sacrificing the wrong leg. Short TP2 ($0.01150 × 50k) and TP3 runner ($0.01090 × 25k) now mechanically in place below mark. **Worst-case chop-through = -$13**, comfortably inside the $100 stated risk budget.

## Project Snapshot

BAS (BNB Attestation Service) is an attestation-layer project on BNB Chain — infrastructure for verifiable credentials / on-chain attestations. See [[daily/2026-04-21]] for fundamentals/tokenomics/unlock deep-dive. Binance perp has no BASUSDT feed — chart reads below use **MEXC:BASUSDT**.

---

## Pivot history (2026-04-23 → 2026-04-24)

### Phase 1 — Flip to naked short (2026-04-23 21:28–22:49 UTC)

| UTC | Action | Size | Price | P&L |
|-----|--------|------|-------|-----|
| 21:28:53 | Market BUY close short | 100k | $0.01850 | **-$122** realized (blended degraded by $0.012799 add) |
| 21:28:57 | Market SELL reopen short | 100k | $0.01846 | Blended refreshed $0.01728 → $0.01846 |
| 21:29–22:14 | 6× market SELL close LONG | 105k | avg $0.01834 | **+$575** realized |
| 22:34–22:46 | 3× market SELL scale short | 70k | avg $0.01852 | Short expanded to 170k @ blended $0.01848 |
| 22:49 | Cancel prior stop ladder | — | — | — |

Phase 1 net realized: **+$453**.

### Phase 2 — 50/50 re-hedge + TP ladder (2026-04-24 06:31–06:53 UTC)

| UTC | Action | Size | Price | P&L |
|-----|--------|------|-------|-----|
| 06:31:46 | Market BUY close short (50%) | 85k | $0.01547 | **+$255** realized |
| 06:33:30 | Limit BUY open long | 100k | $0.015459 | (open) |
| 06:33:30 | TP-market on long placed | 100k | trigger $0.018484 | Ride-up exit |
| 06:34:30 | Prior stop at $0.01401 cancelled | — | — | Replaced |
| 06:41:14 | Stop-market on long placed | 80k | trigger $0.01413 | 80% dump-confirm stop |
| 06:41:15 | Stop-market on short placed | 80.75k | trigger $0.01723 | 95% pump-confirm stop |
| 06:53:04 | TP-market on short placed | 50k | trigger $0.01150 | Short TP2 (4H EMA50) |
| 06:53:04 | TP-market on short placed | 25k | trigger $0.01090 | Short TP3 runner (daily EMA200) |

Phase 2 realized: **+$255**. Cumulative realized since 04-23: **+$708**.

---

## Current Book (2026-04-24 06:53 UTC)

| Leg | Size | Entry | Mark | uPnL | Eff Lev | Role |
|-----|------|-------|------|------|---------|------|
| **LONG** | 100,000 | $0.015459 | $0.015437 | ~$0 | 10x | Ride-up leg |
| **SHORT** | 85,000 | $0.01848 | $0.015437 | **+$258 (+16.45%)** | 10x | Ride-down leg |

### Live Orders

| Order | Type | Side | Size | Trigger | Purpose | Algo ID |
|-------|------|------|------|---------|---------|---------|
| Long ride-up TP | TAKE_PROFIT_MARKET | SELL LONG | 100,000 | $0.018484 | Full long close at short-blended zone on rally | 2000000829805683 |
| Long dump stop | STOP_MARKET | SELL LONG | 80,000 | $0.01413 | 80% long close on downside confirm | 2000000829832460 |
| Short pump stop | STOP_MARKET | BUY SHORT | 80,750 | $0.01723 | 95% short close on upside confirm | 2000000829832486 |
| Short TP2 | TAKE_PROFIT_MARKET | BUY SHORT | 50,000 | $0.01150 | Mechanical cover at 4H EMA50 / deep support | 2000000829867725 |
| Short TP3 (runner) | TAKE_PROFIT_MARKET | BUY SHORT | 25,000 | $0.01090 | Mechanical cover at daily EMA200 / re-hedge zone | 2000000829867745 |

### Residuals on stops / TPs
- After long stops: 20k long remains (hedge vs. ongoing downside)
- After short stops: 4.25k short remains (hedge vs. ongoing upside)
- After short TP2 + TP3 fills: 10k short remains (small runner below $0.01090)

---

## Strategy — Directional Probe (50/50 re-hedge)

### Thesis

After the -18% daily candle on 2026-04-23 and the bounce-free normal-volume pullback, directional conviction is genuinely 50/50. Book set up to **let the market declare direction, then keep dominant exposure on the winning side** — and now with mechanical exits on the short at both support tiers.

- **If price drops to $0.01413** (today's daily low retest): downside confirmed. Long stops, leaving 20k long + 85k short — net short ≈ 65k. Short then rides toward $0.01150 (TP2 fires at 50k) and $0.01090 (TP3 runner fires at 25k). Remaining 10k short is a tiny further runner below $0.01090, close on re-entry-long signal.
- **If price rises to $0.01723**: upside confirmed. Short stops, leaving 100k long + 4.25k short — net long ≈ 95k. Long rides the squeeze to $0.01848 where TAKE_PROFIT_MARKET fires. Short TP2/TP3 remain armed for the far-below scenario (won't trigger on this path).
- **If it chops both triggers**: worst-case -$13 (up-then-down whipsaw), otherwise positive. Chop is cheap.

Rationale for asymmetric close ratios: the short is already +$258 in the black, so a 95% close at $0.01723 still locks meaningful profit (+$101 at that level); the long is at scratch, so only 80% gets sacrificed if it fails. Every combination of scenario paths lands net-positive except the up-then-down whipsaw (-$13).

### Stress-test summary (refreshed)

| Scenario | Path | Net from here |
|----------|------|---------------|
| Down confirms → TP2 fires at $0.01150 | Long stops, 50k of short covers, 10k ride continues | **~+$225** (was +$408, now includes auto-cover efficiency loss on early close) — wait, recompute: long stop -$106 + short TP2 +$349 + remaining 35k short uPnL = -$106 + $349 + 35k × ($0.01848 - $0.01150) = -$106 + $349 + $244 = **+$487** |
| Down confirms → TP3 runner fires | Above + 25k close at $0.01090 | -$106 + $349 + $189 (TP3) + remaining 10k × ($0.01848 - $0.01090) = -$106 + $349 + $189 + $76 = **+$508** |
| Up confirms → $0.01848 | Short stops at $0.01723, long TP fires at $0.01848 | **+$403** |
| Whipsaw ↓↑ → long TP fires | Both stops + long TP on 20k remnant | **+$55** |
| **Worst case: whipsaw ↑↓** | Short stops then long stops, no long TP, TP2/TP3 not reached | **-$13** |
| Full chop back to $0.01544 | Both stops only | **+$8** |

Adding the short TP ladder *improves* the down-scenario by $79–$100 (locks profit mechanically rather than relying on riding with ever-shrinking unrealized margin) and doesn't change any other scenario since TP2/TP3 are far below current mark.

---

## Cycle-Shift / Re-entry-Long Markers

Same 5 markers. Now relevant for: (a) pre-confirmation of the down-scenario if price approaches $0.011; (b) re-establishing a long leg near $0.0110–$0.0115 after the short TPs fire.

| # | Marker | Level | Current state (2026-04-24) |
|---|--------|-------|---------------------------|
| 1 | Daily close above BB mid / SMA50 with above-avg volume | $0.0154 | NOT active (close $0.01523 < $0.0154) |
| 2 | Reclaim daily EMA200, held 48h | $0.0109 | Flagged (close $0.01523 > $0.011, 48h hold pending) |
| 3 | Funding flips negative | — | Positive (+0.00035), not flipped |
| 4 | 4H HH + HL structure | — | Ambiguous — TV shows 4H bullish bias but -18% daily likely damaged structure |
| 5 | Volume expansion: up-candles ≥1.5× down-candles (24h) | — | NOT active (today was strong down-candle) |

**Rule**: ≥2 markers active in the $0.0110–$0.0115 zone ⇒ short TP3 runner should be closing into this anyway, and consider establishing a fresh long leg at accumulation sizing (50–80k).

---

## Invalidation

- **Short invalidation**: daily close above **$0.0167** with above-avg volume. The $0.01723 stop fires after this level — by design (stop-hunting buffer). Kept at $0.01723 per discretion.
- **Long invalidation**: daily close below **$0.01300** with volume (would break the retest-and-recover premise). Stop at $0.01413 catches this early.
- **Original deep invalidation**: daily close below $0.0061 with volume — still the ultimate bear thesis floor.

---

## Open follow-ups

1. **Time stop** — if neither directional stop triggers in 72 hours, reassess. Not mechanical; calendar reminder.
2. **Funding check** — positive funding (+0.00035) means small cost on net-long portion. Monitor if the probe drags.
3. **Post-TP2 re-hedge decision** — when TP2 fires ($0.01150 × 50k cover), 35k short remains before TP3. Decide at that point whether to tighten trailing stop on the 35k or let the TP3 take another 25k. Pre-commit optional: add a stop-market BUY SHORT at $0.01350 × 35k *after* TP2 fires to protect runner on bounce.

---

## Key Levels Reference (refreshed 2026-04-24)

**Resistance (short defends, long rides up):**
- $0.015437 — current mark
- $0.01580–$0.01630 — immediate bounce cluster
- $0.01670 — **short invalidation** (critical)
- $0.01700 — alternate tighter short stop candidate (NOT chosen)
- $0.01715 — prior resistance (chosen ref for $0.01723 stop level)
- $0.01723 — **short pump-confirm stop** (LIVE)
- $0.01810–$0.01848 — short blended / **long ride-up TP** (LIVE at $0.018484)
- $0.01886 — local high (2026-04-23)

**Support (short TPs, long retests):**
- $0.01413 — **long dump-confirm stop** (LIVE) / today's daily low
- $0.01150 — **short TP2** (LIVE) / 4H EMA50
- $0.01090 — **short TP3 runner** (LIVE) / daily EMA200 / re-hedge trigger zone
- $0.00850 — daily SMA50 / BB mid
- $0.00610 — original Invalidation A (deep bear)
- $0.00250 — ultimate bleed target

---

## Trade History (this symbol)

| Trade # | Date | Side | Size | Entry | Exit | P&L | Outcome |
|---------|------|------|------|-------|------|-----|---------|
| 001 | 2026-04-21 | Short | small | — | — | **-$14** | LOSS — repositioned |
| 002 | 2026-04-21 | Short | 100k | $0.01818 | $0.01850 | **-$122** | CLOSED on reset (04-23) |
| 003 | 2026-04-21 | Long (L1) | 45k | $0.01400 | share $0.01834 | share of **+$575** | CLOSED 04-23 |
| 004 | 2026-04-22 | Long (L2) | 60k | $0.01200 | share $0.01834 | share of **+$575** | CLOSED 04-23 |
| 005 | 2026-04-23 | Short (refreshed) | 100k | $0.01846 | partial $0.01547 | **+$255** realized so far | 85k RUNNING |
| 006 | 2026-04-23 | Short (scale-in) | 70k | $0.01852 | — | part of +$258 unreal | RUNNING within 85k |
| 007 | 2026-04-24 | Long (probe) | 100k | $0.015459 | (open) | ~$0 | RUNNING — TP at $0.018484 |

**Cumulative realized since 2026-04-23**: **+$708**. Current open uPnL: **+$258**.

---

## Devil's Advocate

1. **Chop risk**: $0.01413 is -8.5%; $0.01723 is +11.6%. Both plausible in next 24–48h on a fresh -18% daily. Worst whipsaw -$13; beyond that, residuals take over but stay in-budget.
2. **Loose short stop at $0.01723**: price breaks $0.0167 (invalidation) before stop fires. Trade-off accepted to avoid stop-hunting wicks at the structural resistance cluster.
3. **Short TP ladder assumes price doesn't mean-revert between $0.01413 and $0.01150**: if it touches $0.01150 briefly then snaps back above $0.01413, the long stop still fires but the 50k TP2 close has already happened. That's actually fine — just means we exited the short lower than blended on 50k and the remaining 35k is open for further action.
4. **Direction = funding**: net +15k long. Positive funding = small drag. Monitor.
5. **Hidden assumption — ride-up TP at $0.01848 closes ENTIRE long**: spikes past $0.01848 cap upside. Consider splitting to 60k @ $0.01848 + 40k @ $0.01910 (BB upper) if you want more runway.

---

## Monitoring

**Hourly scheduled check** (see `Scheduled/bas-hourly-watch/`, updated 2026-04-24) pulls live book + multi-TF chart and alerts on:
- Any stop or TP trigger (5 live orders tracked)
- Proximity to stop/TP levels (within 2%)
- Re-entry-long conditions ($0.0110–$0.0115 with capitulation signals)
- Time-stop check at 72h if neither directional stop fires

Quiet otherwise.

---

## Links

- [[Trade Log]] — canonical Trades 001–007 entries
- [[daily/2026-04-23]] — pivot narrative (naked-short flip)
- [[daily/2026-04-24]] — re-hedge narrative (directional probe + TP ladder)
- [[Narratives/L1-L2 Infrastructure]]
- [[Strategies/Squeeze Environment Playbook]]
- [[Strategies/FTP Strategies]]
- `Scheduled/bas-hourly-watch/` — live monitoring task (updated 2026-04-24)



---

## Phase 3 — Anxiety unwind (2026-04-25 17:50–18:12 UTC) — **OFF-THESIS LOSS**

> **Status:** Short reduced from 85,000 → **4,170** in two close events during the BAS bounce into $0.018+ zone. Realized loss **~−$106**. This was an **anxiety-driven, off-thesis exit** during a squeeze that the original Phase 2 plan was specifically designed to absorb. Logged as a discipline lesson, not a strategy update. Cumulative realized on BAS still net-positive at **+$602** (was +$708 pre-anxiety unwind).

### What happened

| UTC | Action | Realized PnL | Notes |
|-----|--------|--------------|-------|
| 17:50–17:53 | 13 BUY closes on SHORT | **~−$32** | Biggest single −$13.12 |
| 18:12 | 28 BUY closes on SHORT | **~−$74** | Biggest singles −$21.87, −$8.63, four × −$4.50 |

**Net: ~−$106 realized loss + ~−$1.39 commissions = ~−$107 cost.**

The pre-set $0.01723 short pump-confirm stop (algo ID 2000000829832486) was *designed* for exactly this scenario — and would have triggered automatically if hit cleanly. The realized-loss magnitude is larger than a single stop-fill would account for, indicating **additional manual closes during the bounce** beyond the planned stop.

### Position after Phase 3

| Leg | Size before | Size after | Blended entry change |
|-----|------------:|-----------:|----------------------|
| SHORT | 85,000 | **4,170** | $0.01848 → $0.01547 (high-cost-basis tranches closed; small new short opened lower) |

The TP2 ($0.01150 × 50k) and TP3 ($0.01090 × 25k) ladder orders were also affected — with only 4,170 short remaining, those mechanical exits no longer apply at that scale.

### What this cost vs Phase 2 plan

Per the Phase 2 stress-test:
- **Down-confirm scenario (TP2 fires):** would have been **+$487**
- **Down-confirm scenario (TP3 also fires):** would have been **+$508**
- **Up-confirm scenario ($0.01848 long TP fires):** would have been **+$403**
- **Worst whipsaw (per plan):** −$13

**Actual outcome of Phase 3 unwind: −$106.** Worse than every planned scenario except a partial chop case, and 8x worse than the planned worst-case whipsaw budget.

### Discipline lesson (logged in [[daily/2026-04-25]] and [[Trade Log]])

- The anxiety to act *was the squeeze itself* — the moment positioning data (funding −0.687% at the BAS local top) was screaming "shorts are crowded, this is the squeeze peak."
- Acting on the discomfort converted a working trade into a realized loss.
- **Pre-commit rule (drafted):** *"I do not modify hedged positions outside of (a) a triggered watchdog alert, (b) a planned TP/stop level being hit, or (c) an explicit reassessment session with written reasoning logged."*

### Cumulative state

- Phase 1 (2026-04-23): **+$453** realized
- Phase 2 (2026-04-24): **+$255** realized
- Phase 3 (2026-04-25): **−$106** realized
- **Cumulative realized: +$602**
- Current open uPnL on remaining 4,170 short: **+$0.47**

### Status of the BAS trade going forward

The position is now too small to be the directional probe Phase 2 set up. Two options on the table:
1. **Close the residual 4,170** and end BAS exposure cleanly. Final realized = +$602.
2. **Leave the 4,170 as a tracker** — small enough to ignore, recovers part of the original thesis if BAS does eventually break to $0.011.

Decision pending. Watchdog (`bas-hourly-watch`) still runs but will now report on a near-irrelevant position size.

---

## Links update (2026-04-25)

- [[daily/2026-04-25]] — Phase 3 narrative + discipline lesson
- [[Trade Log]] — Trade 011 (BAS Phase 3 unwind, LOSS)
