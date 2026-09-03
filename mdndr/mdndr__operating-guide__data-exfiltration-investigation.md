<!-- source: https://www.opswat.com/docs/mdndr/operating-guide/data-exfiltration-investigation -->

# Data Exfiltration Investigation

This runbook continues [Critical Alert Triage](/docs/mdndr/operating-guide/critical-alert-triage) for alerts with evidence of unauthorized outbound data transfer. It covers the principal trigger, a **Data Exfiltration Detection Alert** on the Hunt page. It also covers a secondary trigger from routine review. In that review, a threat hunter sees an unusually high client-to-server byte ratio on the Netflows bucket. A future Producer-Consumer Ratio widget on the Dashboard will also surface this pattern. Either path routes into this runbook. The steps take the analyst from "an alert with exfiltration-shaped evidence" to "a triage decision recorded in the incident-management system".

This runbook is for Tier 1 Security Operations Center (SOC) analysts who triage outbound-traffic alerts. Tier 2 analysts use it to resolve escalations. Threat hunters use it to pivot from an unusual upload pattern into a broader compromise investigation. It assumes the analyst already executed Critical alert triage through step 5 when the lead came from a Critical-severity alert. The affected asset, supporting sidebar evidence, repetition history, and same-flow corroboration are already in hand.

First-use acronym expansions in this runbook:

- SOC: Security Operations Center.
- IOC: Indicator of Compromise.
- C2: command-and-control.
- IP: Internet Protocol.
- DNS: Domain Name System.
- TLS: Transport Layer Security.
- SNI: Server Name Indication.
- ASN: Autonomous System Number.
- GeoIP: geographical IP lookup.
- RFC-1918: the Internet Engineering Task Force standard reserving private IP ranges.
- MB: megabyte -- 1,048,576 bytes.
- TIDB: Threat Intelligence Database.
- REPDB: Reputation Database.
- PCR: Producer-Consumer Ratio.
- PCAP: packet capture.
- HTTPS: Hypertext Transfer Protocol Secure.
- HTTP: Hypertext Transfer Protocol.
- FTP: File Transfer Protocol.
- SSH: Secure Shell.
- SFTP: Secure File Transfer Protocol.
- SMB: Server Message Block.
- TCP: Transmission Control Protocol.
- S3: Simple Storage Service.
- SaaS: Software-as-a-Service.
- CI: continuous integration.
- EDR: endpoint detection and response.
- DLP: Data Loss Prevention.
- NAT: Network Address Translation.
- IR: incident response.
- MVP: Minimum Viable Product.
- FRD: Functional Requirements Document.

## [Trigger scenario](/docs/mdndr/operating-guide/data-exfiltration-investigation#trigger-scenario)

An analyst reaches this runbook from one of two starting points. In either case the lead describes an internal host sending materially more bytes to an external endpoint than it received.

- **Primary -- Data Exfiltration Detection Alert on the Hunt page.** The analyst opens the [Hunt Page](/docs/mdndr/operating-guide/hunt-page). The analyst goes to the *All Alerts* bucket. The analyst selects the *Data Exfiltration Detection Alert* sub-tab. A row carries `flow_count`, `total_upload_bytes`, `total_download_bytes`, `upload_ratio`, a 15-minute window, and destination country / ASN / organization. total_upload_bytes uses tens or hundreds of megabytes. total_download_bytes uses tens of megabytes or less. upload_ratio is above 2:1. The severity can be *Critical*, *High*, *Medium*, or *Low*. It depends on the ratio, absolute upload volume, and whether an IOC matched on the destination.
- **Secondary -- unusually high upload ratio spotted during proactive review.** During a routine pass through the *Netflows* bucket, the analyst sorts by `bytes_toserver` descending. The analyst notices a flow, or group of flows to a single destination, where the client-to-server byte count dwarfs the server-to-client count. Analogous leads surface from the *Top Destination IPs* widget on the [Dashboard](/docs/mdndr/operating-guide/dashboard). This occurs when an unfamiliar external destination jumps to the top of the chart. The dedicated Producer-Consumer Ratio (PCR) widget listed in the Dashboard roadmap will expose this pattern directly when it ships.

