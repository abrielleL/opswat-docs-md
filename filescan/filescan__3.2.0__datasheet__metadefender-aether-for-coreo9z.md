<!-- source: https://www.opswat.com/docs/filescan/3.2.0/datasheet/metadefender-aether-for-coreo9z -->

# MetaDefender Aether for Core

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**MetaDefender Aether™ for Core** is OPSWAT’s on-premises zero-day detection solution for MetaDefender Core, built for organizations that need advanced file analysis in regulated, restricted, or air-gapped environments.

Rather than relying on a sandbox alone, Aether for Core brings a **five-layer zero-day detection pipeline** into existing MetaDefender Core workflows. It combines Threat Reputation, Predictive Alin AI Pre-Execution analysis, emulation-based Adaptive Sandbox, Threat Scoring, and ML-powered Threat Hunting to detect known, unknown, and evasive malware before files reach critical systems.

Aether for Core works with existing MetaDefender Core policies and workflows, allowing organizations to add deeper zero-day inspection without rebuilding their file security architecture.

## [1. Five-Layer Zero-Day Detection](/docs/filescan/3.2.0/datasheet/metadefender-aether-for-coreo9z#1-five-layer-zero-day-detection)

### [Layer 1: Threat Reputation](/docs/filescan/3.2.0/datasheet/metadefender-aether-for-coreo9z#layer-1-threat-reputation)

Aether for Core checks files, URLs, IPs, and domains against continuously updated reputation intelligence to identify known threats before deeper analysis.

Reputation intelligence can operate in connected or offline environments, helping organizations block known malware and attacker infrastructure while preserving support for air-gapped deployments.

New indicators discovered through deeper analysis can strengthen local reputation intelligence over time.

### [Layer 2: Static Analysis with Predictive Alin AI](/docs/filescan/3.2.0/datasheet/metadefender-aether-for-coreo9z#layer-2-static-analysis-with-predictive-alin-ai)

**Predictive Alin AI** provides an AI-powered Pre-Execution detection layer for identifying malicious intent before a file is detonated.

It analyzes intrinsic file characteristics, structural signals, entropy patterns, and other features using machine learning rather than relying solely on malware signatures.

Within MetaDefender Core, Predictive Alin AI operates inline with Metascan™ Multiscanning to provide an additional detection signal for previously unseen, low-prevalence, polymorphic, or structurally modified malware.

This earlier decision point helps organizations maintain high-speed file flows while reserving deeper dynamic analysis for files that require further investigation.

### [Layer 3: Dynamic Analysis with Adaptive Sandbox](/docs/filescan/3.2.0/datasheet/metadefender-aether-for-coreo9z#layer-3-dynamic-analysis-with-adaptive-sandbox)

Files requiring deeper investigation can be routed to OPSWAT **Adaptive Sandbox**, which uses emulation-based dynamic analysis to expose behavior that static and traditional VM-based tools may miss.

Instead of depending on a detectable virtual machine, Adaptive Sandbox emulates execution and can explore alternate code paths to reveal:

- Loader chains and multi-stage payloads
- Runtime file and process activity
- Obfuscated scripts
- Command-and-control activity
- Memory and configuration artifacts
- Packed and dynamically reconstructed payloads
- Anti-analysis and environment-aware evasion techniques

Recent detection updates expand analysis for complex Windows installers, downloaded scripts, encoded payloads, HTML threats, obfuscated code, ClickFix variants, AI/ML model files, and other emerging attack techniques.

### [Layer 4: Threat Scoring](/docs/filescan/3.2.0/datasheet/metadefender-aether-for-coreo9z#layer-4-threat-scoring)

Threat Scoring correlates evidence from reputation, static analysis, and dynamic analysis into a confidence-based risk score and actionable verdict.

Instead of requiring security teams to interpret each individual signal independently, Aether for Core prioritizes the highest-risk files and helps reduce false positives, alert noise, and unnecessary investigation.

Current verdict terminology provides clearer guidance:

- **Trusted**
- **No Threat Detected**
- **Undetermined**
- **Low Risk**
- **High Risk**
- **Confirmed Threat**

### [Layer 5: Threat Hunting](/docs/filescan/3.2.0/datasheet/metadefender-aether-for-coreo9z#layer-5-threat-hunting)

