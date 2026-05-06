---
wing: coins
type: coin-profile
symbol: TAO
status: active
narrative:
  - AI Infrastructure
strategy:
  - Long Bottom-Fishing
  - Popular Coin Recovery
position: long
leverage: 20
last_reviewed: 2026-04-22
tunnels:
  - Narratives/AI Infrastructure
  - Strategies/Long Bottom-Fishing Strategy
  - Strategies/Popular Coin Recovery
  - Trade Log
  - daily/2026-04-22
tags:
  - ai-infrastructure
  - bittensor
  - covenant-rug
  - etf-catalyst
  - two-layer-structure
  - cross-margin
---

# TAO — Bittensor

## Project Snapshot

Bittensor — decentralized AI / machine-learning protocol with subnet architecture. Large-cap AI infrastructure play. TAO is the gas/governance token, staked across subnets that earn emissions for producing AI services.

See [[Narratives/AI Infrastructure]] for sector context.

---

## Evolving Thesis (as of 2026-04-22)

Writing this down because the thesis has layers and is moving:

1. **Covenant rug created an artificial dislocation.** Subnet leader stepped away Apr 10, price $340 → $260 on the FUD. The rug damaged narrative but didn't break the protocol. Current $245 reflects sentiment damage, not protocol damage.
2. **Social sentiment is cooling — but early days.** Capitulation hasn't finished. Cooling CT attention is the classic mid-cycle signal: the longs who can't take pain are shaking out, not the bottom yet but the zone is getting close.
3. **Subnet teams are now *incentivized* to rebuild.** The Covenant rug is bearish for the rugger, structurally *bullish* for the remaining operators — they get a reputation premium for being the ones who didn't walk.
4. **ETF on the horizon is a structural upside catalyst.** Not priced in at all at current levels. If this confirms, the whole 2025 AI-infrastructure narrative re-rates off TAO as the anchor asset.
5. **Daily chart shows death cross + MACD bearish.** Chart is not ready yet. But thesis is about accumulating *before* the chart confirms, not chasing after.

**Thesis invalidation:** daily close below **$180**. That's where "Covenant damage was structural after all" becomes plausible and the subnet narrative is genuinely broken.

---

## Current Chart (2026-04-22)

BINANCE:TAOUSDT:

| TF | Price | Move | RSI | Signal |
|----|-------|------|-----|--------|
| 1W | $243.9 | +1.8% | 47.0 (rising) | Neutral; structure bearish but MACD early-bullish |
| 1D | $243.9 | -0.1% | 41.2 (falling) | **Bearish** — death cross EMA50 < EMA200, MACD bearish |
| 4h | $244.1 | +1.3% | 46.9 (rising) | **Bearish alignment** — price < EMA20 < EMA50 |
| 1h | $244.1 | +0.5% | 48.5 (rising) | **Bearish** — below 20 EMA ($244.36) |
| 15m | $244.1 | +0.5% | 51.9 (rising) | Neutral — small bounce attempt |

**Multi-TF alignment: MOSTLY BEARISH, net -3, high confidence.**

**Levels:**
- Overhead: 4h EMA20 $245 · 4h EMA50 $252 · Weekly EMA20 $258 · Daily EMA50 $262 · Daily EMA200 $273 · Weekly EMA50 $297
- Below (Layer 2 tranche zone): $225 · $210 · $200 · $192 · $180 (invalidation)

---

## Position Architecture — Two-Layer Structure

### Layer 1 — "No-miss lean" (active)
- **31 TAO LONG @ $246.02** · 20x leverage · cross-margin
- Unrealized PnL: ~-$69 (-0.9%)
- Purpose: don't be flat if TAO squeezes on ETF headline / sentiment flip before the dip trade works
- Stops:
  - Stop A: **16 TAO @ $234.50** (STOP_MARKET, SELL, LONG, GTC) — algoId `2000000819101411`
  - Stop B: **15 TAO @ $225.50** (STOP_MARKET, SELL, LONG, GTC) — pre-existing order
- Full stop-out loss: -$492 if both fire

### Layer 2 — "Thesis tranches" (live GTC limits placed 2026-04-22)
Four buy limits at 20x / LONG (match Layer 1):

| Tranche | Trigger | Size | Notional | Margin @ 20x | Order ID |
|---------|---------|------|----------|--------------|----------|
| T1 | $225.00 | 20 TAO | $4,500 | $225 | `10780031639` |
| T2 | $210.00 | 30 TAO | $6,300 | $315 | `10780031676` |
| T3 | $200.00 | 40 TAO | $8,000 | $400 | `10780031737` |
| T4 | $192.00 | 30 TAO | $5,760 | $288 | `10780031916` |
| **L2 total** | — | **120 TAO** | **$24,560** | **$1,228** | — |

**Blended basis (full L1 + L2 fill):** 151 TAO · $32,187 notional · **~$213.16 per TAO**

**Critical margin math:** Full book at 20x with ~$1,606 total margin. A move from blended basis $213 to invalidation $180 = -15.5% = 310% of margin wiped. Survival depends on cross-margin equity from the rest of the portfolio. **This is a deliberate choice — lower leverage was offered and declined in favor of notional exposure and not-missing-the-move-up.**

---

## Rule Book for This Position

- **Don't add outside the ladder** — if TAO prints $218, *don't* FOMO in. Wait for T1 at $225 or further down.
- **Don't move stops wider unless thesis invalidates first** — $234.50 and $225.50 are the Layer 1 exit levels. They exist to protect margin for the Layer 2 tranches.
- **If Layer 1 stops fire, Layer 2 is still live** — that's the intended behavior. Losing Layer 1 at $234/$225 and refilling lower at $225/$210/$200/$192 = the structural plan working as designed.
- **If daily closes below $180, thesis invalidates** — revisit. Don't hold through that level assuming it'll bounce.
- **Watch for ETF catalyst and subnet rebuild headlines** — thesis accelerators. If any confirm with TAO still in the $200s, the trade gets pulled forward.

---

## Trade History (this symbol)

| Trade # | Date | Side | Size | Entry | Status | Notes |
|---------|------|------|------|-------|--------|-------|
| Layer 1 | prior | Long | 31 | $246.02 | OPEN | "No-miss lean" |
| L2-T1 | 2026-04-22 | Long (limit) | 20 | $225 | OPEN, unfilled | Thesis tranche |
| L2-T2 | 2026-04-22 | Long (limit) | 30 | $210 | OPEN, unfilled | Thesis tranche |
| L2-T3 | 2026-04-22 | Long (limit) | 40 | $200 | OPEN, unfilled | **Biggest tranche — thesis line** |
| L2-T4 | 2026-04-22 | Long (limit) | 30 | $192 | OPEN, unfilled | Wick buffer below line |

---

## Watch List

- 🔎 **ETF filings / headlines** — primary upside catalyst
- 🔎 **Subnet rebuilds** — which teams are stepping up post-Covenant?
- 🔎 **$200 defense** — how does price act when T3 gets tested? Clean bounce = thesis working. Knife through = thesis in question.
- 🔎 **$180 invalidation** — hard line. Daily close below = revisit.
- 🔎 **Social sentiment trough** — when does CT go silent on TAO? That's usually the bottom signal.

---

## Links

- [[Trade Log]] — canonical trade records
- [[daily/2026-04-22]] — session narrative
- [[Narratives/AI Infrastructure]]
- [[Strategies/Long Bottom-Fishing Strategy]]
- [[Strategies/Popular Coin Recovery]]
