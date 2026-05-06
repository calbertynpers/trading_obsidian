---
wing: projects
type: project
status: spec
created: 2026-04-29
last_reviewed: 2026-04-29
tunnels:
  - Strategies/AI Meme Vaporware Cycle
  - Strategies/BNB Chain Ecosystem Parabolic
  - Strategies/Spot-Driven Long
  - Strategies/FTP Strategies
  - Strategies/Order Placement Anti-Cluster Discipline
  - Strategies/Account Configuration
  - Projects/micro-position-scanner
---

# Project — Microstructure Signal Module

**Status**: Spec / Pre-build
**Owner**: Clint
**Created**: 2026-04-29

---

## Mission

Add a real-time signal source that detects orderbook structure, OI dynamics, and liquidation pressure to **anticipate MM-orchestrated squeezes before they fire**. This becomes a complementary feeder into the existing decision framework — it doesn't replace funding analysis, multi-TF TA, or sector rotation tracking, it joins them.

## Why this fits the existing framework

We already have these signal sources operational:

| Signal source | Status | What it tells us |
|---|---|---|
| Funding signature | Active | Crowding, leverage build-up, spot vs leverage-driven moves |
| Multi-TF technical alignment | Active | Trend structure, momentum, key levels |
| Sector rotation tracking | Active | Cross-asset narrative momentum (AI Vaporware, BNB Chain) |
| Buy% taker analysis | Active (manual) | Demand vs supply on individual candles |
| News/narrative monitoring | Active | Catalyst awareness |
| Cross-correlation tracking | Active | Coordinated moves across thematic baskets |
| [[Projects/micro-position-scanner]] | Active | ~100 tracker positions — sector heatmap |

What's missing — the gap this module fills:

| Signal source | Status | What it would tell us |
|---|---|---|
| Order book depth analysis | **Missing** | Where walls are, where the book is thin, MM intent |
| OI velocity tracking | Crude | Rate of leverage build-up = squeeze fuel loading |
| Long/short positioning ratios | **Missing** | Smart money vs retail positioning lean |
| Liquidation cluster awareness | **Missing** | Where stops are bunched (the magnets) |
| Whale flow detection | **Missing** | On-chain prep for dumps/pumps |
| Aggregate trade size analysis | **Missing** | Institutional clip prints vs retail noise |

## Current pain points (from 2026-04-29 session)

1. **SKYAI 11:30 short squeeze** — buy% only 50.4% on +9% candle was a distribution signal we saw but didn't act on
2. **SKYAI 16:00 long squeeze** — 30 min runway visible (bounce on 54% buy% + funding peak at +0.076%) we didn't capture
3. **BSB cascade liquidation** — 75 min runway visible (rising OI + funding +0.05% + 47% buy% on green candles) we trimmed defensively but didn't add
4. **Stop placement** — fuzz factor works retroactively but not predictively. Liquidation cluster data would let us PRE-position around them, not guess
5. **Naked SKYAI long** — survived a 21% wick by luck, not framework. Real-time OI/depth would have flagged the squeeze risk

## Signal taxonomy (what the module will produce)

Five categories, scored 1-5:

### 1. Squeeze Setup (directional, leveraged)
- OI velocity > +5%/15min with funding climbing → fuel loading
- Long/short ratio extreme (top traders >2:1 either way)
- Order book imbalance (one side 3x thicker than other) within 1% of mark
- **Output**: "SKYAI: phase 3 short setup forming. 4 of 5 signals firing. Confidence: HIGH."

### 2. Liquidation Cluster Proximity (defensive)
- Estimated liquidation level within 2% of current mark
- OI + leverage analysis suggests cascade trigger
- **Output**: "BSB: liquidation cluster detected at $0.61. Position stops should fuzz around this zone."

### 3. Distribution / Accumulation (slow burn)
- Buy% trend across last 8 candles vs price trend
- Aggregate trades show institutional vs retail flow
- **Output**: "ZEREBRO: 8 of last 12 candles green but buy% trending sub-50%. Distribution signature."

### 4. Squeeze Imminent (real-time, T-30min)
- Order book wall removed suddenly (MM about to push)
- Buy/sell aggregate ratio flips with rising volume
- Funding mid-cycle spike anomaly
- **Output**: "SKYAI: $0.27 ask wall just lifted. Long squeeze in 5-15 min. Tighten stops or take profit."

### 5. Post-Squeeze Reset (re-entry)
- Funding decompression
- OI reset
- Volume profile shift to accumulation
- **Output**: "BSB: cascade complete. Funding reset to baseline. Bounce trade window open 30-60 min."

## Data sources

### Tier 1 — Free, immediate (Binance Futures public API)

| Endpoint | Use |
|---|---|
| `/fapi/v1/depth?limit=500` | Order book L2, wall detection |
| `/futures/data/openInterestHist` | OI history at 5m/15m/1h granularity |
| `/futures/data/topLongShortPositionRatio` | Smart money positioning |
| `/futures/data/globalLongShortAccountRatio` | Retail positioning |
| `/futures/data/takerlongshortRatio` | Refined buy% signal |
| `/fapi/v1/aggTrades` | Whale clip detection |
| WebSocket book stream | Real-time depth updates |

### Tier 2 — External (scrape or paid)

