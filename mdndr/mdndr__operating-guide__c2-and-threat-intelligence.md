<!-- source: https://www.opswat.com/docs/mdndr/operating-guide/c2-and-threat-intelligence -->

# C2 and Threat Intelligence

Command-and-control detection is the early-warning layer in MetaDefender NDR. Suricata signatures match *how* a conversation looks on the wire. The C2 family matches *who* the conversation is with. The service checks every observed destination IP and every DNS query name against a curated feed of known threat-actor infrastructure. A match is rarely ambiguous. An internal host that resolves or contacts an entry on the C2 feed is almost always compromised. Thus, the pipeline raises these detections at the top of the severity scale. It carries the IOC evidence inline with the alert so analysts can act without a pivot.

First-use acronym expansions in this chapter:

- C2 — command-and-control.
- IOC — Indicator of Compromise.
- IP — Internet Protocol.
- DNS — Domain Name System.
- FQDN — Fully Qualified Domain Name.
- TLS — Transport Layer Security.
- SNI — Server Name Indication.
- JA3 / JA4 — TLS client fingerprint formats.
- ASN — Autonomous System Number.
- FRD — Functional Requirements Document.

## [What it is](/docs/mdndr/operating-guide/c2-and-threat-intelligence#what-it-is)

The C2 detection family is an enrichment service in the MetaDefender NDR Manager pipeline. It maintains two in-memory indicator lists: malicious IP addresses and malicious DNS names. It loads the lists from the OPSWAT Eyelet threat intelligence feed. It refreshes the lists each hour. Every DNS record and flow record that the sensors emit passes through the service. A match against the loaded lists produces an entity-level enrichment. The aggregator stitches the enrichment back onto the originating event. The alert engine promotes the enriched event to a dedicated C2 alert. The enrichment data stays attached to the event for the life of the record. Thus, the match remains visible on the Hunt page after analysts triage the alert.

## [What it detects](/docs/mdndr/operating-guide/c2-and-threat-intelligence#what-it-detects)

The family covers three complementary observables that together characterize early-stage compromise:

- **Outbound connections to known-bad IP addresses.** An internal host's flow record lists a destination IP that appears on the C2 IP feed. Examples include an active Cobalt Strike team server, a remote administration trojan panel, a known phishing landing page, or a staging host for a named intrusion campaign.
- **DNS resolution of known-bad domains.** An internal host's DNS query resolves a name that appears on the C2 domain feed. DNS catches intent before a connection opens; the query itself is evidence that a compromised host or user-initiated process is attempting to reach threat-actor infrastructure.
- **Resolved-IP reachback.** A DNS response's A-record answer contains an IP on the C2 IP feed. This catches the case where the queried name is unknown but resolves to known-bad infrastructure.

The shipped indicator categories include malware C2 frameworks, named campaign infrastructure, commodity trojan panels, and phishing-kit landing pages. Malware C2 frameworks include Cobalt Strike, Sliver, Mythic, Metasploit Meterpreter, and Havoc. Named campaign infrastructure includes nation-state clusters such as REF7707, Mustang Panda, APT28, and others tracked by the OPSWAT Analyst Network. Every indicator carries its own threat description, confidence rating, and first-seen / last-seen timestamps sourced from Eyelet.

This family intentionally does **not** cover TLS certificate hash, subject-name, and issuer matches. It also does not cover JA3 / JA4 TLS client-fingerprint matches. The Suricata engine handles both through published rules in the OPSWAT InSights rulepack. Thus, they appear as Suricata signatures. [Suricata Signatures](/docs/mdndr/operating-guide/suricata-signatures) documents them.

## [How it works](/docs/mdndr/operating-guide/c2-and-threat-intelligence#how-it-works)

The pipeline moves a candidate observation through four stages:

