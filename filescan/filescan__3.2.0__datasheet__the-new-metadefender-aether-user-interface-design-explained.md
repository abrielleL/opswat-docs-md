<!-- source: https://www.opswat.com/docs/filescan/3.2.0/datasheet/the-new-metadefender-aether-user-interface-design-explained -->

# The New MetaDefender Aether User Interface Design Explained

View as Markdown Ask ChatGPT about this page Ask Claude about this page

MetaDefender Aether 3.2 brings the product experience in line with its five-layer zero-day detection architecture. The interface gives analysts a clearer evidence trail from initial reputation through Pre-Execution AI analysis, dynamic behavior, risk scoring, and threat hunting, making it easier to understand not only the final verdict, but how Aether reached it.

Image Description: MetaDefender Aether presents each layer’s contribution in sequence, giving analysts a clear evidence trail behind the final verdict.

## [Global Navigation & Context Header](/docs/filescan/3.2.0/datasheet/the-new-metadefender-aether-user-interface-design-explained#global-navigation--context-header)

#### [What changed](/docs/filescan/3.2.0/datasheet/the-new-metadefender-aether-user-interface-design-explained#what-changed)

- The experience is framed around **MetaDefender Aether**, OPSWAT’s unified zero-day detection solution, rather than a standalone sandbox.
- Global navigation provides direct access to **Reports, Trends, Hunting, Leaderboard, API, and Feed**.
- Analysis, investigation, and threat intelligence workflows are accessible within the same product experience.

#### [Why this matters](/docs/filescan/3.2.0/datasheet/the-new-metadefender-aether-user-interface-design-explained#why-this-matters)

- Analysts immediately understand they are working in a broader **zero-day detection solution**, not simply viewing sandbox detonations.
- Navigation reflects the operational workflow from file analysis through investigation, correlation, hunting, and response.
- This closes the gap between individual file analysis and broader threat intelligence workflows.

## [Sample Overview Header: File Identity, Attribution & Verdict](/docs/filescan/3.2.0/datasheet/the-new-metadefender-aether-user-interface-design-explained#sample-overview-header-file-identity-attribution--verdict)

#### [What changed](/docs/filescan/3.2.0/datasheet/the-new-metadefender-aether-user-interface-design-explained#what-changed)

- File name, hash, and the **consolidated verdict**, such as Confirmed Threat, are prioritized at the top of the report.
- Contextual tags such as packer, evasion, anti-debug, fingerprinting, and other detected characteristics provide immediate context.
- MetaDefender Aether 3.2 strengthens **Threat Attribution**, providing clearer, evidence-backed classifications about the likely identity and intent of a threat.
- Attribution is calculated independently for the submitted file and for files downloaded, generated, or extracted during analysis.

#### [Why this matters](/docs/filescan/3.2.0/datasheet/the-new-metadefender-aether-user-interface-design-explained#why-this-matters)

- Analysts can quickly answer the first questions that matter: **What is this file, how risky is it, and what does Aether believe it is?**
- Clearer attribution reduces the time spent interpreting ambiguous or heavily qualified classifications.
- Separate attribution for individual components helps analysts distinguish the original delivery file from loaders, downloaded payloads, and other stages of a multi-stage attack.
- The consolidated verdict gives teams a clear decision point while retaining the evidence needed to validate it.

## [Five-Layer Zero-Day Detection Pipeline](/docs/filescan/3.2.0/datasheet/the-new-metadefender-aether-user-interface-design-explained#five-layer-zero-day-detection-pipeline)

#### [What changed](/docs/filescan/3.2.0/datasheet/the-new-metadefender-aether-user-interface-design-explained#what-changed)

MetaDefender Aether 3.2 expands the processing model from four layers to **five coordinated detection layers**:

1. **Threat Reputation**
2. **Static Analysis with Predictive Alin AI**
3. **Dynamic Analysis with Adaptive Sandbox**
4. **Threat Scoring**
5. **Threat Hunting**

Scan results now present a **numbered, sequential view of the Aether layers that analyzed the file**, showing how each stage contributed evidence to the final verdict.

#### [Why this matters](/docs/filescan/3.2.0/datasheet/the-new-metadefender-aether-user-interface-design-explained#why-this-matters)

- Analysts can see how the verdict was built instead of receiving a single unexplained result.
- Each layer answers a different threat question, providing a traceable path from known-threat identification to campaign-level context.
- The interface makes clear that Aether is not simply detonating every unknown file. It applies progressively deeper analysis according to the evidence available.
- This improves explainability and gives analysts more confidence when using Aether results for blocking, investigation, or policy decisions.

## [Predictive Alin AI: Pre-Execution Evidence](/docs/filescan/3.2.0/datasheet/the-new-metadefender-aether-user-interface-design-explained#predictive-alin-ai-pre-execution-evidence)

#### [What changed](/docs/filescan/3.2.0/datasheet/the-new-metadefender-aether-user-interface-design-explained#what-changed)

MetaDefender Aether 3.2 introduces **Predictive Alin AI as Layer 2: Static Analysis**.