The two trigger surfaces converge in this runbook because the investigation is the same. An internal host uploads enough data to an external endpoint that the pattern requires review. A Data Exfiltration Detection Alert attaches the pipeline's windowed aggregate and severity tier. An upload-ratio lead from Netflows or the Dashboard lacks the aggregate. It surfaces the same behavior at the raw-flow level. The evidence steps are identical when the analyst is in the Hunt workspace.

## [Prerequisites](/docs/mdndr/operating-guide/data-exfiltration-investigation#prerequisites)

Before executing this runbook the analyst confirms the following.

- Steps 1 through 5 of [Critical Alert Triage](/docs/mdndr/operating-guide/critical-alert-triage) are complete when the lead is a Critical-severity alert. The incident ticket already contains the affected asset, owner, criticality tier, sidebar evidence summary, and repetition or same-flow correlation. For sub-Critical leads or proactive-hunt leads, record the affected asset and its criticality tier before this runbook.
- A Hunt session open on the originating *Data Exfiltration Detection Alert* tab (for the primary trigger) or on a *Netflows* tab filtered to the upload-heavy flow (for the secondary trigger), with the detail sidebar visible.
- Access to the organization's asset inventory for the affected host.
- A working mental model of the organization's routine outbound upload traffic. Know which corporate Software-as-a-Service (SaaS) backup and file-sync destinations are in daily use. Know which cloud-storage buckets the organization owns or has sanctioned. Know which source-code hosts developers push to. Know which artifact repositories publish builds. Know which business-partner endpoints exchange bulk data on a schedule.
- Access to the incident-management system used by the SOC and to the organization's Data Loss Prevention (DLP) channel if one is in use.
- Awareness of the organization's working hours and sanctioned batch-upload windows. Examples include nightly backup and scheduled reporting exports. Use this context to calibrate the time-of-day reading in step 6 against the local baseline.

If any item is absent, stop. A data-exfiltration investigation without asset context can cause errors. A poor picture of sanctioned upload destinations can also cause errors. These errors can over-escalate legitimate cloud-backup traffic. They can under-escalate genuine compromise. The prerequisites help prevent both failure modes.

## [Investigation steps](/docs/mdndr/operating-guide/data-exfiltration-investigation#investigation-steps)

Each step is numbered. Each step adds a distinct piece of evidence. Each step feeds the decision tree at the end. Execute steps in order even when the verdict looks obvious early. Never record an exfiltration disposition on partial evidence. The same file-direction byte ratio can indicate a benign cloud backup or malicious data theft.

### [1. Open the alert sidebar and capture the core evidence](/docs/mdndr/operating-guide/data-exfiltration-investigation#1-open-the-alert-sidebar-and-capture-the-core-evidence)

On the Hunt page, the analyst clicks the alert row to open the detail sidebar. The sidebar header carries the alert type, the severity label, and the confidence score. The *Data Exfiltration Detection* section lists the pipeline's windowed aggregate:

- `flow_count` -- the total flows the pipeline counted in the 15-minute window for the `(src_ip, dest_ip, dest_port, app_proto)` group.
- `unique_flows` -- the count of distinct 5-tuple flows in the window. It helps distinguish one long session from many short ones.
- `total_upload_bytes` and `total_download_bytes` -- raw byte sums across the window, client-to-server and server-to-client.
- `upload_mb` and `download_mb` -- the byte sums rendered in megabytes.
- `upload_ratio` -- `total_upload_bytes / total_download_bytes`, capped at 999.99 when the server sent zero bytes.
- `malicious_iocs` and `iocs_checked` -- the pipeline's independent IOC check against entities on the destination side.
- `dest_country`, `dest_asn`, `dest_org` -- GeoIP-derived destination characterization.
- `window_start` and `window_end` -- the 15-minute window bounds for the aggregate.

The base network section above carries `src_ip`, `src_port`, `dest_ip`, `dest_port`, `proto`, `app_proto`, and the `community_id` correlator. The analyst captures the full base record so subsequent pivots have a reference point.

When the lead is a proactive-hunt lead rather than an alert, the equivalent fields live on the Netflows row. These fields are `bytes_toserver`, `bytes_toclient`, `pkts_toserver`, `pkts_toclient`, `flow.duration`, and the flow-end reason. The fields also live on the sidebar's *Flow* section. The analyst captures those numbers and proceeds.

