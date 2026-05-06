---
wing: coins
type: coin-profile
symbol: ZBT
status: monitoring
narrative:
  - Spot-driven parabolic
  - Real-demand long candidate
strategy:
  - Spot-Driven Long (new framework — see Strategies/Spot-Driven Long)
position: NONE — alerts set for pullback entry
leverage: TBD on entry
last_reviewed: 2026-04-26
tunnels:
  - Strategies/Spot-Driven Long
  - Strategies/Account Configuration
  - Trade Log
tags:
  - spot-driven
  - parabolic-pullback-entry
  - real-demand
  - alert-and-wait
  - rsi-extreme
---

# ZBT — Monitoring for Spot-Driven Long Entry

> **Status (2026-04-26):** Pumped +49% on the day, +80% from $0.14 baseline, +118% on weekly. Daily RSI 86.4 rising; 4H RSI 81 cooling. Critical signal: **funding stayed at +0.005% baseline through the entire pump** — no perp long crowding, meaning the move is spot-driven real demand, not derivative speculation. **Initially screened as a short candidate but funding signature inverted the read** — this is the canonical example of why **spot-driven parabolics are long candidates, not short candidates**. Currently waiting for pullback entry. Alerts at $0.215 (primary) and $0.168 (better conviction).

## Why this isn't a short

Initial screen looked similar to BSB/AGT (parabolic + extreme RSI + BB above upper band), but funding signature broke the comparison:

| Coin | Pump magnitude | Funding peak | Setup type |
|------|---:|---:|------|
| BSB | +112% | **+0.192%** | Long-crowded top → short candidate ✓ |
| AGT | +115% | **+0.124%** | Long-crowded top → short candidate ✓ |
| **ZBT** | **+80%** | **+0.005%** (baseline through entire pump) | **Spot-driven, real demand → LONG candidate** |

When funding stays flat through a parabolic pump, the move is being driven by spot bid, not perp speculators. There's no positioning extreme to fade — only RSI/BB extension to bet against, which is a much weaker short setup. **Spot demand persists; speculative crowding capitulates.** This is the foundational difference for the [[Strategies/Spot-Driven Long]] framework.

## Chart picture (2026-04-26)

**Daily:**
| | |
|---|---|
| Mark | $0.252 |
| Today change | +48.9% |
| Open / High / Low | $0.169 / **$0.276** / $0.153 |
| Body ratio | 0.68 (strong bullish body) |
| Upper wick | 19.2% (some rejection at $0.276) |
| Lower wick | 13.2% |
| **Daily RSI** | **86.4 rising** (from 76.45) |
| Daily ADX | 47.48 — strong trend |
| BB position | Above upper band ($0.188) |
| MACD | Bullish (histogram growing) |

**4H:**
- Mark $0.2498, change −0.99%
- 4H RSI 81.18 falling from 82.53 (cooling)
- 4H ADX **61.73 — extreme trend strength**
- BB above upper band
- Most recent 4H candle: body 0.09 (doji), upper wick 40.7%, lower wick 50.7% — massive indecision after the run-up

**1H/15m:** Both pulling back ~3-4%, RSI cooling

**Weekly:** +118%, RSI 60.7 rising from 34.7 — weekly has room to extend

**Multi-TF: LEAN BULLISH net +2 (Medium confidence)**

## Funding history (the key signal)

| Time (UTC) | Rate | Mark |
|------------|-----:|-----:|
| 04-25 (all day) | +0.005% | $0.13-0.16 |
| 04-26 00:00 | +0.005% | $0.169 |
| 04-26 04:00 | +0.005% | $0.168 |
| 04-26 08:00 | +0.005% | $0.189 |
| 04-26 12:00 | +0.005% | $0.169 |
| 04-26 16:00 | +0.0000024% | $0.203 |
| 04-26 20:00 | +0.005% | $0.252 |
| Live | +0.005% | $0.250 |

