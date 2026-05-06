---
wing: root
type: trade-log
purpose: Rolling ledger of all closed trades and active positions with outcomes, reasoning, and lessons
last_updated: 2026-04-22
---

# Trade Log — Wins / Losses Ledger

**Purpose.** Cumulative record of every trade that gets closed (win or loss), plus context on why it was entered and why it was exited. Used for pattern recognition: what setups work, what doesn't, where I repeatedly get fooled, and where my edge actually lives.

**Companion notes:**
- [[Portfolio Overview]] — live snapshot of open positions
- [[daily/|Daily journal]] — per-session narrative context
- [[Coins/|Coin profiles]] — per-symbol thesis and technicals
- [[Strategies/Overnight Risk Protocol]] — mandatory checklist before placing any limit that could fill during sleep

---

## Ledger Rules

1. **Every closed trade gets logged** — wins, losses, scratches, and re-positions. No cherry-picking.
2. **Loss is a loss** — if a position turned and got closed, that's a loss regardless of whether a new entry follows.
3. **Re-positions are separate trades** — closing and re-entering = two entries in the ledger.
4. **Partial closes are logged as their own realised row** — remaining runner stays in Open Trades.
5. **Include the "why"** — entry thesis, exit reason, and the lesson (if any). Without the why, the log is useless for learning.
6. **Mark the regime** — was this trade run in `squeeze`, `trend`, `chop`? Matters for strategy post-mortem.
7. **Apply [[Strategies/Overnight Risk Protocol]] before placing any sleep-window limit** — added 2026-04-22 after Trade 003.

---

## Scoreboard (YTD 2026)

| Metric | Value |
|--------|-------|
| Closed trades (incl partial closes) | 3 |
| Wins | 1 |
| Losses | 2 |
| Win rate | 33% |
| Net realized PnL | **+$29** |

---

## Closed Trades — 2026

| # | Date | Symbol | Side | Size | Entry | Exit | P&L ($) | P&L (%) | Regime | Outcome | Notes |
|---|------|--------|------|------|-------|------|---------|---------|--------|---------|-------|
| 001 | 2026-04-21 | BASUSDT | Short | — | — | — | **-$14** | — | squeeze | LOSS | Short against BAS during vertical extension. Position turned, closed to cap loss. Re-entered via Trade 002. [[daily/2026-04-21]] |
| 003 | 2026-04-22 | CHIPUSDT | Short | ~20–22k | $0.068 | ~$0.078 | **-$200** | ~-15% notional | squeeze | LOSS | **Overnight fill + stop-out while asleep (06:00 fill → 07:00 stop).** CHIP is Binance listing-day-2: RSI 100 across 4h/1D at entry, 20% circulating float, tier-1 VC backing. Short thesis valid but timing wrong — shorted into blow-off that wasn't done. Trade was dangerous overnight; generated [[Strategies/Overnight Risk Protocol]]. [[daily/2026-04-22]], [[Coins/CHIP]] |
| 008 | 2026-04-22 | NAORISUSDT | Short (partial close) | 17,500 of 25,000 | $0.07911 | ~$0.06519 | **+$243** | +17.6% notional | squeeze | WIN | **Funding flip bank.** Crime-short entered 2026-04-21 @ $0.07911 at plan trigger level. Funding flipped from +0.109% to -0.00179% (declining) = Phase 2 precursor signal per plan. Closed 70% to bank into the signal; runner of 7,500 stays open for potential Phase 2 climax. [[daily/2026-04-22]], [[Coins/NAORIS]] |

---

## Open Trades — Entered but not yet closed

