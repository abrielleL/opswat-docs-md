<!-- source: https://www.opswat.com/docs/mdndr/operating-guide/alert--flow--and-pcap-pivoting -->

# Alert, Flow, and PCAP Pivoting

This runbook is a meta-reference for pivot patterns that each family-specific runbook uses. It does not describe a triage scenario. It describes the *motion* an analyst performs to move from one Hunt tab to another for evidence. Each other runbook in this chapter refers back to this one for named pivot mechanics. Thus, individual steps do not re-explain how right-click menus, new tabs, and filtered views combine.

This runbook is for Tier 1, 2, and 3 Security Operations Center (SOC) analysts, threat hunters, Managed Security Service Provider (MSSP) analysts, and incident responders. It assumes familiarity with the [Hunt Page](/docs/mdndr/operating-guide/hunt-page) surface: buckets, tabs, the detail sidebar, and the advanced-search query builder.

First-use acronym expansions in this runbook:

- SOC — Security Operations Center.
- MSSP — Managed Security Service Provider.
- IOC — Indicator of Compromise.
- IP — Internet Protocol.
- DNS — Domain Name System.
- HTTP — Hypertext Transfer Protocol.
- TLS — Transport Layer Security.
- SNI — Server Name Indication.
- SSH — Secure Shell.
- SMB — Server Message Block.
- RDP — Remote Desktop Protocol.
- SMTP — Simple Mail Transfer Protocol.
- FTP — File Transfer Protocol.
- QUIC — Quick User Datagram Protocol Internet Connection.
- MDCore — MetaDefender Core.
- PCAP — packet capture.
- PII — personally identifiable information.
- PHI — protected health information.
- CSV — Comma-Separated Values.
- JSON — JavaScript Object Notation.

## [When to use this runbook](/docs/mdndr/operating-guide/alert--flow--and-pcap-pivoting#when-to-use-this-runbook)

Analysts reach this runbook in two situations:

- **From another runbook.** Every family-specific runbook directs the analyst here when a step refers to a pivot by name. These runbooks include [Critical Alert Triage](/docs/mdndr/operating-guide/critical-alert-triage), [C2 Beacon Investigation](/docs/mdndr/operating-guide/c2-beacon-investigation) [Data Exfiltration Investigation](/docs/mdndr/operating-guide/data-exfiltration-investigation), [Malicious File Investigation](/docs/mdndr/operating-guide/malicious-file-investigation), [ML Anomaly Investigation](/docs/mdndr/operating-guide/ml-anomaly-investigation), and [Tunneling Investigation](/docs/mdndr/operating-guide/tunneling-investigation). Use this runbook when the analyst wants the mechanics in full.
- **As a self-training reference.** New analysts read the runbook end-to-end to build a mental map of the pivots available on the [Hunt Page](/docs/mdndr/operating-guide/hunt-page) before they encounter their first Critical alert.

The runbook has four named pivot motions: *alert → flow*, *flow → session*, *session → PCAP*, and *value → hunt*. A short etiquette section follows. It explains how to manage the tab workspace across a long investigation.

## [Pivot taxonomy](/docs/mdndr/operating-guide/alert--flow--and-pcap-pivoting#pivot-taxonomy)

Every pivot on the Hunt page shares three properties. Analysts read a runbook step faster when they know the pivot shape first.

- **Trigger.** The analyst right-clicks either a cell in the results table or a field in the detail sidebar. Both surfaces expose the same context menu; the sidebar is the more common trigger in practice because the analyst is already reading the row's enrichment blocks when the pivot opportunity appears.
- **Action.** The menu entry names the pivot. Options are *Hunt all events from this IP*, *Show all events with this community id*, *Show related events*, *Show related files*, *Search file hash across all events*, and *Copy to clipboard*. Each action carries a fixed filter template that MetaDefender NDR applies in the new tab.
- **Result.** A new tab opens on the appropriate bucket (*All Events*, *Netflows*, or *Files*), pre-filtered to the pivoted value, with the originating tab's time range preserved. The originating tab is never closed or modified by a pivot — the analyst can always return to the lead.

Pivots are cheap. A pivot is a right-click and a tab switch, not a query that the analyst composes. Runbooks assume the analyst performs multiple pivots per alert. They recommend a pivot *even when the answer looks obvious*. Corroborating evidence separates a defensible disposition from a guess.

## [Alert → flow pivot](/docs/mdndr/operating-guide/alert--flow--and-pcap-pivoting#alert--flow-pivot)

