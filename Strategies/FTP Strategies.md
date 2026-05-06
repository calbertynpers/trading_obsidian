---
wing: strategies
type: strategy
status: active
regime:
  - all
tunnels:
  - Strategies/Squeeze Environment Playbook
  - Strategies/Crime Coin Checklist
  - Narratives/Crime Coins
---

# FTP Trading Strategies

## What is FTP (Fade The Pump)?

Short overextended low-cap altcoin pumps that have no fundamental backing. Target coins with whale-controlled supply, no real narrative, and repeating pump-dump cycle patterns. Enter short after the pump, profit on the dump back to base.

---

## Strategy A: Hold (Default)

Do nothing. Thesis intact, funding favorable, volume exhausting. Let the dump play out.

**When to use:** Volume declining on pump, funding positive or neutral, historical pattern strongly supports dump.

---

## Strategy B: Scale-Out and Re-Short (AVOID unless high conviction)

Close 50% of short during pump, re-short at higher price. Blended entry improves.

**The trap:** Each cycle realizes losses permanently. Commissions both ways. If you do this 2-3 times, cumulative realized losses may exceed what the dump recovers. Also resets liquidation price higher.

**Critical rule:** Re-short must be SAME SIZE or smaller. Never add size.

**Total cost accounting:** Track cumulative realized losses across all reshort cycles per position. If that number exceeds what a reasonable dump would recover, the trade is broken.

---

## Strategy C: Hedge Long at 50% (PREFERRED pump response)

Open a long at 50% of short size during a relief dump within the pump.

**Why this beats Scale-Out and Re-Short:**
- No realized losses on the short — original position stays intact
- The long is a separate trade that can be profitable on its own
- If pump continues, the long makes money instead of you eating losses
- Lower total margin than closing and re-opening
- Original entry price on the short is preserved

**Entry timing for the long:**
- Wait for a 10-15% pullback within the pump (relief dump)
- Volume declining on the pullback (profit-taking, not real dump)
- RSI pulling back from overbought but still above 50

**Discipline:** Have a TP on the long (prior pump high or exhaustion level). Don't hold both sides indefinitely in chop.

---

## Strategy D: Close Position

Full exit. Realize the loss/profit and move on.

**When to use:** 2+ kill signals triggered. Funding trap eating profits. Thesis broken.

---

## Strategy E: Funding-Aware Sequential Entry

Enter long-only during the funding farm phase (deeply negative funding = shorts overcrowded, pump likely). Collect funding on the long. Flip to short when top detector confirms exhaustion.

**Phase 1 — Long entry (funding farm):**
- Trigger: funding below -0.1%, pump active, volume still present
- Enter long only. You're collecting funding every 8h.
- Size: half-size. This is a tactical play.
- TP: prior pump high or when top detector scores 7+

**Phase 2 — Flip to short (top confirmed):**
- Trigger: top detector scores 9+, OR funding normalizes toward zero
- Close long (realize profit from pump + funding collected)
- Open short at the same price. Funding is normalizing.

---

## Strategy F: Long-Horizon FTP (Set and Forget)

Enter short after the first major dump confirms the pump-and-dump pattern. Use low leverage (3-5x MAX). Don't touch it for weeks. The dump to zero is inevitable.

**Entry criteria (stricter):**
1. At least one full pump-dump cycle completed (>70% dump from peak)
2. Enter on dead cat bounce, at or near resistance
3. Leverage: 3-5x MAXIMUM — must survive 100%+ interim pumps
4. Size: small enough that 100% move against doesn't breach wallet reserve

**Funding budget:** Calculate max funding cost for 3 months. If 3-month cost exceeds 50% of expected profit, don't enter.

**Management:** NO resets. NO hedging. NO churn. Check weekly, not daily.

---

## Strategy G: Long the Crime (Ride the Manipulation)

Instead of shorting the pump, go long on coins identified as manipulated. Collect funding, ride the squeeze, only flip short after the climax top.

**Identification signals (3+ required):**
1. Uncorrelated/inversely correlated with BTC/market
2. Inorganic price action (flat then brutal vertical moves)
3. Grinding upward with no drawdowns against weak market
4. Very low mindshare relative to valuation
5. Heavily negative funding rate (especially hourly, -1000%+ annualized)
6. Not listed on Hyperliquid (>95% of worst crime coins aren't on HL)
7. Primary spot volume on Bitget
8. TWAP activity visible in orderbooks
9. Low on-chain liquidity, one-sided LP ranges
10. BSC/BNB Chain token

**Sizing:** Small positions only (≤5% of wallet). Asymmetric bets. No tight stop losses.

**When to flip short:** Wait for clear climax squeeze (massive vertical candle, volume spike, liquidation cascade). Short after climax should be immediately comfortable.

---

## Strategy H: Full Lifecycle — Long the Pump, Short the Dump

The complete trade. Go net long during manipulation phase, collect funding, scale out into climax, flip short after top, protect short with profit-funded stop ladder.

**Phase 1 — Net Long:** Ride the crime. Collect funding. Be patient.
**Phase 2 — Scale Out:** Close 50% into the squeeze. Bank profit.
**Phase 3 — Flip Short:** Short funded entirely by long-side profits.
**Phase 4 — Ride the Dump:** Staged profit-taking as price falls.

**The Stop Ladder (calibrated to long-side profits):**
- Stop 1 (tight): Above squeeze high. Loss if hit: ~5-10% of banked profit.
- Stop 2 (breakeven): Short entry price. Net result: still up 100% of long profits.
- Stop 3 (house money floor): 50% of long profits consumed. Hard floor.
- Stop 4 (absolute max pain): 100% of long profits consumed. Walk away flat.

**The discipline:** Stop ladder is non-negotiable. The long phase funds the short phase. If you remove stops, you're back to naked FTP shorting.

---

## Kill Signals — When to Exit a Short

If 2+ trigger simultaneously, take action immediately:

1. **Price Breakout**: Price held above historical resistance for 48h+ with sustained volume
2. **Funding Trap**: Funding rate below -0.5% (shorts getting farmed)
3. **Wallet Risk**: Available balance below $4,500
4. **Trend Reversal**: 4h ADX > 30 with +DI >> -DI (confirmed bullish trend)
5. **Volume Confirmation**: Volume increasing on new highs (fresh buying)

## Exhaustion Signals (Dump Confirmation)

- Volume declining on each successive candle (96%+ collapse from peak = strong)
- Upper wick rejections on 4h candles (>50% upper wick)
- RSI divergence: price new high, RSI lower high
- MACD bearish crossover on 4h
- Stochastic rolling over from overbought
- Funding flipping positive (shorts collecting)

## Position Sizing Rules

- Never exceed original position size on reload/re-entry
- Hedge longs must be smaller than the short (50% max)
- Total margin per position should leave wallet reserve above $4,500
- Funding rate above -0.5% is a hard gate for short entry


## Cross-references


- [[Strategies/Order Execution Protocol]] — gates ALL order placement under this strategy: short entries, stop placement, TP placement, exits. Always propose levels and wait for explicit user confirmation before placing.
