<!-- source: https://www.opswat.com/docs/mdndr/operating-guide/data-retention -->

# Data Retention

Retention policy governs how long each category of data collected by MetaDefender NDR remains queryable before it ages out. This chapter documents the data categories that the platform retains. It documents the default retention periods from the Data Management and Retention Functional Requirements Document (FRD). It also documents retention configuration, enforcement, storage locations, capacity planning, and data export before age-out.

This chapter is for system administrators, Site Reliability Engineers (SREs), and compliance auditors who own the data lifecycle of MetaDefender NDR. It assumes an installed Manager with at least one adopted sensor, an administrator account, and familiarity with the Administration page layout described in the [Administration overview](/docs/mdndr/operating-guide/administration-page).

First-use acronym expansions in this chapter:

- SRE (Site Reliability Engineer)
- FRD (Functional Requirements Document)
- UI (user interface)
- API (application programming interface)
- REST (Representational State Transfer)
- PCAP (Packet Capture)
- TTL (Time-To-Live)
- IOC (Indicator of Compromise)
- SIEM (Security Information and Event Management)
- MVP (Minimum Viable Product)
- CSV (comma-separated values)
- JSON (JavaScript Object Notation), Gbps (gigabit per second).

## [Overview of data categories](/docs/mdndr/operating-guide/data-retention#overview-of-data-categories)

MetaDefender NDR writes every observation it makes to one of six data categories. Each category has distinct retention economics -- alerts are dense and cheap to keep, packet captures are sparse per alert but heavy per record, session telemetry sits in between -- and each category is independently tunable from the other five.

| Category | What it contains | Primary use |
| --- | --- | --- |
| **Alert Data** | Suricata signature alerts, InSights command-and-control (C2) and Intelligence alerts, MetaDefender Core (MDCore) scan-derived alerts, behavioral detection alerts, Random Cut Forest (RCF) machine-learning anomaly alerts, threshold-detection alerts. | Historical investigation, trend analysis, compliance reporting, audit response. |
| **Session Data** | Suricata protocol events -- Domain Name System (DNS), Hypertext Transfer Protocol (HTTP), Transport Layer Security (TLS), File Transfer Protocol (FTP), Server Message Block (SMB), Secure Shell (SSH), Remote Desktop Protocol (RDP), Quick UDP Internet Connections (QUIC), and so on. | Hunt pivoting from an alert to the full per-protocol transaction set. |
| **File Data** | Suricata `fileinfo` events: metadata for every file carved from monitored traffic, including hash, type, and the session context that produced it. | Retrospective lookup of any file the sensor saw, including non-malicious ones. |
| **Flow Data** | Suricata netflow events and flow summaries -- the per-five-tuple connection records. | Long-horizon trend analysis, baseline-drift investigation, long-duration-flow detection. |
| **Packet Captures** | Full or triggered Suricata PCAPs associated with alerts. | Deep per-packet forensic review when session-level telemetry is insufficient. |
| **System and Audit Logs** | Manager and sensor system logs plus the administrative audit trail. | Operational troubleshooting, compliance, forensic review of administrative actions. |

The first five categories are the FRD-enumerated content categories. The sixth -- System and Audit Logs -- is tracked as a distinct retention category by the retention service and is called out explicitly because its retention window is much shorter than the content categories and because its audit-log subset is subject to compliance rules documented in the [Users, Groups, and RBAC](/docs/mdndr/operating-guide/users--groups--and-rbac) chapter.

## [Default retention periods](/docs/mdndr/operating-guide/data-retention#default-retention-periods)

The default retention policy shipped by MetaDefender NDR matches the Data Management and Retention functional definitions.

| Category | Default retention | Floor (minimum under disk pressure) |
| --- | --- | --- |
| **Alert Data** | 365 days | 73 days |
| **Flow Data** | 365 days | 73 days |
| **File Data** | 180 days | 36 days |
| **Session Data** | 60 days | 12 days |
| **Packet Captures** | 14 days | 3 days |
| **System and Audit Logs** | 30 days | 6 days |

