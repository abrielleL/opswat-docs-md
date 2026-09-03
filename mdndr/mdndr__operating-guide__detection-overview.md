<!-- source: https://www.opswat.com/docs/mdndr/operating-guide/detection-overview -->

# Detection Overview

MetaDefender NDR generates alerts from six complementary detection engines. Each engine answers a different question about the network. The questions include signature matches, threat-intelligence matches, malicious file results, traffic patterns, and statistical anomalies. Every engine feeds one unified alert pipeline. The pipeline uses the same severity and confidence vocabulary. This chapter introduces the six families. It traces how a detection travels from the wire to the analyst. It also defines the severity and confidence scales that each later chapter uses.

This chapter is for Tier 1, 2, and 3 Security Operations Center (SOC) analysts, threat hunters, Managed Security Service Provider (MSSP) analysts, and SOC leads. It assumes a MetaDefender NDR deployment. It also assumes familiarity with the [Dashboard](/docs/mdndr/operating-guide/dashboard) and [Hunt Page](/docs/mdndr/operating-guide/hunt-page)

First-use acronym expansions in this chapter:

- SOC — Security Operations Center.
- MSSP — Managed Security Service Provider.
- C2 — command-and-control.
- IOC — Indicator of Compromise.
- TIDB — Threat Intelligence Database.
- REPDB — Reputation Database.
- IDS — Intrusion Detection System.
- AV — antivirus.
- SID — Signature Identifier.
- MITRE ATT&CK — Adversarial Tactics, Techniques, and Common Knowledge.
- DNS — Domain Name System.
- TLS — Transport Layer Security.
- SNI — Server Name Indication.
- JA3 / JA4 — TLS client fingerprint formats.
- DGA — Domain Generation Algorithm.
- NXDOMAIN — Non-Existent Domain DNS response.
- TTL — Time To Live.
- ML — machine learning.
- RCF — Random Cut Forest.
- MVP — Minimum Viable Product.

## [The detection landscape](/docs/mdndr/operating-guide/detection-overview#the-detection-landscape)

MetaDefender NDR ships six detection families. Each family uses a distinct evidence type. Each family runs on its own pipeline stage and produces its own alert shape. Every family converges on the same unified alert stream. The [Hunt Page](/docs/mdndr/operating-guide/hunt-page) and [Dashboard](/docs/mdndr/operating-guide/dashboard) show that stream.

- **Suricata signatures.** Deep-packet-inspection signatures from Proofpoint Emerging Threats Pro and other rulepacks shipped with the OPSWAT InSights rulepack. Classical intrusion-detection matches on packet content, protocol anomalies, and rule metadata. See [Suricata Signatures](/docs/mdndr/operating-guide/suricata-signatures).
- **Command-and-control (C2) threat intelligence.** Exact-match lookups of Internet Protocol (IP) addresses and Domain Name System (DNS) query names against the OPSWAT Eyelet C2 feed. Produces dedicated C2 IP and C2 DNS alerts. See [C2 and Threat Intelligence](/docs/mdndr/operating-guide/c2-and-threat-intelligence).
- **OPSWAT InSights threat intelligence (TIDB and REPDB).** Hash-lookup matches apply to IPs, hostnames, and domain hierarchies across DNS, TLS, and HTTP traffic. The matches use two curated feeds: the high-confidence Threat Intelligence Database (TIDB) and the broader-coverage Reputation Database (REPDB). See [InSights TIDB and REPDB](/docs/mdndr/operating-guide/insights-tidb-and-rpedb)
- **MetaDefender Core file scanning.** MetaDefender NDR submits extracted files to MetaDefender Cloud or an on-premises MetaDefender Core cluster for multi-antivirus (multi-AV) scanning. The pipeline raises three alert tiers on the basis of positive-engine count. See [MetaDefender Core File Scanning](/docs/mdndr/operating-guide/metadefender-core-file-scanning)
- **Behavioral analytics.** RisingWave streaming structured-query-language (SQL) detections produce eight behavioral alert types. These types are Beaconing, Data Exfiltration, Long Duration Flow, Port Scanning, Connection Spray, DNS Tunneling, Domain Generation Algorithm (DGA) activity, and Fast Flux hosting. See [Behavioral Detections](/docs/mdndr/operating-guide/behavioral-detections).
- **Machine-learning (ML) anomaly detection.** Random Cut Forest (RCF) unsupervised anomaly scoring applied per event type (DNS, HTTP, Flow) with configurable score thresholds. See [ML Anomaly Detections](/docs/mdndr/operating-guide/ml-anomaly-detections)