| # | Date | Symbol | Side | Size | Entry (target/filled) | Leverage | Stop | Target(s) | Thesis |
|---|------|--------|------|------|-----------------------|----------|------|-----------|--------|
| 002 | 2026-04-21 | BASUSDT | Short (limit, unfilled) | 100,000 | **$0.017997** | 20x | TBD — see [[Coins/BAS]] | TBD | Re-rack of Trade 001. Thesis intact but entry needs to be at resistance. |
| 004 | 2026-04-22 | TAOUSDT | Long (limit, unfilled) — T1 | 20 | $225.00 | 20x | $180 (group invalidation) | $273 / $297 | Layer 2 thesis tranche — see [[Coins/TAO]]. |
| 005 | 2026-04-22 | TAOUSDT | Long (limit, unfilled) — T2 | 30 | $210.00 | 20x | $180 | $273 / $297 | Layer 2 T2. |
| 006 | 2026-04-22 | TAOUSDT | Long (limit, unfilled) — T3 | 40 | $200.00 | 20x | $180 | $273 / $297 | Layer 2 T3 — **biggest tranche on thesis line**. |
| 007 | 2026-04-22 | TAOUSDT | Long (limit, unfilled) — T4 | 30 | $192.00 | 20x | $180 | $273 / $297 | Layer 2 T4 — wick buffer below thesis line. |
| 008-R | 2026-04-22 | NAORISUSDT | Short (runner) | 7,500 | $0.07911 | 20x | $0.0884745 | Phase 2 climax (vertical + volume + cascade) | Runner from Trade 008 partial close. Free optionality on final squeeze. [[Coins/NAORIS]] |
| 009 | 2026-04-22 | NAORISUSDT | Long (limit, unfilled) — L1 | 20,000 | $0.05639 | 20x | $0.0285 (structural) | $0.08+ reclaim | Pullback scale-in per plan. Order ID `931274429`. |
| 010 | 2026-04-22 | NAORISUSDT | Long (limit, unfilled) — L2 | 20,021 | $0.04795 | 20x | $0.0285 | $0.08+ reclaim | Pullback scale-in (halved from original 40k). Order ID `933834175`. |

**Existing open (pre-session, not logged as individual trades):**
- TAO Layer 1: 31 TAO long @ $246.02 (see [[Coins/TAO]])
- NAORIS Core Long: 12,755 @ $0.06665, effective ~5.7x (see [[Coins/NAORIS]])
- BAS long scale-in plan: parked 150k across $0.014/$0.012/$0.011/$0.0088 (NOT placed)

---

## Patterns Observed

- **Squeeze environment hostile to passive shorts.** Trades 001 and 003 both were conviction short *setups* that failed on *timing* — not thesis. In `squeeze` regime, the setup being right is not sufficient; the entry-to-stop window has to survive one or two violent squeeze legs first.
- **Re-positioning vs holding through.** Closing a turning short and re-entering at a better level (Trade 001 → Trade 002) is legitimate. Holding a squeezing short hoping it'll turn (Trade 003 pre-stop) is not.
- **Overnight / unattended orders = separate risk category.** Trade 003 was a daylight-reasonable setup that became dangerous the moment it was placed to fill during sleep hours. New-listing, extreme-RSI, low-float, VC-backed = "daylight only" territory.
- **Stop hygiene matters more than entry hygiene.** Both losses were capped by actual stop orders on the book. Stops paid for themselves.
- **Plan triggers > P&L triggers for profit-taking.** Trade 008 was banked because a *plan signal fired* (funding flip), not because the number looked big. The plan's signal arrived before crossed decision thresholds for either "bank it all" or "hold it all" — partial close was the correct response to a Phase 2 precursor (not Phase 2 climax).

---

## Lessons Bank

- **2026-04-21 (Trade 001):** In squeeze regime, even small-size shorts can get tagged fast. Enter shorts at structural resistance with stops pre-defined, not leaning into strength hoping.
- **2026-04-21 (Trade 002 setup):** Multi-TF RSI extremes mark a legit fade zone, but 20x leverage leaves no stop-room. Leverage and stop must be internally consistent.
- **2026-04-22 (Trade 003):** **Overnight short on a new Binance listing with 4h/1D RSI 100 is not a trade, it's a coin flip.** A 15% stop is not wide enough for a coin that printed a 57% wick the prior day. If you can't be awake to manage it, you can't place it. This generated the [[Strategies/Overnight Risk Protocol]].
- **2026-04-22 (general):** Crime-coin framework ≠ controlled-blow-off framework. VC-backed new listings with published vesting schedules (CHIP) behave like crime coins but aren't — short-after-climax rule still applies, but "climax" is not the same as "RSI 100".
- **2026-04-22 (Trade 008):** **Funding direction is signal, not a footnote.** Watching funding flip from +0.109% to -0.00179% was the plan's Phase 2 precursor — partial close into the signal locked in realised gains before the expected squeeze. Without the funding datum, the decision to bank would have been P&L-driven (wrong reason, same outcome sometimes).
- **2026-04-22 (Trade 008 follow-up):** **Structural stop with time-based review beats single-price stop on a thesis trade.** NAORIS long now uses: structural auto-stop at $0.0285 (below March grind-up) + 72h reclaim review + 1D-close $0.045 health check + funding-reverts-positive manual kill. One auto-fire, three manual reviews. Honours "ride the crime" without becoming stop-less.

