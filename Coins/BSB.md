---
wing: coins
type: coin-profile
symbol: BSB
status: active
narrative:
  - RWA / Tokenized Asset Infrastructure
  - Cross-chain liquidity infrastructure
strategy:
  - Catalyst-Pump Distribution Short
  - Partial-stop / runner asymmetry
  - Funding-flip Phase 2 framework
position: SHORT 550 @ $0.84784 (eff 10x)
leverage: 10x
last_reviewed: 2026-04-26
tunnels:
  - Strategies/Squeeze Environment Playbook
  - Strategies/Crime Coin Checklist
  - Strategies/Overnight Risk Protocol
  - Strategies/Account Configuration
  - Trade Log
tags:
  - rwa
  - new-listing
  - parabolic-short
  - long-crowded-top
  - asymmetric-stop
  - chip-class-risk
  - tokenized-assets
---

# BSB — Block Street

> **Status (2026-04-26):** SHORT 550 @ $0.84784 entered into the parabolic top. Currently +$35.12 (+7.53%) at mark $0.784. Partial stop at $0.96161 × 281 (51% of position) — the remaining 269 is an intentional naked runner: small enough that the worst-case loss is bounded, with squeeze priced as a higher-conviction re-entry opportunity rather than purely as risk.

## Project Snapshot

**Block Street** — "first Unified Liquidity Layer for on-chain capital markets." Aggregates fragmented liquidity for tokenized real-world assets across Ethereum, BNB Chain, and Base. Single-API access for developers/institutions, cross-issuer execution layer with shared settlement.

**Listing timeline:**
- TGE: March 4, 2026 (~7 weeks ago)
- Binance perp listed: March 25, 2026 (~1 month ago)
- OKX perp listed: April 2, 2026
- KuCoin Futures + Binance Alpha added perp contracts

**Pre-pump baseline (April 24):** ~$0.40 mark. Today's intraday high reached $0.85+ (entry caught the spike). +112% from baseline at peak.

---

## Position

| Leg | Size | Entry | Mark (live) | uPnL | Eff Lev | Notional | Margin |
|-----|------|-------|-------------|------|---------|----------|--------|
| **SHORT** | 550 | $0.84784 | ~$0.784 | **+$35.12 (+7.53%)** | 10x | $431 | $43 |

### Live orders

| Order | Type | Trigger | Size | Purpose | Order ID |
|-------|------|---------|------|---------|----------|
| Partial pump-confirm stop | STOP_MARKET (BUY SHORT) | $0.96161 | 281 (51%) | Mechanical defence on squeeze | 2000000839487480 |

### Intentionally NOT placed (runner exposure)

The remaining **269 tokens have no stop**. Per discussion: small enough that worst-case loss is bounded (~$30 if it runs to $0.96), and the squeeze creates a *higher-conviction re-entry zone* rather than a simple loss event.

### Client-side alerts (not exchange orders)

- TradingView alert at **$0.95** — fires phone notification but is not an exchange-side order. Used as the re-entry trigger, not as a stop.

---

## Strategy — Catalyst-Pump Distribution Short with Asymmetric Runner

### Thesis

A relatively new (1-month-old) RWA infrastructure token pumped from ~$0.40 → $0.85+ on no specific catalyst beyond narrative + derivative speculation. Five-test framework for catalyst-pump distribution all fired:

1. **Catalyst quality** — none specific; just narrative momentum ✓
2. **Volume profile** — derivatives-dominant, spot lagging ✓
3. **Whale activity** — N/A (no on-chain trackers identified)
4. **Funding signature** — **+0.192% peak (longs paying shorts)** — long-crowded top ✓
5. **Structural backdrop** — new listing, no real fundamental shift ✓

The short collects funding (~0.44%/day at peak) instead of paying it. **This is the cleanest funding-favorable parabolic short setup of the session** (better than HYPER, KAT, APE on this metric specifically).

### Funding history (squeeze fuel monitor)

| Time (UTC) | Rate | Mark | Read |
|------------|-----:|-----:|------|
| 04-24 00:00 | +0.005% | $0.40 | Pre-pump baseline |
| 04-24 12:00 | **+0.117%** | $0.50 | First long-crowding spike |
| 04-24 16:00 | +0.061% | $0.44 | Calming |
| 04-25 00:00 | +0.010% | $0.45 | |
| 04-25 12:00 | **+0.071%** | $0.58 | Longs piling back in |
| 04-25 16:00 | **+0.133%** | $0.69 | Heavy long premium |
| **04-25 20:00** | **+0.192%** | $0.75 | **Peak — longs paying ~0.6%/day** |

