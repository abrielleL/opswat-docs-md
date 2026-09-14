<!-- source: https://www.opswat.com/docs/mdndr/configuration-guide/c2-enrichment -->

# C2 enrichment

Enrichment and detection setting (global). This setting applies to every sensor. For conventions, abbreviations, and the other sections, see the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).

**Where:** Administration → Configuration → Enrichment and detection settings → C2 enrichment

Match traffic against command-and-control (C2) threat intelligence. Set the intelligence source and the automatic update schedule.

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Enabled** | Enable this enrichment service. | On | on/off | — |
| **C2 File Check Interval** | Interval in seconds between IOC file update checks. | `300` | number; 10 to 86400; unit: seconds | — |
| **C2 Dns Path** | Path to C2 DNS IOC JSON file. | — | text | Restart needed |
| **C2 Ip Path** | Path to C2 IP IOC JSON file. | — | text | Restart needed |
| **Cloud Auto Update Enabled** `eyelet_auto_update_enabled` | Enable automatic IOC updates from Cloud. Requires a valid Cloud API key. | On | on/off | — |
| **Cloud Auto Update Interval** `eyelet_auto_update_interval` | Interval in seconds between automatic Cloud IOC update checks. | `3600` | number; 900 to 604800; unit: seconds | — |
| **Cloud Base URL** `eyelet_base_url` | Base URL for Cloud API. | `https://eyelet.inquest.net` | text | Restart needed |
| **Cloud API Key** `eyelet_api_key` | API key for Cloud threat intelligence updates. | *(empty)* | text | Sensitive (hidden), Restart needed |
| **Proxy Mode** | Service-level proxy mode: inherit the global upstream proxy, disable proxy use, or use this service's custom proxy settings. | `inherit` | `inherit`, `disabled`, `custom` | Restart needed |
| **Proxy Host** | Custom proxy host for this service when proxy_mode is custom. | — | text | Restart needed |
| **Proxy Port** | Custom proxy port for this service when proxy_mode is custom. | — | number | Restart needed |
| **Proxy Username** | Optional username for the custom service-level proxy. | — | text | Restart needed |
| **Proxy Password** | Optional password for the custom service-level proxy. | *(empty)* | text | Sensitive (hidden), Restart needed |
| **Proxy No Proxy** | Hosts, domains, or CIDR ranges that should bypass the custom service-level proxy. | *(empty)* | list of string | Restart needed |

**Related:** [C2 and threat intelligence](/docs/mdndr/operating-guide/c2-and-threat-intelligence)

---

---

Back to the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).