### [2. Examine the upload volume and upload ratio against the severity tier](/docs/mdndr/operating-guide/data-exfiltration-investigation#2-examine-the-upload-volume-and-upload-ratio-against-the-severity-tier)

Data Exfiltration Detection's severity mapping is mechanical. It uses the ratio and the absolute upload volume. Any IOC match on the destination promotes the alert to *Critical* regardless of the behavioral numbers. The analyst reads the numbers from step 1. The analyst locates the alert on the following ladder.

| Severity | Upload Ratio | Upload volume | Notes |
| --- | --- | --- | --- |
| **Critical** | >= 10:1 | >= 100 MB | *Or* any IOC match, any ratio, any volume. |
| **High** | >= 5:1 with >= 10 MB,  or >= 2:1 with >= 100 MB | -- | Two independent paths into this tier. |
| **Medium** | >= 2:1 | >= 10 MB |  |
| **Low** | >= 2:1 | >= 1 MB | Minimum threshold; many benign uploads land here. |

A threshold-Critical Data Exfiltration alert on 200 MB uploaded at a 15:1 ratio is a larger signal than a threshold-Low alert. The threshold-Low example is 1.5 MB at a 2:1 ratio. The analyst's expectation for corroborating evidence scales accordingly. The analyst also checks the reading against the underlying flow behavior. A single very-large flow and many moderately-large flows have different implications at the same severity tier. Many flows suggest a sustained upload session, such as backup or chunked transfer. One large flow suggests a single-object upload, such as a compressed archive or database dump.

The analyst records the ratio, the volume, the flow count, and the severity tier explicitly in the ticket. *"45 flows totaling 212 MB uploaded against 8 MB downloaded (26.5:1 ratio) over a 15-minute window, severity Critical"* is the kind of note that survives handoff.

### [3. Verify the source is internal and the destination crosses the network boundary](/docs/mdndr/operating-guide/data-exfiltration-investigation#3-verify-the-source-is-internal-and-the-destination-crosses-the-network-boundary)

The pipeline already enforces the directional boundaries at construction. `src_ip` must be inside an RFC-1918 range. `dest_ip` must be outside all RFC-1918 ranges. Thus, every surfaced alert meets these conditions. The analyst confirms them anyway. The same verification surfaces two kinds of misclassification that invalidate the rest of the investigation.

- **Incorrectly-classified internal ranges.** Some organizations extend their internal network into ranges the pipeline does not treat as RFC-1918. Examples include carrier-grade Network Address Translation (NAT) space (`100.64.0.0/10`), link-local (`169.254.0.0/16`), and unique-local IPv6 (`fc00::/7`). When `src_ip` falls into one of those ranges, the flow is internal-to-external only by the pipeline's definition. The analyst verifies against the organization's network diagram before treating the destination as truly external.
- **Public IPs on internal infrastructure.** Some enterprises route specific internal services through public IP ranges the organization owns. When the destination `dest_ip` belongs to an owned public range, the alert is internal-to-internal in practice and the exfiltration hypothesis does not apply. The analyst identifies owned ranges from the asset inventory or from the organization's IP address management record.

When both sides check out, the source is a genuine internal host. The destination is genuinely outside the organization's network. The analyst notes the source's subnet and role. Examples include workstation subnet, server subnet, operational-technology subnet, and guest Wi-Fi subnet. The analyst also notes the destination's reachability path. Examples include direct outbound, through an enterprise proxy, or through a monitored egress point. This context governs how the later vendor-identification step reads the destination.

### [4. Characterize the destination endpoint](/docs/mdndr/operating-guide/data-exfiltration-investigation#4-characterize-the-destination-endpoint)

The destination is the prospective exfiltration endpoint. The analyst characterizes it along three dimensions before pivoting any further, using `dest_country`, `dest_asn`, `dest_org`, and the reverse-DNS name when available.