Funding has stayed positive throughout. Opposite of HYPER's pattern (deeply negative). Direction is favorable for shorts: collecting premium, not paying it.

### Sector context — BSB is an OUTLIER

Cross-checked the major RWA peers on Binance perp (PLUME, ONDO, ENA, PENDLE) — **all are in bearish weekly bias with RSI 33-37, not running.** OM (MANTRA) has no Binance perp data (likely delisted post April 2025 −90% crash).

**No RWA sector wave is running.** BSB is moving in isolation, which:
- Eliminates the "sector tailwind" support for continued upside
- Strengthens the "isolated pump = manipulation likely" read (Viktor signal #2)
- Lowers the structural mean-reversion target

---

## Asymmetric structure (the key insight from this trade)

### Why partial-stop + naked runner is the right structure here

| Component | Size | Behavior | Logic |
|-----------|-----:|----------|-------|
| Stopped portion | 281 | Auto-closes at $0.96161 | Mechanical defence; caps loss on majority of position |
| Naked runner | 269 | No stop, intentional | Small enough that worst-case loss is bounded (~$30 if it runs to $0.96) |
| TV alert at $0.95 | n/a | Phone notification only | Acts as **re-entry trigger** — squeeze creates better cost basis for adds |

### Outcome scenarios

| Scenario | What happens | Net P&L from current state |
|----------|--------------|---------------------------:|
| Thesis plays out — daily reversal candle prints, BSB drops to $0.55 | Both legs ride down; stop never fires | **~+$165** (550 × ($0.85 − $0.55)) |
| Mean reversion to $0.45 (pre-pump baseline) | Stop never fires; full position rides down | **~+$220** |
| Squeeze to $0.96, alert catches you at $0.95, re-short at $0.95 | Stop fires on 281 (−$32); runner of 269 stays open with worse mark; new short adds at $0.95 with better cost basis | Worst case ~−$60 on existing book + opportunity to triple down at higher price |
| Squeeze to $0.96 unattended overnight | Stop fires on 281; 269 runner bleeds further | Bounded by runner size; worst realistic case ~−$80 to −$100 |
| Continued sideways $0.75–$0.85 chop | Funding income accrues (~$2/day) | Slowly positive |

### Pre-commit rule for re-engagement

> *"On contrarian shorts into parabolics, partial-stop / no-stop-on-runner is the correct structure when (a) runner size is small enough that worst-case loss is acceptable, and (b) any squeeze creates a higher-conviction re-entry zone. Treat the alert price as the next entry trigger, not just the warning."*

---

## Add-on confirmation triggers

Adds should size against the **runner** (269), not the original 550, to keep proportional exposure:

| Signal | Add size | Notes |
|--------|---------:|-------|
| 4H closes red below $0.74 | +75-150 tokens | First structural lower low |
| Daily reversal candle (red ≥0.5 body + ≥30% upper wick) | +150-300 tokens | True climax confirmation |
| Failed retest of $0.85+ with rejection candle | +75-150 tokens | Lower high; trend reversal active |
| Funding flips less positive on next 8h settlement | Flag only | Long crowding unwinding |
| Spot/perp gap closes | Flag only | Arbitrage pressure relieved |

**What does NOT count as confirmation:**
- Price dropping a few % more (chasing)
- 1H/15m candles (too noisy on parabolic)
- Tweet sentiment shifting (irrelevant)

---

## Risk assessment — CHIP-class new-listing acknowledgment

This trade matches the [[Trade Log]] Trade 003 (CHIP) profile: recent Binance listing, parabolic with extreme RSI, narrative-driven pump on a low-float token. That trade lost −$200 because the blow-off wasn't done.

**Mitigations applied:**
1. Smaller margin ($43 vs CHIP's larger size)
2. Lower leverage (10x vs CHIP's higher)
3. Partial mechanical stop in place (CHIP had no stop)
4. Runner sized small enough that worst-case is acceptable
5. Funding is favorable to shorts (collecting ~$2/day, not paying like CHIP)
6. RSI not at the absolute 100 extreme like CHIP (88 daily, but 4H already cooling 77 → 70.93)

**Outstanding risks:**
1. New listing parabolics can extend further than rational analysis (CHIP lesson)
2. Runner has no stop — overnight risk if you can't react to alert
3. Spot/perp dislocation could persist longer than expected
4. Token unlock schedule unknown — vesting events could shift dynamics

---

## Crime coin checklist score (per [[Strategies/Crime Coin Checklist]])

| # | Signal | Score |
|---|--------|-------|
| 1 | Uncorrelated with market | ✓ probable |
| 2 | Inorganic flat→vertical | ✓ strong |
| 5 | Heavily negative funding | ✗ FAILS — funding POSITIVE here (long-crowded, not short-crowded) |
| 6 | Not on Hyperliquid | ❓ unverified |
| 4 | Low mindshare | ✗ FAILS — actively traded, multiple exchange perp listings |

**Verdict: NOT a crime coin pattern.** This is a long-crowded parabolic, not a short-crowded one. Different setup category, different playbook. The "Long the Crime" framework explicitly does not apply — this is the opposite trade.

---

## Levels reference

**Resistance (short defends):**
- $0.785 — current mark
- $0.84784 — entry (psychological)
- $0.85+ — today's intraday high
- $0.95 — **TV alert / re-entry trigger** (LIVE)
- **$0.96161 — partial stop on 281 tokens** (LIVE)
- $1.00+ — psychological round number / extreme extension zone

**Support (TPs / mean reversion targets):**
- $0.74 — first 4H lower-low confirmation level
- $0.55 — 4H EMA20 zone (TP1 target if ever placed)
- $0.45 — pre-pump baseline (TP2 target)
- $0.40 — full retrace to baseline (TP3 target)
- $0.30 — spot ATH from April 5 (deep mean reversion)

---

## Open follow-ups

1. **Place TP ladder?** Currently no TPs. Could place: $0.55 × 200, $0.45 × 200, $0.40 × 150 to lock profit if drop happens overnight.
2. **Trailing stop on runner once $0.78 holds?** Move a $0.92 stop on the remaining 269 if 4H confirms direction.
3. **Watch BSB's broader sector behavior** — if PLUME / ONDO / ENA start running, sector wave might support continued BSB upside; if they keep declining, BSB's isolated pump is more vulnerable.
4. **Check Hyperliquid availability** to complete crime coin checklist (signal #6).

---

## Trade History (this symbol)

| Trade # | Date | Side | Size | Entry | Exit | P&L | Outcome |
|---------|------|------|------|-------|------|-----|---------|
| 013 | 2026-04-26 | Short | 550 | $0.84784 | (open) | +$35.12 uPnL | RUNNING — partial stop $0.96161 × 281, runner 269 naked |

---

## Devil's Advocate

1. **New-listing parabolic blow-off can extend further.** CHIP did. RSI 88 with momentum cracking on 4H is a hint, not confirmation.
2. **Long crowding (positive funding) can persist.** Funding has been +0.005% to +0.192% for days; "long crowded" doesn't mean "longs about to capitulate."
3. **Naked runner has no protection.** If price gaps overnight to $1.00+, the 269 takes a meaningful hit before you can react. Bounded but not zero.
4. **Spot venue thin** — if the spot price is being held up by a single bidder on a thin venue (like Bitget), the perp could converge UPWARD if real demand emerges.
5. **Token unlock unknown.** Vesting events for new listings can shift supply dynamics and either extend or terminate the move.

---

## Monitoring

No formal hourly watchdog yet. Manual triggers:
- Daily close (most important)
- 4H structure for lower-high signal
- Funding direction at next 00:00, 08:00, 16:00 UTC settlements
- TV alert at $0.95 (set on phone)

---

## Links

- [[Trade Log]] — Trade 013 entry
- [[daily/2026-04-25]] — full session context including BSB entry analysis
- [[Strategies/Crime Coin Checklist]] — failed checklist (not a crime coin, opposite setup)
- [[Strategies/Squeeze Environment Playbook]]
- [[Strategies/Overnight Risk Protocol]] — applies; partial stop + small runner is the mitigation
- [[Strategies/Account Configuration]] — cross-margin context (worst-case loss is bounded by runner size, not by per-position margin)
- [Block Street price | CoinMarketCap](https://coinmarketcap.com/currencies/block-street/)
- [Block Street | CoinGecko](https://www.coingecko.com/en/coins/block-street/)
- [Binance Announces BSB Futures Listing](https://cryptonews.net/news/market/32604129/)
