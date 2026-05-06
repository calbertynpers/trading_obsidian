---
wing: strategies
type: protocol
status: active
critical: true
last_reviewed: 2026-04-27
tunnels:
  - Strategies/Account Configuration
  - Trade Log
tags:
  - order-placement
  - stop-hunting
  - liquidity-sweep
  - fuzz-factor
  - microstructure
  - protocol
---

# Order Placement: Anti-Cluster Discipline

> **Read this before placing any TP or stop order.** Standard support/resistance levels — round numbers, prior swing highs/lows, BB upper/lower, common EMAs — are stop-hunting magnets. Orders placed AT these levels get clipped by liquidity sweeps. This protocol mandates fuzzed levels: TPs front-run the cluster, stops sit outside it.

## The problem

Market makers and large operators can see orderbook clusters. When they observe stops or TPs accumulated at obvious technical levels, they have economic incentive to:

1. Push price to the cluster
2. Trigger the stops/TPs (creating their counter-side liquidity)
3. Reverse the move

This is most pronounced on:
- **Round numbers** ($0.276, $0.30, $1.00, $0.50, $10.00, etc.)
- **Prior swing highs/lows** (today's high, yesterday's low, recent pivot)
- **Daily EMA200, BB upper/lower** (algo-traded levels, very wide visibility)
- **Whole-cent levels** for low-priced coins ($0.19, $0.20, $0.65)
- **Quarter/half levels** ($0.25, $0.50, $0.75)

