<!-- source: https://www.opswat.com/docs/mdndr/operating-guide/integrations -->

# Integrations

The Integrations section of the Administration page connects MetaDefender NDR to external services. These services extend detection and response beyond the sensor and the Manager's own UI (user interface). This chapter documents four Minimum Viable Product (MVP) integrations. They are MetaDefender Core, MetaDefender Cloud, Syslog to Security Information and Event Management (SIEM) platforms, and threat intelligence. For each integration, it gives the necessary configuration. It also gives health verification steps, credential rotation procedures, and connectivity tests.

This chapter is for system administrators and Site Reliability Engineers (SREs) who own the Manager's outbound connections to third-party services. It assumes an installed Manager with at least one adopted sensor and an administrator account. It also assumes familiarity with the Administration page layout in the [Administration overview](/docs/mdndr/operating-guide/administration-page). See the Manager-global settings in [Manager Configuration](/docs/mdndr/operating-guide/manager-configuration).

This chapter expands each abbreviation at first use. The full list follows:

- MVP -- Minimum Viable Product
- UI -- user interface
- SRE -- Site Reliability Engineer
- SIEM -- Security Information and Event Management
- API -- Application Programming Interface
- REST -- Representational State Transfer
- HTTP -- Hypertext Transfer Protocol
- HTTPS -- Hypertext Transfer Protocol Secure
- TLS -- Transport Layer Security
- UDP -- User Datagram Protocol
- TCP -- Transmission Control Protocol
- IP -- Internet Protocol
- URL -- Uniform Resource Locator
- TI -- threat intelligence
- OSINT -- open-source intelligence
- IOC -- indicator of compromise
- C2 -- command-and-control
- CEF -- Common Event Format
- LEEF -- Log Event Extended Format
- MIME -- Multipurpose Internet Mail Extensions
- SHA-256 -- Secure Hash Algorithm 256-bit
- MD5 -- Message Digest 5
- AV -- antivirus
- CDR -- Content Disarm and Reconstruction
- DLP -- Data Loss Prevention
- RFC -- Request for Comments
- CVE -- Common Vulnerabilities and Exposures
- TTL -- time-to-live
- DNS -- Domain Name System

## [Overview of available integrations](/docs/mdndr/operating-guide/integrations#overview-of-available-integrations)

MetaDefender NDR ships four MVP integrations, each of which addresses a distinct operational need:

| Integration | Purpose | Direction | Transport |
| --- | --- | --- | --- |
| **MetaDefender Core** | Deep multi-AV file analysis of artifacts carved from network traffic, on-premises and air-gappable. | Outbound from the Manager to a MetaDefender Core deployment. | HTTPS REST API. |
| **MetaDefender Cloud** | Hosted alternative to MetaDefender Core backed by the OPSWAT multi-AV service at `api.metadefender.com/v4`. | Outbound from the Manager to OPSWAT's cloud endpoint. | HTTPS REST API. |
| **Syslog / SIEM** | Real-time send of Manager and sensor logs to one or more external SIEM platforms. Categories include audit, engine, system, alert, file-info, enrichment, and session. | Outbound from the Manager to customer-operated SIEM collectors. | UDP port 514 standard Syslog in MVP; TLS-encrypted Syslog (RFC 5425) is PostMVP. |

MetaDefender Core and MetaDefender Cloud are mutually exclusive per deployment. Configure the MetaDefender NDR enrichment service to use one deployment or the other, not both. Syslog supports multiple concurrent destinations.

Every integration runs on the Manager side. Sensors do not hold integration credentials. Sensors do not open outbound connections to third-party services directly. All outbound traffic to MetaDefender Core, MetaDefender Cloud, or a SIEM originates from the Manager. It can also originate from the MetaDefender Core enrichment microservice that runs alongside the Manager.