ML-powered Similarity Search and Threat Pattern Correlation help analysts move beyond the individual file.

Aether can connect suspicious samples with related malware families, infrastructure, tactics, code variants, and attacker campaigns, helping teams determine whether a newly detected threat is part of a broader operation.

This turns file analysis into actionable threat intelligence for SOC investigation, incident response, and proactive hunting.

## [2. Integration and Workflow](/docs/filescan/3.2.0/datasheet/metadefender-aether-for-coreo9z#2-integration-and-workflow)

### [Integrated with MetaDefender Core](/docs/filescan/3.2.0/datasheet/metadefender-aether-for-coreo9z#integrated-with-metadefender-core)

Aether for Core is designed to work directly with existing MetaDefender Core deployments, policies, and security workflows.

Organizations can use **embedded or remote Adaptive Sandbox engine configurations**, depending on their architecture and operational requirements.

For embedded deployments, dynamic file analysis and behavioral threat detection can run directly within the Core environment without requiring a separate sandbox infrastructure stack.

### [Policy-Driven Analysis](/docs/filescan/3.2.0/datasheet/metadefender-aether-for-coreo9z#policy-driven-analysis)

Administrators control which files receive deeper analysis through existing MetaDefender Core workflow policies.

Files can be routed to Adaptive Sandbox based on criteria such as:

- File type
- Scan verdict or risk category
- YARA findings
- Deep CDR™ findings and triggers
- Embedded scripts, macros, or active content
- Other workflow conditions

This allows organizations to focus resource-intensive dynamic analysis on files that need it rather than detonating every file indiscriminately.

MetaDefender Core 5.19 also improves this process by recognizing unsupported file types before Adaptive Sandbox processing, avoiding unnecessary sandbox resource consumption.

### [Unified Results in MetaDefender Core](/docs/filescan/3.2.0/datasheet/metadefender-aether-for-coreo9z#unified-results-in-metadefender-core)

Analysis results are available within the MetaDefender Core management experience, giving security teams a consolidated view of file security evidence.

Depending on the analysis performed, results can include:

- Metascan Multiscanning verdicts
- Predictive Alin AI findings
- Adaptive Sandbox verdicts
- Threat scores
- Threat Indicators
- Extracted IOCs
- File and behavioral evidence
- Malware configuration data
- Reputation intelligence

This provides a more complete picture of the file without forcing analysts to pivot between separate detection tools.

## [3. Designed for On-Premises, Offline, and Regulated Environments](/docs/filescan/3.2.0/datasheet/metadefender-aether-for-coreo9z#3-designed-for-on-premises-offline-and-regulated-environments)

MetaDefender Aether for Core is positioned specifically for organizations that need advanced zero-day detection while retaining control of files and analysis infrastructure.

It supports:

- **On-premises MetaDefender Core environments**
- **Offline and fully air-gapped environments**
- **Embedded Adaptive Sandbox deployments**
- **Remote Adaptive Sandbox deployments**
- **Restricted and regulated file-processing environments**

Offline deployments can continue to perform local reputation and advanced threat analysis without requiring files to be uploaded to a public cloud sandbox.

Aether for Core also supports independent updates to detection logic and threat intelligence, allowing new protections to be delivered more frequently without requiring a complete product upgrade.

## [4. Latest Detection and Analysis Enhancements](/docs/filescan/3.2.0/datasheet/metadefender-aether-for-coreo9z#4-latest-detection-and-analysis-enhancements)

Recent Aether for Core engine updates expand coverage across several high-priority threat areas.

### [Advanced Installer Analysis](/docs/filescan/3.2.0/datasheet/metadefender-aether-for-coreo9z#advanced-installer-analysis)

Deep static extraction and analysis now covers common Windows installer frameworks including NSIS, Inno Setup, InstallShield, Advanced Installer, Wise, WiX, InstallAnywhere, and Actual Installer.

Aether can extract prioritized embedded files, inspect installer scripts, and apply heuristic analysis to custom installers.

### [AI and Machine Learning Model Security](/docs/filescan/3.2.0/datasheet/metadefender-aether-for-coreo9z#ai-and-machine-learning-model-security)

Security analysis has expanded to machine learning model files, using multi-serialization parsing and deep static inspection to identify potentially malicious payloads hidden inside AI/ML artifacts.

