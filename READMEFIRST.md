---
wing: root
type: steering
purpose: First file any agent reads when accessing this vault
---

# AGENT.md — Trading Vault Steering Document

**Read this first.** This document tells you how this vault is structured, how to navigate it, and how to read/write notes correctly.

## Vault Purpose

This is a **trading knowledge base** for crypto futures trading on Binance. It serves as:

1. **State machine** — current positions, portfolio status, market regime
2. **Strategy library** — trading playbooks and decision frameworks
3. **Market intelligence** — narratives, macro context, coin profiles
4. **Trade journal** — daily logs and evolving observations

Your primary job as an agent is to **retrieve the right context for trading decisions**: look up a coin, determine which strategy applies given current market conditions, check if existing positions align, and recommend actions.

## Structure — The Building Metaphor

The vault uses a spatial metaphor: a **building** with **wings** (top-level domains), **rooms** (folders), and **notes** (individual documents). Notes link to each other via `[[wikilinks]]` (tunnels).

| Wing | Folder | Purpose |
|------|--------|---------|
| **Coins** | `Trading/Coins/` | Per-coin profiles: fundamentals, technicals, position state, strategy assignment |
| **Strategies** | `Trading/Strategies/` | Trading playbooks, checklists, and decision frameworks |
| **Narratives** | `Trading/Narratives/` | Market narratives, macro context, sector analysis |
| **Journal** | `Trading/daily/` | Daily market reviews, trade logs, action items |
| **Root** | `Trading/` | Building Map, Portfolio Overview, Trade Log, this steering doc |

## YAML Frontmatter Schema

Every note has YAML frontmatter at the top. This is your **index** — read it before parsing the full note body.

### Coin Notes (`wing: coins`)

```yaml
---
wing: coins
type: coin-profile
symbol: BLUR          # Binance ticker
status: active        # active | watching | closed | dead
narrative:            # list of narrative names this coin belongs to
  - NFT Recovery
strategy:             # list of strategy names that apply
  - Long Bottom-Fishing
position: long        # long | short | hedged | flat
leverage: 75          # current leverage (0 if flat)
last_reviewed: 2026-04-17
tunnels:              # related notes in other wings
  - Narratives/NFT Recovery
  - Strategies/FTP Strategies
tags:                 # freeform tags for filtering
  - clean-tokenomics
  - strong-setup
---
```

### Strategy Notes (`wing: strategies`)

```yaml
---
wing: strategies
type: strategy
status: active        # active | suspended | deprecated
regime:               # market regimes where this strategy works
  - squeeze
  - all
tunnels: []
---
```

### Narrative Notes (`wing: narratives`)

```yaml
---
wing: narratives
type: narrative
heat: hot             # hot | heating | warming | cold | dead
regime: squeeze       # current market regime context
last_reviewed: 2026-04-19
tunnels: []           # related coin and strategy notes
---
```

### Journal Notes (`wing: journal`)

```yaml
---
wing: journal
type: daily
date: 2026-04-19
regime: squeeze       # market regime on that day
---
```

### MOC Notes (`type: moc`)

```yaml
---
wing: root
type: moc
scope: vault          # vault | wing
---
```

## Agent Retrieval Workflows

### "What do I do with [COIN]?"

1. Read `Trading/Coins/[COIN].md` — check `status`, `position`, `strategy`, `narrative`
2. Read each strategy note listed in `strategy` field
3. Check strategy `regime` matches current regime (from latest journal or Narrative Index)
4. Read the narrative note(s) listed in `narrative` field — check `heat`
5. Synthesize: does the position align with the strategy given current regime and narrative heat?

### "What's my current exposure?"

1. Read `Trading/Portfolio Overview.md` for the snapshot
2. For detail: list all notes in `Trading/Coins/`, read YAML frontmatter, filter where `position != flat`
3. Cross-check open orders against `Trading/Trade Log.md` open-trade table

### "What narratives are hot?"

1. Read `Trading/Narratives/Narrative Index.md`
2. Or: list all notes in `Trading/Narratives/`, read YAML frontmatter, filter by `heat`

### "Should I enter a new coin?"

1. Check which narrative the coin belongs to → read that narrative note → is the heat rising?
2. Check applicable strategies by current regime
3. Score the coin against the strategy's entry criteria
4. Check portfolio exposure — how many active positions? Leverage? Wallet reserve?
5. **If the limit will sit into a sleep/offline window, run [[Strategies/Overnight Risk Protocol]] first**

### "What's the current market regime?"

1. Read the most recent daily journal note in `Trading/daily/`
2. Check the `regime` field in its YAML
3. Cross-reference with `Trading/Strategies/Squeeze Environment Playbook.md` if regime is `squeeze`

## Writing Rules

When creating or updating notes:

1. **Always include YAML frontmatter** matching the schema above
2. **Update `last_reviewed`** when modifying a note
3. **Keep `status` and `position` current** on coin notes — these are the most-queried fields
4. **Use `[[wikilinks]]`** to connect related notes (these are the tunnels)
5. **Add new notes to the correct wing folder** — don't put coins in Strategies, etc.
6. **Update the relevant MOC** when adding a new note (Building Map, Narrative Index, or Portfolio Overview)
7. **Log every trade** to `Trading/Trade Log.md` — open trades, closes, realised P&L, lesson-bank entries
8. **Before placing any limit order** that will sit into an unsupervised window, run the [[Strategies/Overnight Risk Protocol]] checklist and record the score in the trade log entry

## Key Concepts

- **FTP (Fade The Pump):** Short overextended pumps. See `Strategies/FTP Strategies.md`
- **Crime Coins:** Insider-manipulated coins. See `Narratives/Crime Coins.md` and `Strategies/Crime Coin Checklist.md`
- **Controlled Blow-Off:** VC-backed fresh listings with heavy float rotation. Surface similar to crime coins, mechanism different. Scored 1–3 on Crime Coin Checklist, but still high overnight risk. CHIPUSDT is the reference case (see [[Coins/CHIP]]).
- **Squeeze Environment:** Current market regime (Apr 2026) producing violent short squeezes. See `Strategies/Squeeze Environment Playbook.md`
- **Overnight Risk Protocol:** 6-point checklist for any limit order being placed into a sleep/offline window. ≥3 signals = overnight-risky, apply remediation ladder. See [[Strategies/Overnight Risk Protocol]]. Origin: Trade 003 CHIPUSDT `-$200` on 2026-04-22.
- **Two-Layer Position Architecture:** Large thesis positions split into (a) no-miss lean — smaller, always-on core and (b) thesis tranches — laddered GTC limits averaging down. See [[Coins/TAO]] for the reference implementation.
- **Market Regime:** The overarching market condition that determines which strategies are safe to run. Currently: `squeeze`

## What Not to Do

- Don't create notes outside the wing folders without good reason
- Don't remove YAML frontmatter — it's the agent-readable index
- Don't update position/leverage data without the user confirming the trade happened
- Don't assume a strategy applies without checking the regime filter
- Don't treat this vault as a trading bot — it's a knowledge base for decision support, not execution
- Don't place overnight limits without running the [[Strategies/Overnight Risk Protocol]] — Trade 003 is on the record for a reason
