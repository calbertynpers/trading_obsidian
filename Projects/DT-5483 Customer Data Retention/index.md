---
type: project
status: analysis
milestone: M1
epic-stage: new-intake
jira-epic: DT-5483
nfb: NFB-463
priority: Medium
team:
  - Clint
  - Daragh
  - Rob
start-date: 2026-04-30
target-date: 
success-metric: 
---

# DT-5483 Customer Controlled Data Retention Policy

## Summary

**Category:** Greenfield project
**NFB:** 463 — Customer controlled data retention policy

Build a data retention management capability that allows the platform to enforce configurable retention policies per org and data category. The feature covers three capabilities:

1. **Default retention policy** — platform-wide defaults per data category (e.g., 24 months for alerts, 18 months for telemetry, 5 years for audit)
2. **Customer-configurable retention** — allow customers to reduce retention below the platform default (down to a defined minimum floor)
3. **Automated enforcement** — cleanup processes that delete or archive data per the active policy, across all data stores (DynamoDB, S3, OpenSearch, MySQL, PostgreSQL, PostGIS)

The platform currently retains nearly all data indefinitely. Out of ~170 catalogued data sources, only 3 have any active retention mechanism (2 DynamoDB tables with TTL, 1 OpenSearch index with ILM). This creates unbounded storage costs, degrading query performance, and leaves customers without control over their own data lifecycle.

**Data lifecycle states** (agreed 22 Apr 2026): Live → Archived → Permanently Deleted. Customers can bypass the archive stage by setting archive period to zero (live → deleted directly).

### Scope

