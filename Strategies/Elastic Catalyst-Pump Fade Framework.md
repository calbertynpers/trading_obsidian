---
wing: strategies
type: strategy
status: active
regime:
  - all
  - late-cycle
  - distribution
  - squeeze
tunnels:
  - Strategies/AI Meme Vaporware Cycle
  - Strategies/FTP Strategies
  - Strategies/Squeeze Environment Playbook
  - Strategies/Order Execution Protocol
  - Strategies/Overnight Risk Protocol
  - Strategies/Account Configuration
  - Coins/BAS
  - Coins/LAB
last_reviewed: 2026-05-05
tags:
  - fade-framework
  - asymmetric-hedge
  - position-sizing
  - cap-confirmation
  - elastic-build
---

# Elastic Catalyst-Pump Fade Framework

> **Concept**: Fade catalyst-driven parabolic moves with a two-stage build, regime-adjusted elasticity criteria, and hedge-as-capacity rather than hedge-as-defense. Net notional is the hard cap on directional risk; gross is allowed to expand under scrutiny when the structure justifies it. Codifies the discipline that turned BAS Phases 1-2 into +$708 and LAB into a recovered position, while specifically protecting against the BAS Phase 3 anxiety-unwind failure mode.

---

## When this framework applies

Use when ALL of these are true:

- Coin has run vertical on a discrete catalyst (news, app launch, narrative flip, partnership, listing)
- Funding signature is positive and elevated (longs paying shorts, indicating crowded long positioning)
- Open interest has saturated relative to spot float
- Local technical extremes present (RSI > 70 on 4h, BB upper band breach, distribution candle, volume climax)
- The coin fits one of: AI meme vaporware, post-launch low-float, catalyst-pump distribution

DO NOT use when:

- Coin has fundamental adoption flow supporting price (real revenue, real users, structural demand)
- Funding is negative or neutral (NOT crowded long — see [[Strategies/Squeeze Environment Playbook]])
- Major macro tailwind in motion (early bull cycle, halving year, structural risk-on)
- More than 3 attempts have been made on the same name in the prior 30 days

---

## The two-stage build

The strategy is NOT a single entry trade. It's a structured build with three distinct stages, each with different sizing logic and triggers.

### Stage 1 — Probe entry

| Parameter | Value |
|---|---|
| Size | 5-15% of max net cap ($500-$1,500 at $10k cap) |
| Leverage | Native to instrument (typically 10-20x) |
| Liquidation buffer | Must be structurally impossible to liquidate at this size given account equity |
| Trigger | Coin meets "when this framework applies" criteria |
| Purpose | Skin in the game — paying attention now, not just watching |

**Entry zone**: anywhere in the late stages of the parabolic move. Stage 1 is not the conviction trade — it's the entry ticket. The early entry is intentionally too small to matter if wrong.

### Stage 2 — Conviction add (the elastic build)

| Parameter | Value |
|---|---|
| Trigger | Elasticity criteria met (regime-adjusted, see below) |
| Size | Up to max net cap minus Stage 1 size |
| Goal | Bring blended entry within 10% of suspected top |
| Purpose | Capture the actual fade with meaningful directional size |

**Stage 2 is what makes this an "elastic" build.** Instead of catching the top on the first try, you let the move stretch, watch for cap-signature confirmation, then add into the rejection. The blended entry climbs but conviction is much higher because the cap is now confirmed by data, not assumption.

LAB execution is the canonical reference: probe at $1.94 (159 contracts), add at $3.97 (320 contracts), blended $3.30 vs $4.03 cap = within reach. The probe was small enough to absorb the full move from $1.94 to $4 without forced exit; the add was timed at the actual rejection wick.

### Stage 3 — Hedge if it extends

| Parameter | Value |
|---|---|
| Trigger | Move extends past Stage 2 add level WITHOUT cap signature confirming |
| Action | Add a LONG hedge leg, NOT additional short |
| Size | Such that net stays at or below max cap |
| Stop placement | Asymmetric stops on the LONG that cascade into bigger short on downside break |
| Purpose | Buy time for the eventual cap without forced exit |