The *alert → flow* pivot answers the question *what is the shape of the connection this alert lives on?* It is the most frequent pivot in first-response triage and anchors every family-specific runbook's early steps.

### [Motion](/docs/mdndr/operating-guide/alert--flow--and-pcap-pivoting#motion)

1. Open the alert row. Use an *All Alerts* tab or any per-family sub-tab. Examples include Suricata Alert, C2 Infrastructure Alert, InSights Alert, MDCore Alert, Beaconing Detection, Data Exfiltration Detection, DNS Tunneling Detection, and ML Random Cut Forest Anomaly.
2. Right-click the `community_id` value. Use the `community_id` column in the row or the equivalent field in the sidebar header. Select **Show all events with this community id**.
3. Review the new *All Events* tab. The tab is pre-filtered to every event that carries the same `community_id`. It includes the original alert, the *Flow* record, protocol sessions, additional alerts, and enrichments. Protocol sessions include DNS, HTTP, TLS, SSH, SMB, RDP, SMTP, FTP, QUIC, and FileInfo. The originating tab remains open for re-entry.

The `community_id` is the 5-tuple correlator. It stitches every event that belongs to the same connection into one view. It is more reliable than a direct pivot on the source-and-destination pair. The correlator accounts for the protocol, ports, and direction. Thus, two distinct flows between the same hosts do not merge.

### [What to examine](/docs/mdndr/operating-guide/alert--flow--and-pcap-pivoting#what-to-examine)

On the new *All Events* tab the analyst scans:

- **The Flow record.** Packets to-server and to-client, bytes to-server and to-client, flow start and end, age, state, termination reason, alerted flag, transaction count, and exception policy. These fields describe the connection shape. A short-duration flow with balanced bytes is a single request-response. A long-duration flow with one-sided upload volume is a streaming transfer. An abnormally terminated flow with a low packet count is a reset or a half-open connection.
- **Related alerts on the same connection.** A single-family alert is a weaker hypothesis than a multi-family cluster. The analyst counts corroborating alerts: a Beaconing Detection co-occurring with a C2 Enrichment and a Suricata signature is three independent signals on one connection.
- **Session records.** One row per protocol transaction the parser emitted during the flow. Their presence tells the analyst which protocols rode the connection and which are worth pivoting into next.

### [When it is enough](/docs/mdndr/operating-guide/alert--flow--and-pcap-pivoting#when-it-is-enough)

The alert → flow pivot is enough when the Flow record and co-occurring alerts answer the open question. For example, the Flow record's packet cadence can corroborate a Beaconing Detection's connection count. In that case, no session-level detail is necessary.

The pivot is not enough when the question is about *what was on the wire*. It is not enough for DNS query names, TLS SNI, HTTP URLs, file contents, or SMTP recipients. These questions require the next pivot.

## [Flow → session pivot](/docs/mdndr/operating-guide/alert--flow--and-pcap-pivoting#flow--session-pivot)

The *flow → session* pivot answers the question *what protocol-level evidence lives on this connection?* It is the natural follow-on when the Flow record and the alert row raise a question the session records can answer.

### [Motion](/docs/mdndr/operating-guide/alert--flow--and-pcap-pivoting#motion)

1. Right-click the `community_id`. Use a Flow row or the *All Events* tab that the previous pivot opened. Select **Show related events**. The same action is available on the row or in the sidebar header.
2. Select the relevant protocol sub-tab. MetaDefender NDR opens a new *All Events* tab scoped to the same `community_id`. Use the per-protocol sub-tab on the *Network Sessions* bucket. Options are **DNS**, **HTTP**, **TLS**, **SSH**, **SMB**, **RDP**, **SMTP**, **FTP**, **QUIC**, and **FileInfo**. Each sub-tab applies the column projection documented in the [Hunt Page](/docs/mdndr/operating-guide/hunt-page) chapter.
3. Read each session row. Select each session row in turn. Read the sidebar's protocol-specific section. Sections include Suricata DNS, Suricata HTTP, Suricata TLS, SSH detail, SMB detail, RDP detail, SMTP detail, FTP detail, Suricata QUIC, and Suricata FileInfo.

### [What each protocol reveals](/docs/mdndr/operating-guide/alert--flow--and-pcap-pivoting#what-each-protocol-reveals)

Different protocols answer different questions on the same connection.

