---
type: project-artifact
project: "[[projects/DT-5483 Customer Data Retention/index]]"
jira-story: DT-5484
status: draft
last-updated: 2026-04-30
---

# Data Asset Inventory & Categorization

**Jira:** [DT-5484](https://provision.atlassian.net/browse/DT-5484) — Inventory and Categorize Data Assets Across All Data Stores
**Parent:** [[projects/DT-5483 Customer Data Retention/index|DT-5483 Customer Data Retention]]

## Purpose

Define the data categories that customers will see when configuring retention policies, and map every platform data source to exactly one category. This is the foundation — enforcement jobs, the API, and the UI all depend on this taxonomy being right.

## Proposed Categories

| # | Category | Customer-Facing Label | What It Covers |
|---|----------|----------------------|----------------|
| 1 | `users` | User Data | User accounts, profiles, invitations, role assignments, contacts, Cognito records |
| 2 | `vehicles` | Vehicle & Asset Data | Vehicle records, asset records, device assignments, vehicle-asset associations |
| 3 | `alerts` | Alerts | All alert types — IMU, IO, DMS, ADAS, speeding, geofence |
| 4 | `trips` | Trips & Journeys | Trip records, daily trips, mileage, spans, sessions, GPS tracking points |
| 5 | `telemetry` | Telemetry | Raw telemetry data, timeseries, ACC transitions |
| 6 | `evidence` | Video & Images | DVR video/image files, file requests, computer vision processing |
| 7 | `reports` | Reports | Generated reports, fault reports, scheduled report output |
| 8 | `audit` | Audit Logs | User activity logs, history tables |
| 9 | `device_state` | Device Status | Device presence, connectivity, bonded state, job/session tracking |

> **[DISCUSSION]** Is 9 the right number? Options to simplify:
> - Merge `device_state` into `telemetry` (both are operational/device data)
> - Merge `reports` into the category of data they contain (alert reports → alerts, trip reports → trips)
> - Make `users` and `vehicles` non-configurable (always indefinite — core entities)
> - Make `audit` non-configurable (always 5 years — compliance)
> That would reduce customer-facing categories to 5: Alerts, Trips & Journeys, Telemetry, Video & Images, Reports

## Proposed Defaults & Minimums

| Category | Default | Customer Min | Customer Max | Rationale |
|----------|---------|-------------|-------------|-----------|
| `users` | Indefinite | — | — | Core entity, persists until deletion request |
| `vehicles` | Indefinite | — | — | Core entity, persists until deletion request |
| `alerts` | 24 months | 12 months | 24 months | Year-over-year comparison, incident review |
| `trips` | 24 months | 12 months | 24 months | Reporting, fleet analysis |
| `telemetry` | 18 months | 6 months | 18 months | High volume, diminishing value |
| `evidence` | 24 months | 12 months | 24 months | Incident evidence, insurance claims |
| `reports` | 24 months | 12 months | 24 months | Report re-download, audit |
| `audit` | 5 years | 24 months | 5 years | Compliance, legal |
| `device_state` | 18 months | 12 months | 18 months | Operational, rebuildable |

> **[DISCUSSION]** Customers can only reduce retention below the platform default, not extend it. Is that right? Some customers (e.g., RMG) want longer retention. Should we allow extending beyond the default for a fee or as a contract option?

## Data Source Mapping

### Alerts

| Data Source | Store | Current Retention | Notes |
|-----------|-------|-------------------|-------|
| `GenericAlert` hierarchy (ImuAlert, IoAlert, DMSAlert, ADASAlert, SpeedingAlert, GeoAlert) | MySQL | None | Highest write volume table. ~10 API Lambdas read. |
| `imu_alerts` | OpenSearch | None | No ILM. High volume. |
| `io_alerts` | OpenSearch | None | No ILM. |
| `dms_alerts` | OpenSearch | None | No ILM. PII (driver behaviour). |
| `adas_alerts` | OpenSearch | None | No ILM. |
| `speeding_alerts` | OpenSearch | Has ILM | Dual-write pattern — template for other indices. |
| `geo_boundary_alerts` / `geo_boundary_alerts-2.1` | OpenSearch | None | v1 may be stale if v2.1 is active write target. |
| `geo_parking_alerts` / `geo_parking_alerts-2.1` | OpenSearch | None | Same as above. |
| `geo_speeding_alerts` / `geo_speeding_alerts-2.1` | OpenSearch | None | Same as above. |
| `AlertTable` | DynamoDB | None | Used by AlertManager. |
| `ThrottleTable` | DynamoDB | None | Transient throttle state. 4 Lambdas. |
| `GeoStateDynamoDBTableName` | DynamoDB | None | Geofence session state. |
| `AlertNotificationsTable` | DynamoDB | None | Notification state. |
| `DDBValidatorRequestsTable` | DynamoDB | None | IMU ML request aggregation. |
| `AlertStatus` | MySQL | None | Linked to GenericAlert. |
| `Prediction` | MySQL | None | ML predictions on ImuAlert. |
| `PotentialImuAlert` | MySQL | None | Pre-validation candidates. Should be ephemeral. |

### Trips

| Data Source | Store | Current Retention | Notes |
|-----------|-------|-------------------|-------|
| `TripTable` | PostgreSQL | None | Detailed trip records. High volume. |
| `DailyTripTable` | PostgreSQL/DynamoDB | None | Core reporting data. 4 Lambdas. |
| `MileageTable` / `MileageTableRpt` | PostgreSQL/DynamoDB | None | Mileage calculations. |
| `SessionModelTable` / `SessionTable` | PostgreSQL/DynamoDB | None | Session tracking. 5 Lambdas. |
| `SpanTable` | PostgreSQL/DynamoDB | None | Time span records. |
| `TripAggregrationTable` | DynamoDB | None | Aggregated trip data. Lower volume. |
| `acc_transitions_table` | DynamoDB | None | ACC state transitions. |
| `Pg_TrackingPoint` | PostGIS | None | GPS points per device per trip. Highest volume in GROM. |
| `Pg_Lines` | PostGIS | None | Trip line geometries. |
| `report_raw_trip` | PostgreSQL | None | Raw trip reporting data. |

### Telemetry

| Data Source | Store | Current Retention | Notes |
|-----------|-------|-------------------|-------|
| `TSModelCTable` | DynamoDB | None | Timeseries model C. Trip calculation pipeline. |
| `TSModelDTable` | DynamoDB | None | Timeseries model D. GPS data for IMU + reporting. |
| `SpanDynamoDBTableName` | DynamoDB | None | Telemetry span data. 4 Lambdas. |
| `TSTable` / `TSTableName` | DynamoDB | None | GPS/speed/ACC telemetry. 5 Lambdas. |
| `SingleSpanModelTable` | DynamoDB | None | Single span telemetry. IMU preprocessing. |
| `input_write_bucket` | S3 | None | Raw SQS event archive. Partitioned by hour. **High volume.** |
| `OutputBucket` | S3 | None | Avro raw data ETL output. |
| `AssetTrackingTable` | DynamoDB | None | Asset location history. |
| `AssetTrackingTimeseriesTable` | DynamoDB | None | Asset tracking timeseries. |

### Evidence

| Data Source | Store | Current Retention | Notes |
|-----------|-------|-------------------|-------|
| `S3FileUploadBucketEU` | S3 | None | DVR video/images. EU region. |
| `S3FileUploadBucketSYD` | S3 | None | DVR video/images. APAC region. |
| `S3FileUploadBucketUS` | S3 | None | DVR video/images. US region. |
| `TempS3FileUploads` | S3 | None | Temporary uploads. Should be ephemeral. |
| `FileRequestsDynamo` | DynamoDB | None | File request tracking. **24 Lambdas.** |
| `CompVisionInputBucket` | S3 | None | CV input images. Should expire after processing. |
| `CompVisionDailyReportS3` | S3 | None | CV daily analysis logs. |

### Reports

| Data Source | Store | Current Retention | Notes |
|-----------|-------|-------------------|-------|
| `S3_Report_Bucket` | S3 | None | Generated org-level reports. |
| `ReportBucket` | S3 | None | Telematics reports. |
| `ScheduledReportsBucket` | S3 | None | Scheduled report output. |
| `DailyFaultReportBackupBucket` | S3 | None | Daily vehicle fault reports (CSV). |
| `DailyAssetFaultReportBackupBucket` | S3 | None | Daily asset fault reports. |
| `report_bucket` | S3 | None | Elastic API query reports. |
| `results_bucket` | S3 | None | Elastic query result staging. |

### Audit

| Data Source | Store | Current Retention | Notes |
|-----------|-------|-------------------|-------|
| `logging_table_name` | DynamoDB | None | User activity logging. **PII.** |
| `UserActivityTable` | DynamoDB | None | User activity logs. **PII.** |
| `*_history` tables (Versioned mixin) | MySQL | None | Automatic snapshot on every ORM flush. Volume unknown. |

### Device State

| Data Source | Store | Current Retention | Notes |
|-----------|-------|-------------------|-------|
| `PresenceTable` | DynamoDB | Has TTL | Vehicle device presence. 14 Lambdas. |
| `AssetDevicePresenceTable` | DynamoDB | None | Asset device presence. |
| `AssetPresenceTable` | DynamoDB | None | Asset fault tracking. |
| `DeviceOnlineTable` | DynamoDB | None | Device online status. |
| `ConnectivityTable` | DynamoDB | None | Device connectivity state. |
| `DDBFirmwareRequests` / `DDBFirmwareSessionTable` | DynamoDB | None | Firmware job tracking. |
| `DDBbatchConfigUpdateRequestsTable` / `DDBbatchConfigUpdateSessionTable` | DynamoDB | None | Config update tracking. |
| `DDBAUSessionTable` | DynamoDB | None | Auto-upload session tracking. |

### Users

| Data Source | Store | Current Retention | Notes |
|-----------|-------|-------------------|-------|
| `Users` (`ent_users`) | MySQL | Soft delete | **PII.** Email, name. |
| `UserProfiles` | MySQL | None | **PII.** Linked to Users. |
| `pendingInvite` | MySQL | Has expiry field | **PII.** Cleanup handler commented out. |
| `user_preferences_dynamo` | DynamoDB | None | **PII.** Should delete with user. |
| `DDBDefaultVehicleAlertDistroEmailsTable` | DynamoDB | None | **PII.** Email addresses stored directly. |
| Cognito user pools (Main, System, Third-party) | Cognito | None | **PII.** `deleteExpiredCognitoUser` commented out. |

### Vehicles

| Data Source | Store | Current Retention | Notes |
|-----------|-------|-------------------|-------|
| `Vehicle` | MySQL | Soft delete | Core entity. |
| `Asset` | MySQL | Soft delete | Linked to vehicles. |
| `VehicleAssetAssociation` | MySQL | Has `association_end` | Historical associations preserved. |
| `LogicalDevice` | MySQL | Soft delete | Device-trackable bridge. |
| `PhysicalDevice` | MySQL | None | IMEI, firmware, model. |
| `orm_dynamo` | DynamoDB | None | Device bonded state cache. 71 Lambdas. Mirror of MySQL. |
| `DDBBondedDevices` | DynamoDB | None | Device-to-vehicle mapping. 10 Lambdas. |

## Retention Gap Summary

| Store | Total Sources | With Retention | Gap |
|-------|-------------|---------------|-----|
| DynamoDB | ~50 tables | 2 (TTL) | 96% |
| S3 | ~30 buckets | 0 | 100% |
| OpenSearch | 16 indices | 1 (ILM) | 94% |
| MySQL | ~50 entities | 0 (soft delete only) | 100% |
| PostgreSQL | ~11 tables | 0 | 100% |
| PostGIS | ~7 tables | 0 | 100% |
| Cognito | 3 pools | 0 | 100% |
| **Total** | **~167** | **3** | **98%** |

## Safety Center Data (TODO)

> **[TODO]** Jong to provide inventory of Safety Center data stores. Expected categories:
> - Driver behaviour scores
> - Driver assignments
> - HST alert data
> - Safety reports
>
> These need to be mapped into the category taxonomy above or may require new categories.

## Next Steps

- [ ] Review categories with Daragh and Rob
- [ ] Incorporate Geotab analysis findings (Daragh)
- [ ] Get Safety Center data inventory from Jong
- [ ] Resolve `[DISCUSSION]` items
- [ ] Publish to Confluence under NFB 463
