<!-- source: https://www.opswat.com/docs/mdndr/operating-guide/c2-beacon-investigation -->

# C2 Beacon Investigation

This runbook continues [Critical Alert Triage](/docs/mdndr/operating-guide/critical-alert-triage) for alerts with command-and-control (C2) evidence. It covers the two cases an analyst encounters most often. One case is a **Beaconing Detection Alert** that surfaced the periodicity of an outbound connection. The other case is a **C2 Infrastructure Alert** that matched the destination or a resolved name against the OPSWAT Eyelet feed. Either alert type routes here from the step-6 hand-off in the generic runbook. The steps take the analyst from "an alert with C2-shaped evidence" to "a triage decision recorded in the incident-management system".

This runbook is for Tier 1 Security Operations Center (SOC) analysts who triage outbound-traffic alerts. Tier 2 analysts use it to resolve escalations. Threat hunters use it to pivot from a beacon lead into a broader compromise investigation. It assumes the analyst already executed Critical alert triage through step 5. The affected asset, supporting sidebar evidence, repetition history, and same-flow corroboration are already in hand.

First-use acronym expansions in this runbook:

- C2: command-and-control.
- SOC: Security Operations Center.
- IOC: Indicator of Compromise.
- IP: Internet Protocol.
- DNS: Domain Name System.
- TLS: Transport Layer Security.
- SNI: Server Name Indication.
- ASN: Autonomous System Number.
- GeoIP: geographical IP lookup.
- DGA: Domain Generation Algorithm.
- RAT: remote-access trojan.
- RFC-1918: the Internet Engineering Task Force standard reserving private IP ranges.
- STDDEV: standard deviation.
- CV: coefficient of variation.
- MVP: Minimum Viable Product.
- RDP: Remote Desktop Protocol.
- SSH: Secure Shell.
- NXDOMAIN: Non-Existent Domain DNS response.
- IR: incident response.
- VPN: Virtual Private Network.
- SaaS: Software-as-a-Service.
- EDR: endpoint detection and response.
- TTL: Time To Live.
- TIDB: Threat Intelligence Database.
- REPDB: Reputation Database.

## [Trigger scenario](/docs/mdndr/operating-guide/c2-beacon-investigation#trigger-scenario)

An analyst opens the [Hunt Page](/docs/mdndr/operating-guide/hunt-page). The analyst goes to the *All Alerts* bucket and sees one of the following rows. In either case, the analyst has opened the detail sidebar. The generic Critical alert triage runbook has identified the alert as a candidate for this family-specific continuation.

- A **Beaconing Detection Alert** on the *Beaconing Detection Alert* sub-tab. The row carries a connection count, a byte coefficient of variation, a server-response ratio, a four-hour window, and a destination ASN. The severity may be *Critical*, *High*, *Medium*, or *Low* depending on connection count and whether an IOC has matched on the destination.
- A **C2 Infrastructure Alert** on the *C2 Infrastructure Alert* sub-tab. The row is always *Critical* / 0.99 confidence. The IOC auto-escalation rule guarantees this. The *C2 Enrichment* sidebar section carries an indicator match. The match can be against an IP, a DNS query name, or an IP resolved from a DNS answer. `match_type` is `ip`, `dns`, or `ip_from_dns`.

The two trigger surfaces converge in this runbook because the investigation is the same. Both describe an internal host that talks to an external endpoint in a way that resembles active C2. A C2 Infrastructure Alert identifies the indicator but not always the cadence. A Beaconing Detection identifies the cadence but not always the infrastructure. A lead on either surface prompts the analyst to look for the other.

## [Prerequisites](/docs/mdndr/operating-guide/c2-beacon-investigation#prerequisites)

Before executing this runbook the analyst confirms the following.

- Steps 1 through 5 of [Critical Alert Triage](/docs/mdndr/operating-guide/critical-alert-triage) are complete. The affected asset, its owner and criticality tier, the sidebar evidence summary, and any repetition or same-flow correlation already live in the incident ticket.
- A Hunt session open on the originating *Beaconing Detection Alert* or *C2 Infrastructure Alert* tab, with the alert's detail sidebar visible.
- Access to the organization's asset inventory for the affected host.
- A working mental model of the organization's routine outbound traffic. Know which corporate Software-as-a-Service (SaaS) endpoints are in daily use. Know which vendor cloud services the endpoint detection and response (EDR) and patching agents contact. Know which office locations or remote sites use Virtual Private Network (VPN) concentrators whose traffic can resemble beacon patterns.
- Access to the incident-management system used by the SOC.