Across the 2026-04-26 session, this manifested as:
- ZBT TP at $0.276 (today's high) — never reached, but the bounce attempt before the dump may have wicked toward this level then reversed
- BSB stop at $0.96 — got close to triggering on the squeeze to $0.93 high (didn't fire but illustrates the risk)
- General observation: TPs at obvious levels frequently get tagged just-shy-of and reverse

## The protocol

### Rule 1 — TPs are placed INSIDE the obvious level (front-run the cluster)

For a SELL TP (closing a long): place 0.3-1.0% **BELOW** the technical level you want to capture
For a BUY TP (closing a short): place 0.3-1.0% **ABOVE** the technical level you want to capture

| Original level | Order direction | Fuzzed level | Why |
|----------------|----------------|--------------|-----|
| TP $0.276 (selling long at today's high) | SELL | **$0.2745** (below) | Fills 0.5% earlier; you skip the wick |
| TP $0.30 (selling long at round) | SELL | **$0.2980** | Fills 0.7% earlier |
| TP $0.65 (closing short at round) | BUY | **$0.6545** (above) | Captures orders aiming for $0.65 |
| TP $0.55 (closing short at round) | BUY | **$0.5520** | Same logic |
| TP $1.00 (closing short at psychological) | BUY | **$1.005-$1.012** | Above the obvious level |

### Rule 2 — Stops are placed OUTSIDE the obvious level (survive the wick)

For a SELL STOP (protecting a long): place 1.0-2.5% **BELOW** the technical invalidation level
For a BUY STOP (protecting a short): place 1.0-2.5% **ABOVE** the technical invalidation level

| Original level | Order direction | Fuzzed level | Why |
|----------------|----------------|--------------|-----|
| Stop $0.190 (long stop at round) | SELL | **$0.184** | 3% below; survives stop-hunt wick |
| Stop $0.96 (short stop above today's high $0.93) | BUY | **$0.972 or $0.985** | Buffer for the wick that hunts $0.96 |
| Stop $0.50 (long stop at round) | SELL | **$0.485** | Below the cluster |
| Stop $1.045 (already off-round) | BUY | **OK as-is** | Already not at an obvious level |

### Rule 3 — Re-entry alerts go INSIDE the level (capture the move)

Same logic as TPs. If you want to re-enter on a squeeze to $0.95, set the alert at $0.945 — fires before the cluster sweep so you have time to act.

### Rule 4 — Always use a randomized offset on every order

Even when a level isn't obviously round, apply a small random offset (0.3-1.0% for TPs, 1.0-2.5% for stops). The randomization itself protects against pattern-recognition by adversarial systems.

**Example:** Two longs entered at the same level get different stops: position A at $0.184, position B at $0.187. If a coordinated sweep targets one, the other survives.

## Fuzz amount table

| Order purpose | Direction | Fuzz amount | Notes |
|---------------|-----------|-------------|-------|
| TP (lock profit) | INSIDE the level | **0.3-1.0%** | Earlier fill, no wick risk |
| Stop loss | OUTSIDE the level | **1.0-2.5%** | Survives stop-hunt wicks |
| Re-entry alert | INSIDE the level | **0.5-1.5%** | Pings before the cluster fires |
| Limit entry (buying a pullback) | INSIDE the support | **0.3-0.8%** above | Fills before the bounce starts |
| Limit entry (selling a bounce) | INSIDE the resistance | **0.3-0.8%** below | Fills before the rejection |

## Application checklist before placing any order

Before firing a TP or stop, run this check:

1. **Is the trigger price a round number?** (e.g., $0.50, $1.00, $10.00)
   → YES: apply fuzz, don't use the round number itself
2. **Is the trigger price the recent swing high/low or today's high/low?**
   → YES: apply fuzz away from the cluster
3. **Is the trigger price an obvious moving average or BB band?**
   → YES: apply fuzz away from the level
4. **Is the trigger price a common percentage from another level?** (e.g., exactly +5% from BB mid)
   → YES: vary by ±0.5%
5. **Is this the same level as another order you already have?**
   → YES: vary by 1-2% to avoid pattern-clustering across your own book

If none of the above apply, the level is probably not a cluster magnet. Use as-is.

## Specific application to current active book (2026-04-27)

| Symbol | Order | Current level | Risk | Suggested fuzz |
|--------|-------|---------------|------|----------------|
| **ZBT** | TP $0.276 | Today's high (HIGH cluster) | HIGH | $0.2745 (would have applied if trade were still active) |
| **ZBT** | TP $0.300 | Round number (HIGH cluster) | HIGH | $0.2965 |
| **ZBT** | TP $0.350 | Round-ish | MEDIUM | $0.3475 |
| **ZBT** | Stop $0.190 | Round number (HIGH cluster) | HIGH | $0.184 |
| **BSB** | Stop $1.04469 | Below 4H R1 ($1.06) — partially fuzzed already | LOW | OK as-is |
| **BSB** | Future TP $0.65 | Round (HIGH cluster) | HIGH | $0.6545 |
| **BSB** | Future TP $0.55 | Round (HIGH cluster) | HIGH | $0.5520 |
| **AGT** | Stop $0.0252 | Above 4H high (specific level) | LOW | OK |
| **AIN** | Stop $0.07545 | Specific number (already fuzzed-style) | LOW | OK |
| **APE** | Stop $0.175 | Above today's high $0.1707 | LOW | OK |

Note: Existing orders are NOT being modified retroactively to avoid order churn. New protocol applies to all orders placed FROM 2026-04-27 onwards.

## Why retroactive modification was rejected

Modifying live orders has costs:
- Cancel+replace creates microsecond exposure where no order is active
- Each modification is a round-trip API call (rate limit consumption)
- Multiple modifications per trade can confuse mental tracking
- The fuzz factor's value is on AVERAGE across many trades, not on any single trade

Going forward, the fuzz convention is mandatory for new orders. Existing orders ride out their current placement.

## Lessons captured

- **Cluster sniping is a real microstructure phenomenon, not paranoia.** It's a documented behavior of large operators in liquid futures markets.
- **The fix is mathematical, not psychological.** Apply the fuzz convention mechanically, don't try to predict each trade individually.
- **Variability across your own book matters too.** If all your stops are at round numbers, you become an easier target for any actor watching your account flow.
- **Small offsets compound.** A 0.5% earlier TP fill that adds up across 50 trades = ~2-3% extra annualized PnL. A stop that survives the wick on 1-in-5 trades = avoiding 20% of unnecessary stop-outs.

## Change log

- **2026-04-27** — Protocol created. Triggered by user observation across 24h of trading that TPs were getting tagged just-shy-of and reversing, and stops were getting hit by wicks that immediately reversed. Multiple specific examples in [[daily/2026-04-26]]. ZBT and BSB orders specifically diagnosed.


## Cross-references


- [[Strategies/Order Execution Protocol]] — **gates the placement step**: this doc defines WHERE to set the level (fuzz factor); Order Execution Protocol defines the CONFIRMATION REQUIRED before the order is placed at that level.
