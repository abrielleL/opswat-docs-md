<!-- source: https://www.opswat.com/docs/mdndr/operating-guide/critical-alert-triage -->

# Critical Alert Triage

This runbook is the general-purpose first-response procedure for any Critical-severity alert in MetaDefender NDR, regardless of which detection family raised it. It runs before any family-specific runbook and determines whether the alert warrants escalation, ongoing monitoring, closure, or a rule-tuning action. When the alert belongs to a family that has its own runbook, this runbook hands off to it at step 6.

This runbook is for Tier 1 Security Operations Center (SOC) analysts who handle the first pass on an alert queue. Tier 2 and Tier 3 analysts use it when they open an alert forwarded from Tier 1. They use it to confirm the upstream triage before deeper investigation. It assumes familiarity with the [Hunt Page](/docs/mdndr/operating-guide/hunt-page) workspace and the six detection families in [Detection Quick Reference](/docs/mdndr/operating-guide/detection-quick-reference).

First-use acronym expansions in this runbook:

- SOC: Security Operations Center.
- IOC: Indicator of Compromise.
- C2: command-and-control.
- TIDB: Threat Intelligence Database.
- REPDB: Reputation Database.
- RCF: Random Cut Forest.
- AV: antivirus.
- IP: Internet Protocol.
- TLS: Transport Layer Security.
- SNI: Server Name Indication.
- DNS: Domain Name System.
- ASN: Autonomous System Number.
- RFC-1918: the Internet Engineering Task Force standard reserving private IP ranges.
- SID: Signature Identifier.
- PCAP: packet capture.
- MITRE ATT&CK: Adversarial Tactics, Techniques, and Common Knowledge.
- DHCP: Dynamic Host Configuration Protocol.
- ARP: Address Resolution Protocol.
- PUA: potentially-unwanted application.
- NAT: Network Address Translation.
- BGP: Border Gateway Protocol.
- EDR: endpoint detection and response.

## [Trigger scenario](/docs/mdndr/operating-guide/critical-alert-triage#trigger-scenario)

An analyst sees a **Critical**-severity alert surface in one of two places:

- The **Recent Alerts** widget on the [Dashboard](/docs/mdndr/operating-guide/dashboard), where the row carries a red *Critical* severity badge.
- The **All Alerts** tab on the [Hunt page](/docs/mdndr/operating-guide/hunt-page), where the analyst is working through a severity-sorted queue.

The alert can come from any detection family. Examples include a Suricata signature match, a C2 Infrastructure Alert, an InSights Alert, an MDCore Alert, a Behavioral Detection, or an ML Random Cut Forest Anomaly. The common factor is the severity label. The unified severity scale sets *Critical* only when a detection carries an IOC match. It can also set *Critical* when a detection clears the highest family-specific threshold. See [Detection Overview](/docs/mdndr/operating-guide/detection-overview). Use this runbook for every Critical alert before you record a disposition.

## [Prerequisites](/docs/mdndr/operating-guide/critical-alert-triage#prerequisites)

Before executing the runbook the analyst confirms the following.

- A signed-in MetaDefender NDR session with a role that grants **Hunting** access.
- Access to the organization's asset inventory or host directory. Use it to identify the affected endpoint by business function, owner, and criticality. The inventory is outside MetaDefender NDR on the MVP end-state.
- Access to the incident-management system used by the SOC (ticket tracker, paging platform, or case-management tool). Every Critical triage produces a record in that system regardless of outcome.
- If the alert is an MDCore Alert, know the organization's file-scanning policy. Know which hosts can receive executables. Know the whitelisted software-distribution paths. If the alert is a C2 or InSights alert, know which third-party Software-as-a-Service (SaaS) endpoints are in routine use. This prevents an incorrect read of legitimate destinations as malicious infrastructure.

If any item is absent, stop. You cannot complete the investigation without asset context or an escalation channel.

## [Investigation steps](/docs/mdndr/operating-guide/critical-alert-triage#investigation-steps)

Each step is numbered. Each step adds a distinct piece of evidence. Each step feeds the decision tree at the end. Execute the steps in order. Do not skip steps when the verdict looks obvious. Never record a Critical-severity disposition on partial evidence.

### [1. Open the alert and confirm severity provenance](/docs/mdndr/operating-guide/critical-alert-triage#1-open-the-alert-and-confirm-severity-provenance)

