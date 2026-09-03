<!-- source: https://www.opswat.com/docs/filescan/datasheet/why-opswat-filescan- -->

# MetaDefender Aether

**MetaDefender Aether™** is OPSWAT’s AI-driven unified five-layer zero-day detection solution, combining Threat Reputation, Predictive Alin AI, Adaptive Sandbox, Threat Scoring, and ML-powered Threat Hunting in a single detection pipeline.

Aether detects known, unknown, and evasive malware before it reaches users and systems, delivering a single, consolidated verdict per file to support faster security decisions across SOC, SIEM, SOAR, and threat-hunting workflows.

**MetaDefender Aether combines five coordinated detection layers:**

### [Layer 1: Threat Reputation](/docs/filescan/datasheet/why-opswat-filescan-#layer-1-threat-reputation)

Checks files, URLs, IPs, and domains against continuously updated reputation intelligence, online or offline, to identify known threats before deeper analysis.

By filtering known malware and attacker infrastructure early, Threat Reputation reduces unnecessary downstream analysis while continuously incorporating new indicators discovered by later Aether layers.

### [Layer 2: Static Analysis with Predictive Alin AI](/docs/filescan/datasheet/why-opswat-filescan-#layer-2-static-analysis-with-predictive-alin-ai)

Predictive Alin AI closes the **Pre-Execution** detection gap by analyzing file structure, behavioral features, and other file characteristics to predict malicious intent in milliseconds, without signatures or sandbox detonation.

The AI-powered engine detects never-before-seen and polymorphic malware before execution, helping stop high-risk files earlier while reducing unnecessary demand on dynamic analysis.

### [Layer 3: Dynamic Analysis with Adaptive Sandbox](/docs/filescan/datasheet/why-opswat-filescan-#layer-3-dynamic-analysis-with-adaptive-sandbox)

Files requiring deeper investigation are analyzed using OPSWAT’s emulation-based Adaptive Sandbox.

Instruction-level emulation triggers malicious behavior and explores alternate execution paths without relying on a detectable virtual machine. It exposes loader chains, runtime artifacts, obfuscated scripts, memory-only payloads, multi-stage attacks, and evasion techniques that static and VM-based tools can miss.

### [Layer 4: Threat Scoring](/docs/filescan/datasheet/why-opswat-filescan-#layer-4-threat-scoring)

Threat Scoring correlates signals from Threat Reputation, Static Analysis, and Dynamic Analysis to assign a confidence-based risk score.

By combining file characteristics, runtime behaviors, threat intelligence, and detection indicators into an actionable verdict, Aether helps security teams prioritize high-risk threats while reducing alert noise and manual triage.

### [Layer 5: Threat Hunting](/docs/filescan/datasheet/why-opswat-filescan-#layer-5-threat-hunting)

ML-powered Similarity Search and Threat Pattern Correlation connect suspicious and unknown samples to related malware, infrastructure, behaviors, tactics, and variants.

This moves analysis beyond an isolated file verdict to reveal malware families, shared infrastructure, and broader attacker campaigns, giving analysts richer context for proactive and retroactive threat hunting.

Together, these five layers address the full Pyramid of Pain, from reusable hashes and infrastructure to attacker tools, behaviors, and TTPs. Attackers are forced to change more than individual files to evade detection, increasing the cost and complexity of maintaining an attack campaign.

## [Key Features Include](/docs/filescan/datasheet/why-opswat-filescan-#key-features-include)

### [Threat Reputation](/docs/filescan/datasheet/why-opswat-filescan-#threat-reputation)

▪ Checks files, IP addresses, URLs, and domains against continuously updated threat intelligence

▪ Supports online and offline reputation analysis for connected and air-gapped environments

▪ Correlates file hashes with known applications, vulnerabilities, and threat data

▪ Supports bulk and individual reputation searches through REST APIs

▪ Continuously strengthens reputation intelligence with indicators discovered during deeper analysis

### [Predictive Static Analysis](/docs/filescan/datasheet/why-opswat-filescan-#predictive-static-analysis)

▪ Uses **Predictive Alin AI** to identify malicious intent before execution

▪ Analyzes structural, behavioral, and object-level file characteristics without detonation

▪ Delivers machine-learning verdicts in milliseconds for supported high-risk file formats

▪ Detects never-before-seen and polymorphic malware that signature-based engines may not recognize

▪ Reduces unnecessary sandbox demand by identifying threats earlier in the detection pipeline

▪ Continuously improves through a zero-day learning loop informed by sandbox-confirmed discoveries from MetaDefender Aether

### [Dynamic Analysis and Adaptive Emulation](/docs/filescan/datasheet/why-opswat-filescan-#dynamic-analysis-and-adaptive-emulation)

▪ Uses instruction-level emulation rather than traditional VM-based execution

▪ Automatically triggers and explores malicious execution paths to expose hidden behavior

▪ Defeats anti-VM, timing, environment, geofencing, and user-interaction evasion techniques

▪ Reveals loader chains, dropped files, process injection, C2 callbacks, memory-only payloads, and multi-stage execution

▪ Supports deep analysis across 120+ file types, including executables, scripts, documents, archives, LNK, and MSI files

▪ Extracts malware configurations and behavioral indicators from supported malware families

▪ Detects phishing impersonation using ML-powered brand detection for 330+ brands

▪ Maps detected activity to MITRE ATT&CK and behavioral frameworks for richer analyst context

### [Threat Scoring](/docs/filescan/datasheet/why-opswat-filescan-#threat-scoring)

▪ Correlates Threat Reputation, Predictive Static Analysis, and Dynamic Analysis signals

▪ Evaluates malicious execution flows, persistence, injection, C2 behavior, obfuscation, and other behavioral indicators

▪ Produces a confidence-based risk score and consolidated file verdict

▪ Helps SOC teams prioritize higher-risk threats and reduce false-positive investigation

▪ Converts complex multi-layer evidence into decision-ready intelligence for automated workflows

### [Threat Hunting](/docs/filescan/datasheet/why-opswat-filescan-#threat-hunting)

▪ Uses machine-learning Similarity Search to identify related malware families, variants, and clusters

▪ Applies Threat Pattern Correlation to connect files with shared infrastructure, behaviors, tactics, and campaigns

▪ Identifies relationships across recompiled, polymorphic, and modified malware samples

▪ Supports MITRE ATT&CK mapping for investigation and threat hunting

▪ Exports intelligence through MISP, STIX 2.1, JSON, HTML, and PDF formats

▪ Supports automated YARA generation and integration with SIEM, SOAR, and threat intelligence workflows

An overview of all current capabilities is available on the MetaDefender Aether product page:

<https://www.opswat.com/products/metadefender/aether>

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