1. **Indicator load.** At startup, the C2 enrichment service loads the current IP and DNS indicator lists from disk. A background updater refreshes the lists hourly from the latest Eyelet feed. The service does not require redeployment to adopt a new indicator. The service holds indicators in memory as hash-table lookups. Thus, match time is constant regardless of list size.
2. **Event consumption.** The service consumes every DNS event and every flow event from the raw sensor stream. The service skips other event types, such as HTTP, TLS, and SMB, at this stage. DNS covers the resolution surface. Flow covers the connection surface. Together, they are sufficient to detect both detection modes listed above.
3. **Exact-match lookup.** For DNS events, the service lowercases every `dns.queries[].rrname` and every A-record answer. It looks them up against the in-memory indicator sets. For flow events, it looks up the destination IP. The DNS lookup is **exact-match only**. An indicator for `evil.example.com` does not match a query for `sub.evil.example.com`. Parent-domain hierarchy matching is the job of the InSights enrichment family. [InSights TIDB and REPDB](/docs/mdndr/operating-guide/insights-tidb-and-rpedb) covers that family. Port-specific IP indicators, such as `IP:PORT`, match only when both IP and port match. Port-agnostic indicators match any port.
4. **Entity enrichment and alert promotion.** When a lookup hits, the service attaches a per-entity enrichment block to the matched field. Examples include `dest_ip_enrichments.c2` on a flow and `dns.queries[].rrname_enrichments.c2` on a DNS query. Another example is `dns.grouped.A_enrichments.c2` on a DNS answer. The enrichment carries the match type and indicator details. Indicator details include value, source feed, score, confidence, description, first-seen, and last-seen. The enrichment also carries a `has_c2_match: true` flag. The aggregator stitches the enrichment back onto the event. The alert engine's C2 rule fires on any enriched event. The alert engine emits a C2 alert at Critical severity and 0.99 confidence.

The Breach Detection FRD describes two match kinds: a *C2 IP Alert* for IP-layer hits and a *C2 DNS Alert* for DNS-layer hits. The `match_type` field on the alert's `c2.matches[]` payload distinguishes them. Values are `"ip"` or `"ip_from_dns"` versus `"dns"`. The Hunt page surfaces both under the *C2 Infrastructure Alert* sub-tab. Both render the same *C2 Enrichment* sidebar section.

## [Trigger conditions](/docs/mdndr/operating-guide/c2-and-threat-intelligence#trigger-conditions)

A C2 alert fires when the enrichment service produces a match and the alert engine's C2 rule sees a truthy `has_c2_match` on any entity in the merged event. The fields below are what analysts read when triaging the alert.

| Field | Meaning |
| --- | --- |
| `c2.matches[]` | List of indicator matches attached to the alert. Typical count is one; multiple entries occur when the same event carries several matched entities (for example, a DNS answer with two A records, both on the feed). |
| `c2.matches[].type` | Match kind: `"dns"` (DNS query name hit), `"ip"` (flow destination IP hit), or `"ip_from_dns"` (IP in a DNS A-record answer hit). |
| `c2.matches[].value` | The indicator value from the feed — the canonical IP or FQDN as it appears in the Eyelet list. |
| `c2.matches[].matched` | The exact value that matched in the event. It is usually identical to `value`. MetaDefender NDR preserves it separately because case-folding and trailing-dot normalization can apply. |
| `c2.matches[].score` | Threat score from the feed on a 0–10 scale (10 is most severe). |
| `c2.matches[].confidence` | Feed-native confidence on a 0–100 scale. Note: this is the *indicator-level* confidence published by Eyelet; the *alert-level* confidence is always 0.99 under IOC auto-escalation. |
| `c2.matches[].source` | Feed-source identifier (for example, `labs-c2` for indicators curated by the OPSWAT Analyst Network). |
| `c2.matches[].description` | Human-readable description of the indicator — commonly names the malware family, actor cluster, and external reference article. |
| `c2.matches[].created`, `last_seen` | First and last observation timestamps from the feed — useful context on whether the indicator is fresh or historical. |
| `c2.matches[].matched_port`, `required_port` | Populated only for port-specific IP indicators; the port that matched and the port the indicator required. |

The alert also carries every standard Suricata-shaped field. These fields include `timestamp`, `flow_id`, `src_ip`, `src_port`, `dest_ip`, `dest_port`, `proto`, `alert.signature`, `alert.signature_id`, `alert.severity`, `alert.category`, and MITRE ATT&CK metadata where applicable. Analysts can pivot into protocol logs and packet capture as they would on a signature-based alert.

