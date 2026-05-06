---
wing: strategies
type: strategy
status: active
regime:
  - squeeze
  - all
tunnels:
  - Strategies/Spot-Driven Long
  - Strategies/FTP Strategies
  - Strategies/Order Placement Anti-Cluster Discipline
  - Strategies/BNB Chain Ecosystem Parabolic
  - Strategies/Account Configuration
  - Strategies/Overnight Risk Protocol
last_reviewed: 2026-04-29
---

# AI Meme Vaporware Cycle

**Status**: Active strategy framework. Codifies the recurring play across [[Coins/SKYAI]] (case #1), [[Coins/ZEREBRO]] (case #2), [[Coins/GRIFFAIN]] (case #6), and the validation watchlist below. Successor pattern to [[Strategies/BNB Chain Ecosystem Parabolic]], applied to AI narrative rotation.

## Parent strategies
- [[Strategies/Spot-Driven Long]] — entry-side framework
- [[Strategies/FTP Strategies]] — exit-side framework (counterpart to phase 3)
- [[Strategies/Order Placement Anti-Cluster Discipline]] — execution rules
- [[Strategies/Account Configuration]] — cross-margin / hedge mode reference

---

## Thesis

AI agent and AI ecosystem tokens during sector rotation phases are narrative-driven assets with thin underlying utility. They pump on belief and dump on rotation. The structural anchor is the **vaporware test**: does the project have real product traction beyond marketing, or is it pure narrative? If vaporware, the cycle is predictable:

1. Narrative ignites → spot-driven parabolic move (real buyers, no leverage crowding)
2. Trend matures → speculation enters → leverage book builds
3. Distribution begins → smart money exits to retail FOMO
4. Narrative cools → 60-80% mean-reversion crash

The trade is to ride phase 1-2 long, then flip to short during phase 3-4. Hedge mode keeps both directions clean.

## Vaporware test (entry filter)

A token qualifies for this strategy if **3+ of the following are true**:

- [ ] Marketing emphasizes "ecosystem" or "platform" language without specific product metrics (DAU, revenue, integrations)
- [ ] Whitepaper/site reads as buzzword soup: "AI-powered", "MCP-enabled", "multi-chain", "agentic" without concrete deliverables
- [ ] Twitter activity > GitHub activity (marketing > development)
- [ ] No external traction outside crypto-twitter — no enterprise customers, no real-world integrations
- [ ] Anonymous or thin team
- [ ] Sub-$500M market cap (room for parabolic + room for crash)
- [ ] Token launched in last 12 months
- [ ] Heavy CEX listing campaign or airdrop activity

If 3+ are true, it's vaporware-pattern. Two sides of the trade are valid.

If <3, it might be a real-product AI play (TAO, FET, RENDER tier) — different framework, longer-hold trend follow.

---

## Phase 1 — Long Entry (spot-driven parabolic)

### Entry signals (all must be present)
- 72h price change ≥ +30% **with funding pinned at +0.005% baseline** (no leverage crowding)
- US-session pump candles with buy% ≥ 55% on initial breakout
- Open interest growing slowly relative to price (OI/MC ratio < 30%)
- 4H breakout above prior consolidation with volume expansion
- AI sector basket showing rotation signal (3+ peers green)

### Anti-signals (rejection)
- Funding already > +0.05% before entry — too crowded, late
- Open interest > 50% of market cap — leverage book too built
- Pump driven by off-hours low-liquidity windows (BSB-style manipulation)
- Buy% on pumps < 50% — wash trading signature
- Single-news-catalyst pump — different framework ([[Strategies/FTP Strategies]])

### Entry execution
- **Don't chase.** Wait for first pullback to consolidation midpoint.
- LIMIT BUY 1.5% inside the cluster (anti-cluster fuzz applied per [[Strategies/Order Placement Anti-Cluster Discipline]])
- Stop 1.5-2.5% below trend invalidation level (below 4H consolidation low)
- 10x leverage maximum (smaller probe sizes preferred at parabolic extension)
- Probe size: $50-100 margin until pattern validates
- If limit will sit into sleep window, run [[Strategies/Overnight Risk Protocol]] first

### TP ladder
- TP1: prior local high (anti-cluster fuzz inside)
- TP2: psychological round + 1.27 fib extension
- TP3: 1.5-1.618 fib extension or 50% extension target

---

## Phase 2 — Trail (sustained narrative trend)

### Hold signals
- Funding stays below +0.05% (spot-driven preserved)
- 4H higher highs continue
- Buy% on pump candles stays above 50%
- AI sector basket continues rotating green
- Daily RSI oscillates 60-75 — extended but not exhausted

### Trim signals
- Funding climbs to +0.04-0.07% — first crowding warning
- Buy% on pumps drops below 50%
- Sector basket starts diverging (1-2 peers rolling)

### Trim action
- Trim 33% at TP1
- Trim 33% at TP2
- Move stop to entry (free trade) when 50% of TP ladder hit
- Track buy% per candle in journal

---

## Phase 3 — Vaporware Short Trigger

### Flip-to-short signals (need 5+ of 7)

1. **Funding climbs above +0.05%** through 2+ consecutive settlements
2. **Open interest doubles** from entry baseline (leverage book now squeezable)
3. **Lower-high pattern on 4H** — first failed re-test of prior peak with volume divergence
4. **Buy% drops below 50%** on 3+ consecutive pump candles (distribution into bids)
5. **Daily RSI extreme (>78)** with bearish divergence vs price
6. **Narrative rotation signal** — 3+ AI sector peers roll over together
7. **Catalyst maturity** — first negative news, dev silence >7 days, exchange delisting risk, competitor launches better metrics

### Short execution

Use Asymmetric Parabolic Short framework via [[Strategies/FTP Strategies]]:
- Initial entry on confirmed lower high
- Stop above ATH + 5% fuzz (anti-stop-hunt)
- Partial-stop tracker structure: 70% size with tight stop, 30% size with wide stop as runner
- Alert as re-entry trigger if first short stops out

### TP cascade (short side)
- TP1: 4H EMA20 reclaim test (~15-25% retrace from peak)
- TP2: prior consolidation breakout zone (~40-50% retrace)
- TP3: pre-pump base (~60-80% retrace = full vaporware mean-reversion)

---

## Phase 4 — Mean Reversion Capture

### Hold signals
- Funding flips negative — shorts crowded but trend confirmed
- Daily lower lows continue
- Volume profile shows distribution complete (declining volume on bounces)

### Cover signals
- 4H higher low printed for the first time
- Funding decompresses from negative back toward zero
- Spot-driven re-accumulation signature (flat funding + buying volume)
- Reached 60-80% retrace from peak

### Re-evaluation
- If post-crash signature shows new spot-driven buyers and project ships product → potential phase 1 re-entry as Sustained Narrative Trend Long
- If signature shows continued distribution and no product → keep short to zero or dust price

---

## Order placement discipline

All orders use [[Strategies/Order Placement Anti-Cluster Discipline]] fuzz factor:

| Order type | Fuzz direction | Magnitude |
|---|---|---|
| LIMIT BUY (long entry) | Inside cluster (above support) | 1.0-1.5% |
| TAKE_PROFIT (long) | Inside cluster (below resistance) | 0.3-1.0% |
| STOP (long) | Below cluster | 1.5-2.5% |
| LIMIT SELL (short entry) | Inside cluster (below resistance) | 1.0-1.5% |
| TAKE_PROFIT (short) | Inside cluster (above support) | 0.3-1.0% |
| STOP (short) | Above cluster | 1.5-2.5% |

Never use exact round numbers, exact prior highs/lows, or exact fib levels as triggers. The market makes liquidity at these zones.

---

## Position sizing (per token)

| Phase | Max size (margin) | Leverage cap |
|---|---|---|
| Phase 1 probe | $50-100 | 10x |
| Phase 1-2 conviction (after TP1 hits) | $200-500 | 10x |
| Phase 3 short entry | $150-300 | 10x |
| Phase 3-4 size add (after first TP hits) | $300-700 | 10-15x |

Never more than 5% of total margin in any single AI vaporware position.

---

## Active Validation Watchlist

| Token | Phase | Entry | Status | Notes |
|---|---|---|---|---|
| [[Coins/SKYAI]] | 1→2 flip executed | Short @ $0.286 → Long @ $0.256 | LIVE | Cascade fired correctly. Long survived 21% wick to $0.20 (16:00 UTC long squeeze). Naked — needs stop. |
| [[Coins/ZEREBRO]] | 1→3 sequence (reversed) | Short @ $0.0236 (-$44 uPnL) | LIVE | Fade-then-flip thesis. Short into bounce, plan to long the dump. |
| [[Coins/GRIFFAIN]] | 1 entry | Long @ $0.01878 | LIVE | Fresh phase 1 entry. uPnL -$28. Stop at $0.01718. |
| [[Coins/AIN]] | 2 trail | Long @ $0.082 | LIVE | +$4.4 uPnL (+17.78%). Sustained Narrative Trend Long original case. |
| [[Coins/AGT]] | 3 short | Short @ $0.024 | LIVE | +$8 uPnL (+15.5%). BNB Chain crossover candidate, vaporware-validated. |
| [[Coins/AIA]] | failed | Long @ $0.060 | -16.6% | Failed phase 1 — no rotation tailwind, narrative cooled before lift. Document as failure case. |
| [[Coins/FHE]] | 1 entry confirmed | Long @ $0.0177 | LIVE | +$0.03 uPnL (+8.6%). Privacy AI angle. Spot-driven sig confirmed. |
| [[Coins/NAORIS]] | 3 short | Short @ $0.1165 | LIVE | -$14 uPnL. Quantum-resistant blockchain. Real product but funding loaded for phase 3 short. |

## Failure cases

### ZBT (case #0 — pre-strategy)
Shorted into spot-driven long signature. Lost $202. The framework conflict (funding flat = real demand) was the structural error. **Lesson: never short spot-driven phase 1.**

### AIA (case #4 — failed phase 1)
Long entry at $0.060 caught the AI narrative but the rotation tailwind didn't materialize. Now -16.6% with no spot-driven re-acceleration. **Lesson: phase 1 entries require sector basket confirmation. Solo pumps without peers green = avoid.**

---

## Cross-references
- [[Strategies/Spot-Driven Long]]
- [[Strategies/FTP Strategies]]
- [[Strategies/Order Placement Anti-Cluster Discipline]]
- [[Strategies/BNB Chain Ecosystem Parabolic]]
- [[Strategies/Account Configuration]]
- [[Strategies/Overnight Risk Protocol]]
- [[Projects/Microstructure Signal Module]] — signal source that feeds entry/exit triggers for this strategy
- [[Coins/SKYAI]] — case #1
- [[Coins/ZEREBRO]] — case #2
- [[Coins/GRIFFAIN]] — case #6
- [[Coins/AIN]] — case #3 sustained
- [[Coins/AGT]] — short cross-pattern
- [[Narratives/AI Infrastructure]] — narrative tracking

## Last updated
2026-04-29 — Initial strategy doc created during SKYAI/ZEREBRO/GRIFFAIN live execution with NAORIS short


## Cross-references


- [[Strategies/Order Execution Protocol]] — gates ALL order placement under this strategy: phase 1 entries, phase 2 trim TPs, phase 3 short flips, stop placement. Always propose levels and wait for explicit user confirmation before placing.