Predictive Alin AI evaluates supported files for malicious intent **Pre-Execution**, before sandbox detonation or runtime behavior is required.

Its result is displayed alongside the multiscanning verdict, allowing analysts to compare signature-based findings with Aether’s machine-learning prediction for the same sample.

#### [Why this matters](/docs/filescan/3.2.0/datasheet/the-new-metadefender-aether-user-interface-design-explained#why-this-matters)

- Analysts gain an additional decision point before resource-intensive dynamic analysis.
- A file that has not been identified by traditional detection engines can still show a high-confidence malicious prediction.
- High-confidence findings can accelerate triage, while uncertain or conflicting samples can continue to Adaptive Sandbox for deeper behavioral analysis.
- Seeing multiscanning and predictive evidence together makes the relationship between known-threat detection and zero-day prediction easier to understand.

## [Threat Indicators Panel: Evidence at a Glance](/docs/filescan/3.2.0/datasheet/the-new-metadefender-aether-user-interface-design-explained#threat-indicators-panel-evidence-at-a-glance)

#### [What changed](/docs/filescan/3.2.0/datasheet/the-new-metadefender-aether-user-interface-design-explained#what-changed)

- Threat indicators are organized by severity, including **Confirmed, High Risk, Low Risk, and Other**.
- **Top Threat Indicators** bring the most meaningful evidence forward.
- Indicators can include behavioral, structural, emulation, evasion, malware classification, and other signals generated across Aether’s analysis pipeline.
- MetaDefender Aether 3.2 expands detection coverage for techniques including **EtherHiding, intentionally malformed .NET assemblies, remote template injection, wiper malware, and ClickFix campaigns**.

#### [Why this matters](/docs/filescan/3.2.0/datasheet/the-new-metadefender-aether-user-interface-design-explained#why-this-matters)

- Analysts can focus on the evidence that contributed most strongly to the verdict rather than reviewing every raw signal equally.
- Risk is contextualized and prioritized, reducing unnecessary investigation.
- New detection coverage provides stronger visibility into threats that hide infrastructure, manipulate file structures, abuse social engineering, or attempt to interfere with automated analysis.
- High-value evidence is available early in the investigation, helping reduce triage time and alert fatigue.

## [Indicators of Compromise](/docs/filescan/3.2.0/datasheet/the-new-metadefender-aether-user-interface-design-explained#indicators-of-compromise)

#### [What changed](/docs/filescan/3.2.0/datasheet/the-new-metadefender-aether-user-interface-design-explained#what-changed)

- IOCs are presented directly alongside analysis rather than being limited to exported reports.
- File, network, registry, infrastructure, and other artifacts discovered during analysis can be reviewed within the investigation workflow.
- MetaDefender Aether 3.2 adds malware configuration extraction for **PrivateLoader and Quasar RAT** and expands IOC coverage in the local Reputation database.

#### [Why this matters](/docs/filescan/3.2.0/datasheet/the-new-metadefender-aether-user-interface-design-explained#why-this-matters)

- Analysts can move directly from detection to action by using extracted indicators for blocking, investigation, threat hunting, or SIEM/SOAR enrichment.
- Malware configuration data can reveal C2 infrastructure, execution parameters, campaign identifiers, and other operational details.
- Newly discovered intelligence can strengthen future reputation and detection decisions, including in offline and air-gapped environments.
- Aether becomes more than a file verdict source. Each investigation can generate intelligence that supports future detection and response.

## [Dynamic Analysis & Emulation Data Visualization](/docs/filescan/3.2.0/datasheet/the-new-metadefender-aether-user-interface-design-explained#dynamic-analysis--emulation-data-visualization)

#### [What changed](/docs/filescan/3.2.0/datasheet/the-new-metadefender-aether-user-interface-design-explained#what-changed)

- **Adaptive Sandbox now powers Layer 3: Dynamic Analysis** in the five-layer Aether pipeline.
- Runtime execution is presented through a simplified process and behavioral view rather than raw VM activity.
- Processes, file activity, network behavior, and other runtime evidence are summarized for faster interpretation.
- MetaDefender Aether 3.2 expands PE emulation with a **configurable virtual file system**, allowing samples to interact with expected files and paths during analysis.

#### [Why this matters](/docs/filescan/3.2.0/datasheet/the-new-metadefender-aether-user-interface-design-explained#why-this-matters)

- Analysts can quickly understand what happened during execution without working through unnecessary environment noise.
- Instruction-level emulation helps reveal malware that uses anti-VM checks, delayed execution, malformed structures, or environmental conditions to avoid traditional sandbox analysis.
- The configurable virtual file system helps expose malware whose execution depends on a particular file, path, or resource being present.
- Analysts gain more control when investigating environment-dependent malware while retaining the speed and scalability of emulation-based dynamic analysis.

## [File Details Panel](/docs/filescan/3.2.0/datasheet/the-new-metadefender-aether-user-interface-design-explained#file-details-panel)

#### [What changed](/docs/filescan/3.2.0/datasheet/the-new-metadefender-aether-user-interface-design-explained#what-changed)