The analyst clicks the Recent Alerts row on the Dashboard. This mounts the Hunt detail sidebar in place. Alternatively, the analyst selects the row on the Hunt page's *All Alerts* tab. The sidebar header shows the alert type, the severity label, and the confidence score.

The first question is *why* the alert is Critical, because Critical on MetaDefender NDR has two distinct meanings:

- **IOC-Critical.** The sidebar carries a C2 Enrichment Section or an InSights Enrichment Section with a matched entity, source feed, and score. The unified pipeline auto-escalates any detection with an IOC match to severity *Critical* and confidence *0.99*. The detection's native threshold is secondary in this case -- a 16-connection Beaconing alert is Critical because its destination is on the C2 feed, not because 16 connections is high.
- **Threshold-Critical.** The sidebar carries no IOC enrichment. The alert reached Critical on the detection family's own threshold. Examples include 50-plus connections in a Beaconing window and six-plus positive AV engines on an MDCore scan. Other examples are a Suricata signature with native severity 1 and a Data Exfiltration with a 10-to-1 upload ratio. A Data Exfiltration with 100-plus megabytes uploaded is also an example.

The distinction changes what the rest of the investigation looks for. IOC-Critical investigations center on *the indicator*. They ask where else on the network anyone communicates with it. They ask what feed tagged it. They ask whether it corroborates another detection on the same host. Threshold-Critical investigations center on *the behavior*. They ask what the metrics look like. They ask whether the pattern is recurrent. They ask whether a legitimate explanation exists.

### [2. Confirm the affected asset and its business criticality](/docs/mdndr/operating-guide/critical-alert-triage#2-confirm-the-affected-asset-and-its-business-criticality)

The analyst reads the **source** and **destination** endpoints on the sidebar's base network section. At least one endpoint is an internal host. The host is either the victim or the infected party. Victim examples include incoming Suricata signature and inbound scan. Infected-party examples include outbound beaconing, data exfiltration, DNS tunneling, and file download. That internal host is the *affected asset*.

The analyst identifies the host in the organization's asset inventory and records three attributes before proceeding:

- **Owner** -- which team or user is responsible for the host.
- **Function** -- what the host does (domain controller, finance workstation, build server, guest Wi-Fi device, operational-technology gateway, Internet of Things sensor).
- **Criticality** -- whether the host is Tier 1 (business-critical, elevated blast radius), Tier 2 (important but not single-point-of-failure), or Tier 3 (commodity endpoint). Tier 1 hosts change the decision tree. A plausibly-benign alert on a domain controller still needs escalation for confirmation. The same alert on a guest Wi-Fi device can close more readily.

If the source is an RFC-1918 address that does not appear in the inventory, check for a DHCP lease mapping. Also check for a recent ARP observation before you proceed. Ghost endpoints on internal subnets are a known blind spot. Without an identity, the analyst cannot set the correct disposition.

### [3. Review the supporting evidence in the sidebar](/docs/mdndr/operating-guide/critical-alert-triage#3-review-the-supporting-evidence-in-the-sidebar)

The sidebar renders a type-specific view of the event with every block the record carries. See [Hunt Page](/docs/mdndr/operating-guide/hunt-page). The analyst scans every section from top to bottom. The analyst records the evidence that justifies the Critical rating. The relevant sections depend on the family.

- **Suricata Alert section.** Signature message, SID, category, MITRE ATT&CK technique and tactic, action (alert or drop), and the printable payload. The analyst reads the signature message to understand the matched behavior. The analyst notes the MITRE technique for cross-reference. The analyst inspects the payload for visible indicators, such as encoded strings, exploit-framework fingerprints, and suspicious user agents.
- **C2 Enrichment section.** Match type (IP or DNS), matched value, confidence, score, and source feed. The analyst captures the matched entity -- it is the centerpiece of the indicator-pivot in step 4.
- **InSights Enrichment section.** Matched entity, feed tagging (TIDB, REPDB, or both), and any additional threat-feed context.
- **MDCore Enrichment section.** Scan result, threat name, positive engines over total engines, scan details per AV engine, and file metadata (SHA-256, filename, size, type). The analyst records the hash and threat name.
- **Behavioral Alert section.** Detection-specific metadata: connection count, byte standard deviation and coefficient of variation, upload and download totals, upload ratio, window bounds, destination country, destination ASN, destination organization, and IOC match status.
- **ML Anomaly fields.** Anomaly score, threshold crossed, model version, and the underlying event type (DNS, HTTP, or Flow). For ML anomalies, *the underlying event payload* is the supporting evidence. It is not a family-specific field block. The analyst reads the network-base section of the underlying event to understand what was anomalous.

