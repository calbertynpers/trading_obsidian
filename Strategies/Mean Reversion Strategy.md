---
wing: strategies
type: strategy
status: active
regime:
  - ranging
  - high-volatility
  - post-flush
tunnels:
  - Strategies/Long Bottom-Fishing Strategy
  - Strategies/Overnight Risk Protocol
---

# Mean Reversion Strategy

## Thesis

When a crypto asset experiences a sharp, momentum-driven flush — characterised by extreme RSI readings, price trading below the lower Bollinger Band, and heavy capitulation volume — it tends to snap back toward its short-term mean (typically the daily EMA20 or EMA50). This strategy exploits that snapback with a disciplined entry, defined stop, and scaled exits at 1R, 2R, and 3R levels.

This is a **counter-trend bounce trade**, not a structural reversal play. The target is the mean (EMA20), not a new high. Position sizes should be small. Speed of recovery matters — if the position doesn't move within 24–48 hours, something is wrong.

**This strategy works best in:**
- Post-capitulation environments (violent single-day dumps of 15–25%+)
- Ranging or consolidating macro conditions (not in active bear cascades)
- Tokens with meaningful liquidity (>$1M daily volume) so entries and exits are clean

**This strategy does NOT work well in:**
- Active macro bear markets or BTC in freefall
- Tokens with impending unlock events or death spiral tokenomics
- Low-liquidity pairs where spreads eat returns

---

## Entry Criteria — All Must Be Present

An agent scanning for mean reversion setups should require ALL of the following before flagging a candidate:

### 1. Extreme Oversold RSI (Primary Signal)

| Timeframe | Threshold |
|-----------|-----------|
| Weekly RSI | < 25 |
| Daily RSI | < 30 |
| 4H RSI | < 25 |
| 1H RSI | < 30 AND rising (early exhaustion signal) |

The 1H RSI must be **rising** (not just low) — this is the key signal that selling pressure is exhausting. A low RSI that is still falling means capitulation is not complete.

### 2. Price Below Lower Bollinger Band (Daily)

Price must be trading **at or below the lower Bollinger Band** on the daily chart (20-period, 2 standard deviations). This confirms statistical overextension from the mean.

### 3. Single-Day Flush of 15%+ OR Multi-Day Decline of 20%+

The setup requires a meaningful deviation from the mean. A gentle 5% drift lower is not a mean reversion opportunity. Look for:
- A single candle down 15–25%+ (panic flush), OR
- A 3–5 day decline of 20%+ with daily RSI dropping below 30

### 4. Candle Wick Evidence

The trigger candle (or the candle immediately following) should show a **lower wick of at least 10% of the candle range**, indicating intraday buyers stepped in. This is evidence of absorption — the flush found buyers.

### 5. Volume Confirmation

Volume on the flush candle should be **elevated relative to the 7-day average** — panic selling drives volume. If volume is flat on a big down move, the move may continue (no climax).

### 6. Macro Check (Agent Must Verify)

Before entering, check:
- Is BTC currently down more than 5% on the day? → **WAIT** (systemic risk, not coin-specific flush)
- Is the token's sector narrative intact? → If the whole sector is crashing, skip
- Is there an active unlock or major negative news catalyst? → Skip (fundamental, not technical)

---

## Entry Execution

**Entry type:** Market order on confirmation of 1H RSI turning upward from below 25, OR limit order placed at the low of the flush candle (anticipatory entry for better R:R)

**Leverage:** 3–5x maximum. Mean reversion against a bearish trend requires room to breathe. High leverage will stop you out on the wick before the reversal.

**Position sizing:** Size for collateral, not notional. The collateral committed to this trade should represent no more than 1–2% of total portfolio value. The leveraged notional will be 3–5x that.

---

## Targets — Scaled Exit (1:2:3 R Structure)

The mean reversion target is the **daily EMA20**. Set three take profit levels:

