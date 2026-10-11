<!-- source: https://www.opswat.com/docs/filescan/release-notes/release-notes-v320 -->

# Release Notes for v3.2.0

View as Markdown Ask ChatGPT about this page Ask Claude about this page
### Date: 31st July 2026

Warning

**Upgrading directly** from versions prior to 2.5.1 to 3.2.0 is **not possible!**

**Recommended Upgrade Path:** First upgrade to **2.5.1**, then install **3.2.0**.

## MetaDefender Aether™ 3.2.0 (including MetaDefender Sandbox™ capabilities)

[MetaDefender Aether](https://www.opswat.com/products/metadefender/aether) 3.2.0 expands the solution into a five-layer Zero-Day Detection pipeline and gives analysts clearer visibility into how each layer contributes to a file verdict. The release adds [Predictive Alin AI](https://www.opswat.com/technologies/predictive-alin-ai) for Pre-Execution Static Analysis, strengthens threat attribution, improves behavioral analysis of executable malware, expands detection for emerging evasion techniques, and provides broader operational logging.

## **What’s new**

**Five-Layer Zero-Day Detection with Predictive Alin AI**

MetaDefender Aether now includes Predictive Alin AI as the new Layer 2 for Static Analysis, expanding the threat processing pipeline from four layers to five:

1. **Threat Reputation:** Checks files and infrastructure against known intelligence

2. **Static Analysis:** Uses Predictive Alin AI to assess malicious intent before execution

3. **Dynamic Analysis:** Emulates suspicious and unresolved files to expose runtime behavior

4. **Threat Scoring:** Correlates evidence into a confidence-based risk score and verdict

5. **Threat Hunting:** Connects samples to related malware families, infrastructure, and campaigns

Image Description: MetaDefender Aether’s five-layer Zero-Day Detection pipeline applies progressively deeper analysis while feeding newly discovered intelligence back into earlier detection layers.

**Predictive Alin AI** assesses files for malicious intent Pre-Execution, before emulation or sandbox analysis. This introduces an earlier, model-based decision point that accelerates triage and helps security teams focus deeper Dynamic Analysis on files that require further investigation.

The new layer strengthens the full Aether pipeline without replacing any existing detection stage. Reputation identifies known indicators, Predictive Alin AI assesses unknown files statically, Dynamic Analysis exposes runtime behavior, Threat Scoring consolidates the evidence, and Threat Hunting connects the file to related threats and campaigns.

**Clearer Evidence Across the Aether Processing Engine**

Scan results now present a numbered, sequential view of each Aether layer that analyzed the file, including reputation, static analysis, dynamic analysis, threat scoring, and threat hunting.

Each layer’s contribution is displayed directly within the result, making it easier for analysts to understand how the final verdict was reached.

Predictive Alin AI results are shown alongside the multiscanning verdict, allowing analysts to compare signature-based findings with the model-based prediction for the same sample.

Image Description: MetaDefender Aether presents each layer’s contribution in sequence, giving analysts a clear evidence trail behind the final verdict.

**More Actionable Threat Attribution**

Threat attribution now provides clearer, evidence-backed classifications in place of ambiguous or heavily qualified tags.

The improved attribution model gives analysts more direct information about a threat’s likely identity and intent. This reduces the time spent interpreting results, supports faster investigation decisions, and increases confidence in downstream response.

Image Description: MetaDefender Aether calculates threat attribution independently for the submitted file and for files downloaded or extracted during analysis.

**More Complete Executable Behavior Analysis**

Aether’s Portable Executable (PE) analysis now supports a configurable virtual file system, allowing samples to interact with the files and paths they expect during emulation.

This enables malware with file-system dependencies to follow more of its intended execution flow, giving analysts a more complete view of file activity, payload behavior, and related indicators of compromise. It also helps reduce the risk that environment-dependent malicious behavior remains hidden during analysis.

Analysts can define files expected by a sample, providing greater control when investigating malware that relies on specific file or path conditions.

**Detection for Emerging Evasion Techniques**

MetaDefender Aether 3.2.0 adds detection coverage for techniques designed to conceal attacker infrastructure or interfere with automated analysis.

New coverage includes:

- **EtherHiding**, which conceals threat actor infrastructure or malicious instructions within blockchain transactions.

- **Intentionally malformed .NET assemblies**, which use manipulated file structures to disrupt or evade automated analysis tools.

These additions help analysts identify threats that attempt to hide behind decentralized services or structural manipulation.

Image Description: MetaDefender Aether extracts the smart-contract address, JSON-RPC call, and blockchain endpoints used by an EtherHiding sample.

**More Accurate Remote Template Injection Detection**

Remote template injection analysis now uses an improved link detection and URL classification pipeline to distinguish genuine injection attempts from ordinary embedded links more accurately.

The updated detection:

- Corrects two indicators that could classify legitimate URLs as malicious.

- Detects malicious IP links concealed through octal encoding.

- Improves differentiation between benign embedded links and suspicious remote template activity.

These changes reduce false positives caused by legitimate URLs while preserving coverage for genuine and obfuscated remote template injection attempts.

---

## **Improvements**

**Centralized and Expanded Syslog Management**

Syslog configuration has moved from the broker configuration file to the Aether Admin Panel, providing a more accessible and centralized way to manage logging settings.

Existing syslog settings are not migrated automatically and must be reconfigured in the Admin Panel. See the [CEF Syslog Feedback](/configuration/cef-syslog-feedback) documentation for migration details.

Syslog coverage has also been expanded to include:

- Authentication events

- Administrator setting changes

- Scan result summaries

This gives security and audit teams greater visibility into user activity, configuration changes, and file analysis results.

**Broader Detection and Intelligence Coverage**

MetaDefender Aether 3.2.0 expands detection and threat intelligence coverage across several additional areas:

- New detection engineering for wiper malware.

- OCR-based CAPTCHA identification, including obfuscated but visually rendered fake CAPTCHAs used in ClickFix attacks.

- New malware configuration extractors for PrivateLoader and Quasar RAT.

- Expanded IOC coverage in the local Reputation database.

Together, these improvements give analysts broader visibility into destructive malware, social-engineering techniques, malware infrastructure, and threats operating in connected, offline, or air-gapped environments.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