## [Severity classification](/docs/mdndr/operating-guide/c2-and-threat-intelligence#severity-classification)

C2 alerts are always raised at Critical severity. This behavior defines the family. The pipeline treats a match against the curated Eyelet feed as a confirmed-threat signal, not a candidate for further triage.

| Trigger | Unified Severity |
| --- | --- |
| Any `c2.matches[]` entry present on the alert (`match_type` of `dns`, `ip`, or `ip_from_dns`). | **Critical** |
|  |  |

The IOC auto-escalation rule described in [Detection Overview](/docs/mdndr/operating-guide/detection-overview) drives this behavior. A C2 feed hit satisfies the auto-escalation trigger by definition. Thus, the pipeline pulls every C2 alert to Critical regardless of the upstream event's severity. A flow record that was previously benign (for example, a low-volume 443-only HTTPS flow) becomes a Critical alert the moment its destination IP matches the feed.

## [Confidence scoring](/docs/mdndr/operating-guide/c2-and-threat-intelligence#confidence-scoring)

C2 alerts are always raised at 0.99 confidence. The confidence scale defined in Detection overview reserves the 0.95–0.99 band for IOC matches and extreme values. Every C2 alert lands in this band by construction.

| Trigger | Alert confidence |
| --- | --- |
| Any C2 feed hit. | **0.99** |

Analysts should not confuse the alert's 0.99 confidence with the `c2.matches[].confidence` feed value. The feed value describes the vendor's confidence in the *indicator*; the alert value describes the pipeline's confidence in the *detection*. An indicator with feed confidence 70 still produces a 0.99 alert — the match is binary and the pipeline treats every hit with the same gravity.

## [Where it appears](/docs/mdndr/operating-guide/c2-and-threat-intelligence#where-it-appears)

C2 alerts appear in four places.

- **Dashboard — Recent Severities donut.** Every C2 alert contributes a Critical slice to the donut. The Top Signature Hits widget is Suricata-only and does not include C2 alerts.
- **Dashboard — Recent Alerts.** Newest C2 alerts flow through the cross-family feed. Clicking a row opens the same sidebar used on the Hunt page.
- **Hunt page —** ***C2 Infrastructure Alert*** **sub-tab.** Under the *All Alerts* bucket, this per-type sub-tab lists every C2 alert with columns for `timestamp`, `alert.signature`, source and destination endpoints, `event_type`, `c2.match_type`, `c2.matched`, `c2.confidence`, `c2.score`, and `c2.source`. This sub-tab lists both the C2 IP match and the C2 DNS match kinds. Analysts filter by the `c2.match_type` column to narrow to one kind.
- **Hunt detail sidebar —** ***C2 Enrichment*** **section.** This section renders on *any* row whose record carries a `*_enrichments.c2` block — not just the C2 alert rows. A DNS session row that matched the C2 feed shows the DNS section alongside the C2 Enrichment section. The row itself is a session event rather than a C2 alert. A flow row with a destination-IP hit does the same. The section lists each match with the full indicator payload inline. When the matched entity is also geolocated, the sidebar's ASN and GeoIP enrichment renders alongside it. Analysts see the destination's country, ASN, and organization without leaving the record.

On the Hunt page's Sessions tab, the `c2` column injects a small enrichment ribbon. The ribbon appears on every DNS, HTTP, TLS, Flow, and protocol-log row that carries a match. Analysts do not have to open a record to see that it is C2-adjacent.

## [Alert payload example](/docs/mdndr/operating-guide/c2-and-threat-intelligence#alert-payload-example)

Abbreviated JSON for a C2 DNS match. The underlying event is a standard Suricata DNS query; the alert adds the `c2` payload and the `alert` block, and the alert engine sets `alert_type: "c2"` and severity `1`.