The "floor" column is a deployment safety net. When disk usage on the retention service's monitored mount crosses the configured pressure threshold, an internal balancer reduces the *effective* retention of the most expendable categories by a fixed step until disk pressure is relieved -- but the effective retention never drops below the floor for a given category. When pressure subsides, the balancer walks the effective retention back toward the administrator-configured value. The balancer preserves the administrator's intent while preventing a runaway disk-full condition that would cause data loss at index-write time.

The deletion-priority order governs which categories give up retention first. The default order -- Flow, then Session, then File Data, then Packet Captures, then Alert Data, then System and Audit Logs -- reflects the relative value of each category to a downstream investigation. Administrators can reorder the priority list; the chosen order applies only during disk-pressure reduction and has no effect on steady-state retention.

## [Configure retention](/docs/mdndr/operating-guide/data-retention#configure-retention)

### [Tunable values](/docs/mdndr/operating-guide/data-retention#tunable-values)

Four values per category are addressable through the configuration surface:

- **Configured retention** (days). The steady-state retention period the administrator wants. Bounded at 7 days at the low end and 3650 days (roughly ten years) at the high end for any category.
- **Floor** (days). The minimum retention that the balancer can enforce under disk pressure.
- **Pressure threshold** (percent). The disk-usage percentage at which the balancer begins reducing effective retention. Default 75%. Applies deployment-wide, not per category.
- **Deletion priority** (ordered list). The order in which the balancer sheds retention from categories under pressure.

Two additional values control how the balancer runs:

- **Step size** (days). How many days of retention the balancer removes from the highest-priority category on each cycle in which disk pressure remains above the threshold. Default 7 days.
- **Check interval** (seconds). How frequently the balancer samples disk usage and decides whether to act. Default 300 seconds (five minutes).

### [Where the settings live](/docs/mdndr/operating-guide/data-retention#where-the-settings-live)

A graphical form under **Administration -> Configuration -> System -> Data Retention** is the MVP target for this setting; the form exposes the per-category configured value, the floor, the pressure threshold, and the deletion-priority ordering, and it previews the disk-usage impact before the **Save** button is engaged. In the current build the form is not yet rendered -- administrators drive the surface through the configuration API exposed by the Manager's service-manager component. `PUT /api/config/ndr-data-retention` writes the per-category and balancer values; `GET /api/config/ndr-data-retention` returns the current state. The setting has identical functional behavior through the form and the REST API. The same validation runs. The same version-controlled persistence applies. The Manager writes the same audit log entry.

Retention values are not edited per sensor or per sensor group. The policy is deployment-wide -- the Manager sets the TTL every retention-governed storage table enforces, and every sensor's data ages out under the same policy.

### [Storage capacity considerations](/docs/mdndr/operating-guide/data-retention#storage-capacity-considerations)

Tightening retention below the default on any category does not immediately reclaim disk space -- it changes the TTL the storage backend enforces on new writes and on its next scheduled purge cycle. Loosening retention past the default consumes additional disk over time as records accumulate; the saved value is validated against the ontology's per-category upper bound, but the Manager does not refuse the save on capacity grounds. Administrators who plan to lengthen retention should confirm the deployment has headroom before committing the change.

### [Propagation](/docs/mdndr/operating-guide/data-retention#propagation)

A save against the retention configuration broadcasts to the storage services that enforce retention -- Elasticsearch (through the `ndr-search-elastic` indexer) and ClickHouse (through the warm and analytics-out services). Each service applies the new policy on its next retention cycle -- typically within a minute for the Elasticsearch sweeper and on the next TTL round-trip for ClickHouse. No service restart is required.

## [Storage backends](/docs/mdndr/operating-guide/data-retention#storage-backends)

MetaDefender NDR uses three storage backends, each optimized for a distinct access pattern. Category-to-backend mapping is a product decision, not a runtime knob; the administrator tunes retention, not placement.

