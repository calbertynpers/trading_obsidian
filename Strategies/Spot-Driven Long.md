---
wing: strategies
type: strategy
status: active
regime:
  - bull-market
  - alt-rotation
  - sector-momentum
tunnels:
  - Strategies/Crime Coin Checklist
  - Strategies/Squeeze Environment Playbook
  - Strategies/FTP Strategies
  - Strategies/Account Configuration
  - Trade Log
tags:
  - spot-driven
  - real-demand
  - parabolic-pullback
  - funding-signature
  - long-strategy
---

# Spot-Driven Long — Strategy Framework

> **Core idea:** When a coin pumps parabolically but **funding stays neutral or only mildly positive**, the move is being driven by real spot demand — not perp speculators. These setups are LONG candidates on pullback, not short candidates on extension. The funding signature is the entire game: it's what distinguishes "real demand parabolic" from "long-crowded blow-off top."

## When this strategy applies

This is a **counter-intuitive long framework** specifically for situations where:

1. A coin has pumped 50%+ in 24-48 hours
2. Daily RSI is overbought (75+)
3. BB is above upper band on D and 4H
4. **CRITICAL:** Funding has stayed at baseline (+0.005% to +0.02%) through the entire pump
5. Multi-TF EMAs are stacked bullish across at least D and 4H
6. ADX is elevated (>40 on either D or 4H)

If criteria 1-3 are met but #4 fails (funding spiked +0.10%+), this is the **opposite setup** — long-crowded top, short candidate per the [[Strategies/Squeeze Environment Playbook]] / catalyst-pump distribution framework.

**The funding signature is the entire game.** It's the single signal that distinguishes:
- "Real demand parabolic" (spot bid → long the pullback) ← THIS strategy
- "Long-crowded blow-off top" (perp speculation → short the parabolic) ← BSB/AGT/APE strategy

## Why it works (mechanism)

When funding stays flat through a major price increase:
- **Perp price is following spot, not leading it**
- No speculative positioning extreme has built up
- Spot buyers have to be real (people putting cash into actual tokens, not chasing perp leverage)
- These buyers don't capitulate at RSI extremes — they're not chart traders

This is the *opposite* of a manipulation pattern. In crime coins ([[Strategies/Crime Coin Checklist]]), the manipulation usually shows up in **deeply negative funding** as professional shorts pile in to fade. In spot-driven moves, neither side is crowded — there's just real demand absorbing supply.

When the inevitable technical pullback comes (RSI works off overbought, BB normalizes), spot demand re-engages because the underlying buying interest hasn't gone away. That's the long entry.

## Identification checklist

Score each signal:

| # | Signal | What to look for |
|---|--------|------------------|
| 1 | Parabolic price action | Daily +30%+ in 24h, OR weekly +50%+ |
| 2 | RSI extreme | Daily RSI > 75, ideally rising |
| 3 | BB above upper band | On D and 4H |
| 4 | **Neutral funding** | **Stayed +0.005% to +0.02% through the entire pump (no spike to +0.05% or higher)** |
| 5 | ADX elevated | >40 on D or 4H |
| 6 | All EMAs stacked bullish | Across D and 4H minimum |
| 7 | Volume confirmation | Spot volume > average; perp OI growing modestly (not exploding) |
| 8 | Spot leads perp | Perp at parity or mild premium to spot (not deep premium = no speculative chase) |

**Need 5+ signals to qualify as spot-driven long candidate.** Critical signal #4 (neutral funding) cannot be substituted — without it, the setup is a different category.

## Entry framework — DO NOT chase

**Never enter at the parabolic high.** R:R is bad and the setup demands patience for pullback.

### Standard entry zones (use alerts, not market orders)

| Zone | Pullback depth | Where it lands | Stop | Risk |
|------|---:|------|------|------|
| **Tactical** | 10-15% | 1H EMA20 zone | Below 1H EMA50 | ~10-12% loss if hit |
| **Standard** | 25-35% | 4H EMA20 zone | Below 4H EMA50 | ~15-18% loss if hit |
| **Deep** | 40-50% | 4H EMA50 / pre-pump baseline | Below 4H EMA200 | ~20-25% loss if hit |

**Best base-rate entry: standard zone (4H EMA20).** Tactical is for high-conviction setups where you can't risk missing it; deep is for highest R:R but lowest fill probability.

### Confirmation required at entry

When the alert fires at the entry zone:
1. ✅ 4H prints higher low (no lower-low break)
2. ✅ Funding still neutral (+0.005% to +0.02%)
3. ✅ Volume on bounce ≥ volume on pullback candles
4. ✅ No daily reversal candle has printed during the pullback
5. ✅ 4H ADX still >40