If any item is absent, stop. A beacon investigation without asset context or the Critical-triage baseline can cause errors. It can over-escalate legitimate software-update traffic. It can under-escalate genuine compromise. The prerequisites help prevent both failure modes.

## [Investigation steps](/docs/mdndr/operating-guide/c2-beacon-investigation#investigation-steps)

Each step is numbered. Each step adds a distinct piece of evidence. Each step feeds the decision tree at the end. Execute steps in order even when the verdict looks obvious early. Never record a C2 disposition on partial evidence.

### [1. Open the alert sidebar and capture the core evidence](/docs/mdndr/operating-guide/c2-beacon-investigation#1-open-the-alert-sidebar-and-capture-the-core-evidence)

On the Hunt page, the analyst clicks the alert row to open the detail sidebar. The section that matters depends on which trigger surface produced the alert.

- **C2 Infrastructure Alert.** The *C2 Enrichment* section lists one or more `c2.matches[]` entries. For each entry, record the match type (`dns`, `ip`, or `ip_from_dns`). Record the `value`, which is the indicator as it appears in the feed. Record the `matched` field, which is the exact value observed in the event. Record the `score` on the 0-10 threat scale. Record the `confidence` on the feed's 0-100 scale. Record the `source` feed identifier. Record the `description` that names the malware family or actor cluster. Record the `created` and `last_seen` timestamps. Port-specific indicators carry `matched_port` and `required_port`. If present, record both fields.
- **Beaconing Detection Alert.** The *Beaconing Detection* section lists `connection_count`, `unique_flows`, `avg_bytes_per_flow`, `avg_packets_per_flow`, and `cv_bytes`. cv_bytes is the coefficient of variation, which is standard deviation (STDDEV) divided by mean. The section also lists `server_response_ratio`, `window_start`, `window_end`, `first_seen`, and `last_seen`. It lists `malicious_iocs`, `iocs_checked`, `dest_country`, `dest_asn`, and `dest_org`.

Either way the base network section above these carries `src_ip`, `src_port`, `dest_ip`, `dest_port`, `proto`, `app_proto`, and the `community_id` correlator. The analyst captures the full base record so subsequent pivots have a reference point.

### [2. Examine the source and destination endpoints](/docs/mdndr/operating-guide/c2-beacon-investigation#2-examine-the-source-and-destination-endpoints)

The source IP is the affected internal host. The analyst identified and profiled it in step 2 of Critical alert triage. The destination is the prospective C2 endpoint. The analyst characterizes the destination along four axes before further pivots:

- **Address class.** An RFC-1918 destination is almost never C2 in an MVP-scope MetaDefender NDR deployment. The Beaconing pipeline excludes RFC-1918 destinations by construction. See [C2 Beacon Investigation](/docs/mdndr/operating-guide/c2-beacon-investigation). A C2 Infrastructure Alert against an RFC-1918 destination points at a recycled or private-space indicator. Record a note for the feed curators rather than an incident. External destinations pass to the next axes.
- **Port and protocol.** A beacon on Transmission Control Protocol (TCP) port 443 that negotiates TLS is the common shape. A beacon on TCP port 80 with plaintext Hypertext Transfer Protocol (HTTP) is less common and more suspicious. A beacon on an unusual port is highly suspicious if `app_proto` is `null` or `failed`. Examples are 8080, 8443, 4444, 1337, or a random high-numbered port. Beacon frameworks frequently hand-roll the transport. Remote-administration ports from a non-administrative host are anomalous on their own. Examples are SSH 22, RDP 3389, and Windows Management Instrumentation 5985 / 5986.
- **Name resolution lineage.** If the alert is a C2 DNS match (`match_type: dns`), the destination is a domain name. If it is `match_type: ip_from_dns`, the IP came from a DNS answer earlier in the same flow. Follow the *Show all events with this community id* pivot in step 4. Find the DNS query that produced the resolution. Record the fully-qualified name.
- **Known-good exceptions.** Legitimate corporate SaaS endpoints, EDR vendors, patching infrastructure, and telemetry collectors often resemble beacons. See *Common False-Positive Patterns*. If the destination falls into one of these categories by ASN or reverse DNS, record the identification and continue. The verdict is not final. The corroborating evidence required for escalation is now higher.