- **Known corporate cloud storage.** The destination resolves to a mainstream cloud-storage or object-store provider the organization has sanctioned. Examples include Amazon Simple Storage Service (S3), Azure Blob Storage, Google Cloud Storage, Backblaze B2, Wasabi, and DigitalOcean Spaces. The ASN and reverse DNS usually identify the provider. If the analyst confirms the sanctioned bucket identity, the hypothesis leans strongly toward sanctioned backup / file-sync. Confirmation can come from the TLS Server Name Indication (SNI), Hypertext Transfer Protocol (HTTP) hostname, or hostname label in the prior DNS record.
- **Recognized business SaaS or partner endpoint.** The destination resolves to a known Software-as-a-Service (SaaS) provider the organization uses. Examples include corporate OneDrive, Google Workspace, Dropbox Business, Box, Salesforce, and a specific managed-file-transfer platform. The destination can also be a business-partner endpoint on an approved data exchange. The hypothesis is similar to sanctioned cloud storage. The verification checklist shifts to user account, sanctioned workflow, and client identity.
- **Unknown third-party endpoint.** The destination resolves to an unsanctioned location for outbound data. Examples include a hosting provider, virtual-private-server reseller, residential or small-business Internet service provider, bulletproof host, or paste / public-file-sharing service. The reverse DNS may be generic or absent. Generic reverse DNS can use numbered customer subdomains. The `dest_org` reads as a reseller rather than a first-party cloud provider. This category carries the heaviest suspicion on its own. It pairs with the protocol reading in step 5 to resolve the hypothesis.

The analyst records the destination characterization explicitly. One shape is *"dest_ip 52.216.72.10, ASN 16509 Amazon.com, reverse DNS* `s3-1.amazonaws.com`*, matched TLS SNI* `company-backups-prod.s3.amazonaws.com` * -- known corporate S3 bucket"*. The other is *"dest_ip 185.x.x.x, ASN 200325 XYZ-Reseller, country RO, no reverse DNS, SNI missing -- unknown third-party hosting"*.

### [5. Check the protocol and the session evidence](/docs/mdndr/operating-guide/data-exfiltration-investigation#5-check-the-protocol-and-the-session-evidence)

The protocol and the session payload either corroborate the destination characterization from step 4 or contradict it. The analyst reads `proto` and `app_proto` from the base section and then pivots to the session tab for the same flow.

From the alert sidebar, right-click `community_id`. Select *Show all events with this community id*. A new *All Events* tab opens on the [Hunt Page](/docs/mdndr/operating-guide/hunt-page). The tab filters results to every protocol transaction, flow record, file extraction, and enrichment that belongs to the same connection. This view exposes:

- **The declared application protocol.** Expect Transmission Control Protocol (TCP) port 443 with `app_proto: https` or `tls` for cloud-storage and SaaS uploads. TCP port 80 with plaintext HTTP for a multi-megabyte upload is atypical outside legacy integrations. Secure Shell (SSH) / Secure File Transfer Protocol (SFTP) on port 22 is associated with off-channel data movement. File Transfer Protocol (FTP) on ports 20-21 and Server Message Block (SMB) on port 445 have the same association. Raw TCP with `app_proto: null` or `failed` on an unusual port also has this association.
- **The TLS session, when the upload is encrypted.** The Server Name Indication (SNI), certificate subject and issuer, and JA3 / JA4 client fingerprint identify the client and endpoint. This applies even when the payload is opaque. A recognizable enterprise-backup-client JA3, corporate-cloud SNI, or valid certificate to the organization's cloud tenancy corroborates the sanctioned hypothesis. An unfamiliar JA3 corroborates the suspicion hypothesis. A self-signed or Let's-Encrypt-issued certificate for a reseller hostname also corroborates it. An SNI that does not resolve back to the destination IP under normal DNS also corroborates it.
- **The HTTP session, when the upload rides plaintext HTTP.** The method is expected to be `PUT` or `POST`. The User-Agent identifies the client software. The URL path and Content-Type hint at the uploaded data. Examples include `application/json`, `application/octet-stream`, `application/zip`, and `multipart/form-data`. Recognizable backup-agent or cloud-client user agents identify sanctioned tooling. Generic `curl`, `Wget`, `python-requests`, or the default User-Agent for a scripting language raise suspicion. This is especially true from a non-developer workstation.
- **The DNS resolution that preceded the flow.** When the destination was reached by name, the DNS query and answer sit on the same `community_id`. The resolved name either confirms the destination characterization (it matches a corporate cloud hostname) or contradicts it (the hostname is a random-looking label under a generic top-level domain).

