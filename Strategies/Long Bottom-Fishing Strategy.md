---
wing: strategies
type: strategy
status: active
regime:
  - all
tunnels:
  - Strategies/FTP Strategies
  - Narratives/Crime Coins
---

# Long Bottom-Fishing Strategy

## Thesis

Target coins at the bottom of their rotation — near all-time lows, beaten down by macro + unlock pressure, with favorable or neutral funding for longs. Position before a potential bull market confirmation.

## Entry Criteria

1. **ATH distance:** >70% below all-time high (more room to recover = more upside)
2. **ATL proximity:** <15% above all-time low (near the bottom)
3. **Market cap:** <$500M (small cap = more explosive upside)
4. **Volume:** >$1M daily (enough liquidity to enter/exit)
5. **Funding rate:** NOT deeply positive (>+0.5% means longs pay too much)
6. **Tokenomics check:** Prefer low FDV/MCap ratio (<3x ideal, <5x acceptable)

## Scoring (Long Profile)

| Component | Weight | Logic |
|-----------|--------|-------|
| ATL proximity | 30% | Closer to bottom = better entry |
| ATH distance | 20% | More room to recover |
| Funding rate | 15% | Negative = longs collect (GOOD) |
| Recent 7d dump | 10% | Deeper dump = better entry |
| Volume anomaly | 10% | Active interest |
| Market cap | 10% | Smaller = more upside |
| FDV ratio | 5% | Lower = less dilution |

## Key Differences from FTP Scoring

| Factor | FTP (Short) | Long (Bottom-Fish) |
|--------|-------------|-------------------|
| Negative funding | BAD (shorts pay) | **GOOD** (longs collect) |
| Recent dump | Not scored | **Bonus** (better entry) |
| ATL proximity | 25% weight | **30% weight** |
| FDV ratio | Higher = good for shorts | **Lower = less dilution for longs** |

## Risk Management

- Size small — these are asymmetric bets, not conviction trades
- Use low leverage (5-10x max) — must survive interim dumps
- Diversify across multiple candidates, don't concentrate
- Set wide invalidation levels, not tight stops (wicks will kill tight stops)
- Calculate funding cost budget for 3 months

## Macro Catalysts to Watch (Apr 2026)

1. US-Iran ceasefire (Apr 8) — Strait of Hormuz reopening
2. Fed QE restarted Dec 2025 ($40B/month bond purchases)
3. Fed funds rate at 3.50-3.75% (six cuts since Sep 2024)
4. New dovish Fed Chair (Kevin Hassett) expected
5. FOMC meeting Apr 28-29 — tone could shift dovish
6. BTC at $75K — needs to break $80K for bull confirmation

## Current Candidates (Apr 17, 2026)

### Tier 1 — Strongest Setup
| Coin | Price | ATL Prox | Funding | Why |
|------|-------|----------|---------|-----|
| [[SAGA]] | $0.028 | 4.3% | -0.13% (collecting) | L1 infra, already hold |
| [[PARTI]] | $0.043 | 2.7% | neutral | Capitulation dump, real revenue |
| [[RESOLV]] | $0.035 | 3.3% | neutral | Stablecoin infra |

### Tier 2 — Strong
| Coin | Price | ATL Prox | Why |
|------|-------|----------|-----|
| [[BLUR]] | $0.025 | 51.7% | Best tokenomics, NFT recovery catalyst |
| [[SONIC]] | $0.037 | 8.1% | Solana L2 gaming, already hold |
| MOVE | $0.019 | 10.4% | L2 infra, 98.7% below ATH |
| ANIME | $0.005 | 12.2% | Already bouncing |

### Already Pumping (Watch for Pullback Entry)
| Coin | Price | 7d Change | Why |
|------|-------|-----------|-----|
| [[BIO]] | $0.034 | +84% | DeSci narrative, Arthur Hayes backing |
| [[AXL]] | $0.060 | +30% | Short squeeze, vesting almost done |



---

## Risk-Tier Sizing Profile (added 2026-05-03)

Bottom-fishing entries are now classified into one of three risk tiers. **Leverage is held constant at 20x; tier varies the *collateral* (and therefore notional).** This keeps liquidation geometry uniform across positions and lets the conviction signal flow cleanly into size.

| Tier | Collateral | Leverage | Notional | Profile |
|------|-----------:|---------:|---------:|---------|
| **A — Conviction** | $30 | 20x | $600 | Top-tier setup: clear utility, active narrative, current rotation in play, history of MM-driven pump-and-dump cycles, clean tokenomics. Highest expectation of MM intervention / pump. |
| **B — Volatility/Lottery** | $20 | 20x | $400 | Mid-tier: moderate conviction, *some* expectation of further downtrend so timing is not yet ideal, OR a credible lottery-ticket move where the asymmetric payoff justifies more than a token stake. |
| **C — Long-tail Skin-in-Game** | $10 | 20x | $200 | Lowest tier: low probability of MM intervention or pump but enough something to want skin in the game (passive narrative exposure, sympathy-rotation candidate, deep-bottom curiosity). Treat as cheap optionality. |

### Tier-assignment factors

A coin's tier is determined by its standing across these dimensions, scored qualitatively in the deep-dive pass:

1. **Utility** — does the protocol/product do something real, with users or revenue?
2. **Narrative alignment** — does it sit in an active or imminent narrative (DeSci, AI, NFT recovery, RWA, etc.)?
3. **Current rotation** — is sector heat moving in or out per `[[Building Map]]` / latest journal regime call?
4. **MM history** — has it had identifiable pump-and-dump cycles before? (Recurrence is the biggest pump-probability signal.)
5. **Tokenomics** — FDV/MCap ratio, unlock schedule, supply pressure.
6. **Bottom geometry** — proximity to ATL, depth of recent dump, base-building structure.
7. **Funding** — neutral or negative funding favours longs collecting; deeply positive funding lowers tier.

A coin clearing the high-level sweep filter starts at Tier C by default. It is *promoted* to B or A only after a deep-dive that documents the upgrade rationale on the coin note.

### Sizing discipline

- **Leverage is invariant at 20x.** Do not adjust leverage to express conviction; adjust the tier (collateral) instead.
- A position can be **promoted** (scale up to next tier) on confirmed thesis progression — narrative heating, structural breakout, MM activity surfacing.
- A position can be **demoted** (trim back) when the thesis weakens or a higher-tier candidate appears and capital must be reallocated.
- **Cross-margin caveat:** at 20x cross, an adverse move on a single position does not liquidate the line in isolation — the whole account absorbs MM. This means a string of losing C-tier picks bleeds equity available for A-tier conviction. Margin budget must be tracked explicitly. See [[Tickets/alpha-scanner/ALS-002]] for the proposed sweep + tracking system.
- **Stop discipline:** wide invalidation rather than tight stops (per the original strategy). At 20x, even a wide stop is a small-collateral trade — the tier *is* the risk control.

### Cross-link

Implementation, sweep methodology, and budgeting live in [[Tickets/alpha-scanner/ALS-002]].