**Stage 3 is the discipline brake.** If the cap doesn't confirm, you don't keep adding — you hedge. The hedge converts the situation from "wait and bleed margin" to "wait and stay productive." When the cap does eventually print, the hedge unwinds and you're back to full directional exposure at the original blended entry.

The hedge is also CAPACITY: holding $20k short + $10k long = $10k net is the same directional bet as $10k naked short, but when the cap confirms and the long closes, you have $20k of "shares to work with" riding the markdown without having to reload at unfavourable prices.

---

## Sizing rules

### Net notional — HARD CAP

```
Max net notional per fade attempt = $10,000
```

Net = absolute value of (long notional − short notional). This is the directional bet.

The net cap is binding always. No exceptions, no overrides. If a Stage 2 or Stage 3 action would push net above $10k, trim or skip the action.

### Gross notional — SCRUTINY TRIGGER

```
Soft guardrail: gross ≤ $30,000
```

Gross = long notional + short notional (absolute, both sides counted).

When gross > $30k, the trade must pass a 5-point scrutiny checklist:

1. **Free margin ≥ 30% of gross** — operational safety against simultaneous adverse moves on both legs during squeeze events
2. **Hedge ratio ≥ 50% of gross** — otherwise you're running a bigger naked position dressed as a hedge
3. **Net is below cap, not at cap** — gross expansion has to buy capacity, not just bigger directional exposure in disguise
4. **Funding cost acceptable for expected hold** — time-decay matters; positive-funding longs and negative-funding shorts both bleed
5. **Position can be unwound in normal liquidity** — if not, gross is a bigger problem than the cap suggests

If all five pass, the over-cap gross is justified. If any fail, trim back to within $30k.

### Stage sizing summary

| Stage | Size of net | Cumulative size |
|---|---|---|
| Stage 1 — probe | 5-15% of cap ($500-$1,500) | 5-15% |
| Stage 2 — add | up to remaining cap | up to 100% of cap |
| Stage 3 — hedge | net stays ≤ cap; gross can expand under scrutiny | net at cap; gross up to scrutiny limit |

---

## Elasticity criteria — regime-adjusted

The threshold for confirming "the cap is in" depends on market regime. Bear-skewed regimes confirm faster (low bar); bull regimes require extreme signals (high bar) because pumps tend to extend further.

### Regime classification

| Regime | Indicators |
|---|---|
| **Bear-skewed** | Macro risk-off ahead (Fed, NFP, jobs cooling) + seasonal weakness (sell in May, summer doldrums) + late-cycle altcoin tape (AI meme exhaustion, declining narrative breadth) |
| **Neutral** | Mixed macro signals, sideways BTC/ETH structure, no dominant narrative direction |
| **Bull / risk-on** | Early cycle, easy money policy, halving accumulation phase, breadth expanding, structural inflows |

### Cap-signal thresholds by regime

| Regime | Required signals | Justification |
|---|---|---|
| **Bear-skewed** | ANY of: funding > +0.20% per 4h, 1h candle wick > 50%, distribution candle on volume | Low bar — environment supports rapid breakdown; single signal often suffices |
| **Neutral** | At least 2 of: funding > +0.30% per 4h, candle wick > 60%, OI bleed > 5% from peak, 4h close failure | Mid-conviction needed; require corroboration |
| **Bull / risk-on** | ALL of: funding > +0.50% per 4h, 4h wick > 60%, OI bleed > 10%, multi-session confirmation | High bar — pumps extend; single signals get faded |

### Stage 2 add trigger

- In bear-skewed regimes: Stage 2 fires on any single cap-signal threshold
- In neutral regimes: wait for at least 2 signals
- In bull regimes: wait for the full set

### Cap confirmation (closes hedge in Stage 3)

Same thresholds, but for closing the hedge leg the bar is the same as the add trigger. Once the cap signature is confirmed, close the long hedge at market and reclaim full directional exposure.