The session evidence usually resolves the ambiguity between *sanctioned corporate cloud* and *unknown third-party endpoint*. If the protocol is opaque and no session evidence is available, the hypothesis stays open. Raw TLS without a usable SNI is an example. The blast-radius and PCAP steps add independent weight.

### [6. Examine the time-of-day pattern](/docs/mdndr/operating-guide/data-exfiltration-investigation#6-examine-the-time-of-day-pattern)

Exfiltration is a timing signal in addition to a volume signal. The analyst reads the `window_start` timestamp against the organization's working hours and the source host's baseline pattern.

- **Business-hours upload from a workstation consistent with the user's role.** A developer workstation pushing a 150 MB build artifact to a sanctioned artifact repository at 14:00 local time is weak evidence of exfiltration even at a 15:1 ratio. The volume and the timing match the workflow.
- **Off-hours upload from a workstation whose user is not working.** The same workstation that uploads 150 MB at 02:30 local time with no scheduled backup window strongly shifts evidence toward exfiltration. The analyst verifies against any sanctioned overnight-backup schedule. The analyst also verifies against the organization's endpoint activity logs if EDR provides them. This helps rule out a legitimate scheduled job.
- **Uploads from a server during a declared backup window.** Database servers and file servers often have nightly or weekly backup windows. These windows produce large, ratio-lopsided uploads to a sanctioned cloud destination. The timing corroborates the sanctioned hypothesis when the window matches. It contradicts the hypothesis when the upload falls outside the scheduled window.
- **Recurring uploads at the same time every day from the same source to the same destination.** The pattern matches a scheduled integration. Examples include automated reporting export, log shipping, and monitoring agent. Find sanctioned integrations in the organization's integration catalog. Unknown recurrences are leads in their own right.

The analyst records the timing reading in the ticket alongside the local working-hours context. *"Window 02:17-02:32 local, off-hours for this workstation's user, no sanctioned backup schedule registered for this host"* is the kind of note the disposition rests on.

### [7. Check for IOC enrichment on the destination](/docs/mdndr/operating-guide/data-exfiltration-investigation#7-check-for-ioc-enrichment-on-the-destination)

This is the single strongest disposition lever in the runbook. The alert sidebar carries the *C2 Enrichment* section whenever any C2 feed match fired on the destination. The *InSights Enrichment* section carries parallel matches from the OPSWAT InSights Threat Intelligence Database (TIDB) and Reputation Database (REPDB) feeds.

- **Any** `c2.matches[]` **entry present.** The alert is IOC-Critical by construction. Severity is *Critical*. Alert-level confidence is *0.99*. The match payload identifies the threat actor or malware family for the indicator. This finding is sufficient for escalation to incident response. See *Decision Tree*.
- **Data Exfiltration pipeline** `malicious_iocs > 0` **with** `iocs_checked > 0`**.** The behavioral pipeline's independent IOC check observed a feed hit on the destination during the window. The pipeline auto-escalates its own severity to *Critical* when this field is truthy. Confidence on the alert rises to 0.99 under the same auto-escalation rule.
- **Parallel InSights match on the destination IP or DNS name.** See [InSights TIDB and REPDB](/docs/mdndr/operating-guide/insights-tidb-and-rpedb) for the feed semantics. A TIDB hit (threat intelligence) is high-confidence. A REPDB hit (reputation) is lower-confidence but still material in aggregate. A REPDB hit on a paste / anonymous-file-sharing category corroborates an exfiltration hypothesis. This is true even without an actor-linked TIDB entry.
- **No IOC match on any feed.** The alert is threshold-Critical (or sub-Critical) on behavioral evidence alone. Escalation now depends on evidence from multiple steps. These steps are volume and ratio in step 2, destination characterization in step 4, protocol and session evidence in step 5, timing evidence in step 6, and blast-radius evidence in the next step.

The analyst records the IOC state explicitly in the ticket. Use *"IOC match present on dest_ip / dns query name / neither"*. This is the single field that changes downstream dispositions.

### [8. Check the blast radius and request a PCAP when session evidence is insufficient](/docs/mdndr/operating-guide/data-exfiltration-investigation#8-check-the-blast-radius-and-request-a-pcap-when-session-evidence-is-insufficient)