Any blocks that are absent tell the analyst something too. A Behavioral Detection with no C2 or InSights enrichment is threshold-Critical and warrants a harder look at the behavior metrics. A C2 Infrastructure Alert with no Beaconing section means the indicator fired on a one-off connection rather than a sustained pattern.

### [4. Check for repetition on the same source or destination](/docs/mdndr/operating-guide/critical-alert-triage#4-check-for-repetition-on-the-same-source-or-destination)

Before the analyst asks *is this threat real?*, the analyst asks *has this happened before?* A recurring pattern changes the disposition. A first-time alert can be a one-off event. The same alert on the same source for the tenth time in a week is a sustained problem.

From the alert row or sidebar, the analyst right-clicks the **source IP** and selects *Hunt all events from this IP*. A new [Hunt Page](/docs/mdndr/operating-guide/hunt-page) tab opens on *All Events* filtered to that IP. The analyst widens the time range to **Last 7 days** and reviews:

- Prior alerts on the same source -- same type, different type, any severity. Count them and note the detection families.
- Whether the current alert's destination appears repeatedly in the source's recent history. Recurrent contact with the same external endpoint over days is a strong signal for C2 beaconing or long-duration tunneling.
- Whether other sources on the internal network talk to the same destination. A shared external indicator across multiple internal hosts raises the blast radius.

The analyst then repeats the pivot on the **destination IP** or **destination domain**. Use *Hunt all events from this IP* or a quick-search on the domain in a new *All Events* tab. This answers the symmetric question. Is anyone else on the network currently communicating with the same external endpoint? The pivot is especially important for IOC-Critical alerts. The external indicator is the anchor. The affected population can extend far beyond the originating host.

Tab persistence preserves these pivot tabs across the investigation so the analyst can return to the original alert and to each pivot view without losing state.

### [5. Correlate with other detection signals on the same flow](/docs/mdndr/operating-guide/critical-alert-triage#5-correlate-with-other-detection-signals-on-the-same-flow)

Multi-signal convergence is the single strongest basis for escalation (see [Investigation Runbooks](/docs/mdndr/operating-guide/investigation-runbooks)). The analyst checks whether other detection families fired on the same connection.

From the alert row or sidebar, the analyst right-clicks the `community_id` column. The analyst selects *Show all events with this community id*. A new *All Events* tab opens. It includes every protocol transaction, flow record, file extraction, and enrichment that shares the connection's 5-tuple correlator. The analyst scans the tab for:

- **Other alert rows** on the same flow. A Beaconing Detection that co-occurs with a Suricata signature alert and a C2 Enrichment gives three signals on one connection, not one.
- **Session records** (DNS, HTTP, TLS, FileInfo) that expose payload metadata. The analyst checks for:

  - TLS SNI, certificate subject, and JA3 / JA4 fingerprints that indicate malicious tooling.
  - HTTP hostnames, user agents, and response content types inconsistent with the traffic's declared purpose.
  - DNS query names that resolved to the destination -- a meaningful domain name changes the read of a bare-IP alert.
  - FileInfo extractions tied to the same flow -- files downloaded or uploaded during the alerting window.
- **The Flow record** -- total bytes, packet counts per direction, flow duration, and abnormal termination reasons.

A single-family alert with no corroborating signals on the same flow is a weaker hypothesis than a multi-family cluster. The analyst records the corroborating signal count and notes which families contributed.

### [6. Hand off to the family-specific runbook](/docs/mdndr/operating-guide/critical-alert-triage#6-hand-off-to-the-family-specific-runbook)

At this point the analyst has a full picture of the alert. This picture includes its severity provenance, IOC or threshold. It includes the affected asset and business criticality. It includes the supporting sidebar evidence and the repetition history on both endpoints. It also includes any correlated signals on the same flow. The final investigation step applies the family-specific runbook. Use it for deeper evidence before you make a disposition.

