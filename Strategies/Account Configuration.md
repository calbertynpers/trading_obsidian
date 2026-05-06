---
wing: strategies
type: account-config
status: canonical
last_reviewed: 2026-04-25
critical: true
tunnels:
  - Portfolio Overview
  - Trade Log
tags:
  - account-setup
  - cross-margin
  - hedge-mode
  - reference
---

# Account Configuration — Canonical Reference

> **Read this first when reasoning about position risk, liquidation, or margin math. Per-position margin numbers from the API are misleading without this context.**

## Margin Mode: **CROSS MARGIN**

The account is on **cross margin**, not isolated. This means:

- **All positions share the entire account balance as their margin pool.**
- A position's "margin_used" field from the API reports the *initial margin* allocated to that position — NOT the buffer between current loss and liquidation.
- **Liquidation is determined by total account equity vs total maintenance margin across all positions**, not by a single position running out of its allocated margin.
- A position can show uPnL of −100% of its initial margin and still be nowhere near liquidation, because the rest of the account equity is backstopping it.

### What this means in practice

When evaluating a single position's risk:
- ❌ DON'T calculate "liquidation price = entry × (1 + 1/leverage)" as if it were isolated
- ❌ DON'T say a position is "at liquidation" because uPnL ≈ −100% of initial margin
- ✅ DO consider the position's contribution to total account margin ratio
- ✅ DO check `total_margin_used` vs total balance for systemic risk
- ✅ DO treat individual position uPnL as P&L, not as remaining-margin-runway

### Stop-loss reasoning under cross margin

- Stops are still meaningful — they cap the **realized loss** when triggered.
- Stop placement should be based on **chart structure** (invalidation level for the thesis), not on protecting against per-position liquidation.
- A "20x leveraged short with $1 margin" doesn't mean "1.05× adverse price = liquidation." It means the loss compounds at 20x of the price move and is funded from total account equity.

### Liquidation reality

The account would only liquidate if:
- Total wallet balance + total uPnL falls below total maintenance margin requirement
- This is a *whole-portfolio* event, not a per-symbol event
- With ~$670 total margin used and a $7,400 TAO position dominating, the real systemic risks are concentrated in the largest positions, not scattered tiny ones

---

## Hedge Mode: **ENABLED**

The account uses Binance Futures **hedge mode** (not one-way mode):
- Can hold simultaneous LONG and SHORT positions on the same symbol
- Each position has its own `position_side` (LONG, SHORT, BOTH)
- Orders must specify `position_side` when modifying or closing
- BAS, NAORIS, and historically other coins have been held this way as paired hedges

---

## Default Leverage Tendencies

Based on observed position patterns:
- **20x default** for: APE, KAT, VVV, BIO, AIA, NAORIS short, TAO (recently bumped from 11x → 20x)
- **10x default** for: BAS short, BIO, NAORIS long, Binance Life short
- **5x default** for: TNSR, NAORIS long (effective), COTI, PIEVERSE
- **1x default** for: most small altcoin probes (NEIRO, PROMPT, BICO, FHE, etc.)

---

## Exchange & Settlement

- **Exchange**: Binance Futures
- **Settlement currency**: BNFCR (Binance Funding Contract Reward — equivalent to USDT for accounting)
- **Position notional measured in**: USDT
- **Funding settled**: every 8 hours (00:00, 08:00, 16:00 UTC)

---

## Reference Use

When the assistant is asked about a position's risk, liquidation distance, or margin sufficiency, it should:

1. **Default to total-portfolio reasoning**, not isolated per-position math
2. **Cite this note** when correcting prior isolated-margin-style analysis
3. **Use stop placement based on chart invalidation**, not on "preventing liquidation"
4. **Treat uPnL** as informational P&L, not as remaining margin runway

---

## Change log

- **2026-04-25** — Note created after assistant repeatedly miscalculated VVV liquidation distance assuming isolated margin. Lesson logged in [[daily/2026-04-25]].


## Cross-references


- [[Strategies/Order Execution Protocol]] — even with cross-margin and hedge mode capacity, every order still requires explicit user confirmation of specific levels before placement.