A destination that only one internal host uploads to is a host-scoped event. A destination that many internal hosts upload to is an environment-scoped event. It is either a coordinated compromise or a benign shared service. Blast radius is decisive evidence.

From the alert row, right-click the **destination IP**. For a DNS-match alert, use the destination domain. Select *Hunt all events from this IP*. Alternatively, run a quick search on the domain in a new *All Events* tab. Expand the time range to *Last 24 hours* or *Last 7 days* as appropriate. Read the result:

- **One source only.** The event is host-scoped. Escalation, containment, and forensic recovery target the affected host.
- **A small handful of sources, all sharing a common software baseline (same EDR agent, same backup agent, same build image).** The shared behavior points at a sanctioned workflow when the destination is a recognized vendor. It points at a coordinated compromise when the destination is unknown. Redraw the blast radius to include the whole set either way.
- **Many sources across business units to a recognized cloud / SaaS provider.** The destination is almost certainly a sanctioned endpoint and the alert volume is a tuning candidate rather than an incident. The analyst still confirms the client identity on at least one sampled connection before closing.
- **Many sources across business units to an unrecognized third-party endpoint.** This is the strongest population-scale exfiltration signal. The investigation escalates immediately to incident response regardless of the behavioral severity tier.

The analyst then opens a second tab with the right-click pivot *Hunt all events from this IP* on the **source IP**. The analyst widens the time range to *Last 7 days*. This tab shows every conversation the affected host has held with any external destination. A host that uploads to one suspicious destination is a host-scoped compromise. A host that uploads to a drifting set of suspicious destinations over days is a longer-horizon problem. This changes the escalation shape.

If the session evidence from step 5 is insufficient, request a PCAP for the flow's time window. Use the organization's PCAP request workflow. Insufficient evidence includes a raw TLS connection with no SNI. It also includes a custom TCP stream with no application-protocol parse. PCAP availability is configuration-dependent and selective on MetaDefender NDR. See [Alert, Flow, and PCAP Pivoting](/docs/mdndr/operating-guide/alert--flow--and-pcap-pivoting). Thus, not every flow has a retained PCAP. If a PCAP is available, inspect file-type magic bytes at the start of the upload. Inspect Content-Type headers for any inner protocol that the capture exposes. Inspect the overall byte cadence. Use these items to judge whether a single large object or a chunked session produced the volume. If a PCAP is unavailable, conclude the investigation on the evidence already collected. Record the gap in the ticket so a disposition on partial evidence is traceable.

## [Decision tree](/docs/mdndr/operating-guide/data-exfiltration-investigation#decision-tree)

The analyst records one of four outcomes. Each branch lists the minimum artifacts captured before the ticket is closed.

