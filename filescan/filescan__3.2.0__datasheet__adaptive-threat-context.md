<!-- source: https://www.opswat.com/docs/filescan/3.2.0/datasheet/adaptive-threat-context -->

# Adaptive Threat Context

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**Bridging the Gap Between Traditional Sandboxes and Reliable Threat Detection**

Sandboxes were originally designed to provide detailed behavioral insights requiring expert analysis, not to replicate traditional antivirus (AV) engine use cases. Historically, sandboxes lacked contextual information about analyzed files, leading to higher false positive rates. Behaviors commonly associated with malware, such as code injection, process manipulation, or network communication, can also occur in legitimate applications, making definitive conclusions challenging.

**MetaDefender Aether addresses this gap with Adaptive Threat Indicators**

Unlike traditional sandboxes, MetaDefender Aether goes beyond surface-level behavioral analysis. Its adaptive threat indicators assess whether specific behaviors and indicators are genuinely malicious for the file type and its extracted contextual elements. This context-aware approach reduces false positives, increases detection accuracy, and enhances the reliability of final verdicts.

### [Use Case Example: Reducing False Positives with Adaptive Context](/docs/filescan/3.2.0/datasheet/adaptive-threat-context#use-case-example-reducing-false-positives-with-adaptive-context)

Installer executables often exhibit behaviors similar to malware, such as creating processes or writing new executables. Traditionally, digital signatures help verify legitimacy, but this isn't always possible in air-gapped environments.

MetaDefender Aether's adaptive context feature automatically downgrades threat indicators when it identifies signed installers, even without external validation. This reduces false positives, particularly for PE files related to Windows API calls, with future support planned for more file types.

**Real scenario:**

Chrome's installer is digitally signed by Google LLC, considered as a `trusted` vendor. In a normal environment, this file would be directly flagged as `benign` because it was signed by a `valid` and whitelisted certificate ([see public report](https://www.filescan.io/uploads/6716232771846600385306b2/reports/c9014c94-3889-4dd8-b88c-dedc4102771d/overview)). However in air-gapped environment we are not able to perform that validation and without adaptive context the file would have been flagged as malicious due to its capabilities, generating a false positive. The screenshot comes from a report of a sandbox scan for a legitimate `Chrome` installer in air-gapped environment.

False positive for the Chrome executable in an air-gapped environment.

With certificate validation unavailable in an air-gapped environment, the legitimate installer triggers a false positive. However, with adaptive threat context enabled, the same file is correctly identified as benign. The report data remains unchanged, but the verdict is adjusted based on the file’s contextual information.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