| Protocol | What the session reveals |
| --- | --- |
| **DNS** | Query name, record type, response code, answer data, Time-To-Live (TTL). Shows *what name resolved*, *whether the resolution succeeded*, *what Internet Protocol (IP) addresses returned*, and in DNS-tunneling scrutiny *what the labels look like*. |
| **HTTP** | Hostname, Uniform Resource Locator (URL), method, status, user agent, referer, content type, response length. Shows *what URL the client requested*, *how the client identified itself*, *what content came back*, and *whether the exchange matches the declared purpose*. |
| **TLS** | Version, SNI, certificate subject and issuer, validity window, JA3 / JA3S / JA4 fingerprints, cipher, session-resumption flag. Answers *what name the client requested* (often the only visible identity inside an encrypted session), *who issued the certificate*, and *whether the client's TLS fingerprint matches known tooling*. |
| **SSH** | Protocol version, client and server software, HASSH client and server fingerprints, key-exchange and cipher algorithms. Answers *what client connected*, *what the server identified as*, and *whether the fingerprint pair matches known tooling*. |
| **SMB** | Command, share, filename, access flags, status. Shows *what file the client read or wrote*, *on which share*, and *whether the action succeeded*. |
| **RDP** | Client name, client build, cookie, version, certificate subject and issuer. Shows *which client connected* and *which target appeared*. |
| **SMTP** | Mail-from, recipients, HELO, attachment filenames, reply codes. Answers *who the mail was from and to*, *what attachments rode it*, and *whether the server accepted delivery*. |
| **FTP** | Command, command data, reply code. Answers *what commands the client issued* and *what file names crossed the control channel*. |
| **QUIC** | Version, SNI, JA3 / JA4 fingerprints, Application-Layer Protocol Negotiation (ALPN). Answers the encrypted-session questions the TLS sub-tab answers for Transmission Control Protocol traffic. |
| **FileInfo** | Filename, magic string, Secure Hash Algorithm 256-bit (SHA-256), Message Digest 5 (MD5), size, state (`CLOSED` when eligible for MDCore enrichment), stored flag. Shows *what files the sensor extracted from the connection* and *which files MD Core scanned*. |

The analyst rarely reads every sub-tab. The runbook step directs which protocol matters. A DNS-family alert directs to the DNS sub-tab. A file-scan alert directs to FileInfo. A data-exfiltration question about upload content directs to HTTP or TLS.

### [Session → file sub-pivot](/docs/mdndr/operating-guide/alert--flow--and-pcap-pivoting#session--file-sub-pivot)

If a session row carries file metadata and the question is about the file, extend the pivot. Right-click the row. Select **Show related files**. A new *Files* tab opens with files extracted from the same flow. Each file row carries the MDCore scan verdict when enrichment has run. Read the row sidebar before you pull the file from archival storage for deeper analysis. The sidebar includes Suricata FileInfo and the MDCore Enrichment section.

### [When it is enough](/docs/mdndr/operating-guide/alert--flow--and-pcap-pivoting#when-it-is-enough)

The flow → session pivot is enough when protocol-level evidence answers the open question. For example, the DNS query name matches or does not match a known indicator. The TLS SNI can identify the destination by name. The SMTP recipient list can name the target user. The pivot is not enough for bytes that the session parser did not surface as structured fields. Examples include encrypted payload bodies, binary command-channel fragments, and protocol-parser edge cases with no session row. Those cases require the PCAP pivot.

## [Session → PCAP pivot](/docs/mdndr/operating-guide/alert--flow--and-pcap-pivoting#session--pcap-pivot)

The *session → PCAP* pivot is the last resort. It answers the question *what were the actual bytes on the wire?* when the alert, the flow record, and the session metadata together do not resolve the question. PCAP inspection is slower, more expensive, and more constrained than any other pivot, so the runbook calls it out explicitly rather than implying it.

### [PCAP availability is selective](/docs/mdndr/operating-guide/alert--flow--and-pcap-pivoting#pcap-availability-is-selective)

MetaDefender NDR does not retain a packet capture for every flow. PCAP retention depends on configuration. The sensor captures selectively based on policy: alert-triggered capture, rolling windows, or tagged hosts. On-sensor storage capacity bounds retention. An analyst can request the PCAP for a flow and find that no capture exists. This runbook accepts that as a valid outcome of the pivot.

The rule is: flows and protocol logs first, PCAP only when they cannot answer the question. Treating PCAP as the default pivot fills sensor storage fast, slows the investigation, and buries the question in packet-level detail the analyst does not need for most dispositions.

### [Motion](/docs/mdndr/operating-guide/alert--flow--and-pcap-pivoting#motion)

