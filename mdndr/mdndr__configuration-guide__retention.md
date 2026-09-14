<!-- source: https://www.opswat.com/docs/mdndr/configuration-guide/retention -->

# Retention

System setting (global). This setting applies to the whole system and to every sensor. For conventions, abbreviations, and the other sections, see the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).

**Where:** Administration → Configuration → System settings → Retention

Control how long the system keeps each data type. Set disk targets and per-type retention limits.

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Check Interval Secs** | Balancer check interval. | `300` | number; 60 to 3600; unit: seconds | — |
| **Pressure Threshold** | Disk usage threshold for retention reduction. | `75` | number; 1 to 99; unit: percent | — |
| **Deletion Priority** | Deletion order by category. | `["flow", "session", "filedata", "pcap", "events", "alert", "analytics_rollups"]` | list of string | — |
| **Disk Mount Path** | Mount path to monitor. | `/` | text | — |
| **Step Size Days** | Retention change per balancer cycle. | `7` | number; 1 to 30; unit: days | — |
| **Flow** | Retention contract for flow data. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | — |
| **Events** | Retention contract for raw event data (`ndr.events`). This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | — |
| **Session** | Retention contract for session data. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | — |
| **Alert** | Retention contract for alert data. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | — |
| **Analytics Rollups** | Retention contract for analytics rollup and summary data (for example ClickHouse `ch_*` tables). This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | — |
| **Filedata** | Retention contract for file analysis data. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | — |
| **Log** | Legacy compatibility retention contract for analytics rollup data. Prefer `analytics_rollups` for new configurations. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | — |
| **Pcap** | Retention contract for packet capture data. This is a group of settings. See the sub-settings below. | *(see the sub-settings)* | group of settings | — |

#### [Retention: RetentionCategoryConfig sub-settings](/docs/mdndr/configuration-guide/retention#retention-retentioncategoryconfig-sub-settings)

*Category-level retention contract. Runtime services map categories such as flow, events, and pcap to concrete tables and views.*

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Configured** | Configured retention target. | `365` | number; 7 to 3650; unit: days | — |
| **Actual** | Effective retention after balancer adjustments. | `365` | number; 3 to 3650; unit: days | — |
| **Min** | Minimum retention floor. | `73` | number; 1 to 365; unit: days | — |

**Related:** [Data retention](/docs/mdndr/operating-guide/data-retention)

---

---

Back to the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).
