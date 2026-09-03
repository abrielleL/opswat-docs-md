<!-- source: https://www.opswat.com/docs/mdndr/operating-guide/suricata-signatures -->

# Suricata Signatures

Suricata signatures are the classical intrusion-detection backbone of MetaDefender NDR. Every sensor runs the Suricata engine against live packet capture. Every signature that fires becomes an alert in the unified detection pipeline. This chapter covers the engine role, the rulepacks shipped with the product, and the native severity model. It also explains how a Suricata alert reaches the analyst.

First-use acronym expansions in this chapter:

- IDS — Intrusion Detection System.
- IPS — Intrusion Prevention System.
- SID — Signature Identifier.
- GID — Generator Identifier.
- ET Pro — Proofpoint Emerging Threats Pro.
- JA3 / JA4 — Transport Layer Security client fingerprint formats.
- SNI — Server Name Indication.
- MITRE ATT&CK — Adversarial Tactics, Techniques, and Common Knowledge.
- DNS — Domain Name System.
- TLS — Transport Layer Security.
- HTTP — Hypertext Transfer Protocol.
- IOC — Indicator of Compromise.
- EVE — Extensible Event Format, Suricata's structured JSON output.

## [What it is](/docs/mdndr/operating-guide/suricata-signatures#what-it-is)

Suricata is an open-source network intrusion-detection engine. It inspects live packet capture against a compiled ruleset of signatures. Each signature is a deterministic, human-readable rule. The rule matches packet contents, protocol metadata, or flow characteristics. When a signature matches, Suricata emits an `alert` record into its EVE JSON stream. MetaDefender NDR runs Suricata inside every sensor. It forwards the EVE stream to the Manager. It converts each Suricata `alert` event into a typed alert. The alert carries the signature text, identifier, network five-tuple, protocol context, and full rule metadata.

## [What it detects](/docs/mdndr/operating-guide/suricata-signatures#what-it-detects)

The shipped ruleset covers the full breadth of published threat activity. It recognizes this activity from packet content and protocol metadata, including:

- Malware command-and-control (C2) beacons, loader downloads, and infection-chain callbacks.
- Exploit attempts against known Common Vulnerabilities and Exposures (CVE) identifiers in HTTP, Remote Desktop Protocol (RDP), Server Message Block (SMB), and other parseable protocols.
- Reconnaissance activity -- port sweeps, banner grabs, directory brute-force.
- Lateral-movement patterns -- SMB relay, PsExec, Windows Management Instrumentation (WMI), pass-the-hash artefacts.
- Exfiltration over HTTP, File Transfer Protocol (FTP), and DNS.
- Phishing delivery -- malicious attachments observed mid-transit, known landing-page URLs.
- Policy violations -- cleartext credential submission, unencrypted protocols on external destinations.
- Suricata-native protocol anomalies -- malformed packets, decode failures, unexpected protocol transitions.

## [How it works](/docs/mdndr/operating-guide/suricata-signatures#how-it-works)

The Suricata engine runs on the sensor, in-line with tapped traffic. It executes three stages in sequence: packet decode (link-layer through transport-layer), protocol parsing (application-layer transactions such as HTTP, DNS, TLS, SMB), and rule matching. Rule matching is driven by a compiled ruleset that MetaDefender NDR assembles from two sources:

1. **The OPSWAT InSights rulepack.** The product ships this rulepack and refreshes it through the feed-update service. It bundles curated Proofpoint ET Pro signatures. It also bundles in-house rules from the OPSWAT local-rules file. Local rules use a structured `metadata` block. Required keys include `signature_severity`, `mitre_tactic_id`, `mitre_technique_id`, `malware_family`, `deployment`, and related tagging. Analysts see those tags on the Hunt page sidebar alongside the signature.
2. **Customer-managed overrides.** Operators can enable, disable, or suppress individual signatures through Policy. MetaDefender NDR applies overrides on top of the shipped rulepack without modifying it. Thus, updates continue to flow into the policy cleanly.

When a rule matches, Suricata writes an `alert` event to the EVE JSON stream. The sensor adapter forwards the event onto the Manager's raw-events stream. The aggregator stitches in any available enrichments. The alert engine emits one incident per Suricata alert through an always-on rule. The rule fires on every event whose `event_type` is `alert`. The incident preserves the upstream Suricata severity; no severity remapping occurs at the alert engine. The result is one analyst-visible alert per signature fire. The alert carries the signature's native severity, identifier, rule-metadata block, and packet context. It also carries any companion protocol record from the same session, such as a DNS query, HTTP transaction, TLS handshake, or file hash.

## [Trigger conditions](/docs/mdndr/operating-guide/suricata-signatures#trigger-conditions)

A Suricata alert fires when the engine's rule match succeeds against an observed packet or stream. The fields below are the ones analysts most often use to understand *why* an alert fired.