- **Escalate -- confirmed or probable exfiltration.** Escalate if the alert is IOC-Critical on any source. IOC-Critical means any `c2.matches[]` entry or `malicious_iocs > 0`. Escalate if the alert is threshold-Critical to an unrecognized third-party destination on a Tier 1 or Tier 2 asset. Threshold-Critical means ratio >= 10:1 with upload >= 100 MB. Escalate if two or more independent indicators converge. Examples include an unrecognized destination, off-hours timing, client User-Agent or JA3 inconsistent with sanctioned tooling, paste-site or file-sharing REPDB hit, or PCAP showing archive-file magic bytes. Escalate if the blast-radius pivot surfaces the same unrecognized destination across multiple business units. The analyst opens an incident response (IR) ticket. The analyst requests endpoint isolation for the affected host or hosts. The analyst hands the source off to forensic recovery. If policy allows indicator-based blocking, the analyst blocks the destination at the perimeter. The analyst engages the organization's Data Loss Prevention (DLP) channel. The analyst transfers the evidence record and pivot tabs into the incident. The *Escalate* branch ends this runbook. Incident-response procedures take over.
- **Monitor -- suspicious but not conclusive.** Use this disposition when the evidence is partial. Examples include a Medium or High Data Exfiltration alert to a known cloud provider. In that case, the sanctioned bucket identity cannot be positively confirmed. Another example is an off-hours upload that matches a previously-declared backup schedule but has no ticket trail. A Tier 3 asset with a one-off ratio-heavy flow and no corroborating signals is also an example. The analyst records the observation in the ticket. The analyst leaves the Hunt tabs open. The analyst schedules a follow-up review, typically within four to twelve hours for Critical severity and twenty-four hours for sub-Critical. If the pattern recurs within the review window, the analyst re-enters at step 1 with accumulated context. If it does not recur and no new evidence appears, the disposition moves to *close as benign*.
- **Close as benign -- identified legitimate explanation.** Use this disposition when the evidence positively identifies a sanctioned upload pattern. Examples include a confirmed corporate S3 bucket or Azure container with a matching SNI. Another example is a client identity that matches a sanctioned backup agent. Client identity includes User-Agent or JA3 fingerprint. The timing must match a declared backup window. The source host must be expected to participate in that workflow. The analyst records the specific fields that justify the conclusion in the ticket. Example: *"destination* `company-backups-prod.s3.amazonaws.com`*, ASN 16509, JA3 fingerprint* `771,49195-...` *matches corporate Veeam backup agent, window 02:00-04:00 aligns with nightly backup schedule for subnet 10.10.8.0/24, closing as benign"*. Later readers can reopen the conclusion when one of those fields changes.
- **Tune the rule -- recurring benign pattern with a scoped policy fix.** Use this disposition when the same sanctioned upload pattern has confirmation multiple times across the same population. The source of the noise is understood. Examples include a specific backup product, artifact repository, or reporting integration. The policy system supports a scoped exclusion. The correct tuning for Data Exfiltration is the scoped allowlist in [Behavioral Detections](/docs/mdndr/operating-guide/behavioral-detections). Add the specific destination to the Policy's exfiltration allowlist. For example, add the corporate S3 endpoint for an approved backup workflow. Do not raise the minimum-upload floor globally. Tuning is a detection-engineering action, not a triage shortcut. The analyst opens a follow-up task against the detection's policy definition. The analyst does not tune inline. The analyst submits the change through the organization's peer-review workflow. The analyst keeps the alert live until the tuned policy deploys. The default disposition for a single confirmed-benign alert is *close*, not *tune*. A single occurrence does not justify reduced coverage.

Record every branch in the incident-management system. The runbook reference, disposition, asset context, ratio / volume / timing / IOC evidence, and pivot tab references form the minimum record. If the disposition is *Escalate*, the record hands off directly into the incident.

## [Common false-positive patterns](/docs/mdndr/operating-guide/data-exfiltration-investigation#common-false-positive-patterns)

A material share of Data Exfiltration alerts have benign explanations. Pattern recognition saves investigation time. It prevents analysts from over-escalation.

- **Sanctioned cloud backup and file-sync uploads.** Corporate OneDrive, Dropbox Business, Google Workspace Drive, Box, iCloud, and enterprise Veeam / Commvault / Rubrik / Acronis backup agents produce large, ratio-lopsided uploads to the vendor's cloud on a schedule. The destination ASN and SNI usually identify the vendor; the client User-Agent or JA3 usually identifies the agent. Disposition: *close* with the vendor identity and the sanctioned workflow recorded. When the same vendor produces sustained alert volume across many hosts, the SOC opens a tuning task against the Data Exfiltration policy to add the destination to the allowlist.
- **Source-code push and artifact-repository uploads.** Developer workstations pushing branches to GitHub, GitLab, Bitbucket, Azure DevOps, or an internal Git server produce ratio-heavy uploads during working hours. Continuous-integration (CI) runners push build artifacts to Amazon Elastic Container Registry, Google Artifact Registry, Nexus, Artifactory, or similar. The source identity (developer workstation, CI runner) and the destination identity (known code or artifact host) resolve this pattern quickly. Disposition: *close* with the sanctioned workflow recorded.
- **Business-integration batch exports.** Scheduled data transfers between the organization and approved partners produce recurring ratio-heavy uploads at the same time every day. Examples include nightly financial reporting, data-warehouse extracts to a shared staging bucket, and compliance exports to a regulator's endpoint. Disposition: *close* with the integration identity recorded. When the same integration generates recurring alerts, the SOC opens a tuning task to add the destination to the allowlist.
- **Video-conferencing and real-time-communication uploads.** Extended Zoom, Microsoft Teams, Google Meet, or Webex sessions can produce ratio-heavy flows. This can occur from a conference-room host or a busy user. The client uploads camera and screen-share streams while it receives mostly control traffic during active speaking. The destination is usually a known media relay. The SNI identifies the vendor. Disposition: *close* when the destination and client are recognized.
- **Telemetry and observability data export.** Application-performance-monitoring agents, log-shipping collectors, metrics forwarders, and endpoint-detection-and-response (EDR) cloud uploaders produce many small, ratio-heavy flows to the vendor's ingestion endpoint. The vendor identity is usually recognizable from the SNI. Disposition: *close* when the vendor is identified; tune via policy only when the same vendor produces sustained alert volume.
- **Misclassified internal destinations.** An internal file server, backup target, or artifact repository that is reachable over a public IP can surface as an exfiltration alert. An internal subnet not in the standard RFC-1918 ranges can do the same. The pipeline enforces those ranges. Disposition: *close* after the analyst confirms the destination identity. Open a follow-up task against the sensor home-net configuration or pipeline RFC-1918 definition when the misclassification is systemic.
- **Red-team, penetration-testing, and attack-simulation activity.** Authorized internal testing produces exfiltration alerts by design; exfiltration-simulation frameworks upload large archives to attacker-controlled cloud endpoints as part of the evaluation. Disposition: *close* once the activity is confirmed with the red-team or vulnerability-management program. Every SOC maintains a communication channel with internal testing teams so these alerts are identifiable on sight.

