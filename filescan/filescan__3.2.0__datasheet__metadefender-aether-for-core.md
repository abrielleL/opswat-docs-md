<!-- source: https://www.opswat.com/docs/filescan/3.2.0/datasheet/metadefender-aether-for-core -->

# MetaDefender Threat Intelligence

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**MetaDefender Threat Intelligence** is OPSWAT’s behavior-enriched threat intelligence solution for detecting zero-day and evasive threats. It combines real-time threat reputation, sandbox-derived behavioral IOCs, and ML-powered similarity search to help security teams investigate threats faster, improve SIEM and SOAR enrichment, and uncover relationships across malware variants, infrastructure, and campaigns.

Global telemetry from OPSWAT Adaptive Sandbox continuously feeds newly discovered indicators and behavioral intelligence back into the service. This creates a feedback loop where unknown threats discovered through dynamic analysis strengthen future reputation checks, investigations, and automated detection.

### [Real-Time Threat Reputation](/docs/filescan/3.2.0/datasheet/metadefender-aether-for-core#real-time-threat-reputation)

Get up-to-date reputation for **hashes, IP addresses, URLs, and domains** to quickly identify known malicious infrastructure and reduce blind spots.

MetaDefender Threat Intelligence correlates information from billions of global indicators and multiple intelligence providers, giving security teams immediate context before deeper investigation is required.

### [Automated Threat Hunting](/docs/filescan/3.2.0/datasheet/metadefender-aether-for-core#automated-threat-hunting)

Move beyond individual indicators to identify **related malware samples, shared attacker infrastructure, and patterns behind evolving attacks**.

Automated correlation helps analysts determine whether a newly discovered file is an isolated threat or part of a wider malware family or campaign.

### [Threat Similarity Enrichment](/docs/filescan/3.2.0/datasheet/metadefender-aether-for-core#threat-similarity-enrichment)

ML-powered similarity search connects new or modified malware with known samples using behavioral artifacts and similarity signals.

This provides additional context even when attackers change hashes, recompile payloads, or create new malware variants, helping analysts accelerate investigations and improve threat prioritization.

Similarity intelligence can identify family and cluster relationships while enriching SIEM, SOAR, and threat-hunting workflows with more meaningful context.

### [Continuously Updated Threat Intelligence](/docs/filescan/3.2.0/datasheet/metadefender-aether-for-core#continuously-updated-threat-intelligence)

MetaDefender Threat Intelligence continuously incorporates new indicators discovered through OPSWAT’s dynamic malware analysis and global threat research.

High-volume lookups scale through REST APIs, providing current intelligence for automated security workflows without requiring teams to maintain their own threat intelligence infrastructure.

For restricted environments, threat intelligence can also support low-egress and offline workflows where direct cloud access is limited.

## [Key Features Include](/docs/filescan/3.2.0/datasheet/metadefender-aether-for-core#key-features-include)

### [Threat Reputation Service](/docs/filescan/3.2.0/datasheet/metadefender-aether-for-core#threat-reputation-service)

▪ Access to **50+ billion hashes, IPs, URLs, and domains**

▪ Supports bulk and individual reputation searches through REST APIs

▪ Scans IP addresses, URLs, and domains using up to **30 intelligence providers**

▪ Correlates file hashes with millions of known applications and CVEs

▪ Continuously incorporates newly discovered IOCs and threat intelligence

▪ Provides reputation context to quickly distinguish known-good, known-bad, and unknown indicators

### [Behavior-Enriched Threat Intelligence](/docs/filescan/3.2.0/datasheet/metadefender-aether-for-core#behavior-enriched-threat-intelligence)

▪ Enriches reputation data with **IOCs discovered through Adaptive Sandbox analysis**

▪ Provides normalized indicators including hashes, IPs, domains, URLs, certificates, and registry artifacts

▪ Adds behavioral context and MITRE-mapped activity to support deeper investigation

▪ Provides threat scores and related evidence for faster prioritization

▪ Feeds newly discovered indicators back into threat intelligence to strengthen future detection

### [Threat Similarity & Pattern Correlation](/docs/filescan/3.2.0/datasheet/metadefender-aether-for-core#threat-similarity--pattern-correlation)

▪ Uses machine learning to identify similarities between new, modified, and known malware

▪ Aggregates verdicts, analysis reports, behavioral artifacts, and IOCs for proactive investigation

▪ Connects related samples to malware families, clusters, shared infrastructure, and campaigns

▪ Helps uncover polymorphic or recompiled variants even when traditional indicators change

▪ Enables analysts to move from a single file or IOC to broader campaign-level context

### [Security Operations Integration](/docs/filescan/3.2.0/datasheet/metadefender-aether-for-core#security-operations-integration)

▪ Integrates with **SIEM and SOAR workflows** for automated enrichment and response

▪ Supports high-volume intelligence lookups through REST APIs

▪ Provides threat intelligence that can be consumed by automated detection, blocking, and investigation workflows

▪ Reduces manual analyst pivoting by bringing reputation, behavioral evidence, similarity signals, and threat context together

▪ Helps reduce false positives and accelerate threat investigation with behavior-enriched intelligence

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