### [3. Evaluate the beacon timing and payload uniformity](/docs/mdndr/operating-guide/c2-beacon-investigation#3-evaluate-the-beacon-timing-and-payload-uniformity)

The beacon is a timing pattern. The sidebar exposes the numbers that make the pattern visible. Examine these fields from the *Beaconing Detection* section. If the alert is a C2 Infrastructure Alert with a beacon block on the same event, examine the equivalent fields.

- `connection_count`**.** The total number of connections the pipeline saw in the four-hour hopping window. Fifteen is the minimum threshold. Fifty-plus is *Critical* by construction. Recurrent connection counts in the thirties and forties across several windows are a strong beacon signal. This is true even when no single window reaches *Critical* on its own.
- `cv_bytes`**.** The byte coefficient of variation over the window. Coefficient of variation below 0.10 means payloads are nearly identical in size. This is the fingerprint of a small, templated beacon check-in. Values up to 0.25 are still consistent with beacons. Above 0.40, the uniformity argument weakens. The pattern is likely human-driven browsing or software with variable-length payloads.
- `avg_bytes_per_flow` **and** `avg_packets_per_flow`**.** Beacons are small. Average flow sizes in the 100-byte to 2-kilobyte range and average packet counts in single digits are characteristic. Flows averaging tens of kilobytes with high packet counts point at file transfer or interactive session rather than beacon check-in.
- **Inter-arrival interval.** The sidebar does not render the raw interval directly. Derive it with `(window_end - window_start) / connection_count`. This produces the average period. A period in the tens-of-seconds-to-minutes range with low variance is beacon-shaped. Intervals that cluster around exact multiples of a minute are the strongest timing signal. Examples are every sixty seconds, every five minutes, or every fifteen minutes. Only a timer-driven process produces that regularity.
- `server_response_ratio`**.** The pipeline defines this as `total_server_packets / (connection_count x 5)`. A ratio below 0.20 means the server sent fewer than five packets per connection on average. This matches the tasking-channel shape where the implant polls and receives a small acknowledgement or a short task.

A destination that scores on three or more of these fields behaves like a beacon. These fields are high and steady `connection_count`, low `cv_bytes`, low `avg_bytes_per_flow`, a rounded-period interval, and low `server_response_ratio`. This applies even if the IOC feed has not flagged the endpoint. Record the scoring explicitly in the ticket. Example: *"connection_count 47 over one hour with cv_bytes 0.08, average flow 312 bytes, period 76.6 seconds, server response ratio 0.11"*.

### [4. Pivot to the flow view filtered by the source-destination pair](/docs/mdndr/operating-guide/c2-beacon-investigation#4-pivot-to-the-flow-view-filtered-by-the-source-destination-pair)

From the alert sidebar, right-click `community_id`. Select *Show all events with this community id*. A new *All Events* tab opens on the [Hunt Page](/docs/mdndr/operating-guide/hunt-page). The tab filters results to every protocol transaction, flow record, file extraction, and enrichment that belongs to the same connection. This view reveals what the summary detection's windowed aggregate cannot:

- **The individual flow rows.** Each flow record carries `timestamp`, `bytes_toserver`, `bytes_toclient`, `pkts_toserver`, `pkts_toclient`, `flow.duration`, and the flow-end reason. The analyst scrolls through the list and looks for the regularity that generated the beacon alert. Look for rows at similar byte counts separated by similar intervals. Also look for outlier rows that carry disproportionately larger payloads. They can indicate the moment a tasking channel turned into data transfer.
- **TLS sessions on the same connection.** Every TLS handshake renders with the Server Name Indication (SNI), certificate subject and issuer, and JA3 / JA4 client fingerprint. Beacons often reuse a specific SNI across thousands of connections. They also produce an identical JA3 fingerprint every time. The fingerprint is the fastest confirmation of a known malware family.
- **HTTP sessions on the same connection.** Beacons that ride plaintext HTTP expose the full request. The request includes method, Uniform Resource Identifier, User-Agent, and response content-type. Uniform User-Agent strings with atypical versioning are characteristic. GET or POST requests to short numeric paths are characteristic. Response bodies of nearly-identical size across hundreds of requests are characteristic.
- **DNS resolutions that preceded the flow.** When the destination was reached by name, the DNS query and answer sit on the same `community_id`. The analyst reads the resolved name, the answer set, and the answer Time To Live (TTL). A very low TTL is a fast-flux indicator. See step 8.