All four integrations respect tenant isolation. The Manager scopes each tenant's integration configuration, credentials, syslog destinations, and per-destination filter rules to that tenant alone. [Users, Groups, and RBAC](/docs/mdndr/operating-guide/users--groups--and-rbac) documents the enforcement model.

## [MetaDefender Core](/docs/mdndr/operating-guide/integrations#metadefender-core)

MetaDefender Core is the on-premises OPSWAT file-analysis product. MetaDefender NDR's MetaDefender Core enrichment submits files from Suricata's file-store to the MetaDefender Core Application Programming Interface (API). The enrichment retrieves multi-AV scan results. It attaches the results as enrichments on the related `fileinfo` event. Enriched file verdicts drive downstream alerts. They appear on the Hunt page when analysts pivot from a file event.

### [Purpose](/docs/mdndr/operating-guide/integrations#purpose)

The AV engines licensed on the MetaDefender Core deployment analyze every file that the enrichment submits in parallel. The enrichment attaches the verdict to the network event. Verdicts include Clean, Infected, Suspicious, and the per-engine signature detail that supports the verdict. The Manager stores the verdict with the flow, session, and file metadata that triggered the extraction.

The enrichment checks the MetaDefender hash cache before it submits any file bytes. Files with a recent cached result usually resolve without re-upload. This conserves scan capacity and API quota. The cache-lookup threshold is tunable (default three days); older cached results trigger a fresh scan.

Although the scan workflow is asynchronous (submit, poll, result), analysts see a single enriched event with the scan verdict inline. The enrichment pipeline handles polls, retries, and timeout records behind the scenes.

### [MVP scope](/docs/mdndr/operating-guide/integrations#mvp-scope)

MVP covers hash lookups, file submission, polls for scan completion, and result enrichment of the `fileinfo` event that triggered it. MetaDefender NDR does **not** connect the following MetaDefender Core capabilities in MVP. They are PostMVP targets:

- YARA-based pre-scan on the sensor
- Content Disarm and Reconstruction (CDR) retrieval of sanitized files
- Data Loss Prevention (DLP) scan
- Vulnerability / Common Vulnerabilities and Exposures (CVE) assessment
- A persistent failed-file retry queue with Manager UI backlog exposure

### [Configuration](/docs/mdndr/operating-guide/integrations#configuration)

Configure the MetaDefender integration from **Administration -> Configuration -> Integrations -> MetaDefender Core**. Key parameters:

| Parameter | Default | Notes |
| --- | --- | --- |
| Deployment mode | Cloud | Selects MetaDefender Cloud (`api.metadefender.com/v4`) or MetaDefender Core (on-premises). Mutually exclusive. |
| Base URL (Core) | *(none -- required when mode=Core)* | Scheme, host, and port of the on-premises MetaDefender Core instance. Must be reachable from the Manager network. |
| Credentials | *(none -- required)* | Cloud: API key only. Core: API key, or username and password for session-based authentication. Stored as Kubernetes secrets; never rendered in logs or audit entries. |
| Hash lookup first | Enabled | Check the MetaDefender hash cache before file byte upload. Disable only for debug. |
| Rescan after (days) | 3 | The enrichment discards cached results older than this threshold and submits a fresh scan. |
| File submission enabled | Enabled | When disabled, only hash lookups run -- no file bytes leave the Manager's network. Useful for privacy-sensitive deployments. |
| Maximum file size (MB) | 100 | The enrichment skips larger files. Set to `0` for unlimited. |
| MIME type skip-list / prefix skip-list | *(empty)* | Comma-separated MIME types or prefixes (e.g., `image/,audio/,video/`) that the enrichment must not submit. |
| Scan rule / workflow | *(empty)* | Optional MetaDefender Core workflow name. When empty, the deployment uses its default workflow. |
| Archive scan / password | Disabled / `infected` | When enabled, MetaDefender extracts and scans archive contents with the configured password. |
| Polling interval / max attempts | 30 sec / 120 | Together these set the per-scan upper bound (default 60 minutes). |
| Rate limit enabled / max concurrent scans | Enabled / 5 | Respects `X-RateLimit-*` headers; caps parallel in-flight scans. Tune downward for shared MetaDefender deployments. |
| Upstream HTTP proxy | *(inherits Manager value)* | When the Manager's Upstream HTTP Proxy has a value, the enrichment routes outbound requests through it. Proxy changes broadcast without restart. |

