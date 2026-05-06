---
wing: coins
type: coin-profile
symbol: NAORIS
status: active
narrative:
  - Crime Coins
strategy:
  - Full Lifecycle (Long Pump → Short Dump)
position: hedged
leverage: 20
last_reviewed: 2026-04-22
tunnels:
  - Narratives/Crime Coins
  - Strategies/Crime Coin Checklist
  - Strategies/Overnight Risk Protocol
  - Trade Log
tags:
  - crime-coin
  - phase-2-precursor
  - hedged-net-long
  - new-listing
---

# NAORIS — Naoris Protocol

**Classification:** Crime Coin (7/10 signals)
**Strategy:** H — Full Lifecycle (Long the Pump → Short the Dump)
**Status:** **Phase 2 Precursor — funding flip observed, awaiting climax**
**Added:** 2026-04-21
**Last major update:** 2026-04-22 — funding flip execution

---

## Current Book (post 2026-04-22 execution)

| Leg | Size | Entry | Lev | Stop | Order ID |
|---|---|---|---|---|---|
| **Core LONG** | 12,755 | $0.06665 | 5.7x eff | $0.0285 (structural) | stop `2000000819308778` |
| **SHORT runner** | 7,500 | $0.07911 | 20x | $0.0884745 | stop `2000000816078881` |
| L1 LIMIT BUY LONG | 20,000 | $0.05639 | 20x | — | `931274429` |
| L2 LIMIT BUY LONG | 20,021 | $0.04795 | 20x | — | `933834175` |
| Structural stop | 52,755 | — | — | `$0.0285` covers all long fills | `2000000819308778` |

**Net:** currently short ~-5,255 (before new pullback fills). If L1 + L2 fill → net long ~45,266.

**Realised on the book:** `+$243` (Trade 008, 17,500 short partial close).

---

## Funding Flip — The Key Signal

| Date | Funding | Direction | Interpretation |
|---|---|---|---|
| 2026-04-21 | +0.109% | positive, increasing | Crime accumulation — longs overcrowded but setup ongoing |
| 2026-04-22 | **-0.00179%** | **negative, declining** | **Shorts piling in. Phase 2 precursor.** |

**Per the original plan:**
> *"Funding: Positive at +0.109% — longs paying ~$3.27/day. Acceptable cost. If/when shorts pile in and funding flips negative, that becomes income."*

**Plan's kill signals for the long (inverted) now reading:**
> *"Funding stays positive and increases (longs overcrowded, no short squeeze fuel)"* → **NO** — funding is negative and deepening. This is the signal we waited for.

**Plan's bull confirmation:**
> *"Bear traps (dump → shorts pile in → reversal → grind up) are bullish."*

**Net read:** we are in **early Phase 2 setup**. Not at climax yet (no vertical + volume spike + liquidation cascade), but the precursor signal fired. This is the moment the plan was designed for.

---

## Execution Pass 2026-04-22

Actions taken in one batch:

1. **Cancelled** original L2 limit (40k @ $0.04795) — replaced with halved 20k clip
2. **Cancelled** L3 limit (20k @ $0.04228) — structurally confused zone
3. **Cancelled** L4 limit (10k @ $0.02864) — thesis-broken price, belongs to a different trade
4. **Cancelled** tight long stop ($0.0634 × 12,500) — noise-level stop-hunt magnet
5. **Closed 70% of short** via market buy — 17,500 of 25,000. Realised `+$243` banked
6. **Placed new L2** — LIMIT BUY LONG 20,021 @ $0.04795 at 20x
7. **Placed structural stop** — STOP_MARKET SELL LONG 52,755 @ $0.0285 (covers all potential long fills)

Short stop at $0.0884745 left unchanged — protects the runner.

**Side effect flagged:** placing L2 at 20x pushed the NAORIS symbol-wide leverage setting to 20x, which recalculated the Core Long's effective leverage from 3.34x → 5.70x. Same position, less margin held. Not dangerous — structural stop at $0.0285 is well above liq at 5.7x — but noted.

---

## The 4-Layer Stop Structure (For This Position)