If 4 of 5 confirm, take the entry. If 3 or fewer, wait for next confirmation candle.

## Targets and exits

**Conservative ladder (recommended):**
- TP1: Retest of recent high (the level the pullback came from)
- TP2: Round-number psychological extension (+5-10% above prior high)
- TP3: 1.272-1.382 fib extension of the original pump

**Cover sizing:** 30% / 40% / 30% across TP1/TP2/TP3 to lock primary profit and leave runner.

**Trail stop after TP1 fires** to entry price — converts trade to risk-free runner.

## Invalidation triggers

Exit fully (or take stop) if any of these:

1. **Funding spikes >+0.05%** — speculators arrived; real-demand thesis is dead
2. **Daily reversal candle prints** during the long position — distribution starting
3. **4H closes below the 4H EMA50** — trend broken
4. **Volume on pullback grows >> bounce volume** — distribution, not consolidation
5. **Weekly RSI hits 80+** — even spot demand can't fight weekly exhaustion forever

## Risk management

- **Sizing:** Treat as standard directional position. Don't oversize even if conviction is high — spot-driven moves still get -30% pullbacks before continuing.
- **Leverage:** 5-10x recommended; not 20x. The pullback gives you cheap entry but the trade needs room to breathe.
- **Stop placement:** Always below the structural support of the entry zone, not based on per-position margin (cross margin context — see [[Strategies/Account Configuration]]).
- **Time horizon:** Days to weeks, not hours. Don't day-trade these — the setup is a swing.

## Comparison to other strategies

