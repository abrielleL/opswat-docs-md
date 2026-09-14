<!-- source: https://www.opswat.com/docs/mdndr/configuration-guide/insights-enrichment -->

# InSights enrichment

Enrichment and detection setting (global). This setting applies to every sensor. For conventions, abbreviations, and the other sections, see the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).

**Where:** Administration → Configuration → Enrichment and detection settings → InSights enrichment

Enrich domains and hosts with OPSWAT InSights reputation data. Set Domain Name System (DNS) resolution and filter options.

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Enabled** | Enable this enrichment service. | On | on/off | — |
| **Dns Resolution Enabled** | Enable DNS resolution for domain IOCs. | Off | on/off | — |
| **Dns Servers** | List of DNS servers for resolution. | `["8.8.8.8", "1.1.1.1"]` | list of string | — |
| **Dns Timeout** | DNS query timeout in seconds. | `2` | number; 1 to 30; unit: seconds | — |
| **Whitelist Enabled** | Enable whitelist checking (exclusion filters). | On | on/off | — |
| **Filter Files Path** | Path to filter files directory. | `/etc/ndr/filters` | text | Restart needed |
| **Cloud Auto Update Enabled** `eyelet_auto_update_enabled` | Enable automatic IOC updates from Cloud. Requires a valid Cloud API key. | Off | on/off | — |
| **Cloud Auto Update Interval** `eyelet_auto_update_interval` | Interval in seconds between automatic Cloud IOC update checks. | `3600` | number; 900 to 604800; unit: seconds | — |
| **Cloud Base URL** `eyelet_base_url` | Base URL for Cloud API. | `https://eyelet.inquest.net` | text | Restart needed |
| **Cloud API Key** `eyelet_api_key` | API key for Cloud threat intelligence. | *(empty)* | text | Sensitive (hidden), Restart needed |
| **Proxy Mode** | Service-level proxy mode: inherit the global upstream proxy, disable proxy use, or use this service's custom proxy settings. | `inherit` | `inherit`, `disabled`, `custom` | Restart needed |
| **Proxy Host** | Custom proxy host for this service when proxy_mode is custom. | — | text | Restart needed |
| **Proxy Port** | Custom proxy port for this service when proxy_mode is custom. | — | number | Restart needed |
| **Proxy Username** | Optional username for the custom service-level proxy. | — | text | Restart needed |
| **Proxy Password** | Optional password for the custom service-level proxy. | *(empty)* | text | Sensitive (hidden), Restart needed |
| **Proxy No Proxy** | Hosts, domains, or CIDR ranges that should bypass the custom service-level proxy. | *(empty)* | list of string | Restart needed |

**Related:** [InSights, TiDB, and RPEDB](/docs/mdndr/operating-guide/insights-tidb-and-rpedb)

---

---

Back to the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).
