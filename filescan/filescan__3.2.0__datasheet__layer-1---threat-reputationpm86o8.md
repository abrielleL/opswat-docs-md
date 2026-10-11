<!-- source: https://www.opswat.com/docs/filescan/3.2.0/datasheet/layer-1---threat-reputationpm86o8 -->

# Layer 3 - Dynamic Analysis

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Force Hidden Threats to Reveal Themselves](/docs/filescan/3.2.0/datasheet/layer-1---threat-reputationpm86o8#force-hidden-threats-to-reveal-themselves)

Some threats cannot be confidently identified from reputation or Pre-Execution analysis alone. When a suspicious or unresolved file requires deeper investigation, **Layer 3 uses OPSWAT Adaptive Sandbox to expose what the file actually does when it executes.**

Adaptive Sandbox uses **instruction-level emulation** rather than relying on a traditional virtual machine. It simulates CPU, operating system, application, and script behavior while controlling execution paths, helping force evasive malware to reveal activity it was designed to hide.

This enables Aether to uncover runtime behavior including:

- Loader chains and multi-stage payloads
- Dropped and generated files
- Process injection and persistence activity
- Obfuscated scripts and shellcode
- Network and command-and-control activity
- Memory-only payloads
- Packers, stagers, and droppers
- Anti-analysis and sandbox-evasion techniques
- Malware configuration data and behavioral IOCs

### [Why Dynamic Analysis Is Layer 3](/docs/filescan/3.2.0/datasheet/layer-1---threat-reputationpm86o8#why-dynamic-analysis-is-layer-3)

Aether does not send every file directly to a sandbox.

**Layer 1: Threat Reputation** quickly resolves known threats.

**Layer 2: Predictive Alin AI** analyzes suspicious files Pre-Execution and predicts malicious intent without requiring detonation.

Files that remain uncertain or require deeper behavioral confirmation can then move to **Layer 3: Dynamic Analysis**.

This staged approach preserves file velocity while reserving deeper, more resource-intensive analysis for the files that genuinely need it.

### [Built to Defeat Evasive Malware](/docs/filescan/3.2.0/datasheet/layer-1---threat-reputationpm86o8#built-to-defeat-evasive-malware)

Modern malware often tries to recognize analysis environments before revealing its true behavior. It may delay execution, check geolocation or system characteristics, look for signs of virtualization, or require specific environmental conditions before activating.

Adaptive Sandbox is designed to overcome these tactics by manipulating execution at the instruction level and exploring alternate code paths.

Instead of waiting for malware to cooperate, Aether actively works to **force hidden behavior into view**.

### [Dynamic Analysis Creates New Intelligence](/docs/filescan/3.2.0/datasheet/layer-1---threat-reputationpm86o8#dynamic-analysis-creates-new-intelligence)

Layer 3 does more than determine whether one file is malicious.

Adaptive Sandbox extracts new behavioral evidence and Indicators of Compromise such as hashes, URLs, domains, IP addresses, dropped files, registry activity, and malware configuration data.

Those discoveries strengthen the wider Aether pipeline:

- **Newly discovered IOCs can strengthen Layer 1 Threat Reputation**, allowing future encounters with the same indicators to be identified earlier.
- **Sandbox-confirmed zero-day discoveries contribute to the learning loop for Layer 2 Predictive Alin AI**, helping improve future Pre-Execution prediction.
- **Behavioral evidence feeds Layer 4 Threat Scoring**, helping determine risk and produce an actionable verdict.
- **Extracted behaviors, IOCs, and malware relationships support Layer 5 Threat Hunting**, connecting individual detections to related variants, infrastructure, and campaigns.

Layer 3 therefore turns an unknown file into reusable threat intelligence, making Aether stronger beyond the initial analysis.

### [Adaptive Sandbox at a Glance](/docs/filescan/3.2.0/datasheet/layer-1---threat-reputationpm86o8#adaptive-sandbox-at-a-glance)

**50K+** analyses per day per server
**120+** supported file types
**~10 seconds** fast-pass analysis
**1,000+** behavioral indicators

Dynamic Analysis provides the behavioral depth Aether needs to confirm what static analysis cannot, expose evasive malware, and convert each new discovery into intelligence that strengthens future detection.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