| Field | Meaning |
| --- | --- |
| `alert.signature` | Human-readable signature name (for example, *ET PRO MALWARE Win32/Emotet Downloader Activity*). |
| `alert.signature_id` | Numeric Signature Identifier (SID). Proofpoint ET Pro SIDs live in the 2,000,000-3,999,999 range. OPSWAT-managed local rules use SIDs in the 1,000,000-1,999,999 range. OPSWAT bands local rules by category, such as malware, exploit, reconnaissance, C2 framework, and exfiltration. |
| `alert.gid` | Generator Identifier. Value 1 denotes the default rule engine. |
| `alert.rev` | Rule revision number. Increments whenever the vendor or OPSWAT updates an existing rule. |
| `alert.category` | Suricata classtype -- a coarse grouping such as *A Network Trojan was Detected*, *Attempted Administrator Privilege Gain*, or *Policy Violation*.alert.category |
| `alert.action` | The action Suricata took. MetaDefender NDR sensors run in detection mode, so this is typically `allowed`; a `blocked` value indicates IPS mode.alert.action |
| `alert.severity` | Suricata-native severity on the 1-4 scale (see below). Drives the alert engine's final severity. |
| `alert.metadata.signature_severity` | The rule author's textual severity tag (`Critical`, `High`, `Medium`, `Low`). Usually matches the numeric severity but surfaced separately for readability. |
| `alert.metadata.mitre_tactic_id`, `mitre_technique_id` | MITRE ATT&CK mapping. Feeds the Dashboard's ATT&CK heatmap. |
| `alert.metadata.malware_family` | Attributed malware family (when known). |
| `alert.metadata.affected_product`, `attack_target`, `deployment` | Targeting and placement hints. |
| `payload` / `payload_printable` | Base64 and printable rendering of the packet bytes that triggered the match. Available when the rule requests packet capture. |
| `community_id` | Stable session fingerprint used for pivoting across sensors and storage backends. |

## [Severity classification](/docs/mdndr/operating-guide/suricata-signatures#severity-classification)

Suricata signatures carry a native severity on a 1-4 scale. MetaDefender NDR preserves that severity through the alert engine and maps it directly onto the unified scale used everywhere else in the product.

| Suricata alert.severity | Label | Unified Severity | Meaning |
| --- | --- | --- | --- |
| **1** | Critical | **Critical** | Confirmed attack signature -- rule author expects a true positive. |
| **2** | High | **High** | Likely malicious activity -- strong indicator but context-dependent. |
| **3** | Medium | **Medium** | Potentially unwanted activity -- triage before closing. |
| **4** | Low | **Low** | Informational or policy violation -- noise tuning may apply. |

Lower numeric value means higher severity. This convention predates MetaDefender NDR and remains visible in the raw EVE payload. The user interface displays the word label, so analysts do not have to translate.

**IOC auto-escalation applies.** If the alert carries a matched entity from the C2, TIDB, or REPDB feeds, the enrichment pipeline stitched it on before the alert fired. The pipeline escalates the alert to **Critical** severity and **0.99** confidence regardless of the signature's native severity. A *Low*-severity policy-violation signature that hit a known C2 destination becomes a Critical alert.

## [Confidence scoring](/docs/mdndr/operating-guide/suricata-signatures#confidence-scoring)

Suricata signatures do not produce a per-alert confidence score in the EVE payload. MetaDefender NDR derives confidence from the rule author's tagging and the presence or absence of an IOC enrichment.

| Condition | Confidence |
| --- | --- |
| Signature fired with an accompanying IOC match on the C2, TIDB, or REPDB feed. | **0.99** (IOC auto-escalation; alert also promoted to Critical). |
| Rule metadata carries `confidence: High` or `signature_severity: Critical`. | **0.90** |
| Rule metadata carries `confidence: Medium` or `signature_severity: High`. | **0.75** |
| Rule metadata carries `confidence: Low` or `signature_severity: Medium`. | **0.60** |
| No confidence tag and `signature_severity: Low` (or absent). | **0.50** |

The OPSWAT-managed local-rule file requires the `confidence` metadata key on every rule. Shipped Proofpoint ET Pro rules carry `signature_severity` but not always `confidence`. Thus, the derivation falls back to the severity tag when confidence is missing.

## [Where it appears](/docs/mdndr/operating-guide/suricata-signatures#where-it-appears)

Suricata alerts appear on three surfaces.