- File metadata including entropy, size, magic information, strings, extracted files, and other structural details is consolidated.
- Extraction counts make it easier to identify files that unpack, generate, download, or contain additional components.
- Attribution can be evaluated separately for extracted and downloaded files rather than treating the entire execution chain as a single object.

#### [Why this matters](/docs/filescan/3.2.0/datasheet/the-new-metadefender-aether-user-interface-design-explained#why-this-matters)

- Analysts can quickly assess packing, obfuscation, structural anomalies, and file complexity.
- Extracted components can be investigated independently to determine their role in a multi-stage attack.
- This helps separate a seemingly benign delivery mechanism from a malicious loader or second-stage payload.

## [Tabbed Deep-Dive Architecture](/docs/filescan/3.2.0/datasheet/the-new-metadefender-aether-user-interface-design-explained#tabbed-deep-dive-architecture)

Detailed analysis is organized into focused views including:

- Threat Indicators
- Emulation Data
- Indicators of Compromise
- Similarity Search
- Disassembly Sections
- YARA Rules
- Extracted Strings and Files

#### [Why this matters](/docs/filescan/3.2.0/datasheet/the-new-metadefender-aether-user-interface-design-explained#why-this-matters)

The interface supports different levels of investigation without forcing every analyst through the same amount of detail.

A SOC analyst can establish the verdict, confidence, and highest-risk evidence quickly. A malware analyst can continue into emulation, disassembly, extracted files, strings, and YARA content.

Threat hunters can move into **Similarity Search** and related threat context to determine whether the sample belongs to a known family, variant, infrastructure cluster, or campaign.

This keeps the initial workflow concise without sacrificing the depth required for advanced investigation.

## [Threat Hunting & Threat Pattern Correlation](/docs/filescan/3.2.0/datasheet/the-new-metadefender-aether-user-interface-design-explained#threat-hunting--threat-pattern-correlation)

#### [What changed](/docs/filescan/3.2.0/datasheet/the-new-metadefender-aether-user-interface-design-explained#what-changed)

- Threat hunting is now explicitly represented as **Layer 5** of the Aether architecture.
- ML-powered Similarity Search and Threat Pattern Correlation connect analyzed samples with related malware, infrastructure, behaviors, and campaigns.
- Threat hunting is part of the same investigation workflow rather than a disconnected enrichment step.

#### [Why this matters](/docs/filescan/3.2.0/datasheet/the-new-metadefender-aether-user-interface-design-explained#why-this-matters)

- Zero-day detection does not end with determining whether one file is malicious.
- Analysts can determine whether a detection is an isolated sample, a modified version of known malware, or part of a broader attacker campaign.
- Similarity and pattern correlation make superficial malware changes less effective by revealing relationships that remain across variants.
- Investigation moves naturally from **file verdict to campaign context**.

## [Centralized Administration & Audit Visibility](/docs/filescan/3.2.0/datasheet/the-new-metadefender-aether-user-interface-design-explained#centralized-administration--audit-visibility)

#### [What changed](/docs/filescan/3.2.0/datasheet/the-new-metadefender-aether-user-interface-design-explained#what-changed)

MetaDefender Aether 3.2 moves **Syslog configuration into the Aether Admin Panel**, centralizing management that was previously handled through the broker configuration file.

Syslog coverage also expands beyond scan-result summaries to include:

- Authentication events
- Administrator setting changes
- Scan result summaries

#### [Why this matters](/docs/filescan/3.2.0/datasheet/the-new-metadefender-aether-user-interface-design-explained#why-this-matters)

- Administrators can manage logging through the product interface instead of maintaining configuration outside the UI.
- Security and audit teams gain better visibility into who accessed Aether, what administrative changes were made, and what analysis activity occurred.
- The expanded event trail strengthens operational oversight and supports regulated or high-security deployments.

**Important upgrade note:** existing Syslog settings are not migrated automatically and must be reconfigured in the Aether Admin Panel after upgrading to 3.2.

## [Bottom Line](/docs/filescan/3.2.0/datasheet/the-new-metadefender-aether-user-interface-design-explained#bottom-line)

MetaDefender Aether 3.2 makes the UI reflect how the product now detects and investigates zero-day threats.

It:

- **Visualizes the complete five-layer zero-day detection pipeline**
- **Introduces Predictive Alin AI Pre-Execution evidence directly into the analysis workflow**
- **Shows how each detection layer contributes to the consolidated file verdict**
- **Provides clearer, evidence-backed threat attribution**
- **Separates attribution across submitted, downloaded, and extracted files**
- **Makes Adaptive Sandbox behavior easier to investigate**
- **Connects individual file detections to related malware and campaigns**
- **Reduces analyst cognitive load and investigation time**
- **Expands administrative and audit visibility**

The result is not simply a redesigned report. It is a clearer representation of Aether’s detection model: **known-threat intelligence, Pre-Execution prediction, dynamic behavioral analysis, risk prioritization, and threat hunting working together in one analyst workflow.**

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