**Governing principle:** use the plan's own strategy. The note's invalidation is *"Price breaks below the March grind-up structure (~$0.03) with volume"* — so the structural auto-stop goes below that. Tighter stops contradict the "ride the crime" thesis; no stop at all ignores the possibility that the thesis is wrong.

| Layer | Type | Trigger | Action | Purpose |
|---|---|---|---|---|
| **1. Structural** | Auto order | Price hits $0.0285 | STOP_MARKET fires, closes all long | Hard invalidation — thesis broken if price below March base |
| **2. Health check** | Manual review | 1D candle closes below $0.045 | Reassess thesis, decide whether to pre-exit | Early warning — if daily structure breaks before $0.0285 |
| **3. Time-based** | Manual review | 72 hours with no reclaim of $0.07 | Reassess thesis, check funding trend | Prevents death-by-chop — if thesis is right, the squeeze shouldn't wait long |
| **4. Funding kill** | Manual exit | Funding reverts positive AND rises | Exit long on next green candle | Plan's original kill signal — if shorts give up, no squeeze fuel |

Only layer 1 auto-fires. Layers 2–4 are review prompts that force re-engagement rather than drift.

**Risk at current size (12,755) if structural stop hits:**
- ($0.06665 - $0.0285) × 12,755 = **`-$486` worst-case on Core Long alone**
- If L1 + L2 fill and stop then hits: (~$0.0489 blended × 52,755) - ($0.0285 × 52,755) = **`-$1,077` worst-case on full long book**

---

## Crime Coin Signals (unchanged from entry)

| Signal | Present | Evidence |
|--------|---------|----------|
| Uncorrelated with BTC | ✅ | BTC -1.4%, NAORIS +29% same day at peak. |
| Inorganic price action | ✅ | Flat at $0.02-$0.03, then vertical. |
| Grinding up against weak market | ✅ | TradingView: "strength in a weak market, buyers actively stepping in" |
| Low mindshare vs valuation | ✅ | $310M FDV, almost no chatter. |
| Not on Hyperliquid | ✅ | |
| Bitget primary spot | ✅ | TGE lister. |
| Low on-chain liquidity | ✅ | ~15% of supply circulating. |
| **Funding flip to negative** | ✅ **(2026-04-22)** | **Previously ❌ at +0.109%. Now -0.00179% declining. Phase 2 precursor fired.** |
| TWAP / controlled books | ❓ | Unverified |
| BSC chain | ❌ | Ethereum |

**Score: 8/10** (up from 7/10) — funding flip added a signal. Still missing confirmed TWAP/controlled books and not on BSC.

---

## Token Fundamentals (reconciliation note)

- **Vault said:** max 4B supply / 599M circulating (15%) / $310M FDV / $46.5M mcap
- **Web search (2026-04-22):** total supply 1B with 4% public at TGE Jul 31 2025
- **Unreconciled.** Either vault is stale or the sources count different things (max issuance vs cap vs redeemable). **Action item:** reconcile before Phase 3 flip-short; the supply math matters for dump targets.
- **Confirmed:** Team 20% + backers 16.23% = ~36% vesting throughout 2026. Substantial unlock overhang all year.
- **Demand-side counter:** Q1 2026 staking launch is live — some supply goes into yield-locks.

---

## Price History

| Date | Event | Price |
|------|-------|-------|
| Aug 2025 | TGE / Listing | $0.046 |
| Aug 2025 | ATH pump | $0.153 |
| Sep-Dec 2025 | Slow bleed | $0.15 → $0.03 |
| Jan-Feb 2026 | ATL zone | $0.014 |
| Mar 2026 | Grind up begins | $0.02 → $0.03 |
| Early Apr 2026 | Chop zone | $0.05 → $0.07 |
| Apr 14 | Pre-pump | $0.057 |
| Apr 21 | Pump high | **$0.078 (+29% 24h, +48% 7d)** — short entry level |
| Apr 22 | Pullback + funding flip | $0.0656 mark |

---

## Chart State (2026-04-22, MEXC feed)

**1D:**
- ADX 42, +DI dominant → trend still bullish
- Golden cross EMA50 > EMA200, price above both
- RSI 57.6 and falling — cooling, not capitulated
- Candle: 56% upper wick — rejection flavour
- 1D BB upper $0.0695, lower $0.049

