---
wing: root
type: moc
scope: vault
---

# Building Map — Trading Vault

Top-level index for the entire vault. Start here, then drill into the wing you need.

## Steering

- [[READMEFIRST]] — How this vault works (read first if you're an agent)
- [[Strategies/Order Execution Protocol]] — **MUST follow for any order action**

## Wings

### Coins — Position State & Coin Profiles
> Current positions, fundamentals, technicals, strategy assignment per coin.

| Coin | Status | Position | Narrative | Strategy |
|------|--------|----------|-----------|----------|
| [[AIA]] | watching | flat | AI Infrastructure | FTP |
| [[AXL]] | active | hedged | Cross-Chain | Long Bottom-Fishing |
| [[BIO]] | active | hedged | DeSci | Long Bottom-Fishing, Strategy G |
| [[BLUR]] | active | hedged | NFT Recovery | Long Bottom-Fishing |
| [[ID]] | watching | flat | Web3 Identity | FTP |
| [[PARTI]] | watching | flat | L1-L2 Infrastructure | Long Bottom-Fishing |
| [[RESOLV]] | watching | flat | Stablecoin Infrastructure | — |
| [[SAGA]] | active | long | L1-L2 Infrastructure | Long Bottom-Fishing |
| [[SONIC]] | active | hedged | Gaming, L1-L2 Infrastructure | — |

→ Full portfolio snapshot: [[Portfolio Overview]]

### Strategies — Trading Playbooks
> Decision frameworks, entry/exit criteria, risk rules.

| Strategy | Status | Regime |
|----------|--------|--------|
| [[Order Execution Protocol]] | **active — gates all order actions** | all |
| [[FTP Strategies]] | active | all (with caveats in squeeze) |
| [[Long Bottom-Fishing Strategy]] | active | all |
| [[Crime Coin Checklist]] | active | all |
| [[Squeeze Environment Playbook]] | active | squeeze |
| [[Macro Bull Setup - April 2026]] | active | all |
| [[AI Meme Vaporware Cycle]] | active | squeeze, all |
| [[Order Placement Anti-Cluster Discipline]] | active | all |
| [[Overnight Risk Protocol]] | active | all |
| [[Spot-Driven Long]] | active | all |
| [[BNB Chain Ecosystem Parabolic]] | active | all |
| [[Account Configuration]] | active | all |

### Narratives — Market Intelligence
> Sector narratives, macro context, heat tracking.

→ Full index: [[Narrative Index]]

| Narrative | Heat |
|-----------|------|
| [[Crime Coins]] | 🔥🔥🔥 Hot |
| [[Perp DEX Infrastructure]] | 🔥🔥🔥 Hot |
| [[Meme L1]] | 🔥🔥🔥 Hot |
| [[AI Infrastructure]] | 🔥🔥 Mixed |
| [[DeSci]] | 🔥🔥 Heating |
| [[Memecoin Squeeze]] | 🔥🔥 Active |
| [[Popular Coin Recovery]] | 🔥 Warming |
| [[Doomed Coin Rotation]] | 🔥 Early |
| [[DeFi Revival]] | 🔥 Warming |
| [[NFT Recovery]] | 🔥 Early |
| [[Cross-Chain]] | 🔥 Warming |
| [[Gaming]] | ❄️ Cold |
| [[L1-L2 Infrastructure]] | ❄️ Cold |
| [[Web3 Identity]] | ❄️ Cold |
| [[Stablecoin Infrastructure]] | 💀 Dead |

### Journal — Daily Logs
> Market reviews, trade decisions, action items.

| Date | Regime | Focus |
|------|--------|-------|
| [[2026-04-19]] | squeeze | Mid-April market review, narrative rotation, action plan |
| [[2026-04-17]] | squeeze | Deep research session, coin evaluations, long_scan tool |

### Projects — Multi-step work
> Build-out specs and tooling.

- [[Projects/micro-position-scanner]] — ~100 tracker positions for sector signal
- [[Projects/Microstructure Signal Module]] — orderbook & squeeze anticipation system (spec)

## Current State (Apr 30, 2026)

- **Market regime:** Squeeze-heavy
- **Macro setup:** Bull setup strengthening, post-Fed
- **Active positions:** 90+
- **Order Execution Protocol:** Active and enforced