### [Stronger Evasion Detection](/docs/filescan/3.2.0/datasheet/metadefender-aether-for-coreo9z#stronger-evasion-detection)

Detection has expanded for techniques including:

- Meaningless infinite loops
- Password-protected malicious macros
- .NET control-flow obfuscation
- Protected .NET constants
- Hexadecimal-encoded JavaScript
- Invisible and deceptive Unicode constructs
- Dynamically reconstructed Base64 payloads

### [Multi-Stage Attack Visibility](/docs/filescan/3.2.0/datasheet/metadefender-aether-for-coreo9z#multi-stage-attack-visibility)

Improved emulation triggering for downloaded scripts helps reveal more of the complete infection chain when initial files retrieve additional payloads from external resources.

Base64 decoding of dynamically generated files also improves visibility into malware that reconstructs later stages only during execution.

### [Expanded File and Web Threat Coverage](/docs/filescan/3.2.0/datasheet/metadefender-aether-for-coreo9z#expanded-file-and-web-threat-coverage)

Recent updates add or improve analysis for:

- EPUB
- VSIX
- CRX
- Complex Windows installers
- HTML data-blob payloads
- QR codes rendered inside documents and emails
- Encrypted Office and PDF documents
- Obfuscated BAT scripts
- AI/ML model files

These improvements help Aether for Core adapt to changing delivery methods without relying exclusively on traditional signatures.

## [5. Primary Use Cases](/docs/filescan/3.2.0/datasheet/metadefender-aether-for-coreo9z#5-primary-use-cases)

### [Secure High-Volume File Workflows](/docs/filescan/3.2.0/datasheet/metadefender-aether-for-coreo9z#secure-high-volume-file-workflows)

Add zero-day detection to files moving through MetaDefender Core, ICAP, Managed File Transfer, email, storage, and other automated file-processing workflows.

Threat Reputation and Predictive Alin AI provide fast early-stage decisions, while suspicious or unresolved files can be escalated to Adaptive Sandbox for deeper analysis.

### [Critical Infrastructure and Air-Gapped Environments](/docs/filescan/3.2.0/datasheet/metadefender-aether-for-coreo9z#critical-infrastructure-and-air-gapped-environments)

Analyze suspicious files locally in environments where sensitive information cannot be submitted to external cloud analysis services.

This is particularly relevant for government, defense, energy, manufacturing, financial services, and other regulated or isolated environments.

### [Files That Cannot Be Sanitized](/docs/filescan/3.2.0/datasheet/metadefender-aether-for-coreo9z#files-that-cannot-be-sanitized)

Executables, installers, patch files, scripts, machine learning models, and certain regulated documents cannot always be addressed through Content Disarm and Reconstruction.

Aether for Core adds behavioral and AI-driven detection for these files without requiring them to be modified.

### [SOC Triage and Incident Response](/docs/filescan/3.2.0/datasheet/metadefender-aether-for-coreo9z#soc-triage-and-incident-response)

Give SOC and malware analysts behavioral evidence, threat scores, IOCs, malware configuration data, and related threat context to support faster investigation and response.

### [Secure Software and Supply Chain Workflows](/docs/filescan/3.2.0/datasheet/metadefender-aether-for-coreo9z#secure-software-and-supply-chain-workflows)

Inspect installers, executables, scripts, packages, and other software artifacts before they are distributed into trusted environments.

Expanded installer extraction and AI/ML model analysis strengthen coverage for modern software and AI supply chains.

## [6. Summary](/docs/filescan/3.2.0/datasheet/metadefender-aether-for-coreo9z#6-summary)

MetaDefender Aether for Core extends MetaDefender Core from multi-layer file prevention into **AI-driven, five-layer zero-day detection**.

It combines:

1. **Threat Reputation** to identify known threats quickly
2. **Predictive Alin AI** to predict unknown threats Pre-Execution
3. **Adaptive Sandbox** to expose evasive behavior through emulation
4. **Threat Scoring** to convert evidence into an actionable risk verdict
5. **Threat Hunting** to connect individual detections to related malware and campaigns

The result is deeper zero-day inspection within existing MetaDefender Core workflows, without forcing organizations to choose between file security, operational throughput, and control of sensitive data.

For regulated, offline, and air-gapped environments, Aether for Core provides a practical way to bring advanced AI-powered and behavioral threat detection directly to the file security perimeter.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