---

## Schema for Future Entries

```markdown
| NNN | YYYY-MM-DD | SYMBOL | Long/Short | Size | Entry | Exit | P&L $ | P&L % | regime | WIN/LOSS/SCRATCH | One-line notes, link to daily [[daily/YYYY-MM-DD]] |
```

When a trade closes:
1. Move the row from **Open Trades** to **Closed Trades** (or add a partial-close row if only partial)
2. Fill in Exit, P&L, Outcome, and Notes
3. Update Scoreboard totals
4. If there's a lesson worth remembering, add it to **Lessons Bank** with the trade #
5. If it reveals a pattern, update **Patterns Observed**
6. Update `last_updated` in YAML



---

## Update — 2026-04-25

### New Closed Trades

| # | Date | Symbol | Side | Size | Entry | Exit | P&L ($) | P&L (%) | Regime | Outcome | Notes |
|---|------|--------|------|------|-------|------|---------|---------|--------|---------|-------|
| 011 | 2026-04-25 | BASUSDT | Short (anxiety unwind) | 80,830 of 85,000 | $0.01848 (blended) | various $0.018+ | **−$106** | ~−7% notional | squeeze | LOSS | **Off-thesis anxiety unwind during the squeeze the Phase 2 plan was designed to absorb.** Per [[Coins/BAS]] Phase 3 section. Closed in two events (17:53 UTC × 13 trades, 18:12 UTC × 28 trades) during BAS bounce into $0.018+. Pre-set $0.01723 stop existed but realized loss exceeds what stop alone would account for — additional manual closes. Cumulative BAS realized still **+$602**. [[daily/2026-04-25]] |

### New Closed Trades — TAO partial restructure

| # | Date | Symbol | Side | Size | Entry | Exit | P&L ($) | P&L (%) | Regime | Outcome | Notes |
|---|------|--------|------|------|-------|------|---------|---------|--------|---------|-------|
| 011b | 2026-04-25 | TAOUSDT | Long (partial) | 1.055 of 31 | $246.02 | various | **−$9.29** (incl. commissions) | ~−0.1% notional | trend | LOSS | Trimmed 1.055 TAO and re-leveraged remaining 29.945 from ~11x → 20x. Not anxiety-driven; deliberate risk increase. Worth tracking whether the leverage bump pays. [[daily/2026-04-25]] |

### New Open Trades

| # | Date | Symbol | Side | Size | Entry (target/filled) | Leverage | Stop | Target(s) | Thesis |
|---|------|--------|------|------|-----------------------|----------|------|-----------|--------|
| 012 | 2026-04-25 | APEUSDT | Short | 5,959 | **$0.1678** | 20x | **$0.1750** (live, algo `2000000837193746`) | $0.135 / $0.115 / $0.105 (TP ladder pending) | **Catalyst-pump distribution short.** Yuga Labs CEO change pumped APE +90% on derivative speculation. Distribution candle confirmed (D1 −13%, 60% upper wick). Whale insider longed-then-flipped-short for 14x. Funding peaked −0.687% at local top — squeeze fuel mostly burned. See [[Coins/APE]]. |

---

## Scoreboard (YTD 2026) — refreshed 2026-04-25

| Metric | Value |
|--------|-------|
| Closed trades (incl partial closes) | 5 |
| Wins | 1 |
| Losses | 4 |
| Win rate | 20% |
| Net realized PnL | **−$86** |
| Net realized PnL (excl Trade 011 anxiety unwind) | **+$20** |

> Note: the Phase 1+2 BAS realized gains (+$708) are tracked in [[Coins/BAS]] but were not previously logged as discrete closed trades in this ledger. If they were retroactively counted, scoreboard would shift heavily positive. Consider back-filling Trades 005a, 005b, 007 closes in next pass.

---

## New Lessons (added 2026-04-25)