| Backend | Role | Categories stored |
| --- | --- | --- |
| **Elasticsearch** | Search-optimized, document-oriented indexing for the Hunt page, the Dashboard, and alert drill-down. | Alert Data, Session Data, File Data (indexed metadata). |
| **ClickHouse** | Columnar analytics store optimized for large-scale aggregations and time-range scans. | Flow Data, behavioral detection output, RCF anomaly detections, plus warm-tier raw flow records. |
| **SeaweedFS** | Object storage for large binary payloads that do not belong in a search index. | Packet Captures and carved files referenced by File Data records. |

Elasticsearch retention is enforced by a periodic sweeper that issues a date-range delete query per governed index and removes documents whose timestamp field is older than the configured retention. Models without a suitable top-level timestamp opt out of retention by configuration; their retention is governed by the parent index's policy or by manual administrator action.

ClickHouse retention is enforced by installing a TTL on every retention-governed table on every configuration change. Expired parts are asynchronously removed by ClickHouse's background merge process. The retention applier refuses to install a TTL shorter than one day on any table as a hard safety cap independent of the ontology floor.

SeaweedFS retention is coupled to the metadata record that references each object. PCAP write paths and the file-carve pipeline both key retention off the per-record timestamp and apply the same TTL as the metadata record in Elasticsearch or ClickHouse. An object is no longer referenced once its metadata record ages out, so the object-store sweeper simply deletes orphans on its sweep cycle.

## [Capacity planning considerations](/docs/mdndr/operating-guide/data-retention#capacity-planning-considerations)

Storage footprint scales primarily with sensor throughput and secondarily with the dominant application protocols on the monitored network. A first-pass estimate multiplies sustained sensor throughput by a per-category bytes-per-flow coefficient and the configured retention days.

Rule-of-thumb factors from representative deployments are below. Real deployments deviate -- a heavily HTTP-weighted network carries more per-flow metadata than a heavily TLS-weighted one, and aggressive file carving on a file-heavy link will inflate File Data and packet-capture storage well above these defaults.

| Category | Rough order of magnitude factor |
| --- | --- |
| Alert Data | Sparse -- hundreds of megabytes per day per 1 Gbps of monitored traffic at typical alert rates. |
| Session Data | Medium -- tens of gigabytes per day per 1 Gbps, skewing higher on DNS- and HTTP-heavy networks. |
| File Data | Light for the metadata record itself; the carved-file object store is the dominant consumer and scales with file activity rather than raw throughput. |
| Flow Data | Largest steady-state footprint -- low hundreds of gigabytes per day per 1 Gbps at line rate. |
| Packet Captures | Sparse but large per record; dominated by the *number* of alerts that trigger capture, not by raw throughput. |

Administrators validate capacity before they lengthen retention. They multiply the estimated daily rate for each category by the proposed retention. They sum the results across categories. They confirm that provisioned storage meets or exceeds the sum with reasonable headroom (typically 30%). This headroom supports burst growth and the balancer's pressure floor. Storage metrics per backend are surfaced in the operational view described in [Health and Monitoring](/docs/mdndr/operating-guide/health-and-monitoring); administrators consult those metrics rather than back-of-envelope estimates once the deployment has run long enough to produce a usage baseline.

## [Data export before aging out](/docs/mdndr/operating-guide/data-retention#data-export-before-aging-out)

Long-horizon retention is cost-bounded; compliance, incident response, and legal hold often require keeping a subset of data beyond the deployment's configured window. MetaDefender NDR supports several export paths; administrators choose the one that matches the data category and the downstream system.