| Exit | Price Level | Quantity | Rationale |
|------|-------------|----------|-----------|
| TP1 | Entry + 1R | ⅓ of position | Lock in first profit, reduce risk |
| TP2 | Entry + 2R | ⅓ of position | Midpoint toward EMA20 |
| TP3 | Entry + 3R (or daily EMA20, whichever comes first) | ⅓ of position | Full mean reversion target |

**R = distance from entry to stop loss**

Once TP1 is hit, move stop to breakeven on the remaining ⅔ position. This makes the trade risk-free once the first target is reached.

---

## Stop Loss

Place stop below the **next structural support level** beneath entry (not a fixed percentage). Typically this is:

- The second pivot support (S2) from TradingView pivot levels
- OR the recent swing low minus a small buffer (0.5–1%)
- Minimum risk: stop must be at least 10% below entry to avoid noise wicks
- Maximum risk: do not risk more than 15% from entry at 1x (so at 5x leverage, ensure the notional stop distance doesn't exceed 3% from entry)

**Stop is firm. Do not move it down** if the trade goes against you. Mean reversion trades either work quickly or they don't work.

---

## Exit Rules — When to Close Early

An agent monitoring a mean reversion position should trigger an early manual close if:

1. **24 hours pass with no upward movement** — if price is flat or drifting lower after 24h, the thesis is failing. Close half.
2. **BTC drops 5%+ intraday** — systemic risk overrides coin-specific setups. Close or reduce.
3. **RSI on 1H falls back below 20** — the bounce failed, capitulation resuming.
4. **New negative fundamental news** on the token (bad news = not a technical flush, fundamental breakdown).
5. **Position held 72 hours with no TP hit** — mean reversion plays are short-duration. If it hasn't moved in 3 days, close it and redeploy.

---

## Scoring Checklist (For Agent Use)

An agent evaluating a potential mean reversion candidate should score it:

| Condition | Points |
|-----------|--------|
| Weekly RSI < 25 | +3 |
| Daily RSI < 30 | +3 |
| 4H RSI < 25 | +2 |
| 1H RSI rising from < 25 | +4 (critical signal) |
| Price below lower BB (daily) | +3 |
| Flush candle 15%+ single day | +3 |
| Lower wick > 10% on flush/next candle | +2 |
| Volume elevated on flush | +2 |
| BTC flat or green today | +2 |
| No active unlock event | +2 |
| Negative funding rate (longs collecting) | +2 |

**Minimum score to flag as candidate: 18/28**
**Minimum score to enter: 22/28**

---

## Risk Management Summary

- **Max collateral per trade:** 2% of portfolio
- **Leverage:** 3–5x only
- **Max duration:** 72 hours (time stop)
- **Stop:** Hard, structural, non-negotiable
- **Scaling:** ⅓ exits at 1R, 2R, 3R
- **Move stop to breakeven:** After TP1 hit
- **Do not average down** — this is a bounce trade, not a conviction hold

---

## Relationship to Other Strategies

| Strategy | Overlap | Key Difference |
|----------|---------|----------------|
| [[Long Bottom-Fishing Strategy]] | Both go long beaten-down coins | Bottom fishing = multi-week hold, lower leverage. Mean reversion = 24–72h bounce, higher leverage, smaller size. |
| [[FTP Strategies]] | Both use RSI extremes | FTP targets shorts at overbought. Mean reversion targets longs at oversold. |
| [[Squeeze Environment Playbook]] | Both time entries carefully | Squeeze = vol breakout. Mean reversion = counter-trend snapback. |

---

## Research Basis

Strategy grounded in the following documented approaches:
- Volatility-optimised RSI mean reversion (FMZQuant, 2025): RSI < 20 on 4H combined with BB lower band break yields strongest crypto bounces
- OKX Research (2025): In crypto futures, multi-timeframe RSI confluence (weekly + daily + 4H all oversold simultaneously) is statistically rare and associated with elevated bounce probability
- ATR-based stop methodology: 2x ATR for stop, 3x ATR as initial target, recalibrated for leveraged positions

*Last updated: 2026-04-23*
