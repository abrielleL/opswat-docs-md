<!-- source: https://www.opswat.com/docs/filescan/datasheet/engine-features -->

# Adaptive Sandbox Features

OPSWAT **Adaptive Sandbox** is the emulation-based dynamic analysis technology that powers **Layer 3 of MetaDefender Aether’s five-layer zero-day detection pipeline**.

When Threat Reputation and Predictive Alin AI cannot confidently resolve a suspicious file, Adaptive Sandbox provides deeper behavioral analysis. Its instruction-level emulation engine forces evasive code paths to execute, extracts actionable Indicators of Compromise (IOCs), and exposes runtime behavior that static analysis and traditional VM-based sandboxes may miss.

Adaptive Sandbox is built for dynamic analysis at enterprise scale, supporting **50K+ analyses per day per server**, **120+ file types**, approximately **10-second fast-pass analysis**, and **1,000+ behavioral indicators**.

## [Deep Structure Analysis](/docs/filescan/datasheet/engine-features#deep-structure-analysis)

Before runtime execution begins, Adaptive Sandbox performs advanced static inspection to understand what is inside the file.

Deep Structure Analysis supports **120+ file types** and can extract:

- Embedded files and active content
- Scripts and macros
- Shellcode
- Images and other embedded objects
- Encoded or obfuscated content
- Executable components
- Potentially malicious artifacts hidden inside complex files

This first stage gives the engine structural context before dynamic execution and helps uncover components that may need deeper analysis.

## [Adaptive Threat Analysis](/docs/filescan/datasheet/engine-features#adaptive-threat-analysis)

Adaptive Sandbox goes beyond passively observing a sample inside a virtual machine.

Its **instruction-level emulation engine** simulates CPU, operating system, application, and script behavior while controlling the execution environment. This allows the engine to manipulate execution flow and trigger malicious code paths that may otherwise remain dormant.

Adaptive Threat Analysis can expose:

- Loader and script behavior
- Multi-stage execution chains
- Packers, stagers, and droppers
- Process injection
- Registry changes
- Dropped files
- Command-and-control callbacks
- Memory-only payloads
- Configuration artifacts
- Anti-analysis and sandbox-evasion techniques

Because the analysis does not depend on a conventional VM environment, malware has fewer environmental signals it can use to recognize that it is being analyzed.

## [Built for Modern Evasion Techniques](/docs/filescan/datasheet/engine-features#built-for-modern-evasion-techniques)

Modern malware increasingly attempts to determine when it is running inside a sandbox and suppress malicious behavior until conditions appear safe.

Adaptive Sandbox is engineered to expose evasive techniques including:

- Geofencing and locale checks
- Long sleep and delayed-execution loops
- Sandbox and environment detection
- Obfuscated VBA
- Corrupted OOXML payloads
- Packed or bloated executables
- Shellcode
- Memory-only payloads
- Multi-stage loaders and droppers

By manipulating execution at the instruction level, Adaptive Sandbox can reveal malicious activity that might never trigger during a conventional VM-based sandbox session.

## [Deep Behavioral IOC Extraction](/docs/filescan/datasheet/engine-features#deep-behavioral-ioc-extraction)

Dynamic analysis generates the behavioral intelligence needed to understand not only whether a file is malicious, but **what it attempted to do**.

Adaptive Sandbox can extract and correlate evidence such as:

- Dropped and generated files
- Registry modifications
- Network callbacks
- URLs, domains, and IP addresses
- Process behavior
- Malware configuration data
- Loader activity
- Persistence behavior
- MITRE ATT&CK-mapped activity
- Other behavioral Indicators of Compromise

These findings provide evidence for Aether’s Threat Scoring layer while also creating intelligence that can be used for investigation, blocking, automation, and future detection.

## [From Detection to Actionable Intelligence](/docs/filescan/datasheet/engine-features#from-detection-to-actionable-intelligence)

Adaptive Sandbox outputs are designed to move directly into security operations rather than remain isolated in a sandbox report.

Structured behavioral intelligence and IOCs can support:

- SOC investigation and triage
- SIEM and SOAR enrichment
- Threat hunting
- Incident response
- MISP workflows
- STIX workflows
- JSON-based automation
- Security policy and blocking decisions

This helps turn a newly discovered zero-day from a one-time detection into intelligence that can improve security decisions across the environment.

## [High-Performance Dynamic Analysis](/docs/filescan/datasheet/engine-features#high-performance-dynamic-analysis)

Traditional VM sandbox farms can introduce significant infrastructure overhead because each analysis depends on provisioning, executing, and resetting a complete operating environment.

Adaptive Sandbox uses a lightweight emulation architecture designed for automated and high-volume file workflows.

Key performance capabilities include:

- **50K+ analyses per day per server**
- **~10-second fast-pass analysis**
- **120+ supported file types**
- **1,000+ behavioral indicators**

This makes dynamic analysis practical not only for post-incident malware research, but also for perimeter inspection, SOC triage, managed file transfer, email, secure gateways, and other high-volume file-processing workflows.

## [A Continuous Zero-Day Learning Loop](/docs/filescan/datasheet/engine-features#a-continuous-zero-day-learning-loop)

Adaptive Sandbox does more than produce a verdict for the file being analyzed.

When dynamic analysis uncovers previously unknown malicious infrastructure, files, domains, URLs, or other IOCs, that intelligence can strengthen **Layer 1 Threat Reputation**, helping future encounters with the same indicators reach a decision earlier in the pipeline.

Sandbox-confirmed zero-day discoveries also contribute to the **Predictive Alin AI learning loop in Layer 2**. Predictive Alin AI models are retrained using threats confirmed through Aether dynamic analysis, helping the Pre-Execution layer recognize structural and behavioral patterns associated with emerging malware before detonation is required.

The result is a reinforcing detection cycle:

**Predict → Analyze → Confirm → Learn → Detect Earlier**

Dynamic analysis confirms what new malware actually does. That intelligence then helps Aether recognize related threats earlier and reduce unnecessary sandbox submissions over time.

## [Flexible Deployment](/docs/filescan/datasheet/engine-features#flexible-deployment)

Adaptive Sandbox can be deployed wherever sensitive files need to be analyzed:

**Cloud**
Elastic malware analysis without requiring customers to manage sandbox infrastructure.

**On-Premises**
Local dynamic analysis with greater control over files, infrastructure, and integrations.

**Air-Gapped**
Offline behavioral analysis for government, defense, critical infrastructure, and other environments where external connectivity is restricted or prohibited.

## [Adaptive Sandbox vs. MetaDefender Aether](/docs/filescan/datasheet/engine-features#adaptive-sandbox-vs-metadefender-aether)

Adaptive Sandbox and MetaDefender Aether serve different roles.

**Adaptive Sandbox is the dynamic analysis engine.**
It uses emulation to force suspicious files to reveal hidden runtime behavior and generates behavioral evidence and IOCs.

**MetaDefender Aether is the complete five-layer zero-day detection solution.**
It combines Threat Reputation, Predictive Alin AI, Adaptive Sandbox, Threat Scoring, and ML-powered Threat Hunting to deliver a consolidated file verdict and broader threat context.

Adaptive Sandbox provides the behavioral depth. Aether turns that analysis into a coordinated detection, learning, prioritization, and threat-hunting workflow.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