- **Dashboard.** The *Recent Severities* donut includes every Suricata alert as one contribution per fire, classified by the unified severity label. *Recent Alerts* shows each newest Suricata alert in the cross-family feed; clicking a row opens the same sidebar used on the Hunt page. *Top Signature Hits* -- unique to this detection family -- is a bar chart of the top signature names by alert count over the selected interval.
- **Hunt page -- ** ***Suricata Alert*** **sub-tab.** Under the *All Alerts* bucket, this per-type sub-tab lists every Suricata alert with columns for `timestamp`, `alert.signature`, source and destination endpoints, `event_type`, `alert.signature_id`, `alert.rev`, `alert.gid`, `alert.metadata`, and the unified `severity` label. Rows are sortable and filterable with the standard Hunt page controls.
- **Hunt detail sidebar -- Suricata Alert section.** Any row that carries a Suricata `alert` block renders the *Suricata Alert* sidebar section alongside the row's network-base section and any companion protocol section (HTTP, DNS, TLS, FileInfo). Signature text, SID, revision, GID, category, action, metadata tags, and the raw packet payload (when present) all appear inline. If the enrichment pipeline added a C2, InSights, or MetaDefender Core hit on the same session, the matching enrichment section renders next to the Suricata section.

## [Alert payload example](/docs/mdndr/operating-guide/suricata-signatures#alert-payload-example)

Abbreviated EVE JSON for an ET PRO malware signature matching a downloader request over HTTP. This example omits Base64 `packet` bytes and verbose header arrays for readability.

JsonCopy{
"timestamp": "2025-11-15T08:42:17.334821+0000",
"flow_id": 1847291847291847,
"in_iface": "ens192",
"event_type": "alert",
"src_ip": "192.168.10.157",
"src_port": 49281,
"dest_ip": "185.117.118.45",
"dest_port": 80,
"proto": "TCP",
"community_id": "1:8K3vN7pL5mQ2rT9uV1wX3yZ5",
"alert": {
"action": "allowed",
"gid": 1,
"signature_id": 2034682,
"rev": 3,
"signature": "ET PRO MALWARE Win32/Emotet Downloader Activity (exe)",
"category": "A Network Trojan was Detected",
"severity": 1,
"metadata": {
"affected_product": ["Windows"],
"attack_target": ["Client_Endpoint"],
"created_at": ["2024_11_01"],
"deployment": ["Perimeter"],
"former_category": ["MALWARE"],
"malware_family": ["Emotet"],
"mitre_attack_id": ["T1204.002", "T1105"],
"performance_impact": ["Low"],
"signature_severity": ["Critical"],
"updated_at": ["2025_10_15"]
},
"app_proto": "http"
},
"http": {
"hostname": "malicious-c2.example.ru",
"url": "/payload/update.exe",
"http_method": "GET",
"protocol": "HTTP/1.1",
"status": 200,
"length": 184320,
"http_user_agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36",
"http_content_type": "application/x-dosexec"
}
}

Two details worth calling out: `alert.severity: 1` maps to the unified *Critical* label; and the companion `http` block drives the HTTP sidebar section that renders next to the Suricata Alert section on the Hunt page. A file-extraction match adds a `fileinfo` block with `sha256` / `sha1` / `md5` on the same record and triggers the MetaDefender Core enrichment path described in [MetaDefender Core File Scanning](/docs/mdndr/operating-guide/metadefender-core-file-scanning).

## [Tuning considerations](/docs/mdndr/operating-guide/suricata-signatures#tuning-considerations)

Suricata's accuracy depends on ruleset hygiene. Three common sources of false positives, and the Policy-managed knobs that address them:

- **Broad rules firing on benign traffic.** Proofpoint ET Pro ships a long tail of low-severity rules that can be noisy in some environments (for example, *ET POLICY* rules matching cleartext HTTP on internal-to-external flows). Operators disable individual Signature Identifiers through Policy without modifying the shipped rulepack. See [Updates Management](/docs/mdndr/operating-guide/updates-management) for the per-SID enable / disable workflow and the per-policy rule overlays.
- **Rules targeting products the environment does not run.** The `metadata.affected_product` and `metadata.attack_target` tags make it possible to filter rules whose target platform is not present in the environment. Use the same Policy workflow to disable rule groups by metadata.
- **Rule revisions changing semantics.** When a rule's `rev` changes, its match surface may widen or narrow. The Updates management surface shows every rulepack update, lists added / removed / modified SIDs, and allows operators to roll an update forward or back per policy.

Analysts should never suppress a signature at the alert engine when suppression at the sensor is possible -- rule-level disable is cheaper than post-hoc filtering and keeps storage utilization bounded.

## [Related runbook](/docs/mdndr/operating-guide/suricata-signatures#related-runbook)

The [Critical Alert Triage](/docs/mdndr/operating-guide/critical-alert-triage) runbook is the first stop for any Critical-severity Suricata alert. Follow-on investigation uses [C2 Beacon Investigation](/docs/mdndr/operating-guide/c2-beacon-investigation) for malware-family and callback signatures. Use [Malicious File Investigation](/docs/mdndr/operating-guide/malicious-file-investigation) when the alert carries a `fileinfo` block. Use [Alert, Flow, and PCAP Pivoting](/docs/mdndr/operating-guide/alert--flow--and-pcap-pivoting) when the analyst must walk from the signature back to the full session capture.
