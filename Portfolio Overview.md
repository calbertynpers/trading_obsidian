---
wing: root
type: moc
scope: wing
last_reviewed: 2026-04-17
---

# Portfolio Overview — April 17, 2026

## Account Summary

| Metric | Value |
|--------|-------|
| Total Balance | $1,764.70 |
| Active Positions | 21 |
| Active Orders | 0 |

## Balances

| Token | Amount | Value |
|-------|--------|-------|
| BTC | 0.0136 | ~$1,020 |
| USDC | 741.21 | $741.21 |
| BNFCR | 1,736.7 | $0.00 |

## Open Positions

### Winners ✅
| Pair | Side | PnL | Notes |
|------|------|-----|-------|
| [[RAVE]] | LONG + SHORT | **+$1,075** | Best performer. Both sides green. |
| [[BIO]] | LONG + SHORT | **+$505** | DeSci pump. Long at $0.03 crushing it. |
| [[LYN]] | LONG | **+$152** | Long doing well. |
| [[TRUST]] | SHORT + LONG | **+$158** | Short working nicely. |
| [[BLUR]] | LONG + SHORT | **+$32** | NFT recovery play. |
| [[SIGN]] | LONG + SHORT | **+$22** | Hedged. |

### Losers ❌
| Pair | Side | PnL | Notes |
|------|------|-----|-------|
| [[SAGA]] | LONG | **-$80** | Underwater at $0.03. Near ATL. |
| [[MBOX]] | LONG | **-$40** | Bleeding. |
| [[AXL]] | LONG + SHORT | **-$26** | Hedged but both sides red. |
| [[TAO]] | LONG + SHORT | **-$9** | Small position, hedged. |

### Flat / Breakeven
| Pair | Side | PnL | Notes |
|------|------|-----|-------|
| [[MAV]] | LONG | +$2.79 | |
| [[SONIC]] | LONG + SHORT | -$0.96 | Hedged, drifting. |

## Leverage Concerns ⚠️

| Pair | Leverage | Risk |
|------|----------|------|
| AXL | 75x | Extremely aggressive. 123% 30-day vol. |
| BLUR | 75x | 1.3% move wipes margin if unhedged. |
| TAO | 75x | Small position but still risky. |
| BIO | 50x | Hot coin, overbought, 60%+ daily swings. |
| SAGA | 25x | More reasonable but underwater. |
| SONIC | 10x | Sensible. |
| LYN | 20x | Reasonable. |
| RAVE | 5x | Conservative. Working well. |



---

## Account Configuration (canonical reference)

> **MARGIN MODE: CROSS** · **HEDGE MODE: ENABLED** · See [[Strategies/Account Configuration]] for full detail.
>
> Per-position "margin_used" from API is initial margin allocated, NOT the runway to liquidation. The entire account equity backstops every position. Liquidation is a whole-portfolio event, not per-symbol. Do not compute isolated-style liquidation distances on individual positions.

This was previously implicit; explicitly logged on 2026-04-25 after repeated miscalculations on VVV. All future risk reasoning should default to total-portfolio context unless explicitly noted otherwise.