If the connection is inspectable, such as plaintext HTTP or DNS, the session evidence usually resolves the ambiguity. If the connection uses encryption, such as TLS, the session evidence narrows the hypothesis but does not prove it. The next steps check the destination population to add independent evidence.

The analyst then opens a second tab with the right-click pivot *Hunt all events from this IP* on the **source IP**. The analyst widens the time range to *Last 7 days*. This tab shows every conversation the affected host has held with any external destination. A host beaconing to one destination is a compromise signal. If the host also makes clean outbound traffic to routine SaaS endpoints, compare the patterns. This helps the analyst decide whether the beacon is an anomaly or whether the entire host is degraded.

### [5. Check destination geography and network owner](/docs/mdndr/operating-guide/c2-beacon-investigation#5-check-destination-geography-and-network-owner)

The sidebar's network enrichment section carries the destination's country (`dest_country`), Autonomous System Number (`dest_asn`), and organization (`dest_org`). These three fields carry substantial triage signal on their own.

- **Unexpected geography.** A host in a corporate finance function that beacons to an unexpected country is a strong signal. High-signal geographies vary by organization. Most analysts maintain a mental list of low-expected-traffic regions for their environment.
- **Hosting ASN versus content ASN.** Destinations that resolve to bulletproof or low-reputation hosting providers add weight to the C2 hypothesis. These providers include regional hosting specialists that threat reports frequently name. Destinations that resolve to known cloud providers are ambiguous. Examples include Amazon Web Services, Microsoft Azure, Google Cloud, Cloudflare, Akamai, DigitalOcean, Linode, Oracle, Hetzner, and OVH. Threat actors rent cloud infrastructure heavily. Thus, the ASN rules neither in nor out.
- **Organization name reverse-lookup.** The `dest_org` field often identifies the operator. When the organization is a recognizable corporate SaaS provider (for example, Microsoft Corporation, Google LLC, Apple Inc., Cloudflare, Zscaler, or a known EDR vendor), the false-positive hypothesis rises. When the organization is a generic reseller or an unknown entity, the indicator-driven hypothesis holds.

Geography and ASN on their own almost never drive a disposition. They change the weight between the indicator hypothesis and the false-positive hypothesis. The analyst records the reading and moves on.

### [6. Check for IOC enrichment on the destination](/docs/mdndr/operating-guide/c2-beacon-investigation#6-check-for-ioc-enrichment-on-the-destination)

This is the single strongest disposition lever in the runbook. The alert sidebar carries the *C2 Enrichment* section whenever any feed match fired; the *InSights Enrichment* section carries parallel matches from the OPSWAT InSights Threat Intelligence Database (TIDB) and Reputation Database (REPDB) feeds.

- **Any** `c2.matches[]` **entry present.** The alert is IOC-Critical by construction. Severity is *Critical*. Alert-level confidence is *0.99*. The match payload identifies the threat actor or malware family for the indicator. This finding is sufficient for escalation to incident response. See *Decision Tree*.
- **Beaconing pipeline** `malicious_iocs > 0` **with** `iocs_checked > 0`**.** The behavioral pipeline's independent IOC check observed a feed hit on the destination during the window. The pipeline auto-escalates its own severity to *Critical* when this field is truthy. Confidence on the alert rises to 0.99 under the same auto-escalation rule.
- **Parallel InSights match on the destination IP or DNS name.** See [InSights TIDB and REPDB](/docs/mdndr/operating-guide/insights-tidb-and-rpedb) for the feed semantics. A TIDB hit (threat intelligence) is high-confidence; a REPDB hit (reputation) is lower-confidence but still material in aggregate.
- **No IOC match on any feed.** The alert is threshold-Critical or sub-Critical on behavioral evidence alone. Escalation now depends on evidence from multiple steps. These steps are timing evidence in step 3, session evidence in step 4, ASN reading in step 5, and blast-radius evidence in the next step.