Suricata signatures run inside the sensor process. The C2, InSights, and MetaDefender Core families run as enrichment services fed from a shared raw-events Kafka topic. The behavioral family runs in a separate RisingWave streaming pipeline. It reads the aggregator's merged event stream. The ML family runs in the RCF pipeline on the same merged stream. All five post-sensor families converge on the alert engine, which applies the rules that translate each stream into a categorized alert.

## [How detections reach the analyst](/docs/mdndr/operating-guide/detection-overview#how-detections-reach-the-analyst)

A detection travels through a fixed pipeline before it becomes an alert on an operator screen. Understanding that pipeline makes the *where* and *when* of each detection family predictable.

1. **Sensor.** A MetaDefender NDR sensor observes traffic on a tapped interface. Suricata parses packets and emits session records. Session records include DNS, HTTP, TLS, SMB, RDP, SMTP, SSH, QUIC, FTP, and FileInfo. Suricata also emits flow records and signature alerts when a rule matches. The sensor publishes all output to the raw sensor-events stream on the Manager.
2. **Enrichment services.** Each enrichment service consumes the raw stream and adds its payload when relevant. C2 looks up IPs and DNS names against the Eyelet feed. InSights does the same against TIDB and REPDB. MetaDefender Core submits extracted files for multi-AV scanning. Per-IP metadata services add Autonomous System Number (ASN) and GeoIP data. Each service publishes enrichment output to an enriched stream. The stream names the event identifier and carries the enrichment status.
3. **Aggregator.** The aggregator waits until every expected enrichment reports for an event. It stitches the enrichments back onto the correct entities on the event. It emits a single merged event. If an enrichment never reports, the aggregator synthesizes a timeout status. The aggregator ships the merged event anyway, so an enrichment stall does not lose an event.
4. **Streaming analytics.** The RisingWave behavioral pipeline and the RCF ML pipeline consume the merged event in parallel. Each pipeline applies its own windowed SQL or anomaly-score logic. Each pipeline publishes findings to dedicated behavioral and ML alert streams.
5. **Alert engine.** A rules engine consumes the merged event stream and the behavioral and ML alert streams. It evaluates a small catalog of rules. The catalog has one rule per detection family and per-tier rules for MetaDefender Core. When a rule matches, the engine produces a typed alert with canonical severity, confidence, and payload. The engine stores the alert and publishes it to downstream consumers.
6. **User interface (UI) surfaces.** The alert reaches the analyst in three places. The [Dashboard](/docs/mdndr/operating-guide/dashboard) shows the Recent Alerts widget and Recent Severities donut. The [Hunt Page](/docs/mdndr/operating-guide/hunt-page) shows the *All Alerts* tab and per-type sub-tabs. For an alert with enrichment, the Hunt detail sidebar renders the enrichment payload inline next to the event.

End-to-end latency from sensor observation to the Hunt table is under ten seconds under normal conditions. Detections that require windowed aggregation add the window size as a delay. These detections include Beaconing, DGA, Fast Flux, Connection Spray, Port Scanning, and Long Duration Flow. A one-hour window detection cannot raise an alert faster than one hour after the first qualifying event.

## [Where each family appears in the UI](/docs/mdndr/operating-guide/detection-overview#where-each-family-appears-in-the-ui)

MetaDefender NDR presents detections consistently across surfaces. Analysts can pivot freely between orientation and investigation.