Closing on a false-positive pattern still requires the runbook's evidence record. *"Looks like a backup"* is not a disposition; *"destination* `company-backups-prod.s3.amazonaws.com`*, ASN 16509, JA3 matches corporate Veeam agent, timing aligns with scheduled 02:00 backup window"* is.

## [See also](/docs/mdndr/operating-guide/data-exfiltration-investigation#see-also)

- [Critical Alert Triage](/docs/mdndr/operating-guide/critical-alert-triage) -- the generic first-response runbook that hands off to this one.
- [C2 Beacon Investigation](/docs/mdndr/operating-guide/c2-beacon-investigation) -- companion runbook when the same destination also carries beacon-shaped evidence; a beacon plus an exfiltration ratio on the same `community_id` is a late-stage-compromise signal.
- [Malicious File Investigation](/docs/mdndr/operating-guide/malicious-file-investigation) -- follow-up runbook when the exfiltration carried a file that MetaDefender Core scanned on the way out, or when an earlier inbound file on the same source host preceded the upload.
- [ML Anomaly Investigation](/docs/mdndr/operating-guide/ml-anomaly-investigation) -- follow-up runbook when the exfiltration correlates with a Random Cut Forest anomaly on the same source.
- [Tunneling Investigation](/docs/mdndr/operating-guide/tunneling-investigation) -- follow-up runbook when the upload rode a DNS or similar covert channel rather than a direct connection.
- [Alert, Flow, and PCAP Pivoting](/docs/mdndr/operating-guide/alert--flow--and-pcap-pivoting) -- the pivot-mechanics meta-runbook referenced by steps 5 and 8.
- [Behavioral Detections](/docs/mdndr/operating-guide/behavioral-detections) -- background on the Data Exfiltration pipeline, including window shape, thresholds, severity and confidence scoring, and tuning guidance.
- [C2 and Threat Intelligence](/docs/mdndr/operating-guide/c2-and-threat-intelligence) -- background on the C2 feed whose matches drive the IOC auto-escalation in step 7.
- [InSights TIDB and REPDB](/docs/mdndr/operating-guide/insights-tidb-and-rpedb) -- parallel intelligence feeds referenced in step 7, including the paste-site and anonymous-file-sharing REPDB categories that corroborate exfiltration hypotheses.
- [Detection Overview](/docs/mdndr/operating-guide/detection-overview) -- unified severity scale, confidence scale, and the IOC auto-escalation rule.
- [Hunt Page](/docs/mdndr/operating-guide/hunt-page) -- tabs, sidebar, right-click pivots, and the *Netflows* bucket used for the secondary-trigger proactive-hunt path.
- [Dashboard](/docs/mdndr/operating-guide/dashboard) -- Top Destination IPs widget used as a secondary lead surface; the Producer-Consumer Ratio (PCR) widget is listed on the Dashboard roadmap and will expose this pattern directly when it ships.