| Setup | Funding signature | Entry timing | This strategy applies? |
|-------|-------------------|--------------|------------------------|
| **Spot-driven parabolic** | Neutral (+0.005-0.02%) | LONG on pullback | ✅ THIS one |
| Long-crowded blow-off top | **Heavily positive (+0.10%+)** | SHORT the parabolic | ❌ Use catalyst-pump short framework |
| Short-crowded squeeze setup | **Deeply negative (-0.10%+)** | LONG the squeeze (Viktor's Crime Coin Long) | ❌ Use [[Strategies/Crime Coin Checklist]] |
| Catalyst-news pump | Negative funding builds AFTER pump | SHORT after distribution candle | ❌ Use APE-style framework |
| Sector breakout | Mixed; check correlation | Trade with the sector | ❌ Different category |

## Worked example — ZBT (2026-04-26)

ZBT pumped +49% on the day, +80% from baseline, +118% on weekly. Daily RSI 86.4 rising, BB above upper band on D and 4H, ADX 47.48 (D) and 61.73 (4H) — all classic exhaustion-extension signals that would normally indicate a SHORT candidate.

But funding stayed at +0.005% baseline through the entire pump:

| Time | Mark | Funding |
|------|-----:|--------:|
| Pre-pump | $0.14 | +0.005% |
| Mid-pump | $0.19 | +0.005% |
| Local high | $0.276 | +0.005% |
| Live | $0.252 | +0.005% |

Comparison to actual short candidates (BSB, AGT) the same day:
- BSB: +112% pump → funding spiked to +0.192% (long-crowded — short candidate ✓)
- AGT: +115% pump → funding rose to +0.124% (long-crowded — short candidate ✓)
- **ZBT: +80% pump → funding stayed at +0.005% (spot-driven — LONG candidate)**

**Conclusion:** ZBT initially screened as a parabolic short, but the funding signature inverted the read. It's a long candidate on pullback to $0.215 (1H EMA20) or $0.168 (4H EMA20), not a short at $0.252.

This was the catalyst that surfaced the "Spot-Driven Long" framework as a distinct strategy, separate from existing parabolic-short and crime-coin-long frameworks.

See [[Coins/ZBT]] for full setup detail.

## Lessons / patterns observed

- **The funding signature is the entire trade direction call.** Same chart pattern (parabolic + RSI extreme + BB stretched) can be a SHORT or a LONG depending purely on funding. Don't trade the chart in isolation.
- **Spot-driven parabolics have lower base-rate of immediate top-printing** than perp-speculator pumps. Real money doesn't capitulate at RSI 86 the way leverage longs do.
- **The pullback always comes** on a parabolic, regardless of whether it's spot-driven or perp-driven. The difference is what happens AFTER the pullback: spot-driven resumes the trend; perp-driven distributes lower.
- **Patience is the entire edge.** The trade is missed entirely if you chase. The trade is asymmetric R:R if you wait for the alert.

## Open follow-ups for this framework

1. **Build base-rate data:** Track how many spot-driven setups (5+ signals match) actually deliver the post-pullback continuation vs how many fail. Need 5-10 worked examples to validate.
2. **Define the failure mode more precisely:** What does the chart look like when a "spot-driven long" actually fails? Funding flipping positive seems to be the main tell — verify against future failures.
3. **Establish position sizing convention:** Right now suggested as "standard directional" — refine based on outcomes.
4. **Cross-reference with [[Narratives/]]:** Does sector membership change the setup quality? (e.g., spot-driven RWA token vs spot-driven memecoin)

## Change log

- **2026-04-26** — Framework created from ZBT screen. First worked example: [[Coins/ZBT]] (monitoring, no entry yet).



---

## First failed worked example — ZBT (2026-04-26)

After ZBT was identified as the canonical example of a Spot-Driven Long candidate, the trade was entered at $0.2268 on what looked like a clean pullback to $0.215-0.220 zone (1H EMA20 area). Trade immediately moved against position from $0.227 → $0.169 (-25%), bounced back to $0.193, and stopped out at $0.190 for a realized loss of **~−$202**.

See [[Coins/ZBT]] for full trade timeline and post-mortem.

### What this teaches the framework

**Failure mode #1 identified: Spot demand can disappear without funding signaling it.**

The framework's core assumption was: *flat funding through a parabolic pump = spot demand intact = price will resume after technical pullback.*

ZBT demonstrated this assumption is INCOMPLETE. Funding rate is a LAGGING indicator of positioning — it only moves significantly when there's a critical mass of new perp positions imbalanced. If spot demand simply stops without speculative perp positioning building up first, funding stays flat while price still drops.

**Implication:** Flat funding is **necessary but not sufficient** evidence of spot-driven demand. Need supplementary real-time confirmation.

### Updated entry confirmation rules (post-ZBT)

Previous rule #1 was: *"Pullback to $0.215 or $0.168 with 4H higher low forming (no LL break)"*

This was interpreted too loosely on ZBT — entry was triggered by price tagging the 1H EMA20 zone, not by a confirmed structural higher low.

**STRICTER REPLACEMENT:**

Entry confirmation #1 (REVISED): **Require a printed 4H higher low.** Specifically:
- Wait for first 4H bounce candle off the pullback zone
- Wait for second 4H pullback that holds ABOVE the first 4H bounce low
- ONLY enter after the second pullback completes and the 4H closes above the prior bounce low

This is structural (not price-touching-EMA) and requires actual bullish 4H structure to print before entry. **Touching a moving average is NOT a structural higher low.**

### Additional supplementary confirmation (new requirement)

Beyond funding being flat (necessary), one of the following supplementary signals should also confirm:

1. **Spot venue volume holding above 24h average** during the pullback — verifies real spot interest
2. **Spot orderbook bid depth visible** — checked manually (not automatable easily but worth eyeballing)
3. **Sector peers also showing spot-driven structure** — if other coins in same narrative basket are flat-funding-pumping, more confidence in the regime
4. **Perp/spot price parity maintained** during pullback — perp shouldn't go to a discount vs spot (would indicate perp shorts piling in, which would normally push funding negative — but if spot is illiquid, the signal might lag)

Without ONE of these supplementary signals, the trade is downgraded from "high conviction Spot-Driven Long" to "speculative long pullback" — sized smaller (max $20-30 margin) or skipped.

### Updated worked example score

| Trade | Result | Notes |
|-------|--------|-------|
| ZBT (2026-04-26) | **LOSS −$202** | Failure mode #1: spot demand evaporated without funding signal lag |

**Worked examples tracked: 1 of 5-10 needed for base-rate validation. Current win rate: 0%.**

The framework remains a valid hypothesis but requires more validation runs before being assigned conviction sizing. Until 5+ setups are tracked, treat any Spot-Driven Long as **probe-sized only** ($30-50 margin max), with strict adherence to the updated confirmation rules.

### Discipline lesson

**Don't trust new frameworks before validation.** Spot-Driven Long had ONE worked example to validate against (ZBT) and it failed. Going forward:
- New frameworks require 5+ tracked setups before being eligible for conviction sizing
- During validation phase, all entries are probe-sized
- Failure modes get documented immediately and inform next iteration

This is the correct epistemic stance for a freshly-derived framework. **The framework is a hypothesis, not a recipe.**

### Change log update

- **2026-04-27** — First failed worked example (ZBT) added. Entry confirmation rules tightened to require printed 4H higher low. New failure mode #1 documented. Supplementary confirmation requirement added. Framework status downgraded to "validation phase" — probe-sized only until 5+ examples tracked.


## Cross-references


- [[Strategies/Order Execution Protocol]] — gates ALL order placement under this strategy: long entries, stop placement, TP placement, scale-ins. Always propose levels and wait for explicit user confirmation before placing.