A C2 Infrastructure Alert reaches this step with an IOC match by definition. The alert cannot fire without one. A Beaconing Detection Alert may or may not. The analyst records the IOC state explicitly in the ticket. Use *"IOC match present on dest_ip / dns query name / neither"*. This is the single field that changes downstream dispositions.

### [7. Check the destination across the rest of the network](/docs/mdndr/operating-guide/c2-beacon-investigation#7-check-the-destination-across-the-rest-of-the-network)

A beacon destination that only one internal host contacts is a host-scoped compromise. A beacon destination that many internal hosts contact is an environment-scoped event. It is either a coordinated compromise or a benign shared service. Blast radius is decisive evidence.

From the alert row, right-click the **destination IP**. For a DNS-match alert, use the destination domain. Select *Hunt all events from this IP*. Alternatively, run a quick search on the domain in a new *All Events* tab. Expand the time range to *Last 24 hours* or *Last 7 days* as appropriate. Read the result:

- **One source only.** The compromise is host-scoped. Escalation, isolation, and forensic recovery target the affected host.
- **A small handful of sources, all in the same business unit.** Check whether the hosts share a common software baseline. Examples include the same EDR agent, patching policy, or internal build image. If they do and the behavior matches a known vendor, the false-positive hypothesis rises. If they do not, the shared behavior is a coordinated-compromise signal. Redraw the blast radius to include the whole set.
- **Many sources across business units.** Two possibilities dominate. The destination can be a routine vendor endpoint that landed on a feed. This is a known false-positive pattern, usually resolved by the vendor identity in step 5. The destination can also serve a campaign-scale compromise that is already lateral. Do not decide on population size alone. The IOC state in step 6 and vendor identity in step 5 usually resolve the ambiguity.

### [8. Examine the domain name for DGA characteristics](/docs/mdndr/operating-guide/c2-beacon-investigation#8-examine-the-domain-name-for-dga-characteristics)

Use this step only when the destination was reached by name. That means a DNS query preceded the flow. The alert's `match_type` is `dns` or `ip_from_dns`. The *Show all events with this community id* pivot in step 4 can also surface a DNS record. For bare-IP flows with no resolved name, skip this step.

The analyst reads the queried name from the *DNS Session* section in the sidebar. The analyst can also read it from the DNS row in the pivoted *All Events* tab. Several characteristics raise suspicion of a Domain Generation Algorithm (DGA). A DGA manufactures hundreds or thousands of candidate domains per day. Thus, the operator can rotate through them:

- **Random-looking second-level label.** Names like `xz8kqt4p7vg2rx.example` or `qwertyuiopasdfghjk.example` consist of characters with high entropy and no pronounceable structure. Contrast against legitimate domains whose labels pronounce as words or abbreviations.
- **Consistent label length.** DGA families often produce labels of a fixed length; several queries to `aaaaaaaaaa.example`, `bbbbbbbbbb.example`, `cccccccccc.example` all with the same length strongly suggests a rotation.
- **Unusual top-level domain.** Country-code top-level domains and niche top-level domains -- `.xyz`, `.top`, `.click`, `.info`, `.cc`, `.ws`, `.su`, `.tk` -- are disproportionately represented in DGA tooling because they are inexpensive to register.
- **Short answer TTL.** Fast-flux infrastructure holds answer TTLs to a few seconds or tens of seconds so the resolved IP can rotate rapidly. A five-second TTL on a domain whose purpose is legitimately long-lived is anomalous.
- **High Non-Existent Domain (NXDOMAIN) ratio for the parent.** Pivot on the parent (second-level) domain. Filter the *DNS Session* tab for the last hour. This shows whether the parent serves many non-existent subdomains. That is a DGA fingerprint. The separate DGA Detection from [Behavioral detections](/docs/mdndr/operating-guide/behavioral-detections) will flag it on its own cadence.

A domain that meets several of these criteria is strong corroborating evidence for a C2 hypothesis. A domain that meets none is weak evidence for DGA. Examples include a short, pronounceable, branded name under a mainstream top-level domain. This does not rule out C2 on legitimate-looking fronting infrastructure. Threat actors purchase expired domains whose prior reputation was benign.

## [Decision tree](/docs/mdndr/operating-guide/c2-beacon-investigation#decision-tree)

