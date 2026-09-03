<!-- source: https://www.opswat.com/docs/filescan/datasheet/layer-2---static-analysis -->

# Layer 2 - Static Analysis

## [Predict Unknown Threats Before Execution](/docs/filescan/datasheet/layer-2---static-analysis#predict-unknown-threats-before-execution)

**Layer 2 adds AI-powered prediction between known-threat detection and dynamic analysis.**

After Layer 1 Threat Reputation identifies what is already known, **Predictive Alin AI** analyzes unresolved files Pre-Execution to determine whether they show the characteristics of malicious content, without relying on signatures or sandbox detonation.

Predictive Alin AI analyzes file structure, behavioral features, embedded objects, imports, payload characteristics, and other intrinsic signals using machine learning. This allows Aether to identify never-before-seen, low-prevalence, polymorphic, and structurally modified malware before it has a chance to execute.

### [At a Glance](/docs/filescan/datasheet/layer-2---static-analysis#at-a-glance)

- **Purpose:** Predict malicious intent Pre-Execution
- **Speed:** P90 50 ms | P99 under 100 ms
- **False positive rate:** As low as 0.1%
- **Execution required:** No
- **Connectivity:** Online or fully offline
- **Best for:** High-volume enterprise file workflows
- **Current file coverage:** PE, ELF, Mach-O, and PDF

## [Why Layer 2 Matters](/docs/filescan/datasheet/layer-2---static-analysis#why-layer-2-matters)

Signature-based detection is highly effective when a threat is already known. The challenge begins when an attacker changes the file faster than signatures and reputation intelligence can catch up.

Predictive Alin AI helps close that gap.

Instead of asking whether a file matches a known threat, Layer 2 asks a different question:

**Does this file look and behave structurally like something malicious, even if we have never seen it before?**

That gives Aether an additional decision point before execution. High-risk files can be identified earlier, while uncertain samples can continue to Layer 3 Adaptive Sandbox for deeper behavioral analysis.

The result is faster zero-day detection without forcing every unknown file through resource-intensive dynamic analysis.

## [Built for High-Volume File Flows](/docs/filescan/datasheet/layer-2---static-analysis#built-for-high-volume-file-flows)

Predictive Alin AI is designed for environments where file inspection must happen at operational speed.

Machine-learning verdicts are delivered in milliseconds, making Layer 2 suitable for security workflows such as:

- Managed file transfer
- Email and attachment inspection
- ICAP and secure gateway workflows
- File uploads and downloads
- Software and supply chain inspection
- Cloud and enterprise content flows
- Air-gapped and regulated environments

Predictive Alin AI runs alongside **MetaScan™ Multiscanning**, adding a predictive signal where traditional anti-malware engines may not yet have a signature or known reputation.

This allows organizations to strengthen zero-day detection without disrupting file velocity.

## [What Predictive Alin AI Is Designed to Detect](/docs/filescan/datasheet/layer-2---static-analysis#what-predictive-alin-ai-is-designed-to-detect)

Layer 2 is particularly valuable against malware that attempts to evade known-threat detection through modification rather than completely new attack techniques.

Predictive Alin AI helps identify:

- Previously unseen malware
- Low-prevalence threats
- Polymorphic malware variants
- Structurally modified executables
- Obfuscated samples
- Suspicious embedded objects and payload characteristics
- Threats not yet represented in traditional signature catalogs

Because analysis takes place Pre-Execution, malicious files can be identified before they create runtime artifacts such as dropped files, registry modifications, process injection, or command-and-control connections.

## [How Layer 2 Fits Into the Aether Pipeline](/docs/filescan/datasheet/layer-2---static-analysis#how-layer-2-fits-into-the-aether-pipeline)

Aether uses progressively deeper analysis rather than treating every file the same.

**Layer 1: Threat Reputation**
Identifies known-good and known-bad files and infrastructure quickly.

**Layer 2: Static Analysis**
Predictive Alin AI evaluates unresolved files in milliseconds and predicts malicious intent without execution.

**Layer 3: Dynamic Analysis**
Files requiring deeper confirmation move to Adaptive Sandbox, where instruction-level emulation exposes actual runtime behavior.

**Layer 4: Threat Scoring**
Evidence from reputation, predictive analysis, and dynamic behavior is correlated into a confidence-based risk score.

**Layer 5: Threat Hunting**
Similarity Search and Threat Pattern Correlation connect detections to related malware, infrastructure, variants, and campaigns.

This architecture allows Aether to **analyze smarter instead of simply analyzing more**.

## [A Zero-Day Learning Loop](/docs/filescan/datasheet/layer-2---static-analysis#a-zero-day-learning-loop)

Predictive Alin AI does not operate as a static machine-learning model.

When Layer 3 Adaptive Sandbox confirms new zero-day malware, those discoveries can be used to retrain Predictive Alin AI and strengthen future Pre-Execution detection.

This creates a continuous learning cycle:

**Predict → Analyze → Confirm → Retrain → Predict Earlier**

A threat that requires dynamic analysis today can help Aether recognize related malicious characteristics earlier tomorrow.

Layer 3 therefore provides more than behavioral confirmation. Its sandbox-confirmed zero-day discoveries help improve the predictive intelligence used by Layer 2.

## [Supported Scope](/docs/filescan/datasheet/layer-2---static-analysis#supported-scope)

Predictive Alin AI currently supports:

### [Executable Formats](/docs/filescan/datasheet/layer-2---static-analysis#executable-formats)

- **PE** for Windows
- **ELF** for Linux and Unix environments
- **Mach-O** for macOS and Apple platforms

### [Productivity Formats](/docs/filescan/datasheet/layer-2---static-analysis#productivity-formats)

- **PDF**

Predictive Alin AI is available across MetaDefender environments and supports both connected and offline deployment models.

## [The Role of Layer 2](/docs/filescan/datasheet/layer-2---static-analysis#the-role-of-layer-2)

Layer 1 identifies what Aether already knows.

**Layer 2 predicts what may be malicious before it executes.**

Layer 3 then proves what unresolved threats actually do.

By placing Predictive Alin AI between reputation and dynamic analysis, MetaDefender Aether can stop more zero-day threats earlier, reduce unnecessary sandbox demand, and maintain the speed required for enterprise-scale file security.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