| Source | Cost | Value |
|---|---|---|
| Coinglass liquidation heatmaps | Free tier (scrape) / $79-499/mo API | Aggregated liquidation level estimates |
| Hyblock Capital | $99-299/mo | True OI, retail/institutional split |
| CoinAnk | Free (scrape) | Alternative liquidation data |

### Tier 3 — On-chain whale tracking

| Source | Cost | Value |
|---|---|---|
| Arkham Intelligence | Free tier + paid alerts | CEX deposit detection, whale movements |
| Nansen | $150/mo | Smart money labels |
| Whale Alert | Free | Large transfer notifications |

## Integration points (how it ties to existing work)

### Reads from
- **Active position list** — symbols with capital deployed (priority 1)
- **Watchlist** — symbols with cascades pending or being tracked (priority 2)
- **Sector basket** — full AI/BNB Chain/etc rotation members (priority 3)
- **[[Projects/micro-position-scanner]]** — ~100 tracker positions feed sector heatmap signals

### Writes to
- **Knowledge base journal** — daily signal log entries under `daily/`
- **Telegram alerts** — for priority 1 signals (real-time)
- **Strategy doc updates** — when a pattern recurs across cases, update the relevant strategy doc
- **Trade Log** — annotate trades with which signals fired pre-entry
- **Coin docs** — append signal events to `Coins/[SYMBOL].md`

### Triggers / hooks into
- **Existing scheduled task framework** (BAS watchdog model)
- **Existing position management** — could auto-tighten stops on signal
- **Existing strategy framework** — signals become entry/exit confirmation criteria

## Phases

### Phase 1 — MVP (week 1, ~4-6 hours effort)

**Deliverable**: Scheduled task running every 10-15 min, scanning watchlist symbols, flagging top-priority signals.

Signals included:
- OI velocity (1h growth >5%)
- Funding extremes (>+0.08% or <-0.08%)
- Buy% trend divergence (rising price + falling buy%)
- Long/short ratio extremes

Output: structured JSON to knowledge base + Telegram for any HIGH-confidence flag.

No external data dependencies. Pure Binance API.

### Phase 2 — Order book layer (week 2, ~6-8 hours)

**Deliverable**: Add order book depth analysis to the scanner.

Features:
- Wall detection (single levels >5% of total depth)
- Imbalance scoring
- Wall persistence tracking (when does a wall move/disappear?)
- Pre-squeeze imminent flag (sudden wall removal + volume surge)

### Phase 3 — Liquidation cluster proxy (week 3, ~4-6 hours)

**Deliverable**: Estimate liquidation clusters from public data.

Method:
- Pull OI by leverage tier (where available)
- Combine with price history + assumed leverage distribution
- Output cluster zones with confidence scores
- Cross-reference against existing stop placements
- Refine the fuzz factor empirically

### Phase 4 — External data integration (month 2, optional)

If Phase 1-3 demonstrate value:
- Coinglass API or scraper for actual liquidation heatmaps
- Arkham wallet tracking for whale flow
- Real-time WebSocket streams for sub-minute alerts

### Phase 5 — Auto-action (month 3+, optional)

When signals fire with high confidence + position is exposed:
- Auto-tighten stops on long-side squeeze risk
- Auto-add to position on confirmed setup signal
- Manual override always available

## Success metrics

How we'll know if this is working:

1. **Detection rate**: Could we have flagged BSB cascade 30+ min ahead? (Backtest against this session's data)
2. **False positive rate**: Signals that didn't lead to a move within 2h
3. **Signal-to-action lag**: How fast can we act on a flag?
4. **PnL attribution**: Trades helped/saved by signals (logged in trade journal)
5. **Learning rate**: Are signal thresholds improving over time?

Quarterly review: cull underperforming signals, promote new ones identified in journal.

## Open questions

- [ ] Do we want auto-action (Phase 5) or always manual approval?
- [ ] Telegram alerts: only HIGH confidence, or also MEDIUM? (Spam vs miss tradeoff)
- [ ] Watchlist size: just active positions, or also full sector baskets? (Compute cost vs coverage)
- [ ] Order book depth granularity: every 5 min adequate, or need WebSocket real-time?
- [ ] How do we backtest signals? (Build historical replay or learn live only?)
- [ ] Storage: signal events in knowledge base files (Obsidian) or separate database?
- [ ] When does paid Coinglass become worth it vs free scraping?

## Cross-references (existing framework docs)

- [[Strategies/AI Meme Vaporware Cycle]] — entry/exit framework that consumes these signals
- [[Strategies/BNB Chain Ecosystem Parabolic]] — cross-correlation pattern that benefits from imbalance detection
- [[Strategies/Spot-Driven Long]] — funding signature framework — this module refines its trigger conditions
- [[Strategies/FTP Strategies]] — short framework — this module provides squeeze warning
- [[Strategies/Order Placement Anti-Cluster Discipline]] — fuzz factor — this module gives DATA for empirical fuzz calibration
- [[Strategies/Account Configuration]] — cross-margin context

## Suggested next steps

1. Confirm the signal taxonomy is the right shape (or adjust)
2. Decide Phase 1 scope: lock in 4-6 signals to start
3. Build Phase 1 MVP scanner + scheduled task
4. Run live for 1 week alongside existing manual workflow
5. Review which signals fired and which trades they would have helped
6. Iterate

---

**Last updated**: 2026-04-29 — initial spec drafted during live SKYAI / BSB cascade observation
