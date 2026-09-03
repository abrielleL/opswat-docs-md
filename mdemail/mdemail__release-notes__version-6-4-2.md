<!-- source: https://www.opswat.com/docs/mdemail/release-notes/version-6-4-2 -->

# Version 6.4.2

| Version | 6.4.2 |
| --- | --- |
| Release date | 12th August, 2026 |
| Scope | Besides minor improvements and fixes, this release introduces telemetry for MetaDefender® Email Gateway Security: operational metrics can now be exported to OTLP (OpenTelemetry Protocol) compatible collectors for live monitoring of licensing, email delivery, and pipeline health. |

## [New & Improved](/docs/mdemail/release-notes/version-6-4-2#new--improved)

### [Telemetry Export to OTLP Collectors](/docs/mdemail/release-notes/version-6-4-2#telemetry-export-to-otlp-collectors)

MetaDefender Email Gateway Security can now export operational metrics — license status, email delivery duration, live pipeline health (never email content or personal data), etc. — to OTLP collectors, to the default OPSWAT collector, or to both, protected by TLS (Transport Layer Security) 1.2 or newer. Telemetry is disabled by default.

For details see [Telemetry](/docs/mdemail/configuration/telemetry), [Registry configuration](/docs/mdemail/configuration/registry-configuration#hkey_local_machinesoftwareopswatmetadefender-email-securityinternal), [Proxy configuration](/docs/mdemail/configuration/settings#proxy-configuration).

## [Fixed](/docs/mdemail/release-notes/version-6-4-2#fixed)

### [CEF Extension Fields for SOC Logs](/docs/mdemail/release-notes/version-6-4-2#cef-extension-fields-for-soc-logs)

SOC (Security Operations Center) level log messages in CEF (Common Event Format) carried their parameters only in the message text, leaving the extension block without them. The parameters are now included as structured fields in the extension block, so SIEM tools receive parseable details.

SOC message parameters

In upcoming releases of Email Gateway Security it is planned to remove SOC-level log message parameters from the Name field text. The SOC-level log message parameters will be kept in the Extension field only.

**Customers who have configured their SIEM/SOAR/etc. systems to depend on the SOC-level log message parameters being in the Name field should migrate to the new structure.**

For details see [Registry configuration](/docs/mdemail/configuration/registry-configuration) and [CEF log message format.](/docs/mdemail/operating/cef-syslog-message-format)
