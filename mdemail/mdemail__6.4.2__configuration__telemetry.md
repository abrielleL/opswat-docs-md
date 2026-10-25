<!-- source: https://www.opswat.com/docs/mdemail/6.4.2/configuration/telemetry -->

# Telemetry

View as Markdown Ask ChatGPT about this page Ask Claude about this page

MetaDefender Email Gateway Security can export operational metrics to OTLP (OpenTelemetry Protocol) compatible collectors. Telemetry gives operators live visibility into licensing status, email processing performance, and pipeline health from their own monitoring dashboards, and can optionally share the same metrics with OPSWAT to support product improvement and faster support.

Disabled by default

Telemetry is disabled by default, on new installations and after upgrades alike.

No sensitive data

Exported metrics contain product health data only: no email content, addresses, or other personal or sensitive data is ever transmitted.

## [Configuring telemetry](/docs/mdemail/6.4.2/configuration/telemetry#configuring-telemetry)

Telemetry is configured on **Settings / Telemetry**. Access to this page requires the dedicated **Telemetry** right (for details see [Roles](/docs/mdemail/6.4.2/configuration/users#roles)).

Disabled by default

The Telemetry right is disabled by default for each role except *Administrators*.

| Option | Description |
| --- | --- |
| **Enable telemetry** | Master switch. Enables or disables telemetry data collection. When disabled, no metrics are collected or sent. |
| **Send telemetry to OPSWAT** | Sends the collected telemetry to OPSWAT for analysis. Turning this on automatically adds the OPSWAT Collector (`https://egs-telemetry.metadefender.com:4318/v1/metrics`) to the list of collectors as a read-only entry. |
| **Collector list** | The collectors that receive the metrics. Metrics are exported to every configured collector simultaneously. Each entry shows the Metric Endpoint URL, whether an API key is set, and the protocol used. |

To register your own collector, select **Add collector** and provide:

- **Metric Endpoint URL** — the OTLP metrics endpoint of your collector
- **Use API Key authentication** — enable when the collector requires an API key, then enter the key in the **API Key** field

The transport protocol (OTLP over HTTP or gRPC) is derived from the endpoint URL and displayed in the **Protocol** column of the collector list.

Collector connections always use TLS (Transport Layer Security) 1.2 or newer with certificate verification. Metrics are exported once per minute by default (see [Registry configuration] for tuning). Configuration changes take effect without a service restart.

Network requirements

When **Send telemetry to OPSWAT** is enabled, the product must be able to reach the OPSWAT Collector on port 4318 (HTTPS) or 4317 (gRPC). For details see [Ports](/docs/mdemail/6.4.2/installation/prerequisites#ports).

Telemetry follows the product proxy configuration; environment proxy variables are never used. For details see [Proxy configuration](/docs/mdemail/6.4.2/configuration/settings#proxy-configuration).

Auditing

The following telemetry actions are recorded in the [Audit Log](/docs/mdemail/6.4.2/operating/audit-log):

- enabling or disabling telemetry,
- changing the **Send telemetry to OPSWAT** setting, and
- adding, editing, or removing collectors.
## [Exported metrics](/docs/mdemail/6.4.2/configuration/telemetry#exported-metrics)

| Metric | Type | What it reports |
| --- | --- | --- |
| `egs_license_days_remaining` | Gauge | Days until the current license expires |
| `egs_licensed_users` | Gauge | Licensed users currently in use |
| `egs_licensed_users_entitlement` | Gauge | Maximum number of licensed users allowed by the license |
| `egs_email_processing_duration_seconds` | Histogram | End-to-end duration between receiving and delivering an email. Recorded only for delivered emails (not for quarantined, rejected, or failed ones) |
| `egs_job_queue_depth` | Gauge | Total number of emails waiting in the processing queue |
| `egs_oldest_pending_job_age_seconds` | Gauge | Age of the oldest unprocessed email job |
| `egs_emails_in_state` | Gauge | Live number of email jobs per processing state (`pending`, `processing`, `sending`, `reprocessing`, `resending`), with the state as attribute |
