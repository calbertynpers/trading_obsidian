---
type: meeting-prep
date: 2026-04-30
project: "[[projects/DT-5483 Customer Data Retention/index]]"
participants:
  - Clint
  - Daragh
  - Rob
  - Paulo
---

# Data Retention — Meeting Agenda (30 Apr 2026)

Related: [[projects/DT-5483 Customer Data Retention/index]]

## Action Item Follow-ups (from 22 Apr)

- [ ] **Daragh — Geotab analysis**: Did you get to look at Geotab's data retention? What categories do they expose to customers? How do they present it?
- [ ] **Rob — Lifecycle rule proposals**: Any progress on the per-store implementation options (S3, DynamoDB, MySQL, OpenSearch)?
- [ ] **Clint — Categorization doc**: I've drafted the categorization from the discovery doc. Do we want to review the 9 categories today or circulate first?

## Safety Center Scope (Jong)

- [ ] Has Jong been invited to this call or the next one? We agreed last time he needs to be in on this.
- [ ] What data does the Safety Center own that needs retention policies? Driver behaviour scores, driver assignments, HST alert data — do we have a list?
- [ ] Does the Safety Center have its own data stores, or does everything flow through the Cameramatics platform stores?

## RMG Urgency (separate from this feature but needs a decision)

- [ ] Have we created the separate NFB/epic for RMG 3-year retention? The October 2026 deadline is 5 months away.
- [ ] Do we know exactly which S3 buckets have the 12-month TTL that will start deleting RMG video data? Can we just extend those TTLs as an immediate fix?
- [ ] Is the 8-year archive requirement confirmed by RMG, or is that our assumption?

## Category and Policy Decisions

- [ ] Are 9 categories too many for customers to configure? Should we collapse some (e.g., merge `device_state` into `telemetry`, merge `reports` into the category of data they contain)?
- [ ] Should some categories be non-configurable — always follow platform default? (`device_state`, `audit`?)
- [ ] Do we agree on the proposed defaults and minimums, or does anyone want to adjust? (24 months most things, 18 months telemetry, 5 years audit)

## Lifecycle States (confirm the 22 Apr agreement)

- [ ] Are we settled on three states: Live → Archived → Permanently Deleted? Last call we agreed archive can be bypassed (period = 0). Still good?
- [ ] What does "archived" physically mean per store? S3 Glacier transition is obvious. What about MySQL — separate schema? Read-only replica? Or just "old data we haven't deleted yet"?

## Technical Direction

- [ ] Archive before delete, or hard delete for MySQL/PostgreSQL? This is the biggest open design question and affects effort significantly.
- [ ] Do we need cross-store coordination (alert exists in MySQL + OpenSearch + S3 evidence — all three need cleanup together), or can we tolerate eventual consistency?

## Next Steps

- [ ] Can we assign the 6 child stories on DT-5483 today? They're all unassigned.
- [ ] What's our target for completing M1 (discovery & categorization)? Can we aim for end of next sprint?

## Notes

*Space for meeting notes — fill in during/after the call.*