| Surface | What the operator sees per family |
| --- | --- |
| **Dashboard -- Recent Severities** | Every detection family contributes to the donut chart, classified by severity. |
| **Dashboard -- Recent Alerts** | Newest alerts from every family, most recent first. Clicking a row opens the same sidebar used on the Hunt page. |
| **Dashboard -- Top Signature Hits** | Suricata signature family only -- the top signature identifiers by alert count. |
| **Hunt page -- ** ***All Alerts*** **tab** | Mixed stream of every alert type with common columns (timestamp, protocol, source and destination endpoints, alert type, severity). |
| **Hunt page -- per-type sub-tabs** | One sub-tab per detection family: *Suricata Alert*, *C2 Infrastructure Alert*, *InSights Alert*, *MDCore Alert*, behavioral sub-tabs (one per alert type), and *ML Random Cut Forest Anomaly*. |
| **Hunt detail sidebar -- Suricata Alert section** | Rendered on any row that carries a Suricata signature match: signature, SID, category, MITRE technique. |
| **Hunt detail sidebar -- C2 Enrichment section** | Rendered on any row with a C2 feed match: match type, matched value, confidence, score, source feed -- one block per matched entity. |
| **Hunt detail sidebar -- InSights Enrichment section** | Rendered on any row with a TIDB or REPDB match: matched entity, feed tagging, and match metadata -- one block per matched entity. |
| **Hunt detail sidebar -- MDCore Enrichment section** | Rendered on any FileInfo row scanned by MetaDefender Core: scan result, threat name, positive-engine ratio, per-engine details, file metadata. |
| **Hunt detail sidebar -- Behavioral Alert sections** | One section per behavioral detection key (Beaconing, Data Exfiltration, Long Duration, DNS Tunneling, DGA, Fast Flux, Port Scan, Connection Spray, and the composite aggregates). Renders detection-specific metadata: connection counts, byte ratios, window bounds, destination country / ASN / organization. |
| **Hunt detail sidebar -- ML Anomaly fields** | For ML Random Cut Forest Anomaly rows, the standard network-base section plus any companion protocol sections. RCF-specific fields appear inline. A later release will add a dedicated sidebar section. |

Note on enrichment rendering: one record can fire several sidebar sections at once. A DNS session row that matched a TIDB entry renders the DNS section alongside the InSights Enrichment section. A FileInfo row with a MetaDefender Core hit renders the FileInfo section alongside the MDCore Enrichment section. This is intentional -- the sidebar is a composite view of every block the record carries.

## [The unified severity scale](/docs/mdndr/operating-guide/detection-overview#the-unified-severity-scale)

Every alert MetaDefender NDR produces carries a severity level drawn from the same four-level scale. The alert engine sets severity on the basis of the detection's trigger conditions.

Suricata signatures carry their own native severity on a 1-4 scale. The scale is 1 = Critical, 2 = High, 3 = Medium, 4 = Low. The alert engine maps this one-to-one onto the unified scale above. Analysts do not have to translate between them.

| Severity | Severity | Meaning | Typical Trigger |
| --- | --- | --- | --- |
| **Critical** | Confirmed threat or extreme anomaly. | An IOC match on the entity, or a threshold that indicates active compromise (for example, 50+ connections in a beaconing window, 6+ positive antivirus engines, a signature marked Critical). | Confirmed threat or extreme anomaly. |
| **High** | Strong indicator of malicious activity. | Exceeds a major threshold (for example, 30+ connections in a beaconing window, 3-5 positive antivirus engines, a REPDB match that also carries a TIDB hit). | Strong indicator of malicious activity. |
| **Medium** | Moderate anomaly; warrants investigation. | Exceeds a moderate threshold (for example, 20+ connections in a beaconing window, a REPDB-only match, an aggregate behavioral finding). | Moderate anomaly; warrants investigation. |
| **Low** | Mild anomaly; informational. | Meets the minimum threshold for the detection (for example, 15 connections in a beaconing window, 1-2 positive antivirus engines -- likely false positive territory). | Mild anomaly; informational. |

## [The confidence scale](/docs/mdndr/operating-guide/detection-overview#the-confidence-scale)

Every alert also carries a confidence score expressed as a floating-point number. Confidence ranges from **0.40** to **0.99**, with the bands defined as follows.

Analysts use confidence to order work within a severity tier. Among ten *Medium* alerts, analysts triage the one at 0.78 confidence before the one at 0.42.