---

## Per-attempt cost budget

```
Max realised + unrealised cost per fade attempt = $400 (4% of net cap)
```

This is the "I was wrong on this attempt" line. If a single attempt's total cost is approaching $400, the position must be trimmed or closed regardless of conviction.

The budget covers:

- Adverse MTM during the build phase
- Hedge premium (long-leg interest costs, funding paid)
- Stop-out losses if invalidation triggers
- Funding paid on adverse-direction holds

If $400 would be breached at a specific price level, that level is the framework-required SHORT-side stop. For SKYAI today: $0.92 is the budget-breach level on the current 3,500 short + 1,500 long structure.

The $400 budget is per attempt. Multiple attempts on the same name within 30 days share the same $400 budget — i.e., you don't get $400 fresh per attempt, you get $400 total across all attempts on that name in 30 days.

---

## Time stop — 1 week reassessment

```
Reassessment date = First entry date + 7 days
```

At reassessment, run this decision tree:

| Price action since entry | Decision |
|---|---|
| Broke materially below first support → thesis playing out | **Continue**: hold, ride the markdown, take TPs as planned |
| Still ranging, no resolution either direction | **Walk away**: take whatever P&L exists, exit cleanly. The cap didn't materialize this cycle. Don't add hope-based size |
| Broke above invalidation → stop already fired | **Done**: trade is closed, log the L, move on |
| Above original entry with no rollover yet | **Hold or exit at scratch**: if hedge is intact and cost-budget under control, ok to give it another 3-5 days; otherwise exit and reset |

The time stop prevents the "it'll come back eventually" trap. Markets do correct, but tradeable corrections happen within weeks, not quarters. If the move hasn't started in 7 days, the setup is wrong — not the timing.

---

## Max attempts per name

```
Maximum 3 attempts per name in any 30-day window
```

Prevents commitment escalation and concentration risk. A coin that won't roll is telling you the regime is different than your model thinks. After 3 failed attempts, walk away from that name for at least 30 days.

The 3-attempt limit is across all stages — i.e., if you opened, hedged, closed, and re-opened, that's 2 attempts. Re-hedging an existing attempt is not a new attempt.

---

## Hedge close criteria

The Stage 3 hedge closes on the FIRST of:

1. **Cap signature confirmed** per the regime-adjusted threshold (e.g., 4h close below key support + funding stays positive + OI bleed)
2. **Invalidation reached** — pre-defined level above the cap that would constitute "the cap thesis is wrong"
3. **Time stop hit** — 7 days from entry, regardless of price action
4. **Cost budget approaching breach** — if the attempt is at $300+ realised+unrealised cost and price still elevated, close hedge to take any long-leg profit and reduce gross

Hedge close criteria MUST be written down in the relevant `Coins/[SYMBOL].md` note BEFORE the hedge is opened. Discretionary "I think the cap is in" closes are forbidden — they are the BAS Phase 3 failure mode in disguise.

---

## Required pre-commitments per trade

Before any Stage 1 entry, the following must be on paper in the relevant `Coins/[SYMBOL].md` note:

- Suspected top zone (the level the 10% rule applies to)
- Stage 2 add trigger (specific elasticity criteria)
- Stage 3 hedge level and ratio
- LONG-leg stops (cascade levels and sizes)
- SHORT-leg stop (cost-budget invalidation)
- Cap-confirmation criteria (specific signals to close hedge)
- TP ladder (for the markdown phase)
- Time-stop reassessment date

Trades without these pre-commitments are not framework-compliant. They may still be taken, but log them as discretionary, not framework — different P&L attribution, different review process.

---

## Reference cases

### LAB — 2026-04-29 to 2026-05-02 — Textbook execution

| Stage | Action | Outcome |
|---|---|---|
| 1 — Probe | SHORT 159 @ $1.94 | Small, expendable |
| 2 — Add | SHORT +320 @ $3.97 | Caught rejection wick at $4.03 cap. Blended $3.30 vs $4.03 cap = ~18% from cap. Position recovered from −$194 to +$70 within 30 minutes |
| 3 — Hedge | Not needed; cap printed at Stage 2 add level |