**Persistently flat at +0.005% through a +80% pump.** No long crowding. No short crowding. Pure neutrality on perp positioning while spot price grinds higher. This is the spot-bid signature.

## Levels reference

**Resistance:**
- $0.252 — current mark
- $0.264 — 4H high (today's bounce zone)
- **$0.276 — today's daily high** (clear invalidation if broken with volume)
- $0.30 — psychological round number
- $0.35-$0.40 — 1.272-1.382 fib extension of the pump (TP3 zone if long works)

**Support / pullback entry zones:**
- $0.236 — 4H BB upper turning support (immediate, ~−6% pullback)
- $0.215-$0.220 — **PRIMARY ENTRY** — 1H EMA20 zone (~−13-15% pullback)
- $0.20 — round number / 1H EMA50 area
- $0.168 — **BETTER CONVICTION ENTRY** — 4H EMA20 (~−33% pullback)
- $0.140 — 4H EMA50 / pre-pump baseline (full retrace; trend invalidation if breached)

## Long entry plan

**Primary entry zone: $0.215-$0.220**
- 1H EMA20 area, ~15% pullback
- Most likely first level to be tested if move pauses
- Stop at $0.190 (below 1H EMA50 / round-number support)
- Loss if hit: ~12% from entry
- Targets: $0.276 (TP1) / $0.30 (TP2) / $0.35-0.40 (TP3)

**Better entry zone: $0.168-$0.175**
- 4H EMA20 zone, ~33% pullback
- Higher-conviction entry if patient
- Stop at $0.140 (below 4H EMA50 / pre-pump baseline)
- Loss if hit: ~17% from entry
- Targets same as above; better R:R from lower entry

**Sizing on entry:** Normal directional position size — ~$40-50 margin, 10x leverage = ~$400-500 notional. At $0.215 = ~1,800-2,300 tokens. At $0.168 = ~2,900-3,700 tokens.

## Confirmation before entering

**Take the long only if all of these hold at the alert level:**
1. Pullback to $0.215 or $0.168 with 4H higher low forming (no LL break)
2. Funding stays neutral (+0.005% to +0.02%) or only mildly positive
3. Volume on bounce attempts >= volume on pullback candles (real buyers re-engaging)
4. No daily reversal candle in between (no red body ≥0.5 with upper-wick rejection)
5. 4H ADX stays >40 (trend still alive)

## Invalidation (do NOT take long)

1. **Funding spikes >+0.05%** on next 8h settlement → speculators joining, real demand thesis weakened
2. **Daily reversal candle prints** → distribution starting
3. **4H closes below $0.168** → trend broken on intermediate TF
4. **Weekly RSI hits 80+** → weekly exhaustion piles on daily exhaustion
5. **Volume on pullback >> volume on bounce** → distribution, not consolidation

## What if it just keeps going up?

If ZBT breaks above **$0.276 with conviction** and funding stays neutral, the pullback opportunity is gone. Don't chase — accept it as a trade missed by being disciplined. Set the long aside; the next setup will come.

## Open follow-ups

1. **Set alerts at $0.215, $0.168, $0.276, and $0.140** (decision triggers)
2. **Re-pull funding at next 8h settlement** to verify whether spot-driven thesis still holds
3. **Check spot vs perp price** to confirm spot is leading (perp shouldn't be at a discount; should be at parity or mild premium)
4. **Identify what ZBT actually is** (token name, project, listing date) to assess catalyst risk

## Trade History (this symbol)

| Trade # | Date | Side | Size | Entry | Exit | P&L | Outcome |
|---------|------|------|------|-------|------|-----|---------|
| — | — | (none yet) | — | — | — | — | MONITORING — alerts set |

## Links

- [[Strategies/Spot-Driven Long]] — new strategy framework derived from ZBT analysis
- [[Strategies/Account Configuration]] — cross-margin context
- [[Trade Log]] — will be updated when entered
- [[daily/2026-04-26]] — entry analysis context (rolling from 2026-04-25 session)



---

## Trade closure (2026-04-27 ~early UTC) — LOSS

**Status update:** Trade closed at stop $0.190. Realized loss ~−$202 on 5,496 tokens.

### Timeline

| Event | Time (UTC) | Price | Notes |
|-------|------------|------:|-------|
| Entry LONG | 2026-04-26 22:49 | $0.2268 | On apparent pullback to $0.215-0.22 zone |
| Continuation down | 2026-04-26 23:00-04-27 00:00 | $0.227 → $0.169 | **−25% within hours of entry**, no bounce structure |
| Bounce attempt | 2026-04-27 morning | $0.169 → $0.198 | Recovery insufficient to retest entry |
| Stop fired | 2026-04-27 ~early | $0.190 | Mechanical exit at framework invalidation |

### Why this trade failed (diagnosis)

The Spot-Driven Long thesis assumed: *flat funding through the pump = spot bid intact = price will resume after pullback.*

**What actually happened:** Spot demand evaporated faster than funding signaled it. The flat +0.005% funding rate at the time of entry was a LAGGING indicator — by the time funding would have moved, price had already crashed −25%.

**Specific framework violations on entry:**

1. **Confirmation rule #1 ("4H higher low forming") was assumed, not verified.** Entry was triggered by price tagging the 1H EMA20 zone at $0.227. We never waited for an actual 4H higher low to print. The pullback was mid-fall, not a confirmed reversal.

2. **The "pullback to support level" interpretation was too loose.** Touching a moving average ≠ structural higher low. Real higher low requires: prior swing low → bounce → next pullback that holds ABOVE the prior swing low. We had only the first leg.

3. **No real-time spot-flow confirmation.** We assumed flat funding meant spot bid was holding. There was no independent verification (e.g., spot orderbook depth check, on-chain flow, spot venue volume). We trusted the funding signal alone.

### What this teaches the framework

ZBT becomes the canonical first failure example for [[Strategies/Spot-Driven Long]]. The framework needs two updates:

1. **Strict entry confirmation** — require a printed 4H higher low (clear bounce + held pullback above the bounce low), not just price touching a support EMA
2. **New failure mode documented** — "spot demand can dry up without funding signaling it; flat funding is necessary but not sufficient evidence"

### Trade economics

| | |
|---|---|
| Entry | $0.2268 × 5,496 (10x leverage on margin reduced from 20x to 10x at some point) |
| Exit (stop) | ~$0.190 |
| Realized loss | **~−$202** |
| Vs framework worst-case prediction | $0.190 stop = framework primary stop ✓ — performed exactly as designed |

The structure protected the trade. The thesis was wrong. **The structural discipline is what kept this from being a $500 loss.** Stop at framework invalidation level fired exactly as planned.

### Lessons taken

- **Don't trust new frameworks before validation.** Spot-Driven Long had ONE worked example (this one) and it failed. Need 5-10 setups tracked before assigning conviction sizing.
- **Confirmation rules exist for a reason — verify all of them.** Skipping the "printed higher low" check converted a probabilistic setup into a coin flip.
- **Stop placement saved the trade.** A different operator without the structural stop discipline would have ridden this to a much bigger loss hoping for recovery.
- **Funding signature is necessary but not sufficient.** Need supplementary confirmation (real spot flow, structure print, sector co-movement) to verify the spot-driven thesis is actually live.

Trade is now CLOSED. Moving on. See [[daily/2026-04-26]] for full session context and [[Strategies/Spot-Driven Long]] for framework updates.

---

## Trade History (this symbol) — UPDATED

| Trade # | Date | Side | Size | Entry | Exit | P&L | Outcome |
|---------|------|------|------|-------|------|-----|---------|
| 015 | 2026-04-26 | Long | 5,496 | $0.2268 | ~$0.190 (stop) | **~−$202** | **LOSS** — first failed Spot-Driven Long worked example |