- **2026-04-25 (Trade 011) — Anxiety is a market signal, not an action trigger.** The BAS squeeze that prompted the off-thesis unwind was *itself* the diagnostic signal that the move was about to resolve in our favour (funding −0.687% at the local top = peak short positioning). Acting on the discomfort converted a working trade into a $106 realized loss. The Phase 2 stress-test had already pre-computed the worst-case whipsaw at −$13; actual cost was 8x worse than budgeted. **Pre-commit rule (drafted):** *"I do not modify hedged positions outside of (a) a triggered watchdog alert, (b) a planned TP/stop level being hit, or (c) an explicit reassessment session with written reasoning logged."* To be promoted to a formal protocol in [[Strategies/]].

- **2026-04-25 (Trade 012) — Catalyst-pump distribution is a repeatable setup.** Five-test framework now defined (catalyst quality / volume profile / whale activity / funding signature / structural). When all five fire — as they did on APE — the trade becomes mechanical. Stages 0-2 of the decay sequence already played out on APE; stages 3-5 are the harvest zone.

- **2026-04-25 (cross-trade) — Funding direction is now a confirmed strategy primitive, not a footnote.** This is the second time in five days the funding-flip framework has been the right decision tool — first NAORIS Trade 008 partial close, now APE Trade 012 entry timing and BAS Trade 011 (mis)read. Promote from Lessons Bank to active framework: track funding as a first-class signal alongside price/volume/structure.

---

## New Patterns (added 2026-04-25)

- **Anxiety-driven exits during planned squeezes destroy trade economics.** Trade 011 is the exact opposite of the discipline applied in Trade 008 (NAORIS funding-flip partial close). Same setup pattern (squeeze ahead of resolution); opposite operator response. The plan side won; the anxiety side lost. Pattern needs a structural prevention — the pre-commit rule is the mechanism.

- **News-pump shorts on structurally-broken tokens are high-conviction setups.** APE pumped +90% with no cash-flow catalyst on a token in a 2+ year downtrend. Whale insider flip + extreme funding + distribution candle all stacked. This is a different setup category from "fade the parabolic" (KAT-style) — the decay mechanics are slower (5-10 days vs 24-48h) but more reliable because the structural backdrop is bearish. Consider a dedicated playbook entry in [[Strategies/]].

- **Operator state is a leading indicator.** When the urge to act on a working trade peaks, the trade is usually about to resolve in our favour. Worth journaling the *feeling* alongside the *data* — over time, "I want to do something right now" should become recognised as a fade signal on operator decisions, not a market signal on the position.



---

## Update — 2026-04-26 (BSB entry)

### New Open Trade

