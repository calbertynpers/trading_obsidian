---
type: project
jira-epic: DT-4306
parent-epic: NFB-496
status: analysis
milestone: M1
epic-stage: scoped
priority: high
team:
  - Clint Albertyn
  - Sahil Dadia
  - Daire McCluskey
start-date: 2025-09-30
target-date: 2026-05-01
success-metric: "POC demo delivered to Bcurve stakeholders with functional agent query→response flow across all 5 in-scope question categories"
---

# DT-4306 Gen AI POC — Cameramatics AI Interface

## Summary

POC to develop and integrate the Cameramatics AI Interface — a chatbot that enables clients to ask natural-language questions about fleet data and receive analytical responses from an LLM-based agent. The agent runs on Agent Core with MCP tools connecting to the ORM (MySQL) and Reporting (PostgreSQL) databases. Part of the broader NFB-496 Generative AI initiative.

**Project category:** Greenfield (new AI capability, no existing infrastructure to extend)

## ⚠️ Status

**Updated: 2026-04-27**

POC nearing completion. Streamlit front-end built but not yet deployed — blocked on Seb availability for EC2 hosting setup. Reporting DB connectivity completed 2026-04-27 (trips data now functional). MCP development (DT-5402) in dev. Priority escalated from Medium to **High** at Bcurve call — GenAI is one of two major 2026 business deliverables.

Key blocker: front-end hosting deployment. Once resolved, Bcurve lead gets access for curated stakeholder demos.

MVP timeline target: ~3 months from now. Scoping work to begin immediately in parallel with POC finalization. Permissions/org boundary enforcement flagged as critical for MVP but not yet researched.

## Scope

### Included
- MCP development (integration and testing) — 12 tools across identity, admin, data query, diagnostic categories
- Reporting DB integration into MCP
- Front-end demo interface (Streamlit)
- Eval question documentation and benchmark catalog
- Agent evaluation framework (Marimo notebooks + LLM-as-judge)

### Not Included (POC)
- Production-grade UI/UX (polish goes into actual front-end later)
- Permissions/org boundary enforcement (flagged for MVP scope)
- Guardrails implementation (out-of-scope handling, topic restrictions)
- Long-term maintenance post-launch

### In-Scope Questions (Agent should answer)
1. "What are the most utilized vehicles in my fleet?" → `get_fleet_utilisation_summary`
2. "Which vehicles had the highest idling time recently?" → `get_fleet_utilisation_summary`
3. "Show me vehicles with the highest risk in the past 7 days" → `get_vehicle_risk_summary`
4. "Which drivers were at risk of falling asleep this week?" → `get_vehicle_alerts` (dmsfatiguealert)
5. "Show me vehicles operated outside business hours" → `get_vehicle_trips`

### Out-of-Scope Questions (Agent should decline gracefully)
1. "Show me maintenance alerts for this month"
2. "Which routes are most frequently used?"
3. "Give me a summary of fuel consumption by vehicle"

## Documents

