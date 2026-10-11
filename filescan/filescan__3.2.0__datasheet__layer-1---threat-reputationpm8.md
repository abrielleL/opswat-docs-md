<!-- source: https://www.opswat.com/docs/filescan/3.2.0/datasheet/layer-1---threat-reputationpm8 -->

# Layer 4 - Threat Scoring

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Prioritize What Matters Most](/docs/filescan/3.2.0/datasheet/layer-1---threat-reputationpm8#prioritize-what-matters-most)

**Layer 4 turns evidence from across the Aether detection pipeline into an actionable, confidence-based risk verdict.**

By the time a file reaches Threat Scoring, Aether may already know its reputation, have a Pre-Execution prediction from Predictive Alin AI, and have detailed runtime evidence from Adaptive Sandbox.

Threat Scoring brings those signals together.

Instead of forcing analysts to interpret reputation lookups, machine-learning predictions, behavioral indicators, and sandbox results independently, Layer 4 correlates the evidence to determine **how strongly the file demonstrates malicious intent and how urgently it should be handled**.

The result is clearer prioritization, less alert noise, and faster security decisions.

## [At a Glance](/docs/filescan/3.2.0/datasheet/layer-1---threat-reputationpm8#at-a-glance)

- **Purpose:** Turn multi-layer evidence into an actionable risk verdict
- **Inputs:** Threat Reputation, Predictive Alin AI, and Adaptive Sandbox findings
- **Evaluates:** File structure, runtime behavior, malicious techniques, and threat context
- **Output:** Confidence-based risk scoring and verdict
- **Best for:** SOC triage, automated policy enforcement, and high-volume file security
- **Pipeline role:** Convert detection evidence into a decision before Layer 5 Threat Hunting adds broader campaign context

## [Why Layer 4 Matters](/docs/filescan/3.2.0/datasheet/layer-1---threat-reputationpm8#why-layer-4-matters)

Finding suspicious behavior is not the same as knowing how much it matters.

A file might contain an unusual script, contact an unfamiliar domain, use obfuscation, or exhibit one suspicious execution pattern. Any individual signal may be insufficient to make a confident decision.

Threat Scoring looks at the evidence **together**.

Aether correlates what was known before execution, what Predictive Alin AI identified from the file itself, and what Adaptive Sandbox observed during runtime.

This allows multiple weak or ambiguous signals to become meaningful when they appear as part of a broader malicious pattern.

Rather than giving analysts another list of findings to investigate, Layer 4 helps answer:

**How much risk does the combined evidence actually represent?**

## [What Threat Scoring Evaluates](/docs/filescan/3.2.0/datasheet/layer-1---threat-reputationpm8#what-threat-scoring-evaluates)

Threat Scoring considers evidence across file structure, execution behavior, and threat intelligence, including:

- Malicious execution flows
- Loader and injection patterns
- Script obfuscation
- Persistence techniques
- Command-and-control behavior
- Malware family characteristics
- Behavioral threat indicators
- MITRE ATT&CK mappings
- Malware Behavior Catalog mappings
- Relationships between static file structure and observed runtime behavior

The value comes from correlation. A single suspicious characteristic may not determine the verdict, but several related indicators can expose malicious intent with much greater confidence.

## [How Layer 4 Fits Into the Aether Pipeline](/docs/filescan/3.2.0/datasheet/layer-1---threat-reputationpm8#how-layer-4-fits-into-the-aether-pipeline)

Each Aether layer answers a different question.

**Layer 1: Threat Reputation**
Do we already know this threat?

**Layer 2: Static Analysis**
Does Predictive Alin AI detect signs of malicious intent Pre-Execution?

**Layer 3: Dynamic Analysis**
What does the file actually do when its behavior is exposed?

**Layer 4: Threat Scoring**
**What does all of that evidence mean, and how risky is the file?**

**Layer 5: Threat Hunting**
What other malware, infrastructure, variants, or campaigns is the threat connected to?

Layer 4 is the point where detection evidence becomes a security decision.

## [From Signals to a Consolidated Verdict](/docs/filescan/3.2.0/datasheet/layer-1---threat-reputationpm8#from-signals-to-a-consolidated-verdict)

Security teams often have no shortage of detection data. The harder problem is deciding which signals justify action.

Threat Scoring reduces that burden by correlating evidence across Aether rather than treating each detection technology as an independent source of truth.

This helps security teams:

- Prioritize the highest-risk files first
- Reduce time spent investigating low-value signals
- Reduce false positives and alert noise
- Apply more consistent allow, block, or quarantine decisions
- Feed clearer verdicts into automated security workflows
- Give analysts the supporting evidence behind the decision

For high-volume environments, this matters as much as detection efficacy. A security system that identifies suspicious activity but cannot distinguish urgency simply moves the bottleneck to the analyst.

## [Detect Malicious Intent Across Multiple Signals](/docs/filescan/3.2.0/datasheet/layer-1---threat-reputationpm8#detect-malicious-intent-across-multiple-signals)

Modern malware frequently changes superficial characteristics to avoid detection.

Attackers can modify hashes, repackage executables, alter scripts, or make small changes to a payload without fundamentally changing how the attack operates.

Threat Scoring makes those minor modifications less effective because it evaluates **relationships across structure, behavior, and execution technique**, rather than relying on a single indicator.

Repeated loader behavior, injection patterns, persistence mechanisms, C2 activity, and other malicious techniques can still contribute to a high-risk verdict even when individual file characteristics change.

## [How Layer 4 Raises the Cost for Attackers](/docs/filescan/3.2.0/datasheet/layer-1---threat-reputationpm8#how-layer-4-raises-the-cost-for-attackers)

Threat Scoring operates higher on the **Pyramid of Pain**, where detection begins to focus on attacker tools and TTPs rather than easily replaced indicators.

By correlating malicious behaviors, Layer 4:

- Makes reused execution patterns easier to recognize
- Exposes malicious intent across multiple weaker signals
- Reduces the effectiveness of simple payload modifications
- Forces attackers to change how their tools behave, not just how their files look
- Makes evasion increasingly dependent on redesigning behavioral techniques and attack logic

Changing a hash is easy. Changing how an attack works is considerably harder.

## [The Role of Layer 4](/docs/filescan/3.2.0/datasheet/layer-1---threat-reputationpm8#the-role-of-layer-4)

Layers 1 through 3 generate evidence.

**Layer 4 decides what that evidence means.**

Threat Scoring converts reputation intelligence, Pre-Execution AI predictions, and observed runtime behavior into a confidence-based risk verdict that analysts and automated systems can act on.

That gives Aether a critical capability beyond simply finding suspicious activity:

**It helps security teams know what actually deserves their attention.**

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
