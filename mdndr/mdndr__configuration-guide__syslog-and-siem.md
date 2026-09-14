<!-- source: https://www.opswat.com/docs/mdndr/configuration-guide/syslog-and-siem -->

# Syslog and SIEM

System setting (global). This setting applies to the whole system and to every sensor. For conventions, abbreviations, and the other sections, see the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).

**Where:** Administration → Configuration → System settings → Syslog / SIEM

Send system logs to one or more external security information and event management (SIEM) platforms.

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Enabled** | SIEM Integration Enabled. | Off | on/off | Restart needed |
| **Destinations** | SIEM Destinations. This is a group of settings. See the sub-settings below. | — | list of groups | Restart needed |

#### [Syslog / SIEM: SiemDestination sub-settings](/docs/mdndr/configuration-guide/syslog-and-siem#syslog--siem-siemdestination-sub-settings)

*A single, independently configured SIEM destination (FRD FR-002). For syslog destinations, endpoint is a hostname/IP and port/protocol/message_format apply. For URL/token destination types (splunk_hec, datadog, elasticsearch, otlp_http), endpoint is the target URL and the auth sub-block carries the authentication (HTTP Basic username/password for elasticsearch/otlp_http, or a bearer/api-key token; HEC token / Datadog API key). For cloud/data-lake types (aws_cloudwatch, aws_s3, azure_monitor, gcp_logging, gcp_chronicle) the provider auth + target live in the aws / azure / gcp sub-blocks and endpoint is unused (except as an optional AWS endpoint override).*

| Setting | What it does | Default | Allowed values | Notes |
| --- | --- | --- | --- | --- |
| **Name** | Advanced setting for this service. Change only if you understand the effect. | *(empty)* | text | — |
| **Enabled** | Advanced setting for this service. Change only if you understand the effect. | Off | on/off | — |
| **Type** | Advanced setting for this service. Change only if you understand the effect. | `syslog` | `syslog`, `splunk_hec`, `datadog`, `elasticsearch`, `otlp_http`, `aws_cloudwatch`, `aws_s3`, `azure_monitor`, `gcp_logging`, `gcp_chronicle` | — |
| **Endpoint** | Advanced setting for this service. Change only if you understand the effect. | *(empty)* | text | — |
| **Port** | Advanced setting for this service. Change only if you understand the effect. | `514` | number; 1 to 65535 | — |
| **Protocol** | Advanced setting for this service. Change only if you understand the effect. | `udp` | `udp`, `tcp`, `tcp+tls` | — |
| **Message Format** | Advanced setting for this service. Change only if you understand the effect. | `rfc5424` | `rfc5424`, `cef`, `json` | — |
| **Auth** | Advanced setting for this service. Change only if you understand the effect. | *(see the sub-settings)* | group of settings | — |
| **Index** | Advanced setting for this service. Change only if you understand the effect. | — | text | — |
| **TLS** | Advanced setting for this service. Change only if you understand the effect. | *(see the sub-settings)* | group of settings | — |
| **Categories** | Advanced setting for this service. Change only if you understand the effect. | *(see the sub-settings)* | group of settings | — |
| **Field Selection** | Advanced setting for this service. Change only if you understand the effect. | — | list of string | — |
| **Buffer** | Advanced setting for this service. Change only if you understand the effect. | *(see the sub-settings)* | group of settings | — |
| **Retry** | Advanced setting for this service. Change only if you understand the effect. | *(see the sub-settings)* | group of settings | — |
| **Rate Limit** | Advanced setting for this service. Change only if you understand the effect. | *(see the sub-settings)* | group of settings | — |
| **Failover Group** | Advanced setting for this service. Change only if you understand the effect. | — | text | — |
| **Aws** | Advanced setting for this service. Change only if you understand the effect. | *(see the sub-settings)* | group of settings | — |
| **Azure** | Advanced setting for this service. Change only if you understand the effect. | *(see the sub-settings)* | group of settings | — |
| **Gcp** | Advanced setting for this service. Change only if you understand the effect. | *(see the sub-settings)* | group of settings | — |

**Related:** [Integrations](/docs/mdndr/operating-guide/integrations)

---

---

Back to the [Administration configuration reference](/docs/mdndr/configuration-guide/administration-configuration-reference).
