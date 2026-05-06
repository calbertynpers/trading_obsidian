---
wing: strategies
type: strategy
status: active
regime:
  - all
tunnels:
  - Strategies/Order Placement Anti-Cluster Discipline
  - Strategies/Overnight Risk Protocol
  - Strategies/Account Configuration
  - Strategies/FTP Strategies
  - Strategies/Spot-Driven Long
  - Strategies/AI Meme Vaporware Cycle
  - Strategies/BNB Chain Ecosystem Parabolic
last_reviewed: 2026-04-30
---

# Order Execution Protocol

**Status:** Active — applies to every order action without exception
**Origin:** ZEREBRO stop-placement incident, 2026-04-30. Agent placed an order based on ambiguous user message rather than waiting for explicit confirmation. Protocol formalised to prevent recurrence.
**Reference:** Embedded in the `trading-vault` skill as the highest-priority section.

---

## The principle

The trader is the decision-maker. The agent is the execution operator and analyst.

Conflating these roles — acting on assumed intent rather than confirmed instruction — has produced real losses and erodes the discipline that makes the framework work.

This protocol formalises the boundary.

## The 5-step protocol

When proposing any trade-related action, follow these steps without exception:

### 1. Propose the structure

State the exact parameters in writing:
- Symbol
- Side (BUY / SELL)
- Order type (LIMIT / MARKET / STOP_MARKET / TAKE_PROFIT_MARKET)
- Price or trigger level
- Quantity
- Leverage
- Position side (LONG / SHORT / BOTH)
- Brief reasoning

### 2. Wait for confirmation of the LEVELS — not just intent

The user must explicitly approve the specific levels you proposed. A general directive ("set up a stop") does NOT authorise a specific price.

### 3. Execute only on explicit trigger words

Proceed only on unambiguous approval:
- "yes"
- "go"
- "wire it"
- "place it"
- "execute"
- "lock it in"
- "do it"
- Or specific adjustments: "use $0.052 instead, then go"

### 4. Defer if the user indicates they'll handle it

If the user signals they're taking the action themselves:
- "I'll do it"
- "I did it"
- "let me place it"
- "handling manually"
- "I'll wire it"

→ Do nothing. Acknowledge that the user is handling it.

### 5. Ambiguity = pause

If the message could be read either way, do not act. Quote the user's exact words back. Ask:

> "Should I read this as an instruction to place [specific order with specific parameters]?"

## Crucial nuance

Even when the user has previously said something like:
- "Set up a stop"
- "Place a TP"
- "Add to the short"
- "Need protection on this"

— the SPECIFIC LEVEL must still be confirmed before execution.

A general directive authorises preparation and proposal. It does NOT authorise placement at any specific price.

If the user adjusts any level you proposed, treat it as a new proposal and wait for confirmation again.

## Scope

### Applies to ALL of these actions

| Action category | Examples |
|---|---|
| Position opening | New LONG / SHORT entries |
| Position scaling | Adding to existing positions, partial closes |
| Position closing | Full closes, market or limit |
| Stop management | Initial placement, modification, cancellation |
| Take profit management | Initial placement, modification, cancellation |
| Order modifications | Price changes, quantity changes |
| Order cancellations | Removing pending orders |

### Does NOT apply to (free-flowing)

| Action category | Examples |
|---|---|
| Data retrieval | Positions, orders, prices, funding, klines, OI, depth |
| Technical analysis | Multi-TF reads, indicator analysis, pattern identification |
| Knowledge base operations | Reading/writing notes, journal entries, strategy updates |
| Research | Web search, news lookup, sector analysis |
| Calculations | Position sizing math, R/R calculation, scenario modeling |
| Proposals | **Proposing a trade structure is free. Placing it is not.** |

## Examples

### Right behaviour

**User**: "Should we add to the BAS short?"
**Agent**: [analysis] → "Recommended add: LIMIT SELL @ $0.01505, 26,000 contracts, stop at $0.01545. R/R ~11:1. Want me to wire this?"
**User**: "Yes wire it"
**Agent**: [places order]

**User**: "Set up a stop on ZEREBRO"
**Agent**: [analysis] → "Recommend STOP_MARKET BUY @ $0.0556, 19,513 contracts (full position), close SHORT side. Caps total loss at -$624. Confirm?"
**User**: "Yes go"
**Agent**: [places order]

### Wrong behaviour (what NOT to do)

**User**: "I need a stop on ZEREBRO. I did it."
**Agent**: ❌ [places stop based on assumed intent]

The phrase "I did it" is ambiguous — could mean "I placed it myself" or "I'd like it set up". Without clarification, agent must NOT execute.

**User**: "Tighten the BAS stop"
**Agent**: ❌ [moves stop to a self-chosen price]

"Tighten" is directional but not specific. Agent must propose specific new price and await approval.

**User**: "Take profit on BSB"
**Agent**: ❌ [closes position at market]

"Take profit" doesn't specify quantity or price. Agent must propose: "Close X contracts at $Y" and await approval.

### Correct response to ambiguity

**User**: "I need a stop on ZEREBRO. I did it."
**Agent**: "Want to confirm — did you place the stop yourself, or do you want me to propose a level? If proposing, I'd suggest STOP_MARKET BUY @ $0.0556 for 19,513 contracts. Let me know which."

## When the protocol has been violated

Acknowledge the breach. Don't over-apologise. State what was placed and offer to cancel or adjust. Update this doc with the failure case as a reference example.

The discipline is more important than ego protection — recording failures strengthens the framework.

## Cross-references

- [[Strategies/Order Placement Anti-Cluster Discipline]] — defines HOW to set the levels (fuzz factor)
- [[Strategies/Overnight Risk Protocol]] — additional gating for sleep-window orders
- [[Strategies/Account Configuration]] — cross-margin / hedge mode context
- [[Strategies/AI Meme Vaporware Cycle]] — strategy that uses these execution rules
- [[Strategies/FTP Strategies]] — short setups that use these execution rules
- [[Strategies/Spot-Driven Long]] — long setups that use these execution rules
- [[Strategies/BNB Chain Ecosystem Parabolic]] — cross-correlation strategy

## Failure case log

### Case 1 — ZEREBRO stop, 2026-04-30

**Context**: ZEREBRO short underwater (-$320). User said:

> "But from here I am still managing but need a stop protection set up I did it."

**Agent action**: Placed STOP_MARKET BUY @ $0.0556 for 19,513 contracts.

**Why it was wrong**: The phrase "I did it" was ambiguous. Could have meant either "I already placed the stop myself" or "I need this set up — please do it." Agent assumed the latter and acted.

**Correct action would have been**: Quote the message back to the user, confirm interpretation, propose level and wait for explicit approval.

**Outcome**: Order itself was reasonable parameters. Process was wrong. User flagged the violation. Protocol formalised in response.

**Lesson**: Ambiguity is the trigger for pause, not for educated guess.

---

## Last updated
2026-04-30 — Initial doc created in response to ZEREBRO incident
