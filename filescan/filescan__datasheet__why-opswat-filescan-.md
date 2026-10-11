<!-- source: https://www.opswat.com/docs/filescan/datasheet/why-opswat-filescan- -->

# MetaDefender Aether

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**MetaDefender Aether** (previously known as MetaDefender Sandbox) is a next-generation unified Zero-Day detection solution, combining the proven capabilities of MetaDefender Sandbox with built-in Threat Intelligence, Threat Scoring and Threat Hunting - all delivered as a single adaptive detection pipeline.

**MetaDefender Aether** combines four tightly integrated layers:

**Layer 1: Threat Reputation**

Real-time and offline reputation checks for files, URLs, IPs, and domains filter out known threats instantly using global intelligence from billions of indicators.

**Layer 2: Static Analysis (Predictive Alin AI]**

Machine learning reads the structure of each file before anything runs, with no signatures and no detonation. High-confidence clean files leave in milliseconds and high-confidence threats are blocked. Only uncertain files go on to the sandbox, so most files never need dynamic analysis.

**Layer 3: Dynamic Analysis (MetaDefender Sandbox Engine)**

Unknown and suspicious files are executed in an emulation-based sandbox that bypasses anti-VM and timing-based evasion. Runtime behaviors, loader chains, scripts, and artifacts are exposed even when malware tries to stay dormant.

**Layer 4: Threat Scoring**

Behavioral indicators, reputation context, and detection logic are correlated to assign a confidence-based risk score—helping SOC teams prioritize what truly matters.

**Layer 5: Threat Hunting**

Machine-learning similarity search connects unknown samples to known malware families, infrastructure, and campaigns, enabling proactive hunting and retroactive analysis.

This unified approach addresses the entire Pyramid of Pain, forcing attackers to continually rewrite tools, behaviors, and infrastructure to evade detection.

## [Key features include](/docs/filescan/datasheet/why-opswat-filescan-#key-features-include)

**Reputation Service**

▪ Scans IP Addresses, URLs, and domains using up to 30 Providers

▪ Correlates hashes to millions of known applications and CVEs

▪ Continuously updates its Threat Intelligence Database

▪ Supports bulk and individual searches via REST API

▪ Enhances visibility with comprehensive intelligence

**Dynamic Analysis**

▪ YARA & Malware Config Extraction for the most prevalent malware families

▪ Detects evasive malware & sandbox aware threats through our inhouse Threat Indicator Library

▪ Detection of .NET loaders & suspicious binary anomalies

▪ Brand Detection Model, identifying phishing impersonation attempts, with OCR capabilities

▪ Supporting wide array of file types for analysis Advanced Emulation

▪ Powered by Next-Gen Advanced PE Emulator Beta—purpose built to outpace traditional sandboxes

▪ Defeats Anti-VM, anti-debug, and time based evasion—no manual tuning required

▪ Unpacks multi-stage payloads, decrypts runtime packers, and reveals hidden IOCS

▪ Detects fileless malware, customer loaders, and sandbox- aware threats missed by legacy tools

▪ Shellcode execution, memory dump integration, and event tracking for deeper behavioral insights

**Threat Hunting & Forensics**

▪ MITRE ATT&CK mapping and machine learning similarity search

▪ Web threat detection with ML-based multi-label classification, including content and style analysis

An overview of all features is available on the up-to-date product page:

<https://www.opswat.com/products/metadefender/aether>

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