Result: Position recovered, framework executed cleanly. Demonstrates that the small probe + late conviction add is the right structure when the cap is reachable.

### BAS Phases 1-2 — 2026-04-23 to 2026-04-24 — Successful asymmetric hedge

Net realised: +$708 across two phases. Demonstrated the directional probe with hedge structure — the inspiration for Stage 3 of this framework.

### BAS Phase 3 — 2026-04-25 — Anxiety-unwind failure mode

Net realised: −$106 (off-thesis exit during squeeze). The TP2/TP3 ladder was mechanically in place; manual closes during the bounce converted a working trade into a realised loss.

This is the failure mode this framework is specifically designed to prevent. The pre-commitment rules + cost budget + hedge close criteria all exist because of Phase 3.

### BSB — 2026-04-25 — Asymmetric stop validation

Catalyst-pump short with 51% partial stop + 49% naked runner. Validated the asymmetric structure that underlies Stage 3 hedge stops. See `[[Coins/BSB]]`.

### SKYAI — 2026-05-05 — Active validation case

Currently running. Stage 1 probe at $0.578, Stage 2 add at $0.756 (within 10% of $0.80 local top), Stage 3 hedge at $0.769 with cascade stops at $0.73262 / $0.71. Cap signature: 84.8% upper wick on 1h (one strong signal in bear-skewed regime), funding +0.11% (below threshold), OI flat. **Cap candidate, not yet confirmed.** First test case for this framework codified.

---

## Active validation watchlist

Track the next 5 fade attempts against this framework. Each one logs:

- Did pre-commitments exist before Stage 1?
- Was the elasticity criteria threshold met before Stage 2?
- Did Stage 3 fire as designed if needed?
- Was the cost budget respected?
- Did the time stop fire if applicable?
- Final P&L vs framework-modeled expected outcome

After 5 attempts, recalibrate parameters: max net cap, gross scrutiny threshold, cost budget, time-stop window, regime-threshold tiers.

| # | Coin | First entry | Status | P&L | Framework-compliant? |
|---|------|-------------|--------|-----|---------------------|
| 1 | SKYAI | 2026-05-05 | Active | TBD | Pending SHORT-side stop placement |
| 2 | — | — | — | — | — |
| 3 | — | — | — | — | — |
| 4 | — | — | — | — | — |
| 5 | — | — | — | — | — |

---

## Connection to existing strategy library

This framework codifies the practical execution of the conceptual playbooks:

- [[Strategies/AI Meme Vaporware Cycle]] — the WHY (which coins to fade, narrative-cycle timing)
- [[Strategies/FTP Strategies]] — the WHAT (fade-the-pump category)
- [[Strategies/Squeeze Environment Playbook]] — the WHEN (regime context, squeeze identification)
- **[[Strategies/Elastic Catalyst-Pump Fade Framework]] — the HOW** (this doc; sizing, staging, hedging, exits)
- [[Strategies/Order Execution Protocol]] — the discipline layer (level confirmation before placement)
- [[Strategies/Overnight Risk Protocol]] — the sleep-window safeguard
- [[Strategies/Account Configuration]] — cross-margin context for risk math

---

## Open follow-ups

1. **Calibration after 5 attempts** — review parameters once the watchlist is filled
2. **Per-attempt cost-tracking sheet** — automate so per-attempt cost is queryable rather than reconstructed
3. **Regime classification automation** — convert the bear/neutral/bull tier to a calculation, not a feel
4. **Linkage to Coins/BAS Phase 3** — formalise the "this is the failure mode this framework prevents" cross-reference

---

## Discipline statement

> *"I do not size into a fade beyond the net cap. I do not add to a position outside the pre-defined stages. I do not close a hedge outside the pre-defined cap-confirmation criteria. I do not exceed 3 attempts on a name in 30 days. The framework is the floor, not the ceiling — discretion adds discipline within it, not against it."*