| Alert Family | Runbook |
| --- | --- |
| Beaconing Detection, C2 Infrastructure Alert (IP or DNS), any Critical carrying a C2 Enrichment | [C2 Beacon Investigation](/docs/mdndr/operating-guide/c2-beacon-investigation) |
| Data Exfiltration Detection, any Critical with an anomalous upload-ratio pattern | [Data Exfiltration Investigation](/docs/mdndr/operating-guide/data-exfiltration-investigation) |
| MDCore High, Medium, or Low AV Detection; any Critical with an MDCore enrichment carrying `threat_found` | [ML Anomaly Investigation](/docs/mdndr/operating-guide/ml-anomaly-investigation) |
| ML Random Cut Forest Anomaly | [ML Anomaly Investigation](/docs/mdndr/operating-guide/ml-anomaly-investigation) |
| DNS Tunneling Detection or DNS Tunneling Hourly aggregate | [Tunneling Investigation](/docs/mdndr/operating-guide/tunneling-investigation) |
| Suricata Alert, InSights Alert (not combined with any of the above), or any family not covered by a dedicated runbook | Continue this runbook to the decision tree |

The [Alert, Flow, and PCAP Pivoting](/docs/mdndr/operating-guide/alert--flow--and-pcap-pivoting) meta-runbook documents the pivot patterns every family-specific runbook uses and is the reference for any pivot step whose motion is unfamiliar.

## [Decision tree](/docs/mdndr/operating-guide/critical-alert-triage#decision-tree)

The analyst records one of four outcomes. Each branch lists the minimum artifacts to capture before ticket closure.

- **Escalate.** The evidence indicates a confirmed or probable threat. Escalate if the alert is IOC-Critical on a Tier 1 or Tier 2 asset. Escalate if the alert is threshold-Critical and at least one additional detection family corroborates it. The corroboration can occur on the same flow or same source over the trailing seven days. Escalate if an MDCore alert reports a found threat with six or more positive engines. Escalate if a Suricata signature of native severity 1 fires with corroborating behavioral or enrichment evidence. The analyst opens an incident ticket. The ticket includes the alert identifier, asset identity, sidebar evidence summary, pivot tab references, and corroborating signals. The runbook hand-off at step 6 resumes inside the incident.
- **Monitor.** The evidence is suggestive but not conclusive. Examples include single-signal alerts and IOC-Critical on a low-criticality asset with no prior history. Another example is threshold-Critical with no repetition and no corroboration. The analyst leaves the Hunt tab and pivot tabs open. The analyst records the current observations in the ticket. The analyst schedules a follow-up review, typically within four to twelve hours for Critical severity. If the pattern recurs, the analyst re-enters at step 1 with the accumulated context. If the pattern does not recur within the review window, the disposition moves to *close as benign*.
- **Close as benign.** The evidence positively identifies a legitimate explanation. Examples include a destination that resolves to a known corporate SaaS endpoint. Other examples include a legitimate installer file hash from a whitelisted update channel. A software-update client can produce a beaconing pattern. A monitored Virtual Private Network (VPN) tunnel can produce a long-duration flow. A known environment change, such as a new subnet or load balancer, can explain the anomaly score. The analyst records the specific fields that justify the conclusion in the ticket. Example: *"destination 52.84.0.0/15 is AWS CloudFront, confirmed by ASN enrichment; user agent matches internal software update client"*. Later readers can reopen the conclusion if one of those fields changes.
- **Tune the rule.** The same benign pattern has confirmation multiple times across the same population. The source of the noise is understood. The policy system supports a scoped exclusion. Tuning is a detection-engineering action, not a triage shortcut. The analyst opens a follow-up task against the detection's policy definition. The analyst does not tune inline. The analyst submits the change through the organization's peer-review workflow. The analyst keeps the alert live until the tuned policy deploys. The default disposition for a single confirmed-benign alert is *close*, not *tune*.

Record every branch in the incident-management system. The runbook reference, disposition, asset context, evidence summary, and pivot tab references form the minimum record.

## [Common false-positive patterns](/docs/mdndr/operating-guide/critical-alert-triage#common-false-positive-patterns)

Critical alerts produce a recurring set of false positives across deployments. Pattern recognition saves investigation time. It prevents the analyst from over-escalation.

