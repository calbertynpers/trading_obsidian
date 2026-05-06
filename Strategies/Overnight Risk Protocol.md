---
wing: strategies
type: strategy
status: active
regime:
  - all
tunnels:
  - Strategies/Squeeze Environment Playbook
  - Strategies/FTP Strategies
  - Strategies/Crime Coin Checklist
  - Trade Log
created: 2026-04-22
trigger_trade: "Trade 003 (CHIPUSDT, -$200 overnight stop-out)"
---

# Overnight Risk Protocol

**One-line rule:** *If a limit order could fill while the trader is asleep, the setup must survive a violent squeeze against it with no human intervention — or it doesn't get placed.*

This protocol is **mandatory** before placing any new limit order that could execute during the trader's sleep window (roughly 22:00–07:00 local). Generated after Trade 003 (CHIPUSDT -$200) where a reasonable daylight short became a bad overnight trade purely because of *when* it filled.

---

## The 6-Point Checklist

Run this on every limit BEFORE placing. If **3 or more** signals fire, the order is **overnight-risky**.

| # | Signal | What makes it dangerous |
|---|--------|------------------------|
| 1 | **New listing (<30 days)** | No established structure, thin book, air pockets, uncapped squeeze potential |
| 2 | **Multi-TF RSI >85 on 2+ TFs at entry** | Overbought doesn't mean topped — squeezes extend through "impossible" RSI levels |
| 3 | **Low float + unlock overhang (<25% circulating)** | Cornered supply = asymmetric upside on any positive headline |
| 4 | **Tier-1 VC / big-name backing** | Positive headline risk (partnerships, integrations) more likely than for noise coins |
| 5 | **Thin orderbook / no 1D or 1W chart history** | Price can move 15%+ with low real volume; stops can slip |
| 6 | **Trader offline > 4 hours** | No manual adjustment possible; stop is the only defense |

---

## What to Do When the Checklist Fires

If 3+ signals fire, the order is **overnight-risky**. Options in descending order of discipline:

### 1. Defer placement until awake (best)
Don't place. Wait for a daylight window where you can watch the fill and adjust dynamically.

### 2. Widen the stop beyond the next structural rejection
Not just "a few % above current" — beyond the next round-number resistance, prior squeeze high, or 2x the average daily range. Accept larger worst-case loss in exchange for surviving overnight noise.

### 3. Reduce size by 50%+
If you must place the order overnight, size down so the worst-case loss is still tolerable even if the stop blows through.

### 4. Use scheduled cancellation (if supported)
Place the limit with a "cancel at 05:00" or similar if the venue supports it. Gets the order off the book before the dangerous squeeze window.

### 5. Use a scale-in ladder, not a single trigger
Replace `short 20k @ $0.068` with `short 5k @ $0.068 + 5k @ $0.075 + 5k @ $0.082 + 5k @ $0.090`. Single-point squeezes can only take out one tranche at a time.

---

## What NOT to Do

- ❌ Place a tight-stop limit on a squeezing new listing "because the RSI is extreme"
- ❌ Assume "it can't go higher from RSI 100"
- ❌ Treat stop distance as adequate without checking how far yesterday's wick traveled
- ❌ Short during sleep without a daylight intervention plan
- ❌ Rely on cross-margin to save you — cross equity erodes under portfolio drawdowns

---

## Symbols / Categories That ALWAYS Hit This Rule

These are "daylight only" by default, even if only 1–2 signals from the checklist fire:

- **Any Binance new listing within 7 days of listing date** — Trade 003 pattern
- **Any coin flagged as `crime` in its narrative** — see [[Narratives/Crime Coins]]
- **Any coin printing its ATH on the current weekly candle** — still in price discovery
- **Any coin with negative funding <-50%/yr** — squeeze-fuel primed

---

## Workflow Integration

**Before placing any limit order:**

1. Run the 6-point checklist (above)
2. Cross-check against "always daylight only" categories
3. If flagged, choose from the remediation options
4. Document the decision in the [[Trade Log]] entry — what signals fired, why you placed anyway (or deferred)

**When the agent (Claude) is asked to place a limit:**

1. Before placing, the agent will surface the checklist results to the user
2. If 3+ signals fire, the agent will explicitly ask whether to defer, widen, reduce, or proceed anyway
3. The decision path gets logged in the vault

---

## Origin

This protocol exists because of Trade 003 (2026-04-22, CHIPUSDT -$200). The short thesis was correct — CHIP was overextended listing-day-1 with RSI 100 across 4h/1D. What was wrong was that the limit was placed late evening to fill overnight, and by 06:00 CHIP was squeezing again. Filled at $0.068, stopped at $0.078 by 07:00. All six signals were present and none were flagged before placing.

**Rule:** From 2026-04-22 forward, no limit goes on the book without the checklist run.

---

## Links

- [[Trade Log]] — see Trade 003 for the origin case
- [[daily/2026-04-22]] — session where this was created
- [[Strategies/Squeeze Environment Playbook]] — parent macro-regime context
- [[Strategies/Crime Coin Checklist]] — related "don't short before climax" framework
- [[Coins/CHIP]] — origin-trade coin profile


---

## Update — 2026-04-30: Sibling Protocol Added

A related but distinct protocol now exists for **scheduled macro events** (FOMC, CPI, NFP, Fed speeches): [[Strategies/FOMC and Macro Event Protocol]].

The key distinction: this protocol covers *probabilistic* overnight risk (new listings, extreme RSI, low float). The FOMC protocol covers *calendar-certain* volatility events that are known days in advance.

When both apply simultaneously (e.g. a macro event followed immediately by a sleep window), apply the stricter constraint from each.

**Trigger for the new protocol:** Three stop-outs on 2026-04-29 (SKYAIUSDT -$114, NAORISUSDT -$136, GRIFFAINUSDT -$57) during and after the FOMC announcement. Total avoidable loss: **-$307**. See [[Trade Log]] Trades 017–019.


## Cross-references


- [[Strategies/Order Execution Protocol]] — applies to overnight limits as well: the 6-point checklist in this doc identifies the risk; Order Execution Protocol gates the actual placement of the order with explicit user confirmation of levels.