The analyst records one of four outcomes. Each branch lists the minimum artifacts captured before the ticket is closed.

- **Escalate -- confirmed or probable C2.** Escalate if the alert is IOC-Critical and the blast radius is host-scoped or coordinated-compromise-scoped. IOC-Critical means any `c2.matches[]` entry or `malicious_iocs > 0`. Escalate if the alert is threshold-Critical on Beaconing evidence on a Tier 1 or Tier 2 asset. Beaconing evidence includes fifty-plus connections with `cv_bytes` under 0.10. Corroborating session evidence includes recognizable JA3, suspicious SNI, or uniform HTTP pattern. Escalate if two or more independent indicators converge. Examples include an IOC hit on destination, a suspicious DGA-shaped name, and a server-response ratio below 0.20. The analyst opens an incident response (IR) ticket. The analyst requests endpoint isolation for the affected host. The analyst hands the host off to forensic recovery. If policy allows indicator-based blocking, the analyst blocks the destination at the perimeter. The analyst transfers the evidence record and pivot tabs into the incident. The *Escalate* branch ends this runbook. Incident-response procedures take over.
- **Monitor -- suspicious but not conclusive.** Use this disposition when the evidence is partial. Examples include a Beaconing alert with moderate connection counts and no IOC hit. Another example is a C2 Infrastructure Alert on a destination that is a recognized cloud provider. A matching pattern on a Tier 3 asset with no corroborating signals is also an example. The analyst records the observation in the ticket. The analyst leaves the Hunt tabs open. The analyst schedules a follow-up review, typically within four to twelve hours for Critical severity and twenty-four hours for sub-Critical. If the pattern recurs within the review window, the analyst re-enters at step 1 with the accumulated context. If it does not recur and no new corroboration appears, the disposition moves to *close as benign*.
- **Close as benign -- identified legitimate explanation.** Use this disposition when the evidence positively identifies a recognized pattern. Examples include a confirmed corporate SaaS endpoint with a matching `dest_org` and matching client identity. Client identity can include User-Agent or JA3 fingerprint. Other examples include a known software-update client and red-team or vulnerability-scanning activity. The analyst records the specific fields that justify the conclusion in the ticket. Example: *"destination 52.84.0.0/15, Amazon Web Services CloudFront, JA3 fingerprint matches internal EDR agent, pattern consistent with telemetry check-in"*. Later readers can reopen the conclusion if one of those fields changes.
- **Tune the rule -- recurring benign pattern with a scoped policy fix.** Use this disposition when the same benign pattern has confirmation multiple times across the same population. The source of the noise is understood, such as a specific vendor's telemetry or a specific internal management workflow. The policy system supports a scoped exclusion. Tuning is a detection-engineering action, not a triage shortcut. The analyst opens a follow-up task against the detection's policy definition. The analyst does not tune inline. The analyst submits the change through the organization's peer-review workflow. The analyst keeps the alert live until the tuned policy deploys. The default disposition for a single confirmed-benign alert is *close*, not *tune*. A single occurrence does not justify reduced coverage.

Record every branch in the incident-management system. The runbook reference, disposition, asset context, indicator or timing evidence, and pivot tab references form the minimum record. If the disposition is *Escalate*, the record hands off directly into the incident.

## [Common false-positive patterns](/docs/mdndr/operating-guide/c2-beacon-investigation#common-false-positive-patterns)

A non-trivial share of Beaconing and C2 Infrastructure alerts have benign explanations. Recognizing the patterns saves investigation time and keeps analysts from over-escalating.