- Eval framework spec: `.kiro/specs/agent-eval-framework/` (requirements, design, tasks)
- MCP tools reference: [Confluence — MCP tools](https://provision.atlassian.net/wiki/spaces/DT1/pages/4078862344/MCP+tools)
- Agent source: `cameramatics_snap_agent` repo

## Jira Tickets

| Key | Summary | Type | Status | Assignee |
|-----|---------|------|--------|----------|
| DT-5402 | MCP development | Story | In Dev | Sahil Dadia |
| DT-5422 | Finalisation of Frontend Streamlit App | Story | Analysis | Daire McCluskey |
| DT-5427 | Conduct final demo of POC front-end interface | Story | Blocked | Unassigned |
| DT-5432 | Documentation: Eval Questions (Approved/UnApproved) | Story | Analysis | Clint Albertyn |

## Key People

| Person | Role |
|--------|------|
| Clint Albertyn | Data team lead, eval framework, question catalog |
| Sahil Dadia | MCP development |
| Daire McCluskey | Front-end Streamlit app |
| Seb | Infrastructure/hosting (EC2 deployment) |
| Bcurve team (Adar) | Stakeholder, demo recipient, timeline driver |

## Meeting Log

### 2026-04-27 — GenAI POC/MVP Timeline Planning (Bcurve)

**Key decisions:**
1. POC target: end of this week (2026-05-02)
2. Priority escalated to High — GenAI + body cam are the two major 2026 deliverables
3. MVP timeline target: ~3 months (AWS reference point)
4. Background work (eval framework, question catalog) proceeds in parallel
5. No UI/UX polish needed for POC demo
6. Demo is curated only — Bcurve lead demos personally to selected stakeholders

**Concerns raised:**
- Permissions/org boundary enforcement — critical for MVP, not yet researched
- MVP scope undefined — needs scoping to hit 3-month target
- Guardrails not in place for customer-facing deployment

**Action items:**
- Deploy Streamlit to EC2 (blocked on Seb) → Dara/Seb
- Update priority to High in Jira → Clint
- Begin MVP scoping and roadmap → Clint
- Research permissions/org boundary enforcement → Team
- Follow-up call Tuesday 2026-04-29

## Impact Analysis: Bcurve Call vs Eval Framework Requirements

### Validations (meeting confirms requirements are on track)

- **Question catalog with golden standards** — Clint described exactly this to Bcurve. Maps to R1 (Test Case Library) and R2 (Out-of-Scope Ground Truth).
- **Iterative improvement loop** — "make changes, rerun tests, track score over time" workflow described. Maps to R15 and R14.
- **Out-of-scope handling** — explicitly mentioned "questions we don't want answered" including off-topic. Maps to R2 and R9.
- **Multi-model comparison** — mentioned comparing AWS models vs Claude. Supported by R16 (Configuration Snapshot).
- **Background work approved** — Bcurve greenlit eval framework work in parallel with POC.

### Gaps Identified (new concerns not covered in current requirements)

**1. Permissions / Org Boundary Eval Dimension — NEW REQUIREMENT NEEDED**
Bcurve flagged that the agent must enforce user permissions and org hierarchy. Current requirements have 6 eval dimensions but none cover data access control. Needs:
- New eval dimension: `permission_compliance`
- Test cases with different user personas (org admin vs regular user)
- Ground truth specifying which data each test user should/shouldn't see
- **Note:** Partially deterministic if enforced at ORM/MCP layer. Add as future eval dimension pending permissions research.

**2. Multi-Model Benchmarking — ENHANCEMENT TO R16**
Config snapshot should explicitly include: model provider, model version, temperature, and model-specific parameters as first-class fields.

**3. Remote Agent Connectivity — NOTE FOR R3**
Eval harness needs to connect to deployed (EC2-hosted) agent, not just local. Add note to R3 about supporting both local and remote agent endpoints.

**4. Ground Truth Data Dependency — NOTE FOR R1**
Ground truth is tied to test environment data. If test data is stale/incomplete, evals produce misleading scores. Need mechanism to refresh ground truth when test data changes.

### Concerns

**1. Timeline pressure vs framework completeness** — 3-month MVP target is aggressive. Recommendation: start lean with test library + code graders (R1-R6), add model graders (R7-R8) second, defer full dashboard (R14) and improvement summary (R15).

**2. Permissions research is a blocker** — Can't write permission_compliance test cases until enforcement mechanism is designed. Eval framework will initially measure quality without measuring security/access control.

**3. Jira priority mismatch** — DT-4306 is still Medium in Jira but Bcurve confirmed High. Needs updating.

## Open Questions

- [ ] What is the MVP scope? Needs definition to hit 3-month target
- [ ] Where should permissions be enforced? (data layer, API, MCP, agent prompt, or combination)
- [ ] What test environment data is available and how current is it?
- [ ] Should the eval framework also support Bedrock/AWS models for comparison?


## Eval Framework Backlog


### MVP

| Ticket | Title | Status | Spec |
|--------|-------|--------|------|
| [[projects/DT-4306 GenAI POC/backlog/AEF-001\|AEF-001]] | Design & Architecture | ✅ Done | `.kiro/specs/agent-eval-framework/` |
| [[projects/DT-4306 GenAI POC/backlog/AEF-002\|AEF-002]] | MVP Eval Framework — Complete Eval Loop | Not Started | Pending (current Kiro spec) |

**AEF-002 Sub-Tickets:**
- **AEF-002a:** Core data models + test case library + seed cases
- **AEF-002b:** Agent client + transcript capture + basic Marimo notebook
- **AEF-002c:** Code graders + grader pipeline + property tests
- **AEF-002d:** Response quality model grader (Claude)
- **AEF-002e:** Eval runner + result persistence + test corpus buildout

### Post-MVP Enhancements

| Ticket | Title | Priority | When to Pick Up | Spec |
|--------|-------|----------|-----------------|------|
| [[projects/DT-4306 GenAI POC/backlog/AEF-003\|AEF-003]] | Data Interpretation Model Grader | Medium | When data interpretation errors are a common failure mode | Not Started |
| [[projects/DT-4306 GenAI POC/backlog/AEF-004\|AEF-004]] | Multi-Trial Reliability (Pass@K) | Medium | When seeing inconsistent results between runs | Not Started |
| [[projects/DT-4306 GenAI POC/backlog/AEF-005\|AEF-005]] | Result Visualisation Dashboard | Medium | After 3-4 eval runs with data to compare | Not Started |
| [[projects/DT-4306 GenAI POC/backlog/AEF-006\|AEF-006]] | Human Grading Interface | Low | When team wants to validate automated grading | Not Started |
| [[projects/DT-4306 GenAI POC/backlog/AEF-007\|AEF-007]] | Config Snapshots & Cross-Model Benchmarking | Medium | When comparing Claude vs Bedrock | Not Started |
| [[projects/DT-4306 GenAI POC/backlog/AEF-008\|AEF-008]] | Rubric Template Management | Low | When editing rubrics frequently | Not Started |
| [[projects/DT-4306 GenAI POC/backlog/AEF-009\|AEF-009]] | Improvement Analysis Engine | Low | When team runs evals independently | Not Started |
| [[projects/DT-4306 GenAI POC/backlog/AEF-010\|AEF-010]] | Remote Agent Support (EC2) | Medium | When Streamlit demo is deployed | Not Started |
| [[projects/DT-4306 GenAI POC/backlog/AEF-011\|AEF-011]] | Permission Compliance Eval Dimension | High | After permissions enforcement is implemented | ⚠️ Blocked |
| [[projects/DT-4306 GenAI POC/backlog/AEF-012\|AEF-012]] | Guardrails / Topic Restriction Eval Dimension | Medium | When preparing for customer-facing deployment | Not Started |
