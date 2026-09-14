<!-- source: https://www.opswat.com/docs/mdndr/configuration-guide/administration-configuration-reference -->

# Administration configuration reference

This page lists every setting on the **Administration → Configuration** page in MetaDefender NDR. It tells you what each setting does, the default value, the allowed values, and when a change needs a restart. Use this page as the reference for day-to-day configuration.

This page is for the customer administrator who manages a MetaDefender NDR deployment. It assumes an installed Manager, at least one adopted sensor, and an administrator account. For the layout of the Administration area, see the [Administration overview](/docs/mdndr/operating-guide/administration-page). For host-level Manager settings, see [Manager configuration](/docs/mdndr/operating-guide/manager-configuration).

## [Abbreviations](/docs/mdndr/configuration-guide/administration-configuration-reference#abbreviations)

This page expands each abbreviation at first use. The full list follows:

- CA — certificate authority
- C2 — command-and-control
- DGA — domain generation algorithm
- DNS — Domain Name System
- ICAP — Internet Content Adaptation Protocol
- IP — Internet Protocol
- ML — machine learning
- MIME — Multipurpose Internet Mail Extensions
- NTP — Network Time Protocol
- OIDC — OpenID Connect
- RCF — Random Cut Forest
- SAML — Security Assertion Markup Language
- SIEM — security information and event management
- SMTP — Simple Mail Transfer Protocol
- SSO — single sign-on
- TLS — Transport Layer Security
- URL — Uniform Resource Locator

## [Before you begin](/docs/mdndr/configuration-guide/administration-configuration-reference#before-you-begin)

- You need the administrator role. The Configuration page is available only to administrators.
- Open the page at **Administration → Configuration**.
- A setting marked **Sensitive** holds a secret, such as a password or an API key. The page does not show the current value.
- A setting marked **Restart needed** takes effect only after the service restarts.

## [How settings are scoped](/docs/mdndr/configuration-guide/administration-configuration-reference#how-settings-are-scoped)

The Configuration page groups settings into four scopes:

1. **System settings (global)** — settings for the whole system.
2. **Enrichment and detection settings (global)** — settings for the enrichment and detection services.
3. **Manager settings (per host)** — settings for one Manager host.
4. **Sensor settings (per sensor)** — settings for one sensor.

A global setting applies to every sensor. A per-host or per-sensor setting applies to one target only. Set a per-host or per-sensor value for each target that needs a different value.

## [How to read the setting tables](/docs/mdndr/configuration-guide/administration-configuration-reference#how-to-read-the-setting-tables)

Each setting table has these columns:

- **Setting** — the label on the page. The configuration key follows in code font.
- **What it does** — the function of the setting.
- **Default** — the default value.
- **Allowed values** — the type, the list of choices, or the number range.
- **Notes** — flags for required, sensitive, or restart-needed settings.

## [Configuration sections](/docs/mdndr/configuration-guide/administration-configuration-reference#configuration-sections)

Each section below is its own page. Select a section to see its settings.

### [System settings](/docs/mdndr/configuration-guide/administration-configuration-reference#system-settings)

- [Authentication](/docs/mdndr/configuration-guide/authentication)
- [Retention](/docs/mdndr/configuration-guide/retention)
- [Syslog and SIEM](/docs/mdndr/configuration-guide/syslog-and-siem)
- [Update](/docs/mdndr/configuration-guide/update)
- [Manual update](/docs/mdndr/configuration-guide/manual-update)

### [Enrichment and detection settings](/docs/mdndr/configuration-guide/administration-configuration-reference#enrichment-and-detection-settings)

- [IP enrichment](/docs/mdndr/configuration-guide/ip-enrichment)
- [C2 enrichment](/docs/mdndr/configuration-guide/c2-enrichment)
- [InSights enrichment](/docs/mdndr/configuration-guide/insights-enrichment)
- [MetaDefender Core enrichment](/docs/mdndr/configuration-guide/metadefender-core-enrichment)
- [Behavioral analytics — thresholds](/docs/mdndr/configuration-guide/behavioral-analytics-thresholds)
- [Behavioral analytics — exclusions](/docs/mdndr/configuration-guide/behavioral-analytics-exclusions)
- [Behavioral analytics — services](/docs/mdndr/configuration-guide/behavioral-analytics-services)
- [RCF streaming](/docs/mdndr/configuration-guide/rcf-streaming)

### [Manager settings](/docs/mdndr/configuration-guide/administration-configuration-reference#manager-settings)

- [DNS (Manager)](/docs/mdndr/configuration-guide/manager-dns)
- [NTP (Manager)](/docs/mdndr/configuration-guide/manager-ntp)
- [SMTP](/docs/mdndr/configuration-guide/smtp)
- [Upstream proxy](/docs/mdndr/configuration-guide/upstream-proxy)
- [ICAP](/docs/mdndr/configuration-guide/icap)
- [TLS](/docs/mdndr/configuration-guide/tls)

### [Sensor settings](/docs/mdndr/configuration-guide/administration-configuration-reference#sensor-settings)

- [Policy (sensor)](/docs/mdndr/configuration-guide/sensor-policy)
- [DNS (sensor)](/docs/mdndr/configuration-guide/sensor-dns)
- [NTP (sensor)](/docs/mdndr/configuration-guide/sensor-ntp)
- [Proxy (sensor)](/docs/mdndr/configuration-guide/sensor-proxy)
- [Suricata](/docs/mdndr/configuration-guide/suricata)

## [Related documentation](/docs/mdndr/configuration-guide/administration-configuration-reference#related-documentation)

- [Administration overview](/docs/mdndr/operating-guide/administration-page)
- [Manager configuration](/docs/mdndr/operating-guide/manager-configuration)
- [Sensor management](/docs/mdndr/operating-guide/sensor-management)
- [Data retention](/docs/mdndr/operating-guide/data-retention)
- [Integrations](/docs/mdndr/operating-guide/integrations)
- [MetaDefender Core file scanning](/docs/mdndr/operating-guide/metadefender-core-file-scanning)
- [C2 and threat intelligence](/docs/mdndr/operating-guide/c2-and-threat-intelligence)
- [Behavioral detections](/docs/mdndr/operating-guide/behavioral-detections)
- [ML anomaly detections](/docs/mdndr/operating-guide/ml-anomaly-detections)
- [Suricata signatures](/docs/mdndr/operating-guide/suricata-signatures)
- [Updates management](/docs/mdndr/operating-guide/updates-management)
- [Users, groups, and RBAC](/docs/mdndr/operating-guide/users--groups--and-rbac)