| # | Date | Symbol | Side | Size | Entry (target/filled) | Leverage | Stop | Target(s) | Thesis |
|---|------|--------|------|------|-----------------------|----------|------|-----------|--------|
| 013 | 2026-04-26 | BSBUSDT | Short | 550 | **$0.84784** | 10x | **$0.96161 × 281 (51%)** — partial stop, naked runner of 269 (intentional) — TV alert at $0.95 = re-entry trigger | $0.55 / $0.45 / $0.40 (TP ladder pending) | **Catalyst-pump distribution short on RWA new listing.** Block Street pumped from $0.40 → $0.85+ on narrative momentum, no specific catalyst. Funding **POSITIVE** +0.192% peak (long-crowded top — opposite of HYPER pattern). Daily RSI 88 still rising; 4H RSI cooling 77→70.93. NOT classified as crime coin (signals #4 and #5 fail). RWA peers (PLUME, ONDO, ENA, PENDLE) all in bearish weekly bias — BSB is isolated outlier, no sector wave. CHIP-class new-listing risk acknowledged; mitigated via 10x leverage (not 20x), partial mechanical stop, small naked runner. See [[Coins/BSB]]. |

### Position state at log time

- Mark: ~$0.784 → uPnL **+$35.12 (+7.53%)**
- Margin used: $43 (cross-margin context — worst-case loss is bounded by runner size, not per-position margin per [[Strategies/Account Configuration]])

---

## New Lessons (added 2026-04-26)

- **2026-04-26 (Trade 013) — Asymmetric stop structure for contrarian shorts into parabolics.** When sizing a parabolic short where the squeeze risk is real but the structural thesis is sound: use a **partial stop on the majority of the position** (mechanical defence) combined with **a smaller naked runner** sized so worst-case loss is acceptable. The TV alert at the squeeze level becomes a **re-entry trigger** at better cost basis, not just a warning. This converts the squeeze from pure risk into optionality. Validated structurally by stress-test math: every scenario except a deep unattended overnight gap lands inside an acceptable loss range, and the squeeze-and-re-engage path actually IMPROVES prospective trade economics.

  **Pre-commit rule:**
  > *"On contrarian shorts into parabolics, partial-stop / no-stop-on-runner is the correct structure when (a) runner size is small enough that worst-case loss is acceptable, and (b) any squeeze creates a higher-conviction re-entry zone. Treat the alert price as the next entry trigger, not just the warning."*

- **2026-04-26 (cross-trade) — Catalyst-pump short framework now validated across two distinct funding signatures.** APE (Trade 012) was the *short-crowded* version (negative funding, paying to hold). BSB (Trade 013) is the *long-crowded* version (positive funding, collecting premium to short). Both work — the setup type is "exhausted parabolic," not "crowded position." Funding direction tells you whether you're being paid or paying to express the trade, not whether the trade is right.

---

## New Patterns (added 2026-04-26)

- **Sector-isolation strengthens single-token shorts.** When a token is pumping but its narrative peers are flat or declining (BSB vs PLUME/ONDO/ENA), the move is "isolated" rather than "sector-driven." Isolated parabolics have weaker continuation odds because there's no rotation flow supporting the trade — once the single buyer/manipulator stops, mean reversion has no narrative bid to fight against.

- **TV alert as re-entry trigger.** Client-side price alerts (not exchange orders) used as the cue to *add to a working short at a better price*, rather than only as warnings. Pattern works when the trade structure pre-commits to "if alert fires, evaluate adding rather than panicking." Requires phone access and discipline to act on alert rather than freeze.



---

## Update — 2026-04-27 (ZBT closed loss + framework lessons)

### New Closed Trade

| # | Date | Symbol | Side | Size | Entry | Exit | P&L ($) | P&L (%) | Regime | Outcome | Notes |
|---|------|--------|------|------|-------|------|---------|---------|--------|---------|-------|
| 015 | 2026-04-26 → 2026-04-27 | ZBTUSDT | Long | 5,496 | $0.2268 | ~$0.190 (stop) | **~−$202** | ~−16% notional | spot-driven-pullback | LOSS | First failed worked example for [[Strategies/Spot-Driven Long]]. Spot demand evaporated faster than funding signaled it. Entry was triggered by price tagging 1H EMA20, NOT by confirmed 4H higher low — confirmation rule #1 was assumed not verified. Trade dropped −25% within hours of entry. Stop fired at framework invalidation as designed. See [[Coins/ZBT]] post-mortem and [[Strategies/Spot-Driven Long]] failure mode update. |

---

## Scoreboard (YTD 2026) — refreshed 2026-04-27

| Metric | Value |
|--------|-------|
| Closed trades (incl partial closes) | 6 |
| Wins | 1 |
| Losses | 5 |
| Win rate | 17% |
| Net realized PnL | **−$288** |

> Note: Several active trades are running in significant profit but not yet closed (APE +$113 unrealized, BSB ~+$150 realized + $55 unrealized partial closes, AGT +$25 realized + $12 unrealized). When current runners close, scoreboard will shift positive. Realized losses are concentrated in: BAS Phase 3 anxiety unwind (−$106), ZBT spot-driven failure (−$202), CHIP overnight short (−$200), TAO restructure cost (−$9). The pattern lessons matter more than the raw scoreboard at this phase.

---

## New Lessons (added 2026-04-27)

### Lesson — Spot-Driven Long framework: first failure (Trade 015 / ZBT)

The framework's core assumption — *"flat funding through a parabolic pump = spot demand intact = price will resume after pullback"* — is INCOMPLETE. ZBT proved that **spot demand can disappear without funding signaling it first.** Funding is a lagging indicator that only moves significantly when there's a critical mass of new perp positions. If spot buyers simply stop without speculative perp positioning building up first, funding stays flat while price still drops.

**Updated framework rules (logged in [[Strategies/Spot-Driven Long]]):**
- Entry confirmation #1 must be a **printed** 4H higher low (bounce + held pullback above the bounce low), NOT just price tagging an EMA support
- Add supplementary confirmation requirement: spot venue volume / orderbook depth / sector co-movement / spot-perp parity
- Framework status downgraded to "validation phase" — probe-sized only ($30-50 margin max) until 5+ tracked setups exist

### Lesson — Order placement matters: cluster discipline (new protocol)

User observed that TPs and stops at obvious technical levels (round numbers, prior swing highs/lows, BB upper/lower, EMAs) frequently get tagged just-shy-of and reverse. This is documented market microstructure (liquidity sweep / stop hunt).

**New protocol created: [[Strategies/Order Placement Anti-Cluster Discipline]]**

Rule: TPs front-run the cluster (placed 0.3-1.0% INSIDE the obvious level), stops sit outside the cluster (placed 1.0-2.5% OUTSIDE the obvious level). Round numbers and prior swing highs/lows are NEVER used as exact trigger prices. Going forward, the fuzz convention is mandatory for all new orders. Existing orders are not retroactively modified (avoid churn).

### Lesson — Don't trust new frameworks before validation

ZBT was the FIRST worked example for the Spot-Driven Long framework, taken at conviction sizing without prior validation runs. It failed.

**New rule:** New frameworks require 5+ tracked setups before being eligible for conviction sizing. During validation phase, all entries are probe-sized ($30-50 margin max). Failure modes get documented immediately and inform next iteration.

This is the correct epistemic stance. The framework is a hypothesis, not a recipe.

---

## New Patterns (added 2026-04-27)

- **Lagging-indicator failure mode for positioning-based frameworks.** Funding rate, OI, long/short ratio — all are lagging indicators. They only move when positioning rebalances, not when underlying spot demand changes. Frameworks that rely solely on positioning signals to predict price action will have a structural blind spot when spot dynamics shift before positioning catches up. Need real-time spot-flow confirmation as supplement.

- **Order cluster sniping is real and exploits operator laziness.** The path of least resistance for a trader is to place orders at "obvious" levels (round numbers, prior highs/lows, BB bands). The path of profit for an MM is to hunt those levels. Add fuzz to break out of the obvious-cluster bucket.

- **Frameworks need failure-mode documentation as soon as they fail.** When a strategy hits its first miss, document the diagnosis BEFORE the next trade attempt. Otherwise the same failure mode recurs with no learning. ZBT's diagnosis is now explicit in the framework doc and informs every future Spot-Driven Long entry.


---

## Update — 2026-04-29/30 (BSB full cycle + FOMC stop-outs)

### New Closed Trades

| # | Date | Symbol | Side | Size | Entry | Exit | P&L ($) | P&L (%) | Regime | Outcome | Notes |
|---|------|--------|------|------|-------|------|---------|---------|--------|---------|-------|
| 013 | 2026-04-26 → 2026-04-29 | BSBUSDT | Short | 550 (residual 29 at close) | $0.84784 | ~$0.3241 (flip to long) | **+$1,276** | ~+64% on residual | pump-dump | WIN | **Full dump cycle captured.** Parabolic short from $0.85 rode the -61% collapse to the capitulation wick at $0.326. Most of the position was closed incrementally on the way down; 29-unit residual held to near-bottom. Short closed and flipped to long at $0.3241. Early position absorbed brief losses (~-$119) before the collapse. Total short-leg net ~+$1,276. See [[Coins/BSB]], [[2026-04-29]]. |
| 016 | 2026-04-29 | BSBUSDT | Long | 6,000 | $0.3241 | $0.389 / $0.480 / $0.453 (blended) | **+$684** | +40.1% notional | bounce | WIN | **Capitulation flip long.** Entered at the short close price, 10x cross. TP1 at $0.389 (~2,110 units) and TP2 at $0.480 (~1,770 units) filled automatically. Remaining ~2,100 units manually closed at ~$0.453 — judgment call to bank before $0.588/$0.740 TPs, forgoing ~$285–$610 further upside. Manual close decision sound given low-liquidity token bounce risk. See [[2026-04-29]]. |
| 017 | 2026-04-29 | SKYAIUSDT | Short | — | ~$0.286 | various | **-$114** | — | FOMC event | LOSS | **FOMC stop-out (partial).** Position had banked +$111 in profits (11:46 + 12:24 UTC closes) before a reversal hit at 16:05 UTC (-$175 gross) — right in the FOMC volatility window. Small residual loss at 01:41 UTC (-$2.48). New smaller short (123 units) is still open and currently profitable. Net closed loss -$114. **Root cause: position exposed during FOMC announcement window. See [[Strategies/FOMC and Macro Event Protocol]].** |
| 018 | 2026-04-29/30 | NAORISUSDT | Short (partial close) | ~portion of 10,236 | ~$0.1165 | triggered ~01:40 UTC | **-$136** | — | FOMC follow-through | LOSS | **Post-FOMC overnight stop-out.** All 11 fill records landed at exactly 01:40:57 UTC — single stop-market sweep in the middle of the night. Likely post-FOMC volatility continuation. Position still partially open (10,236 units at $0.1165 avg, currently +$44.79 unrealised). **Root cause: stop not widened for macro event window. See [[Strategies/FOMC and Macro Event Protocol]].** |
| 019 | 2026-04-29 | GRIFFAINUSDT | Long | — | entered ~13:03 UTC | stopped ~16:00 UTC | **-$57** | — | FOMC event | LOSS | **FOMC stop-out (full).** Position entered at 13:03 UTC, stopped exactly at 16:00:10 UTC — directly in the FOMC announcement volatility spike. Position fully closed, no residual. Clean entry-to-stop cycle within ~3 hours. **Root cause: new position opened within hours of known FOMC event. See [[Strategies/FOMC and Macro Event Protocol]].** |

---

### Scoreboard (YTD 2026) — refreshed 2026-04-30

| Metric | Value |
|--------|-------|
| Closed trades (incl partial closes) | 11 |
| Wins | 3 |
| Losses | 8 |
| Win rate | 27% |
| Net realized PnL | **+$1,365** |

> Note: The three FOMC stop-outs (Trades 017, 018, 019) total **-$307** in avoidable losses. Against the BSB full cycle (+$1,960 net), the day was still a strong positive. But all three losses shared the same root cause — positions exposed during a known scheduled macro event. The [[Strategies/FOMC and Macro Event Protocol]] was created from this session.

---

### New Lessons (added 2026-04-30)

- **2026-04-29 (Trades 017, 018, 019) — FOMC is a scheduled risk event, not a market surprise.** All three stop-outs happened in the 16:00 UTC FOMC volatility window (SKYAI, GRIFFAIN) or the post-FOMC overnight continuation (NAORI). This was avoidable. The event date was known in advance. A 1-hour pre-FOMC window to close or hedge stop-exposed positions, and a 30-minute post-announcement hold before re-entering, would have saved ~$307. **New rule: no open stop-exposed positions within 1 hour of FOMC announcement. See [[Strategies/FOMC and Macro Event Protocol]].**

- **2026-04-29 (Trade 016) — Capitulation flip long is a high-conviction setup when done at the right moment.** Entering long at the exact close of a -61% dump, immediately after closing the short, was psychologically difficult but structurally sound. The TP ladder did its job on the lower rungs. The manual close of the upper tranche (~$0.453 vs $0.588/$0.740 targets) was a legitimate risk/reward call on a low-liquidity token — the bounce had run +48% and there was no clear continuation catalyst.

- **2026-04-29 (cross-trade) — FOMC losses don't cancel BSB wins, but they're still avoidable alpha leakage.** The net day was +$1,960 BSB vs -$307 FOMC = +$1,653. But the correct framing is: the BSB trade was earned through setup and execution; the FOMC losses were donated through inattention to the calendar. Treat them separately.

---

### New Patterns (added 2026-04-30)

- **Scheduled macro events create predictable volatility clusters.** FOMC, CPI, NFP, Fed speeches — all create sharp, non-directional volatility spikes within a known time window. Stops get hunted regardless of trade direction. This is structurally identical to the overnight new-listing risk (Trade 003 / CHIP) but occurs in a daytime, calendar-predictable window. The mitigation is the same: remove exposure before the event fires.

- **Post-announcement follow-through can outlast the session.** NAORI's stop fired at 01:40 UTC — ~8 hours after the initial FOMC spike. The event's volatility didn't end at the announcement; it rippled through the night. Positions held through FOMC need wider stops OR full removal until the dust settles (typically 24–48h after the announcement).