**4h:**
- ADX 52 very strong +DI
- MACD just bearish crossover (histogram -0.000004)
- Pivot $0.0554, R1 $0.0604, R2 $0.069, S1 $0.0467, S2 $0.0418

**1h:**
- Below EMA20/EMA50
- Stoch 6.5/4.3 deeply oversold → bounce likely

**Volume:** 1D candle range 9.05% on 2.1M volume — meaningful move but baseline average unknown, so distribution vs orderly is unclear.

---

## Trade Plan Status — Phased

### Phase 1: Net Long (Ride the Crime) — ENTERED AND PARTIALLY UNWOUND

Original target: 50K long / 35K short / net long 15K. Actual at entry: 12,755 long / 25,000 short = net short (imbalanced toward short). Post 2026-04-22: 12,755 long / 7,500 short = net long 5,255 with pullback ladder pending.

If L1 + L2 fill → ~52,755 long / 7,500 short = **net long ~45,255**, blended long entry ~$0.0579. This is the plan's intended structure, arrived at via pullback accumulation rather than top-ticking the initial entry.

### Phase 2: Scale Out (When Climax Begins) — ACTIVE SETUP

**Current status:** Funding flip fired. 7,500 short runner positioned for the squeeze.

**Triggers to close short runner (any 2 of 4):**
- Massive vertical candle (>20% in <4h)
- Volume spike (>3x recent 4h avg) — need baseline first
- Liquidation cascade visible on liquidation heatmap
- Funding at extreme negative (< -0.05%)

**Triggers to also take long profits:**
- Same list above. When Phase 2 climax confirms, close 50% of long into the squeeze, trail remaining 50% with stop below last 4h candle low.

### Phase 3: Flip Short (Profit-Funded) — NOT YET

Defined in plan. Triggered by climax over + price fails to reclaim high + volume collapses + funding normalises.

### Phase 4: Ride the Dump — NOT YET

Staged TP at -50% below short entry, pre-pump base, trail with weekly EMA20.

---

## Key Risks

1. **Phase 2 setup is NOT Phase 2 climax.** Funding flipped but no vertical + volume yet. If the next move is a slow chop sideways rather than a squeeze, the short runner bleeds funding and the long holds but gains nothing.
2. **Supply discrepancy unreconciled.** 1B vs 4B total supply is material for FDV math and dump targets. Fix before flipping short.
3. **2026 unlock drip.** Team/backer tokens unlocking throughout 2026 is ongoing supply pressure. No discrete cliff identified but cumulative effect is real.
4. **It's on Binance.** More participants = harder to manipulate. Could be more organic than it looks.
5. **Stop-hunt risk on the long.** Structural stop at $0.0285 is deep, which is the point — but if a sharp wick prints below (e.g. a cascading long-liq event on a random weekend) and immediately recovers, we exit with the runner still in place catching the recovery down. Accept this.
6. **Overnight risk for the long stop.** Auto-stop is fine overnight (no action needed). L1 and L2 limits could fill overnight — they passed [[Strategies/Overnight Risk Protocol]] check: new listing ✅ extreme RSI ❌ (cooling) low float ✅ tier-1 VC ✅ thin book ✅ trader offline ✅ → 5/6 signals = overnight-risky. Remediation applied: tranche-laddered size, structural stop covers fills, long is thesis-aligned (pullback adds).

---

## Log

| Date | Action | Notes |
|------|--------|-------|
| 2026-04-21 | Research complete | 7/10 crime signals. Strategy H selected. |
| 2026-04-21 | Initial entry | 50K long / 35K short target @ $0.0782, 20x cross. Actual filled: 12,755 long / 25,000 short. |
| 2026-04-22 | **Funding flip observed** | +0.109% → -0.00179% declining. Phase 2 precursor fired. |
| 2026-04-22 | **Execution pass** | Cancelled L3, L4, old L2, old long stop. Closed 70% of short (realised +$243). Placed halved L2 and structural stop @ $0.0285. 4-layer stop structure documented. |
| 2026-04-22 | Supply reconciliation flagged | 1B vs 4B discrepancy — action item pre-Phase 3. |