- **Software-update and telemetry beacons.** Operating-system update agents, browser update channels, EDR agents, antivirus update services, and vendor telemetry clients check in to well-known infrastructure on a fixed schedule. The shape -- regular interval, uniform payload, high connection count, low server-response ratio -- is indistinguishable from a C2 beacon without the destination context. The destination ASN and organization usually identify the vendor (Microsoft, Apple, Google, Cloudflare, Akamai, a specific EDR vendor). Disposition: *close* with the vendor identity recorded. If the same vendor produces sustained alert volume across many hosts, the SOC opens a tuning task against the Beaconing policy.
- **Push-notification services.** Mobile device management and push-notification infrastructure maintain persistent outbound connections with small, periodic keepalives. Examples include Apple Push Notification Service, Firebase Cloud Messaging, and corporate mobile-device management servers. These keepalives score on every Beaconing metric. The client identity is usually visible in the TLS SNI and JA3 fingerprint. Disposition: *close* when the client and destination are recognized.
- **VPN concentrators and remote-desktop gateways.** Always-on VPN clients and remote-desktop gateway keepalives produce long-duration, regularly-spaced traffic that resembles beaconing on flow metadata alone. The destination is usually the organization's own VPN endpoint or a known commercial VPN provider, and the `community_id` pivot surfaces the VPN handshake. Disposition: *close* once the VPN identity is confirmed.
- **Recycled indicators and indicator false positives.** Occasionally a domain or IP that was indicator-worthy at one point has been reclaimed by a benign tenant and the feed has not yet retired the entry. The destination's current reverse DNS, HTTP hostname, or TLS certificate subject identifies the new owner. Disposition: *close* and file a feed-review request upstream; local suppression is not the MetaDefender NDR pattern for this family (see [C2 and Threat Intelligence](/docs/mdndr/operating-guide/c2-and-threat-intelligence)).
- **Cloud-fronted services sharing IPs with known-bad tenants.** A Cloudflare, Akamai, or Amazon Web Services IP may carry legitimate traffic on one hostname and malicious traffic on another. A Beaconing alert on a shared IP with no SNI or hostname evidence is ambiguous; the session data from step 4 resolves the ambiguity by surfacing the actual requested name. Disposition: *close* when the name is benign and documented in the ticket; escalate when the name is missing or matches a suspicious pattern.
- **Red-team, penetration-testing, and attack-simulation activity.** Authorized internal testing produces Critical C2 alerts by design -- tools like Cobalt Strike, Sliver, and Mythic are the calibration targets for the C2 family. Disposition: *close* once the activity is confirmed with the red-team or vulnerability-management program. Every SOC maintains a communication channel with internal testing teams so these alerts are identifiable on sight.
- **Network-monitoring and synthetic-transaction agents.** Synthetic-monitoring probes, uptime-check services, and internal network-monitoring agents make many small, regularly-spaced outbound connections that score as beaconing. The destination and client identity usually identify the monitor. Disposition: *close* with the monitoring identity recorded.

Closing on a false-positive pattern still requires the runbook's evidence record. *"Looks like a software update"* is not a disposition; *"destination Microsoft Update, ASN 8075, User-Agent* `Windows-Update-Agent/10.0`*, JA3* `cd08e31494f9531f560d64c695473da9`*, closing as benign"* is.

## [See also](/docs/mdndr/operating-guide/c2-beacon-investigation#see-also)

- [Critical Alert Triage](/docs/mdndr/operating-guide/critical-alert-triage) -- the generic first-response runbook that hands off to this one.
- [Data Exfiltration Investigation](/docs/mdndr/operating-guide/data-exfiltration-investigation) -- follow-up runbook for any beacon investigation whose `community_id` pivot surfaced a Data Exfiltration alert on the same flow.
- [ML Anomaly Investigation](/docs/mdndr/operating-guide/ml-anomaly-investigation) -- follow-up runbook for any beacon investigation whose same-source correlation surfaced a Random Cut Forest anomaly.
- [Tunneling Investigation](/docs/mdndr/operating-guide/tunneling-investigation) -- follow-up runbook when the DNS evidence in step 8 suggests the beacon rides on a covert DNS channel rather than on a direct connection.
- [Alert, Flow, and PCAP Pivoting](/docs/mdndr/operating-guide/alert--flow--and-pcap-pivoting) -- the pivot-mechanics meta-runbook referenced by steps 4 and 7.
- [C2 Beacon Investigation](/docs/mdndr/operating-guide/c2-beacon-investigation) -- background on the C2 family, including match types, feed sources, and the IOC auto-escalation rule.
- [InSights TIDB and REPDB](/docs/mdndr/operating-guide/insights-tidb-and-rpedb) -- parallel intelligence feeds referenced in step 6.
- [Detection Overview](/docs/mdndr/operating-guide/detection-overview) -- unified severity scale, confidence scale, and the IOC auto-escalation rule.
- [Hunt Page](/docs/mdndr/operating-guide/hunt-page) -- tabs, sidebar, right-click pivots, and the *All Events* tab used throughout this runbook.