| Range | Meaning |
| --- | --- |
| **0.95-0.99** | Very high -- IOC match or extreme values. Effectively a "this is really bad" marker. |
| **0.80-0.94** | High -- strong behavioral signal with corroborating evidence. |
| **0.60-0.79** | Moderate -- behavioral anomaly is present but warrants context. |
| **0.40-0.59** | Low -- meets the detection threshold but may be benign. |

## [IOC auto-escalation rule](/docs/mdndr/operating-guide/detection-overview#ioc-auto-escalation-rule)

When a detection carries an IOC match, the unified pipeline applies one hard override. IOC matches include any matched entity from the C2 feed or the InSights TIDB or REPDB feeds. **The pipeline escalates the alert to severity Critical and confidence 0.99 regardless of the detection family's normal thresholds.**

This rule applies to every family that can carry an IOC reference. A Beaconing detection with 16 connections (normally *Low* severity) that hits a destination on the C2 IP feed is raised as *Critical* at 0.99 confidence. A Long Duration Flow of 3,700 seconds (normally *Medium*) to a REPDB-listed domain is raised as *Critical* at 0.99. The rule is intentional and not tunable: once a detection crosses with a known-bad indicator, the signal is too strong to demote.

Analysts interpreting Critical alerts therefore distinguish between *threshold-Critical* (the behavioral or file-scan evidence alone was strong enough to reach Critical) and *IOC-Critical* (the evidence tripped the auto-escalation). The alert sidebar enrichment sections make the distinction visible. An IOC-Critical alert shows the matched entity and source feed in the C2 or InSights Enrichment section. A threshold-Critical alert carries only the family-native metadata.

## [Detection family quick reference](/docs/mdndr/operating-guide/detection-overview#detection-family-quick-reference)

The table below summarizes the six families at a glance.

| Family | Engine | Primary Trigger | Severity range | Hunt sub-tab |
| --- | --- | --- | --- | --- |
| **Suricata signatures** | Suricata IDS engine in the sensor | A shipped rule matches packet content, protocol metadata, or flow characteristics (rule fires at signature severity 1-4). | Critical / High / Medium / Low (native 1-to-1 mapping) | Signature Alert |
| **C2 threat intelligence** | `c2` enrichment in the Manager pipeline | Exact-match IP or DNS name hit against the Eyelet C2 feed. | Critical (IOC auto-escalation always applies) | *C2 Infrastructure Alert* |
| **InSights TIDB and REPDB** | `insights` enrichment in the Manager pipeline | Hash match against the TIDB (high-confidence) or REPDB (reputation) feeds on any IP, hostname, or domain hierarchy in the event. | Critical (IOC) -- High on TIDB-only -- Medium on REPDB-only | *InSights Alert* |
| **MetaDefender Core file scanning** | `mdcore` enrichment submitting to MetaDefender Cloud or Core | Extracted file returns a multi-AV scan result with >=1 positive engine. | Critical (IOC) -- High (6+ engines) -- Medium (3-5) -- Low (1-2) | *MD Core Alert* |
| **Behavioral analytics** | RisingWave streaming SQL over merged events | Windowed aggregate crosses a detection-specific threshold (for example, 15+ connections in a 4-hour beaconing window; 2:1 upload ratio on a 15-minute exfiltration window). | Critical / High / Medium / Low per detection (IOC auto-escalation applies to all) | One sub-tab per behavioral alert type (Beaconing, Data Exfiltration, Long Duration Flow, DNS Tunneling, DGA, Fast Flux, Port Scan, Connection Spray, and the composite aggregates)**.** |
| **ML anomaly (RCF)** | RCF anomaly scoring per event type | Event's anomaly score crosses the per-event-type threshold (DNS: 3.0 -- HTTP: 8.0 -- Flow: 20.0). | Medium (pass-through; family does not set native severity on MVP) | *ML Random Cut Forest Anomaly* |

The rest of this chapter group covers each family in full. Each chapter uses the same template: what it is, what it detects, how it works, trigger conditions, severity classification, confidence scoring, UI surfaces, a representative alert payload, tuning considerations, and a cross-link to the matching [Investigation Runbooks](/docs/mdndr/operating-guide/investigation-runbooks) entry.
