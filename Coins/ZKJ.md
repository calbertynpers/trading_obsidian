---
wing: coins
type: coin-profile
symbol: ZKJ
status: active
narrative:
  - L1-L2 Infrastructure
strategy:
  - Mean Reversion Strategy
position: long
leverage: 5
last_reviewed: 2026-04-23
tunnels:
  - Strategies/Mean Reversion Strategy
  - Narratives/L1-L2 Infrastructure
tags:
  - ZK
  - L2
  - infrastructure
  - oversold
  - mean-reversion
  - bounce-trade
---

# ZKJ — Polyhedra Network (ZKJ)

**Sector:** Zero-Knowledge / L2 Infrastructure
**Binance Pair:** ZKJ-USDT
**Last Reviewed:** 2026-04-23

## Overview

Polyhedra Network is a ZK infrastructure project building cross-chain interoperability and proof systems using zero-knowledge cryptography. ZKJ is the native token. It sits in the ZK/L2 infrastructure narrative which has been broadly depressed throughout Q1 2026 due to macro pressure and general L2 fatigue.

---

## Key Metrics (Apr 23, 2026)

| Metric | Value |
|--------|-------|
| Price at entry | ~$0.0155 |
| Entry date | 2026-04-23 |
| Original position entry | $0.01937 (existing long) |
| Mean reversion position entry | ~$0.0155 (market) |
| Daily RSI at entry | 27.0 (oversold) |
| 4H RSI at entry | 19.65 (deeply oversold) |
| Weekly RSI at entry | 19.9 (extreme) |
| Daily candle on entry day | -16.7% (flush candle) |
| Lower Bollinger Band (daily) | Price below lower band |
| Daily EMA20 | ~$0.0193 (mean reversion target) |
| Support S2 | $0.0139 |

---

## Why This Trade Was Taken — Mean Reversion Thesis

ZKJ experienced a violent single-session flush of ~16.7% on April 23 2026, with multi-timeframe RSI reaching extreme oversold territory simultaneously across weekly (19.9), daily (27), and 4H (19.65). This is a statistically rare confluence. The 1H RSI was observed rising from 16.66 to 21.76, indicating the first signs of selling exhaustion.

Price was trading below the lower Bollinger Band on the daily — confirming statistical overextension from the mean.

**This is a tactical mean reversion bounce trade, not a structural long.** The target is a snapback to the daily EMA20 (~$0.019–0.020), approximately 25% from entry.

**Risk acknowledged:** The broader trend for ZKJ is firmly bearish. Death Cross active (EMA50 < EMA200 on daily). Price trading well below all major EMAs. This trade is against the trend and sized accordingly.

---

## Active Position (Apr 23, 2026)

### Mean Reversion Trade (New — Apr 23)

| Parameter | Value |
|-----------|-------|
| Side | LONG |
| Leverage | 5x |
| Collateral | ~$15 |
| Notional | ~$75 |
| Size | 4,839 ZKJ |
| Entry price | ~$0.0155 (market) |
| Stop loss | $0.0135 |
| TP1 | $0.0175 — 1,613 units (⅓) |
| TP2 | $0.0195 — 1,613 units (⅓) |
| TP3 | $0.0215 — 1,613 units (⅓) |
| Max risk | ~$9.68 |
| Max reward | ~$19.36 |
| R:R | 1:2 (to TP2) / 1:3 (to TP3) |
| Time stop | Close if no movement by 2026-04-26 |

### Existing Long (Pre-existing)

| Parameter | Value |
|-----------|-------|
| Side | LONG |
| Entry price | $0.01937 |
| Status | -19.74% (as of entry date for new trade) |
| Strategy | Not a mean reversion trade — pre-existing position |

---

## Technical Picture (Entry — Apr 23, 2026)

**Daily:**
- RSI: 27.0 — oversold (fell sharply from 39.95 prior session — one-day capitulation)
- MACD: Bearish crossover
- Bollinger Bands: Price **below lower band** — statistically overextended
- Stochastic: K=3.88, D=4.73 — deeply oversold
- ADX: 23.81, -DI (28.53) > +DI (23.38) — bearish but not extreme trend strength
- Candle: -16.7% with 17.7% lower wick — absorption evidence
- All SMAs and EMAs above price (bearish structure)

**4H:**
- RSI: 19.65 — extreme oversold
- MACD: Bearish
- EMA alignment: Price < EMA20 < EMA50 < EMA200

**1H:**
- RSI: 21.76 — **rising from 16.66** (key trigger signal)
- This upward turn on 1H RSI from extreme levels is the entry confirmation

**Weekly:**
- RSI: 19.9 — extreme oversold
- MACD: Bullish crossover (momentum shift beginning on longer timeframe)
- Long-term structure: Bearish (death cross, price well below EMA20/50)

**Support / Resistance:**
- S1: $0.0166 (already broken)
- S2: $0.0139 — stop placed just below here
- S3: $0.0060 — catastrophic support
- Resistance R1: $0.0244 (daily EMA pivot)
- Daily EMA20: ~$0.0193 (primary target)

---

## Monitoring — Agent Instructions

An agent monitoring this position should:

1. **Check every 4 hours** while position is open
2. **Close full position immediately** if:
   - Price breaks below $0.0135 (stop triggered — do not override)
   - BTC drops more than 5% intraday (systemic risk)
   - 1H RSI falls back below 18 after entry (failed bounce)
3. **Alert on TP hits** — each TP fills ⅓ of position automatically via standing orders
4. **After TP1 hits** — confirm stop has been moved to breakeven ($0.0155) on remaining position. If exchange orders don't auto-adjust, cancel and replace.
5. **Time stop: 2026-04-26** — if no TP has been hit by this date, close the full position regardless of PnL. Mean reversion plays are short-duration.
6. **Do not add to position** — this is a fixed-size bounce trade, not a conviction build.

---

## What Success Looks Like

| Scenario | Outcome |
|----------|---------|
| TP1 hit ($0.0175) | +$3.23, stop moved to breakeven, position ⅔ size |
| TP2 hit ($0.0195) | +$9.68, position ⅓ size, at mean |
| TP3 hit ($0.0215) | +$19.36, full exit |
| Stop hit ($0.0135) | -$9.68, clean loss, no further action |
| Time stop (Apr 26) | Close at market, accept result |

---

## Narrative Context

ZKJ sits in the ZK / L2 infrastructure narrative which has been broadly depressed. No specific token catalyst was identified for this trade — it is a pure technical mean reversion play triggered by extreme multi-timeframe oversold conditions following a -16.7% flush. The lack of a fundamental catalyst is a risk: if the flush was news-driven (not purely technical), the bounce may be weaker or absent.

See [[Narratives/L1-L2 Infrastructure]] for broader sector context.

---

## Risk Factors

1. **Existing long underwater** — there is already a pre-existing ZKJUSDT long at $0.01937 that is ~20% underwater. Adding this position increases total ZKJ exposure. If the token continues to fall, losses compound.
2. **Bearish macro structure** — Death Cross, price below all EMAs. This is a trade against the trend.
3. **No fundamental catalyst** — pure technical play. If selling is fundamental (not panic), bounce may not materialise.
4. **Small cap / low liquidity** — spread and slippage can affect execution quality.
5. **Short duration** — if the bounce doesn't happen in 72 hours, it may not happen at all.

*Last updated: 2026-04-23*