Credentials reload through the configuration-broadcast channel after rotation. No pod restart is necessary.

### [How file events reach the enrichment](/docs/mdndr/operating-guide/integrations#how-file-events-reach-the-enrichment)

Files from the sensor's Suricata file-store produce a `fileinfo` event. The enrichment consumes the event and extracts the SHA-256. If SHA-256 is unavailable, it extracts the MD5. The enrichment filters events that fail the MIME or size checks. It opens the carved file from the sensor's file-store or from object storage. The sensor never transfers the carved file directly to MetaDefender. The Manager-side enrichment reads the file and submits it over the Manager's outbound connection.

### [Verification](/docs/mdndr/operating-guide/integrations#verification)

A healthy MetaDefender Core integration produces three observable signals:

1. **Connectivity probe on save.**

   - When administrators save the integration form, the Manager probes the configured endpoint.
   - It uses `/apikey/info` for Cloud and `/version` for Core.
   - The form displays success or a detailed error.
   - The Manager saves the integration only after probe success.
2. **Enrichment statuses on merged events.**

   - The enrichment reports `status=enriched` when files produce a scan result.
   - It reports `status=enabled` when filters exclude files.
   - Filter causes include too large, skipped MIME type, and hash-lookup-only mode.
   - A `timeout` status means the enrichment did not return a result before the aggregator's time-to-live (TTL) expired.
   - Investigate `timeout` status.
3. **Scan counters.**

   - The enrichment's `/api/metrics` admin endpoint exposes `mdcore.scan.{submitted,completed,failed,timeout}` and `mdcore.cache.{hit,miss}`.
   - A healthy integration shows convergence between `submitted` and `completed`.
   - Healthy values do not show elevated `failed` or `timeout`.

## [MetaDefender Cloud](/docs/mdndr/operating-guide/integrations#metadefender-cloud)

MetaDefender Cloud is the hosted alternative to MetaDefender Core. Configuration and operational behavior match MetaDefender Core with these differences:

- **Endpoint.** Base URL is `https://api.metadefender.com/v4`, owned by OPSWAT. Administrators do not override it except for regional endpoints published by OPSWAT.
- **Authentication.** API-key only; Cloud does not support session-based authentication.
- **Connectivity probe.** The integration probes `/apikey/info` (Cloud does not expose `/apiversion`), which both validates the API key and returns account and license metadata.
- **Rate limit.** Cloud enforces stricter per-key rate limits than a typical Core deployment. Keep the `Maximum concurrent scans` value at its default until you confirm the subscription's quota headroom.
- **Network path.** The Manager must reach `api.metadefender.com` outbound. Deployments that route all outbound traffic through a proxy must populate the [Upstream HTTP Proxy](/docs/mdndr/operating-guide/manager-configuration) value.

Deployments typically choose MetaDefender Cloud when they do not operate a Core instance. They also must accept the data-share implications of file sample submission to a hosted multi-AV service. Air-gapped and regulated deployments use MetaDefender Core exclusively.

## [SIEM integration via Syslog](/docs/mdndr/operating-guide/integrations#siem-integration-via-syslog)

The Manager forwards logs to one or more external SIEM platforms over Syslog. SIEM integration is the primary mechanism that sends MetaDefender NDR events to customer pipelines. These pipelines provide long-term retention, cross-source correlation, and compliance reports.

### [What the Manager sends](/docs/mdndr/operating-guide/integrations#what-the-manager-sends)