**Included:**
- Data categorization taxonomy (9 proposed categories: users, vehicles, alerts, trips, telemetry, evidence, reports, audit, device_state)
- Platform default retention periods and customer-configurable minimums per category
- Enforcement mechanisms per data store (DynamoDB TTL, S3 lifecycle, OpenSearch ILM, MySQL/PostgreSQL scheduled purge)
- RetentionPolicy data model and CRUD API
- Customer-facing settings UI
- Deletion audit trail
- Cross-store consistency (e.g., alert deleted from MySQL + OpenSearch + S3 evidence)
- Safety Center data (Jong's team — to be brought in)

**Excluded (separate workstreams):**
- RMG-specific 3-year retention / 8-year archive (separate NFB — urgent, October 2026 deadline)
- GDPR right-to-be-forgotten (per-user deletion — different mechanism)
- EU data residency / multi-region hosting
- Driver assignment data migration from Safety Center
- Data anonymization for analytics (deferred to later iteration)

### Success Criteria

- All ~170 data sources have a defined retention policy
- Enforcement running on platform defaults across DynamoDB, S3, and OpenSearch (Milestone 2 quick wins)
- Customer-configurable retention available via API and UI
- MySQL/PostgreSQL purge jobs running for highest-volume tables
- Deletion audit trail in place

## ⚠️ Status

*Bootstrapped 30 Apr 2026.* Epic created today (DT-5483) in New Intake sprint. 6 child stories exist, all in Analysis, unassigned, no estimates. Significant prior work exists: Confluence discovery doc (11 Mar 2026) with full data catalog, proposed data model, 9 data categories, enforcement approaches, and 5-phase rollout. Meeting held 22 Apr 2026 with Daragh, Rob, and Paulo — agreed on data lifecycle states, action items assigned (categorization doc → Clint, lifecycle rule proposals → Rob, Geotab analysis → Daragh). Jong (Safety Center) to be invited to next call. No `requirements.md` or `architecture.md` yet in Obsidian — the Confluence doc is the primary artifact. Next step: finalize data categorization document and assign child stories.

## Jira Comment Briefing

No comments on the epic or child issues yet — the epic was created today (30 Apr 2026). All context lives in the Confluence discovery doc and the 22 Apr meeting transcript.

**Key context from the 22 Apr 2026 meeting (Clint, Daragh, Rob, Paulo):**

- **RMG urgency surfaced**: RMG requires 3-year frontline data retention. Come October 2026 (1-year go-live anniversary), current 12-month S3 TTLs will start deleting video data. This needs a separate NFB and immediate action — don't make it dependent on the full retention feature.
- **8-year archive for RMG**: After 3 years live, data should be archived for an additional 5 years (8 years total).
- **Data lifecycle agreed**: Live → Archived → Permanently Deleted. Archive can be bypassed (set archive period to zero). This is simpler than the 4-state model in the original doc.
- **Scope is holistic**: Must cover Safety Center (Jong's team) too, not just the Cameramatics platform. Driver data, safety scores, and HST data all need retention policies.
- **GDPR parked**: Anonymization vs deletion question raised but deferred. Focus on retention mechanics first. AWS Standard Contractual Clauses noted for US hosting. EU data residency is a separate concern entirely.
- **Geotab as benchmark**: Daragh to research Geotab's data retention implementation — they've invested heavily in this and their approach is likely fit-for-purpose globally.
- **Action items from call**:
  - Clint: Separate data categorization document
  - Rob: Lifecycle rule implementation proposals per service type (S3, DB, DynamoDB, Elastic)
  - Daragh: Geotab competitor analysis
  - Invite Jong to next week's call
- **Next call**: Same time the following week (week of 28 Apr — may have already happened or be imminent)

## Documents

| Document | Status | Notes |
|----------|--------|-------|
| [Confluence: NFB 463 Discovery Doc](https://provision.atlassian.net/wiki/spaces/RAS/pages/3974823939) | Published (v2, 11 Mar 2026) | Primary artifact — problem statement, data model, categories, enforcement approaches, open questions, phasing |
| Confluence sub-pages (9 category catalogs) | Published (11 Mar 2026) | Per-category data source catalogs: Users, Vehicles, Alerts, Trips, Telemetry, Evidence, Reports, Audit, Device State |
| `analysis/data-retention-discovery.md` | Workspace file | Source doc for the Confluence page — 9 categories, 3 milestones, 13 priority sources |
| `analysis/data-retention-catalog.md` | Workspace file | Detailed per-store catalog: ~50 DynamoDB tables, ~30 S3 buckets, 16 ES indices, MySQL entities, PostgreSQL tables |
| `analysis/data-retention-confluence.md` | Workspace file | Confluence-formatted catalog with Lambda cross-references per data source |

## Jira Tickets

| Key | Type | Summary | Status | Assignee |
|-----|------|---------|--------|----------|
| [DT-5483](https://provision.atlassian.net/browse/DT-5483) | Epic | Customer Controlled Data Retention Policy (Milestone 1 — Discovery & Categorization) | Analysis | Clint |
| [DT-5484](https://provision.atlassian.net/browse/DT-5484) | Story | Inventory and Categorize Data Assets Across All Data Stores | Analysis | Unassigned |
| [DT-5485](https://provision.atlassian.net/browse/DT-5485) | Story | Define Data Lifecycle States and Transitions | Analysis | Unassigned |
| [DT-5486](https://provision.atlassian.net/browse/DT-5486) | Story | Assess Current Data Retention Practices and Gaps | Analysis | Unassigned |
| [DT-5487](https://provision.atlassian.net/browse/DT-5487) | Task | Evaluate Technical Enforcement Mechanisms per Data Store | Analysis | Unassigned |
| [DT-5488](https://provision.atlassian.net/browse/DT-5488) | Story | Draft Initial Customer-Facing Retention Policy Configuration Options | Analysis | Unassigned |
| [DT-5489](https://provision.atlassian.net/browse/DT-5489) | Task | Map Data Flows and Identify Data Movement Between Lifecycle States | Analysis | Unassigned |

## Proposed Data Model

From the Confluence discovery doc — starting point for discussion:

```
RetentionPolicy
├── id (UUID)
├── org_id (FK → Org, nullable — null = platform default)
├── data_category (enum: users, vehicles, alerts, trips, telemetry, evidence, reports, audit, device_state)
├── retention_months (int) — how long to keep data live from creation date
├── archive_months (int) — how long to keep in archive after live period (0 = skip archive)
├── created_by (FK → Users)
├── created_on (datetime)
├── updated_by (FK → Users)
├── updated_on (datetime)
└── is_active (bool)
```

**Resolution logic:** Enforcement job looks up policy for org + category. If none exists, falls back to platform default (org_id IS NULL).

### Proposed Defaults

| Category | Default Retention | Customer Minimum | Rationale |
|----------|------------------|------------------|-----------|
| `users` | Indefinite | N/A | Core entity — persists until deletion request |
| `vehicles` | Indefinite | N/A | Core entity — persists until deletion request |
| `alerts` | 24 months | 12 months | Year-over-year comparison, incident review |
| `trips` | 24 months | 12 months | Reporting, fleet analysis |
| `telemetry` | 18 months | 6 months | High volume, diminishing value over time |
| `evidence` | 24 months | 12 months | Incident evidence, insurance claims |
| `reports` | 24 months | 12 months | Report re-download, audit |
| `audit` | 5 years | 24 months | Compliance, legal |
| `device_state` | 18 months | 12 months | Operational, rebuildable from MySQL |

> **[DISCUSSION]** Are 9 categories the right granularity? Should some be non-configurable (e.g., device_state always follows platform default)?

> **[DISCUSSION]** Should `audit` have a higher minimum than other categories to satisfy compliance?

## Highest Priority Data Sources

From the catalog — these have the highest volume, no retention mechanism, and the most cost/performance impact:

| # | Data Source | Store | Category | Why Priority |
|---|-----------|-------|----------|-------------|
| 1 | `GenericAlert` hierarchy | MySQL | alerts | Highest write volume table. Unbounded growth. |
| 2 | All alert indices (except `speeding_alerts`) | OpenSearch | alerts | 10 indices with no ILM. |
| 3 | `Pg_TrackingPoint` / `Pg_Lines` | PostGIS | trips | GPS points per device per trip. Highest volume in GROM. |
| 4 | `TripTable` / `DailyTripTable` | PostgreSQL | trips | Trip data never purged. |
| 5 | Timeseries tables (TSModelC/D, SpanDynamoDB) | DynamoDB | telemetry | Accumulates indefinitely. |
| 6 | Regional file upload buckets (EU/SYD/US) | S3 | evidence | DVR video/images. No lifecycle policy. |
| 7 | Expired Cognito users | Cognito | users | Cleanup handler commented out. PII accumulating. |
| 8 | `logging_table_name` | DynamoDB | audit | PII audit data with no retention. |
| 9 | `FileRequestsDynamo` | DynamoDB | evidence | 24 Lambdas write to it. No TTL. |
| 10 | `input_write_bucket` | S3 | telemetry | Raw SQS events. High volume, never expired. |

## Enforcement Approach Per Store

| Store | Mechanism | Complexity |
|-------|-----------|-----------|
| DynamoDB | TTL attribute (native auto-delete) | Low |
| S3 | Lifecycle policies (expiration + Glacier transition) | Low |
| OpenSearch | ILM policies (hot → warm → delete) | Low–Medium |
| MySQL | Scheduled purge Lambda (batch delete, FK cascade ordering) | High |
| PostgreSQL | Scheduled purge Lambda (partition-based if available) | High |
| PostGIS | Scheduled purge Lambda | High |
| Cognito | Fix commented-out cleanup handler | Low |

## Proposed Milestones (Full Feature)

This epic covers Milestone 1. The full feature spans 5 milestones:

### M1 — Discovery & Categorization (this epic)
- Finalize data category taxonomy
- Define data lifecycle states and transitions
- Assess current retention practices and gaps
- Evaluate enforcement mechanisms per store
- Competitor analysis (Geotab)
- Draft customer-facing configuration options

### M2 — Quick Wins (DynamoDB TTL + S3 Lifecycle + OpenSearch ILM)
- Add TTL to high-volume DynamoDB tables
- Add S3 lifecycle policies to data buckets
- Apply ILM to all OpenSearch alert indices
- Fix Cognito expired user cleanup
- *Estimated: 3–4 sprints*

### M3 — Retention Policy Data Model & API
- Create `RetentionPolicy` ORM entity + seed data
- Build CRUD API (admin-only initially)
- Build UI settings page
- *Estimated: 2–3 sprints*

### M4 — MySQL & PostgreSQL Enforcement
- Alert hierarchy purge Lambda (MySQL)
- Trip/mileage purge Lambda (PostgreSQL + PostGIS)
- History table audit and purge
- *Estimated: 3–5 sprints*

### M5 — Cross-Store Coordination & Polish
- Cross-store deletion coordinator
- Customer notification before enforcement
- Deletion audit trail
- Legal hold capability (if required)
- *Estimated: 2–3 sprints*

## Open Questions

### Policy Design
| # | Question | Status |
|---|----------|--------|
| Q1 | Platform default retention period per category? | Proposed — needs confirmation |
| Q2 | Customer minimum retention period? | Proposed — needs confirmation |
| Q3 | Are 9 categories the right granularity? | Open |
| Q4 | Per-org only, or per-org + per-node? | Open |
| Q5 | Grace period before hard deletion? | Open |
| Q6 | What happens to data when org is disabled/deleted? | Open |

### Technical Design
| # | Question | Status |
|---|----------|--------|
| Q7 | Archive before delete, or hard delete (MySQL/PostgreSQL)? | Open |
| Q8 | Cross-store consistency mechanism? | Open |
| Q9 | FK cascade handling for alert deletion? | Open |
| Q10 | Per-org or global enforcement runs? | Open |
| Q11 | Backfill retention metadata for existing data? | Open |

### Compliance & Legal
| # | Question | Status |
|---|----------|--------|
| Q16 | Regulatory minimums per data type per jurisdiction? | Open |
| Q17 | Legal hold capability needed? | Open |
| Q18 | GDPR right-to-be-forgotten interaction? | Parked — separate mechanism |
| Q19 | Deletion audit trail requirements? | Open |

## Key People

| Person | Role |
|--------|------|
| Clint | Data team lead, epic owner, data categorization |
| Daragh | Product/architecture, Geotab competitor analysis |
| Rob | Platform engineering, lifecycle rule implementation proposals |
| Paulo | Project coordination |
| Jong | Safety Center lead (to be brought in for HST data scope) |

## Related Work

- **RMG 3-Year Retention** — Separate NFB needed. Hard deadline October 2026 (1-year go-live anniversary). S3 TTLs will start deleting video data. Must not be blocked on this feature.
- **Driver Assignments** — Ongoing workstream to bring driver assignment data from Safety Center into Cameramatics. Related because that data will need retention policies too.
- **MySQL 8 Migration** — Removed query cache that previously masked unbounded table growth performance impact. Makes retention enforcement more urgent.

## Milestone Tracker

- [ ] M1: Requirements documented
- [ ] M1: Technical research completed
- [ ] M1: Solution proposal documented
- [ ] M2: POC executed and findings documented
- [ ] M3: Go/no-go decision recorded

### Definition of Ready (M3 → M4)

- [ ] Measurable goal (`success-metric` defined)
- [ ] Target date set
- [ ] Requirements complete (all `[DISCUSSION]` items resolved)
- [ ] Approval recorded (decision note in `decisions/`)
- [ ] Jira subtasks estimated and assigned
- [ ] Sprint allocated
- [ ] Open questions resolved (blocking items only)