- **Software-update beacons.** Operating-system update agents, browser update channels, EDR agents, and telemetry clients check in to well-known infrastructure. The schedule can look like C2 beaconing. It has regular intervals, uniform payload sizes, and high connection counts over long windows. The destination ASN and reverse DNS usually identify the vendor. Examples include Microsoft, Apple, Google, Cloudflare, Akamai, or a specific EDR vendor. The IOC feeds do not flag them. Set disposition to *close* with the vendor identity recorded. Tune through policy only if the same software covers a large population and produces sustained noise.
- **Cloud backup and file-sync uploads.** Endpoints with configured cloud backup (corporate OneDrive, Dropbox Business, Google Workspace, Box) produce outbound upload volumes that trip Data Exfiltration thresholds. The destination resolves to the backup vendor's storage cluster. The user agent or TLS SNI identifies the client. Set disposition to *close* when the destination and client are recognized. Escalate if the destination is unknown or the client's presence on the host is unexpected.
- **Legitimate large file downloads flagged by MDCore.** Installers that include packers, installers signed but marked as PUA, and development tools flagged by heuristics can produce MDCore alerts with one to two positive engines. Set disposition to *close* when the file is recognized and its delivery path is legitimate. Escalate if the file reaches a Tier 1 host outside the sanctioned software-distribution channel.
- **Service discovery and telemetry as DNS tunneling.** Some telemetry protocols, BGP anycast routing health checks, and service-discovery mechanisms emit DNS queries with unusually long labels, unusual record types, or high unique-subdomain counts. Set disposition to *close* after the analyst identifies the parent domain and source service. Tune through policy only if a specific vendor's DNS pattern generates recurring alerts across a known population.
- **Internal-to-internal alerts from misclassified subnets.** If the sensor's home-net configuration incorrectly marks an RFC-1918 subnet as external, internal traffic can trip these detections. A NAT boundary that misrepresents the source can cause the same result. Set disposition to *close*. Open a follow-up task against the sensor configuration.
- **Load-balancer and proxy artifacts.** Forward proxies, reverse proxies, and load balancers that rewrite source IPs can create an impossible destination count for one host. This can fire Connection Spray or anomaly detections. Set disposition to *close* after the analyst confirms the proxy identity. Tune through policy by excluding the proxy IP from the affected detection.
- **Red-team and vulnerability-scanning activity.** Authorized internal red-team exercises and vulnerability scanners produce Critical alerts by design -- they use real exploit traffic, real C2 tooling, and real malware samples. Triaged as *close* once the activity is confirmed with the red-team or vulnerability-management program. Every SOC maintains a communication channel with internal testing teams so these alerts are identifiable on sight.

Closing on a false-positive pattern still requires the runbook's evidence record. *"Looks like a software update"* is not a disposition; *"destination Microsoft Update Services, ASN 8075, user agent Windows-Update-Agent"* is.

## [See also](/docs/mdndr/operating-guide/critical-alert-triage#see-also)

- [Investigation Runbooks](/docs/mdndr/operating-guide/investigation-runbooks) -- the runbook mindset and pivot-pattern vocabulary used throughout this chapter.
- [C2 Beacon Investigation](/docs/mdndr/operating-guide/c2-beacon-investigation) -- family-specific continuation for C2 and Beaconing alerts.
- [Data Exfiltration Investigation](/docs/mdndr/operating-guide/data-exfiltration-investigation) -- family-specific continuation for Data Exfiltration alerts.
- [Malicious File Investigation](/docs/mdndr/operating-guide/malicious-file-investigation) -- family-specific continuation for MDCore alerts.
- [ML Anomaly Investigation](/docs/mdndr/operating-guide/ml-anomaly-investigation) -- family-specific continuation for RCF Anomaly alerts.
- [Tunneling Investigation](/docs/mdndr/operating-guide/tunneling-investigation) -- family-specific continuation for DNS Tunneling alerts.
- [Alert, Flow, and PCAP Pivoting](/docs/mdndr/operating-guide/alert--flow--and-pcap-pivoting) -- the pivot-mechanics meta-runbook referenced by every step.
- [Detection Overview](/docs/mdndr/operating-guide/detection-overview) -- unified severity scale, confidence scale, and the IOC auto-escalation rule.
- [Hunt Page](/docs/mdndr/operating-guide/hunt-page) -- tabs, sidebar, right-click pivots, and the advanced-search query builder.
- [Dashboard](/docs/mdndr/operating-guide/dashboard) -- Recent Alerts row action that mounts the Hunt sidebar for in-place triage.
- [Severity and Confidence](/docs/mdndr/operating-guide/severity-and-confidence) -- full definitions of severity labels and confidence bands.