- **Alert Data and Session Data.** The Hunt page supports exporting any result set as CSV or JSON. Analysts or administrators who hold a pending matter export the relevant result set before its retention window expires and file the export with the organization's case-management system.
- **SIEM-forwarded events.** Deployments that forward events to a SIEM retain the long-horizon copy in that SIEM according to that system's own retention policy. The SIEM integration is documented in the [Integrations](/docs/mdndr/operating-guide/integrations) chapter.
- **Packet Captures.** PCAPs associated with an alert can be downloaded through the Hunt page's alert-flow PCAP pivot. The download is the full capture file, suitable for offline review in Wireshark, tshark, or a purpose-built analysis tool.
- **Carved files.** File Data records link to the carved file in object storage; the Hunt page offers a direct download for each record. Administrators export files subject to litigation hold or that an investigation requires beyond the File Data retention window.
- **Audit log.** The audit log is exportable through the audit viewer documented in [Users, Groups, and RBAC](/docs/mdndr/operating-guide/users--groups--and-rbac). Compliance teams routinely archive the audit export to long-term storage independent of the deployment.

There is no automated "snapshot and freeze" workflow in MVP -- long-term preservation is a deliberate export step, not a passive consequence of the retention policy. Organizations that need an automated long-term archive wire the SIEM integration and forward the categories that matter to a system with the desired retention.

## [Quick-start checklist](/docs/mdndr/operating-guide/data-retention#quick-start-checklist)

The checklist below confirms retention is configured per the organization's policy and that the enforcement pipeline is healthy across the storage backends.

| Item | Action | Verification |
| --- | --- | --- |
| Category values reviewed | Compare each category's configured retention to organizational policy. | `GET /api/config/ndr-data-retention` returns values matching policy for Alert, Flow, Session, File, Packet Capture, and System/Audit Log categories. |
| Floor values reviewed | Confirm the floor per category is acceptable as a worst-case under disk pressure. | The floor on every category is no lower than the organization's minimum legally-required retention. |
| Pressure threshold set | Confirm the disk-usage percentage that triggers the balancer matches deployment expectations. | The configured pressure threshold matches policy; an induced pressure event in a staging environment triggers the balancer at the expected percentage. |
| Deletion priority confirmed | Confirm the order in which categories shed retention under pressure matches the organization's value ranking. | The configured priority list is the intended order. |
| Elasticsearch retention active | Confirm the Elasticsearch retention sweeper is running and scheduled. | Documents older than the configured age are absent from a date-range sample query on every governed index. |
| ClickHouse TTL applied | Confirm every retention-governed ClickHouse table has an active TTL matching the configured value. | `SHOW CREATE TABLE` for each governed table shows the expected `TTL` clause; expired parts are absent on the next merge cycle. |
| Object-store sweep confirmed | Confirm object-store orphans are being removed on schedule. | Object-storage metrics show steady-state or decreasing orphan count. |
| Disk usage reviewed | Confirm disk usage on the retention-monitored mount is comfortably below the pressure threshold. | Health and monitoring dashboards show disk usage with at least the target headroom. |
| Capacity estimate re-run | After any retention change, re-run the category-by-category storage estimate against provisioned capacity. | Projected steady-state footprint is within the provisioned capacity with the target headroom preserved. |
| Export paths exercised | For each export path the organization will rely on, perform a one-time drill from the Hunt page or the SIEM integration. | The export completes, the exported artifact is well-formed, and the destination system accepts it. |
| Audit entries visible | Spot-check the audit log for the most recent retention-configuration change. | The audit viewer shows the change with actor, prior value, new value, and timestamp. |

## [See also](/docs/mdndr/operating-guide/data-retention#see-also)

- [Administration Page](/docs/mdndr/operating-guide/administration-page) -- the Administration page structure, access control, audit trail, and chapter map.
- [Manager Configuration](/docs/mdndr/operating-guide/manager-configuration) -- the Data Management and Retention entry in the sixteen-setting Manager Configuration reference table.
- [Integrations](/docs/mdndr/operating-guide/integrations) -- SIEM integration for long-horizon retention of exported events.
- [Users, Groups, and RBAC](/docs/mdndr/operating-guide/users--groups--and-rbac) -- audit-log retention and the audit viewer used to verify every retention-configuration change.
- [Health and Monitoring](/docs/mdndr/operating-guide/health-and-monitoring) -- the operational view where administrators confirm disk usage, storage-backend health, and retention-sweep activity.
