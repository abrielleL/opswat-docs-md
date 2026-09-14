<!-- source: https://www.opswat.com/docs/mdndr/configuration-guide/update -->

# Update

System setting (global). This setting applies to the whole system and to every sensor. For conventions, abbreviations, and the other sections, see the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).

**Where:** Administration → Configuration → System settings → Update

Control the automatic update service. Set the update source and the proxy that the update service uses.

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Proxy Mode** | Service-level proxy mode: inherit the global upstream proxy, disable proxy use, or use this service's custom proxy settings. | `inherit` | `inherit`, `disabled`, `custom` | Restart needed |
| **Proxy Host** | Custom proxy host for this service when proxy_mode is custom. | — | text | Restart needed |
| **Proxy Port** | Custom proxy port for this service when proxy_mode is custom. | — | number | Restart needed |
| **Proxy Username** | Optional username for the custom service-level proxy. | — | text | Restart needed |
| **Proxy Password** | Optional password for the custom service-level proxy. | *(empty)* | text | Sensitive (hidden), Restart needed |
| **Proxy No Proxy** | Hosts, domains, or CIDR ranges that should bypass the custom service-level proxy. | *(empty)* | list of string | Restart needed |
| **System Update URL** | Cloud endpoint used to check for available NDR system updates. Must be https: this channel carries the update API key and drives package installation, so cleartext transport is rejected. | — | text | — |
| **System Update API Key** | API key for Cloud system update checks and package downloads. | *(empty)* | text | Sensitive (hidden) |
| **System Update Auth Header** | HTTP header name for system update authentication. Use query:<name> only when the provider cannot accept a header — a query-string token is recorded in proxy and provider access logs. | `Authorization` | text | — |
| **System Update Auth Scheme** | Authentication scheme prepended to the system update API key for header authentication. Leave empty to send the raw key. | `Bearer` | text | — |
| **System Update Channel** | NDR system update channel requested from Cloud. | `stable` | text | — |
| **System Update Check Interval** `system_update_check_interval_hours` | Interval in hours between automatic Cloud system update checks. | `24` | number; 1 to 168; unit: hours | — |
| **System Update Auto Download** | Automatically download and stage available NDR system updates after a scheduled check. Applying the update still requires operator action unless automatic apply is enabled. | Off | on/off | — |
| **System Update Auto Apply** | Automatically apply available NDR system updates after scheduled checks. Enable only for environments that allow unattended maintenance. | Off | on/off | — |
| **Sensor Update Auto Apply** | Automatically apply available sensor software updates to the fleet. Off by default; when off, sensor updates are operator-gated and applied on demand. | Off | on/off | — |
| **Sensor Update Channel** | Sensor software update channel requested for the fleet. | `stable` | text | — |
| **Sensor Update Maintenance Window Enabled** | Restrict automatic sensor updates to a daily maintenance window. When enabled, auto-apply only runs inside the configured window. | Off | on/off | — |
| **Sensor Update Maintenance Start Hour** | Hour of day (0-23) when the sensor update maintenance window begins, evaluated in the timezone selected by sensor_update_maintenance_timezone. | `0` | number; 0 to 23; unit: hour-of-day | — |
| **Sensor Update Maintenance Timezone** | Reference timezone for the sensor update maintenance window start hour. Defaults to UTC for deterministic fleet-wide behavior. | `utc` | `utc`, `sensor_local` | — |
| **Sensor Update Maintenance Duration** `sensor_update_maintenance_duration_hours` | Length in hours of the sensor update maintenance window starting at the configured start hour. | `4` | number; 1 to 24; unit: hours | — |
| **Sigpack Auto Update** | Enable automatic Suricata signature pack downloads from Cloud. | Off | on/off | — |
| **Sigpack Check Interval Minutes** | Interval in minutes between Cloud sigpack update checks. Minimum 15 minutes. | `60` | number; 15 to no maximum; unit: minutes | — |
| **Sigpack Cloud API Key** `sigpack_eyelet_api_key` | API key for Cloud sigpack downloads. | *(empty)* | text | Sensitive (hidden) |

**Related:** [Updates management](/docs/mdndr/operating-guide/updates-management)

---

---

Back to the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).
