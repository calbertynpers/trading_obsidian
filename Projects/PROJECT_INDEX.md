---
type: index
last-updated: 2026-04-30
---

# Project Index

Master index of all projects tracked in the Obsidian vault.

---

### [[projects/DT-5483 Customer Data Retention/index|DT-5483 Customer Controlled Data Retention Policy]]
**Priority:** Medium · **Status:** Analysis (M1) · **Team:** Clint, Daragh, Rob · **Epic:** DT-5483
**Updated:** 2026-04-30

Build customer-configurable data retention policies with automated enforcement across all data stores (DynamoDB, S3, OpenSearch, MySQL, PostgreSQL, PostGIS). Currently ~170 data sources with only 3 having any retention mechanism. 9 proposed data categories, lifecycle states (live → archived → deleted), and 5-milestone rollout. Significant prior work: Confluence discovery doc (Mar 2026), full data catalog, and stakeholder meeting (22 Apr 2026). Related: RMG 3-year retention (separate NFB, urgent October 2026 deadline).

**Related Projects:** None yet

---

### [[projects/DT-4306 GenAI POC/index|DT-4306 GenAI POC]]
**Priority:** Unknown · **Status:** Unknown · **Team:** Unknown · **Epic:** DT-4306
**Updated:** 2026-04-30

*Pre-existing project folder — not yet assessed. Needs review.*

---

## Cross-Project Relationship Map

```
DT-5483 Customer Data Retention
  ├── related: RMG 3-Year Retention (separate NFB, not yet created)
  ├── related: Driver Assignments (Safety Center data)
  └── context: MySQL 8 Migration (removed query cache, makes retention more urgent)
```
