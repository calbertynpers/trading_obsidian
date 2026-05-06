---
wing: coins
type: coin-profile
symbol: APE
status: active
narrative:
  - NFT / Yuga Labs ecosystem
  - Catalyst-pump distribution short
strategy:
  - Catalyst-Pump Distribution Short
  - Funding-Flip Phase 2 framework
position: SHORT 5,959 @ $0.1678 (eff 20x)
leverage: 20x
last_reviewed: 2026-04-25
tunnels:
  - Strategies/Squeeze Environment Playbook
  - Strategies/FTP Strategies
  - Trade Log
tags:
  - nft
  - yuga-labs
  - catalyst-distribution
  - news-pump-short
  - whale-confirmed
  - insider-trading-context
---

# APE — ApeCoin (Yuga Labs ecosystem)

> **Status (2026-04-25):** Short into the dead-cat zone of a +90% news-driven pump. Catalyst was Yuga Labs naming Michael Figge as CEO (effective ~April 16, market priced it April 24). Distribution candle confirmed on daily (-13%, 60% upper wick). Stop at **$0.1750** (above today's bounce high), targets ladder to $0.135 / $0.115 / $0.105. Whale insider trading activity flipped short near the top — independent confirmation. Funding deeply negative (−0.687% peak at 2026-04-25 00:00 UTC) = squeeze fuel mostly burned.

## Project Snapshot

ApeCoin (APE) is the governance token of the ApeCoin DAO, originally a Yuga Labs-affiliated ecosystem token tied to Bored Ape Yacht Club, MAYC, ApeChain, and adjacent NFT properties. Token has been in a multi-year downtrend; weekly EMA200 is at $2.24 vs price $0.16. Long-term structurally bearish, dependent on narrative-driven catalysts for short-term moves.

**Exchange feeds**: Binance has BASUSDT — use `BINANCE:APEUSDT` for chart reads. (Spot trading widely available across major venues.)

---

## The catalyst — Yuga Labs leadership change

**Effective ~April 16, 2026:** Yuga Labs named **Michael Figge** as CEO (former head of product), with co-founder **Greg Solano** moving to board chairman alongside the original 9GAG co-founder. Confirmed publicly on **BAYC's 5th anniversary**.

The market priced it on **April 24** with a 90% spike from $0.10 → $0.19 (intraday high $0.28), volume +6,031% past $1B, derivatives volume +6,460% to $2.9B, OI +228% to $119M.

Reaction signature:
- Pure speculative-derivatives flow (spot didn't lead, it followed)
- $82.69M total liquidations in the move ($45.6M longs + $37.08M shorts)
- News articles framed Figge appointment as "the most substantive catalyst APE has had in over a year" — bullish framing acknowledged
- **Whale insider trading**: per Onchain Lens + Lookonchain, an account deposited 75 ETH (~$174K), longed APE before the news for **+$1.79M (14x)**, then immediately **flipped short for another +$488K**. Total **$2.27M / 14x return**. Independent confirmation that smart money treated it as a one-event catalyst, not a sustained re-rating.

---

## Position

| Leg | Size | Entry | Mark (live) | uPnL | Eff Lev | Notional | Margin |
|-----|------|-------|-------------|------|---------|----------|--------|
| **SHORT** | 5,959 | $0.1678 | ~$0.16061 | **+$42.84 (+4.28%)** | 20x | $957 | $47.85 |

### Live orders

| Order | Type | Trigger | Size | Purpose | Algo ID |
|-------|------|---------|------|---------|---------|
| Pump-confirm stop | STOP_MARKET (BUY SHORT, reduce-only) | $0.17500 | 5,959 (full) | Above today's bounce high; close if dead-cat invalidated | 2000000837193746 |

**TP ladder (planned, NOT yet placed):**
| TP | Trigger | Size | Profit if hit |
|----|---------|------|--------------:|
| TP1 | $0.135 | 2,000 | **+$65.60** |
| TP2 | $0.115 | 2,400 | **+$126.72** |
| TP3 | $0.105 | 1,559 | **+$97.34** |

Total if all three fill: **~+$290** (vs current +$43).

---

## Strategy — Catalyst-Pump Distribution Short

### Thesis

A leadership-change catalyst with no immediate cash-flow or token-utility impact pumped a structurally-broken token by 90% in hours. Volume profile (derivatives-dominant) and on-chain positioning (whale flipped short) both signal **distribution at the top, not accumulation**. Price returns to ~50-60% retrace of the move once narrative excitement decays.

### Five-stage decay framework (this is the playbook)

| Stage | Description | Status (2026-04-25) |
|-------|-------------|---------------------|
| Day 0 | News drops, +50-90% spike | ✅ April 24, $0.10 → $0.28 high |
| Day 1 | Distribution candle, long upper wick, RSI exhaustion | ✅ Daily -13%, 60% upper wick, RSI 86 → 71 |
| Day 2 | Dead-cat bounce; funding goes deeply negative as fader-shorts pile in | ✅ Bounce $0.152 → $0.171; funding −0.687% peak |
| Day 3-5 | Lower high prints; true markdown to 50-60% retrace | ⏳ Pending — watch for failure to take out $0.180–$0.185 |
| Day 5-10 | Stabilization at new equilibrium near pre-news baseline | Target zone: $0.10–$0.13 |

### Mechanics that confirm the setup

1. **Catalyst quality test** — does the news change cash flows, token utility, or only narrative? CEO appointment = narrative only. ✅ Catalyst-pump signature.
2. **Volume profile test** — does spot lead derivatives, or vice versa? Derivatives +6,460% vs spot follow-through. ✅ Speculative.
3. **Whale activity test** — what are the bigger accounts doing? Insider longed-then-flipped-short. ✅ Smart money confirms fade.
4. **Funding signature test** — does funding flip negative on the way up (squeeze coming) or stay positive (real demand)? Peaked at −0.687%. ✅ Crowded short during pump = squeeze fuel that's now mostly burned.
5. **Structural test** — is the asset in a multi-year downtrend with no fundamental shift? Weekly EMA200 at $2.24 vs price $0.16. ✅ Long-term bear, news doesn't reverse multi-year structure.

All five tests fired. This is a textbook setup.

### Funding history (squeeze fuel monitor)

| Time (UTC) | Rate | Mark | Read |
|------------|-----:|-----:|------|
| 04-23 16:00 | +0.0038% | $0.103 | Pre-news baseline (slightly long) |
| 04-24 00:00 | +0.009% | $0.102 | Last positive reading |
| 04-24 08:00 | **−0.067%** | $0.112 | Move starting; shorts piling in |
| 04-24 16:00 | **−0.251%** | $0.174 | Heavy short crowding during pump |
| **04-25 00:00** | **−0.687%** | $0.181 | **Local-top short positioning extreme** |
| 04-25 08:00 | **−0.191%** | $0.185 | Persistently negative |
| 04-25 16:00 | **−0.126%** | $0.154 | Decaying after the dump candle |
| Live (~20:00) | **−0.148%** | $0.165 | Still meaningfully negative |

**Read:** Peak short positioning (−0.687%) likely already burned at the local top. Funding has been persistently negative for 24+ hours but the *peak* is in. Squeeze risk diminishing daily.

---

## Levels reference

**Resistance (short defends; if these break, thesis weakens):**
- $0.16500 — current mark
- $0.16690 — 1H EMA20 (just rejected, acted as resistance)
- $0.16780 — entry (psychological)
- **$0.17070** — today's intraday high
- **$0.17500 — pump-confirm stop (LIVE)**
- $0.18000–$0.18500 — 4H supply zone (real "thesis broken" level; daily reversal candle invalidated above here)
- $0.18860 — 2026-04-23 high (prior pivot)
- $0.22000 — daily EMA200 (long-term resistance ceiling)
- $0.22270 — daily intraday high during pump
- $0.28 — 6-month high during euphoria spike

**Support (TP zones; markdown targets):**
- $0.15240 — daily intraday low
- $0.13500 — **TP1 target** (4H R1, prior pivot)
- $0.13290 — 4H R1 reference
- $0.12000 — 4H R2 reference
- $0.11500 — **TP2 target** (intermediate support)
- $0.10500 — **TP3 target** (overshoot beyond pre-news baseline)
- $0.10000 — pre-news baseline; psychological floor
- $0.07630 — 4H S1 (deep mean-reversion target if narrative fully breaks)

---

## Cycle-shift / Invalidation markers

**Trade is invalidated if any of these fire:**
1. **4H closes above $0.175** with body strength → narrative re-ignites; stop fires automatically
2. **Fresh news catalyst** within days (Figge announces product roadmap, NFT-tied utility, partnership, etc.) → re-evaluate; thesis depends on the move being a one-event spike
3. **Funding flips positive sustained** → peak-short position has unwound; squeeze risk gone but so is the crowded-short fade signal — re-evaluate setup quality
4. **Daily close above $0.180** with above-avg volume → daily reversal candle from 04-24 invalidated; bullish continuation possible
5. **Whale wallet on-chain trackers show insider closing the short** → smart money out; should follow

**Trade is confirmed if:**
1. **Lower high on 4H** below $0.1707 in next 6-12 hours → bounce stalled
2. **4H RSI fails to reach 70** on the bounce leg (currently 60.14)
3. **Volume on bounce attempts shrinks** → speculators losing interest
4. **Funding stays negative but stops getting MORE negative** → peak short positioning has passed (already happening — in progress)
5. **4H closes back below $0.152** → reclaim of the breakdown level fails

---

## Probability bands by Sunday close (per user thesis: $0.11 by Sunday)

| Outcome | Probability |
|---------|------------:|
| $0.13 by Sunday close (base case — first support test) | ~55% |
| $0.115 by Sunday close (extended capitulation) | ~30% |
| $0.11 by Sunday close (user's call — needs cascade) | ~15-20% |
| Wick to $0.10 intraday on Sunday liquidity vacuum | ~10% |
| Bounces to $0.18+ instead (squeeze wins; stop fires) | ~15% |

**Direction: ~75% probable.** **Magnitude (full $0.11 by tomorrow): ~20% tail.** Both worth respecting.

---

## Open follow-ups

1. **Place TP ladder** ($0.135 × 2,000 / $0.115 × 2,400 / $0.105 × 1,559) to convert directional bet into structured exit. Pending user confirmation.
2. **Watchdog** — consider lighter-weight hourly check (4H lower-high detection, funding sign flip, stop proximity).
3. **Whale wallet monitoring** — find the insider's address from on-chain trackers; alert on close of their short.
4. **Re-entry plan** — if stops fire and APE re-rallies above $0.18, look for next dead-cat at $0.20+ for re-entry on second distribution candle.

---

## Trade History (this symbol)

| Trade # | Date | Side | Size | Entry | Exit | P&L | Outcome |
|---------|------|------|------|-------|------|-----|---------|
| 012 | 2026-04-25 | Short | 5,959 | $0.1678 | (open) | **+$42.84** uPnL | RUNNING — stop $0.1750, TP ladder pending |

---

## Devil's Advocate

1. **Catalyst could compound.** If Yuga Labs announces a product roadmap, NFT utility upgrade, or partnership in the next week, the news cycle re-fires and APE could break $0.18+. Stop at $0.175 catches this — but the loss (~−$43) is meaningful.
2. **20x leverage on a parabolic short** = thin margin for error. Liquidation around ~$0.176; stop sits inside but margin for slippage is tight.
3. **Short-side crowding** is real (funding −0.148%). If APE bounces hard before resuming downtrend, the squeeze could clip the stop before the thesis plays out.
4. **TP ladder not yet placed** = trade is still naked-on-the-upside vs targets. Without TPs, profit-taking decisions become discretionary in real-time, which is when discipline fails (see today's BAS lesson).
5. **Time decay is in our favour, not against** — news pumps lose narrative steam over days, not weeks. Patience is the edge.

---

## Monitoring

No formal hourly watchdog yet. Manual checks recommended:
- Daily close (most important — confirms next leg)
- 4H structure for lower-high signals
- Funding direction (peak unwinding)
- Whale wallet activity (if address found)

---

## Links

- [[Trade Log]] — Trade 012 entry
- [[daily/2026-04-25]] — entry context, news, whale data, decision narrative
- [[Strategies/Squeeze Environment Playbook]]
- [[Strategies/FTP Strategies]]
- [AMBCrypto — APE 90% pump / whale insider trading](https://ambcrypto.com/apecoin-jumps-90-as-whale-takes-14x-profit-sparking-insider-trading-concerns/)
- [Phemex — What Is ApeCoin and Why It Surged 92%](https://phemex.com/academy/what-is-apecoin-and-why-it-surged)
- [NullTX — Yuga Labs leadership change](https://nulltx.com/apecoin-rises-88-as-yuga-labs-leadership-change-whale-wager-sparks-market-sentiment/)