1. Confirm that session metadata cannot answer the question. Typical cases include an absent session row. Another case is a session row with the relevant field in the payload body. Examples are an encrypted TLS application record or an HTTP request body truncated by parser size. A suspected protocol anomaly between sessions is another case. Examples are an unexpected reset or a malformed handshake.
2. Record the exact flow identity. Record the `community_id`, the source and destination 5-tuple, and the flow start and end timestamps. Use the timestamps from the Flow record. Record any alert identifier that the PCAP request should cite.
3. Request the PCAP. Follow the SOC's PCAP-request workflow to retrieve a capture slice for the recorded time window. Restrict the window to the minimum necessary. A two-hour slice for a ten-minute flow wastes sensor storage and slows retrieval. [Sensor Management](/docs/mdndr/operating-guide/sensor-management) covers on-demand PCAP capability and the exact retrieval interface. This runbook scope stops at *request the PCAP* because the retrieval surface is an administrative concern.
4. Inspect the PCAP. Open the retrieved PCAP in the SOC's standard packet analysis tool. Inspect the payload for the specific question that session metadata could not answer.

### [PCAP handling discipline](/docs/mdndr/operating-guide/alert--flow--and-pcap-pivoting#pcap-handling-discipline)

PCAPs carry more than the question under investigation. They carry everything the sensor saw on the wire during the capture window. This can include PII, PHI, authentication material, or unrelated traffic. Follow the SOC's data-handling and redaction procedures for the captured file. Keep the PCAP out of shared systems that are not authorized for full-traffic data. Dispose of the file on completion. Runbook dispositions refer to specific findings from the PCAP. For example, *"HTTP POST body at offset 0x1234 contains Base64-encoded credential dump"*. They do not refer to the PCAP file itself.

### [When the pivot fails](/docs/mdndr/operating-guide/alert--flow--and-pcap-pivoting#when-the-pivot-fails)

If the PCAP is unavailable for the requested window, the pivot returns *no result*. Causes include exhausted sensor capacity, disabled capture on the affected segment, or expired retention. Do not escalate harder. Widen the session-metadata search. Use a longer time window, adjacent connections from the same source, or related flows with the same destination. Document the PCAP gap on the ticket. This gives future capture policy tuning the evidence to justify the change.

## [Value → hunt pivot](/docs/mdndr/operating-guide/alert--flow--and-pcap-pivoting#value--hunt-pivot)

The *value → hunt* pivot is the simplest of the four and the one analysts use most casually. It answers the question *where else has this value appeared?*

### [Motion](/docs/mdndr/operating-guide/alert--flow--and-pcap-pivoting#motion)

1. Right-click a value. The value can be an IP, a domain, a SHA-256 or MD5 hash, a `community_id`, a signature message, a user agent, or a TLS fingerprint. Use a table cell or the sidebar's protocol-specific or enrichment section.
2. Select the pivot action. The context menu shows pivot actions that match the value type. The catalog is the same on every tab. The value drives the context menu, not the tab bucket.

| Menu Action | Scope | Result |
| --- | --- | --- |
| **Copy to clipboard** | Any value | The system places the value on the system clipboard. Analysts use it to paste into advanced search, external lookup tools, or the ticket evidence record. |
| **Hunt all events from this IP** | Any IP-valued cell (source or destination) | A new *All Events* tab opens filtered to rows where the IP appears in either 5-tuple position. The originating tab's time range carries over. |
| **Show related events** | Any row | A new *All Events* tab opens filtered to the row's `community_id`. Equivalent to the *flow → session* pivot when used on a Flow or session row. |
| **Show all events with this community id** | Any row with a `community_id` | A new *All Events* tab opens on that `community_id`. This is the *alert → flow* pivot when used from an alert row. |
| **Show related files** | Any row with a flow or session context | A new *Files* tab opens filtered to files extracted from the same flow. |
| **Search file hash across all events** | Any SHA-256 or MD5 cell | A new *All Events* tab opens on every event that references the hash. These events include the upstream HTTP download, SMB write, SMTP delivery, downstream MDCore scan result, and any alert the hash fired. |

### [Time range is load-bearing](/docs/mdndr/operating-guide/alert--flow--and-pcap-pivoting#time-range-is-load-bearing)

Every value → hunt pivot inherits the originating tab's time range. If the analyst widens the time range before the pivot, the pivoted tab inherits the wider window. This helps check whether an indicator has a multi-day or multi-week history. If the analyst pivots from a narrow window, the pivoted tab is also narrow. For example, *Last 15 minutes* on a real-time tab can miss prior occurrences. Runbook steps specify the window explicitly when analysts must check a seven-day repetition pattern.