JsonCopy{
"timestamp": "2025-11-15T08:42:17.334821+0000",
"flow_id": 1847291847291847,
"event_type": "alert",
"alert_type": "c2",
"src_ip": "192.168.10.157",
"src_port": 51023,
"dest_ip": "10.0.0.53",
"dest_port": 53,
"proto": "UDP",
"app_proto": "dns",
"community_id": "1:8K3vN7pL5mQ2rT9uV1wX3yZ5",
"alert": {
"action": "allowed",
"gid": 1,
"signature_id": 1000001,
"rev": 1,
"signature": "MetaDefender NDR C2 DNS Match — update.hobiter.com",
"category": "A Network Trojan was Detected",
"severity": 1
},
"dns": {
"type": "query",
"queries": [
{"rrname": "update.hobiter.com", "rrtype": "A"}
]
},
"c2": {
"matches": [{
"type": "dns",
"value": "update.hobiter.com",
"matched": "update.hobiter.com",
"score": 10,
"confidence": 90,
"source": "labs-c2",
"description": "REF7707 infrastructure — espionage cluster suspected to be related to a Chinese state-sponsored threat actor group. Reported infrastructure includes malware staging, C2, and data exfiltration endpoints used by multiple backdoor trojans.",
"created": "2025-04-08T00:41:07Z",
"last_seen": "2025-10-17T14:51:02Z"
}]
},
"rule_name": "C2InfrastructureDetection",
"rule_salience": 10,
"triggered_at": "2025-11-15T08:42:17.498112Z"
}

A C2 IP match looks the same with two differences. A `flow` block with five-tuple counters replaces the `dns` block. The `c2.matches[].type` field is `"ip"`. It is `"ip_from_dns"` when the destination came from a DNS A-record answer rather than from the flow itself. A single alert can carry multiple `c2.matches[]` entries — for example, a DNS response whose answer set contains two A records that both appear on the feed.

## [Tuning considerations](/docs/mdndr/operating-guide/c2-and-threat-intelligence#tuning-considerations)

The C2 family is deliberately low-knob. OPSWAT curates the indicator lists upstream. Trust in the feed is part of the family's design. Operators do not suppress individual indicators the way they suppress noisy Suricata signatures. The Policy-managed knobs that exist apply to the service and to the feed:

- **Enable or disable the C2 enrichment service.** Operators toggle the enrichment on or off through Policy. Disabling the service leaves the pipeline running — no crash, no dropped events — and suppresses all downstream C2 alerts. See [Updates Management](/docs/mdndr/operating-guide/updates-management) for the per-policy enrichment toggle.
- **Feed update cadence.** The default update interval is one hour. Operators on constrained networks may lengthen it; teams running high-sensitivity environments may shorten it. The feed-update workflow, the manual-trigger procedure, and the distribution-status dashboard all live in Updates management.
- **Port-specific indicators.** A small number of IP indicators carry a `:PORT` qualifier. These match only when both IP and port match, so lateral port rotation by an attacker can evade them. Operators who want coarser matching should treat port-specific indicators as strict and complement them with additional behavioral coverage (Long Duration Flow, Beaconing — see [Behavioral Detections](/docs/mdndr/operating-guide/behavioral-detections)).

False-positive behavior is rare. It usually traces to recycled infrastructure, such as an IP or a domain that was indicator-worthy and later returned to a benign tenant. When an analyst confirms a false positive, flag the indicator for upstream review. Local suppression is not the MetaDefender NDR pattern for this family.

## [Related runbook](/docs/mdndr/operating-guide/c2-and-threat-intelligence#related-runbook)

Every Critical-severity C2 alert starts with [Critical Alert Triage](/docs/mdndr/operating-guide/critical-alert-triage). Follow-on investigation for C2 DNS and C2 IP matches uses [C2 Beacon Investigation](/docs/mdndr/operating-guide/c2-beacon-investigation). The runbook identifies the originating host. It correlates the C2 match with surrounding beaconing or long-duration-flow evidence from [Behavioral Detections](/docs/mdndr/operating-guide/behavioral-detections). It pivots to the full flow and packet capture via [Alert, Flow, and PCAP Pivoting](/docs/mdndr/operating-guide/alert--flow--and-pcap-pivoting). It confirms whether any payload transferred before containment.