The Manager forwards seven categories of logs. The Manager sends each category in real time. It preserves full context: community identifier, sensor identifier, tenant identifier, and group identifier. Thus, a SIEM can correlate across sources without loss of MetaDefender NDR-specific provenance.

| Category | Contents |
| --- | --- |
| **Audit** | User and system actions -- logins, policy changes, sensor adoption and disown, configuration modifications, role assignments. |
| **Engine** | Suricata engine events, rule reloads, detection-engine lifecycle, signature-apply acknowledgments. |
| **System** | Operating-system, service, and resource-related logs from the Manager and from every adopted sensor. |
| **Alert** | Every alert MetaDefender NDR produces -- Suricata signature alerts, C2 alerts, MetaDefender Core verdicts, machine learning anomaly detections, behavioral threshold detections. |
| **File info** | Every `fileinfo` event -- carved artifact metadata, with or without a MetaDefender Core verdict. |
| **Enrichment** | Threat-intelligence enrichment results applied to events (InSights TIDB / REPDB hits, C2 feed matches, |
| **Session** | Suricata protocol events: HTTP, Domain Name System (DNS), TLS, Flow, Netflow, Remote Desktop Protocol, and operational-technology protocols. |

Administrators use per-destination and per-group rules to filter what each destination receives. A typical deployment sends Audit, Alert, and Enrichment to a compliance-tier SIEM with long retention. It sends higher-volume Session and File info categories to a separate analytics-tier SIEM or omits them.

### [Transport and properties](/docs/mdndr/operating-guide/integrations#transport-and-properties)

MVP ships UDP port 514 standard Syslog only. Each destination uses 514 by default. To use a non-standard port, override the destination port. The integration supports multiple concurrent destinations. Each destination has its own filter rules, facility and severity mapping, and optional structured-format override. RFC 5424 is the default. CEF and LEEF are selectable for destinations whose SIEM expects those formats. Administrators scope destinations to one or more sensor groups. For example, they can restrict a destination to alerts and enrichment for a specific site's sensor group.

The integration enforces tenant isolation. No log record crosses a tenant boundary. It buffers outbound logs during transient SIEM unavailability. It replays them when the destination recovers. It sanitizes every outbound message against log-injection attacks before it leaves the Manager.

TLS-encrypted Syslog (RFC 5425) and Syslog over Transmission Control Protocol (TCP) with TLS are PostMVP targets. The integration's architecture supports a migration path with minimal configuration. Administrators re-use the same destination records. They supply TLS credentials through the syslog-forward certificate store, which ships in MVP.

### [UI and REST surfaces](/docs/mdndr/operating-guide/integrations#ui-and-rest-surfaces)

In MVP the SIEM integration is API-first. The Manager exposes the surface through these REST endpoints. All endpoints have the `/api/server` prefix:

| Endpoint | Purpose |
| --- | --- |
| `GET /syslog-forward` | Retrieves the current syslog-forward configuration -- destinations, filter rules, format selections. |
| `POST /syslog-forward` | Updates the configuration. The Manager validates the new configuration and broadcasts it through the central configuration pipeline. It writes an audit entry on success. |
| `POST /syslog-forward/test` | Runs the SIEM connectivity test against a specified destination and does not save a configuration change. |
| `POST /syslog-forward/certificates` | Uploads the TLS client certificate and key for a destination. The Manager retains it in a dedicated certificate store. This store is separate from the Manager's HTTPS certificate store. The endpoint is available now so the store is ready for the PostMVP TLS transport. |
| `GET /syslog-forward/certificates` | Lists currently uploaded syslog-forward certificates and their status. |
| `DELETE /syslog-forward/certificates` | Removes an uploaded syslog-forward certificate. |

OPSWAT plans a graphical Administration surface for the same configuration in a subsequent release. The REST surface above is the MVP-supported mechanism.

### [Built-in connectivity test](/docs/mdndr/operating-guide/integrations#built-in-connectivity-test)

Every destination supports a **SIEM Connectivity Test** through `POST /api/server/syslog-forward/test`. The test does these actions:

1. Sends a probe syslog message to the destination.
2. Reports success or failure with detailed diagnostics. Diagnostics include unreachable host, port blocked, invalid response, and TLS handshake failure.
3. Runs against a prospective destination and does not change the persistent configuration.

Administrators run the connectivity test at initial configuration. They run it after any change to the destination. They also run it when a SIEM stops message receipt.

### [Status and observability](/docs/mdndr/operating-guide/integrations#status-and-observability)

Every destination has a real-time status indicator. It shows connection health, recent transmission rate, and the age of the last successful delivery. The audit log and Manager health view show a destination in a `Failed` state. The [Health and status](/docs/mdndr/operating-guide/health-and-monitoring) chapter describes the specific metrics.

The audit log captures the Manager's own syslog send activity with full attribution. This includes destination changes, buffer high-water events, and connectivity-test outcomes.

## [Common procedures](/docs/mdndr/operating-guide/integrations#common-procedures)

### [Add a new SIEM destination and run the connectivity test](/docs/mdndr/operating-guide/integrations#add-a-new-siem-destination-and-run-the-connectivity-test)

1. Prepare the destination parameters.

   - Set the hostname or IP address.
   - Set the UDP port (514 unless the SIEM expects otherwise).
   - Set the facility and severity mapping.
   - Select CEF or LEEF structured format if the SIEM needs it.
2. Issue `POST /api/server/syslog-forward/test` with the prospective destination fields.

   - The Manager sends a probe message.
   - It returns success or a detailed error.
3. If the test succeeds, issue `POST /api/server/syslog-forward` with the complete destination and its filter rules.

   - The Manager validates the configuration.
   - It saves the configuration.
   - It broadcasts the change.
   - It writes an audit entry.
4. Run the connectivity test again against the saved destination record. This step confirms the Manager's Syslog path.
5. Watch the destination's status indicator on the Manager's health view.

   - Confirm that log messages flow on the SIEM side.
   - Recent audit entries are the simplest confirmation.
6. If the destination scope applies only to specific sensor groups, trigger a representative event on a sensor in scope.

   - For example, send a low-criticality test alert.
   - Confirm that only the expected destinations receive the message.

### [Rotate the MetaDefender API key](/docs/mdndr/operating-guide/integrations#rotate-the-metadefender-api-key)

Credential rotation for MetaDefender Cloud or MetaDefender Core is a single-operator change with no service impact.

1. Obtain the new API key from the MetaDefender administration console. For MetaDefender Cloud, use the OPSWAT portal.
2. Open **Administration -> Configuration -> Integrations -> MetaDefender Core**.

   - Update the API key field.
   - The Manager runs a connectivity probe with the new credential before it saves the change.
   - A probe failure keeps the previous credential and returns the error.
3. On probe success, the Manager saves the change.

   - It broadcasts the new credential to the active enrichment service.
   - No restart is necessary.
4. Confirm that the rotation landed.

   - Watch `mdcore.scan.submitted` advance on the enrichment's `/api/metrics` admin endpoint.
   - Or select a recent `fileinfo` event on the Hunt page.
   - Confirm that MetaDefender Core enrichment data attaches to later events.
5. After the new credential is in service, revoke the old credential on the MetaDefender side.
6. Confirm that the audit log records the credential rotation.

   - It records the actor, the integration, and the outcome.
   - The Manager never writes the credential value to the audit log.

### [Rotate an integration credential used across a fleet](/docs/mdndr/operating-guide/integrations#rotate-an-integration-credential-used-across-a-fleet)

The MetaDefender Core integration runs Manager-side. Thus, credential rotation is a single-location change regardless of the number of sensors in the deployment. The same rule applies to the Upstream HTTP Proxy credential. Both changes propagate through the configuration-broadcast mechanism in [Manager Configuration](/docs/mdndr/operating-guide/manager-configuration). No per-sensor intervention is necessary.

## [Quick-start checklist: verify integrations](/docs/mdndr/operating-guide/integrations#quick-start-checklist-verify-integrations)

| Item | Action | Verification |
| --- | --- | --- |
| MetaDefender mode selected | Configure the integration for Cloud or Core -- not both. | The Integrations form displays the selected mode. The opposite mode's credential fields are empty. |
| MetaDefender endpoint reachable | Save the integration and let the Manager run its connectivity probe. | The form returns success; the audit log records the configuration change. |
| Hash-lookup round-trip | Trigger a known-good file download on a sensor. | `mdcore.cache.hit` or `mdcore.cache.miss` advances on `/api/metrics`. The merged event carries `status=enriched` for the MetaDefender Core enrichment. |
| File submission round-trip | Trigger a benign file download whose hash is not in the MetaDefender cache. | `mdcore.scan.submitted` and `mdcore.scan.completed` advance within the poll timeout. The merged event carries a scan verdict on the `fileinfo` event. |
| MIME and size filters sensible | Review the MIME skip-list and size cap against the deployment's file-mix expectations. | Frequently scanned categories pass: executables, archives, and office documents. The deployment skips high-volume categories that it does not need. |
| Syslog destination configured | Register at least one destination for the deployment's SIEM. | `GET /api/server/syslog-forward` returns the destination. The connectivity test reports success. |
| Syslog categories scoped | Confirm each destination's filter rules match the intended log scope of the SIEM. | Audit, alert, and enrichment records arrive at expected volume. The design includes or excludes high-volume session and file-info records. |
| Syslog reaches the SIEM | Trigger a recent administrative action. | The SIEM shows the audit entry within seconds. The destination's health indicator reports a recent successful delivery. |
| Buffer size is correct | Confirm the buffer depth matches the deployment's SIEM-availability expectations. | A brief simulated outage does not exceed the buffer. The buffer drains on recovery. |
| Upstream proxy configured | When applicable, confirm Upstream HTTP Proxy has a value. | MetaDefender Cloud and Updates reachability probes succeed. Enrichment metrics advance. |
| InSights feed currency | Confirm the Manager's InSights feed version is current. | Updates view shows recent successful updates. Fleet-wide distribution status equals **Applied**. |
| Tenant isolation honored | For multi-tenant deployments, confirm no log record or credential crosses a tenant boundary. | Tenant administrators see only destinations and credentials owned by the tenant. |
| Audit entries visible | Spot-check the audit log for recent integration changes. | Each integration event appears with actor, outcome, and correlation identifier. Credential values are absent. |

## [See also](/docs/mdndr/operating-guide/integrations#see-also)

- [Administration overview](/docs/mdndr/operating-guide/administration-page) -- the Administration page structure, access control, audit trail, and chapter map.
- [Manager Configuration](/docs/mdndr/operating-guide/manager-configuration) -- the Integration Settings, Syslog Configuration, Upstream HTTP Proxy, and SSL Certificate surfaces that control integration behavior.
- [Sensor Management](/docs/mdndr/operating-guide/sensor-management) -- Policy assignment, per-sensor configuration, and fleet-level operations that interact with integration scope.
- [Users, Groups, and RBAC](/docs/mdndr/operating-guide/users--groups--and-rbac) -- tenant isolation of integration credentials and syslog destinations; audit-log retention.
- [Updates Management](/docs/mdndr/operating-guide/updates-management) -- the InSights feed distribution pipeline.
- [Data Retention](/docs/mdndr/operating-guide/data-retention) -- how local retention policy interacts with Syslog send (Syslog send does not reduce local retention obligations).
- [Health and status](/docs/mdndr/operating-guide/health-and-monitoring) -- metrics and status indicators for each integration.