### [Advanced-search alternative](/docs/mdndr/operating-guide/alert--flow--and-pcap-pivoting#advanced-search-alternative)

If the context menu does not name the pivot target explicitly, compose the query manually in the advanced-search builder. Examples include a Suricata Signature Identifier, a Behavioral Detection's destination Autonomous System Number, or an ML Random Cut Forest anomaly score threshold. [Hunt page — Search and filtering](/docs/mdndr/operating-guide/hunt-page) documents the mechanics. The result has the same shape as a context-menu pivot. A new tab opens scoped to the value, but the analyst assembles the filter by hand.

## [Pivot etiquette](/docs/mdndr/operating-guide/alert--flow--and-pcap-pivoting#pivot-etiquette)

Pivot-driven investigations produce many tabs quickly. Tab hygiene keeps the workspace useful rather than overwhelming.

- **Open tabs purposefully.** A pivot that does not answer a specific open question is clutter. The analyst asks *what question does this pivot answer?* before performing it, and closes the resulting tab if the question turns out to be already answered elsewhere.
- **Keep the lead tab open.** The originating alert tab is the return address for the investigation. Analysts do not close it until the disposition is recorded.
- **Close stale pivot tabs.** A pivot tab that has served its purpose — the repetition check returned no prior occurrences, the community-id view confirmed a single-signal alert — is closed immediately. The workspace carries one to five active investigation tabs on a typical triage, not twenty.
- **Name tabs implicitly through ordering.** Tabs can be reordered by drag. Analysts group related pivots together (for example, *All Alerts* → *alert's community_id* → *alert's source IP*) so the chain reads left to right.
- **Export, do not screenshot, when the evidence must leave the Hunt page.** The CSV and JSON export on the tab action menu produces a machine-readable artifact the ticket can cite. Screenshots are a last resort for evidence that cannot be expressed as a row set.
- **Rely on persistence for long investigations.** Every tab — its bucket and detection type, time range, search expression, column customization, sort, and pagination — persists across sign-out and sign-in. An investigation that spans a shift change resumes in the incoming analyst's workspace exactly where the outgoing analyst left off. The lead tab and the pivot chain survive a browser restart, a session expiry, and a sign-in from a different machine.
- **Row selection does not persist.** The detail sidebar's open state and the selected-row highlight reset at sign-in. If analysts must return to a specific row, they bookmark it with a row filter. For example, paste the row's `community_id` into the tab's quick-search. Do not rely on the selection itself.

Investigations that outrun the workspace's useful tab count indicate a structural problem, not a discipline problem. If an analyst manages more than ten active tabs, reshape the investigation into fewer, broader queries. Do not continue to add pivots. At that point, the family-specific runbook usually directs escalation to Tier 2 or Tier 3.

## [See also](/docs/mdndr/operating-guide/alert--flow--and-pcap-pivoting#see-also)

- [Investigation Runbooks](/docs/mdndr/operating-guide/investigation-runbooks) — the runbook mindset and the summary pivot vocabulary this runbook expands.
- [Critical Alert Triage](/docs/mdndr/operating-guide/critical-alert-triage)— the generic first-response runbook that exercises every pivot in this reference.
- [C2 Beacon Investigation](/docs/mdndr/operating-guide/c2-beacon-investigation) — uses the *alert → flow* pivot on `community_id` and the *value → hunt* pivot on the destination indicator.
- [Data Exfiltration Investigation](/docs/mdndr/operating-guide/data-exfiltration-investigation) — uses the *alert → flow* pivot for the Flow record and the *flow → session* pivot into HTTP and TLS for upload evidence.
- [Malicious File Investigation](/docs/mdndr/operating-guide/malicious-file-investigation) — uses the *value → hunt* pivot on the file hash and the session → file sub-pivot for carrier-protocol evidence.
- [ML Anomaly Investigation](/docs/mdndr/operating-guide/ml-anomaly-investigation) — uses the *flow → session* pivot to read the underlying event payload that scored anomalous.
- [Tunneling Investigation](/docs/mdndr/operating-guide/tunneling-investigation) — uses the *value → hunt* pivot on the parent domain and the *flow → session* pivot into concurrent TLS and HTTP sessions.
- [Hunt Page](/docs/mdndr/operating-guide/hunt-page) — the detailed reference on tabs, buckets, sub-tabs, sidebar renderers, right-click context menus, and the tab-persistence model.
- [Sensor Management](/docs/mdndr/operating-guide/sensor-management) — PCAP capture policy, retention bounds, and the on-demand retrieval interface referenced in the PCAP pivot.
