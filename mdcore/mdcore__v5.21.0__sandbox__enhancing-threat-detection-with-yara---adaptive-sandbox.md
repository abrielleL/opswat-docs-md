<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/sandbox/enhancing-threat-detection-with-yara---adaptive-sandbox -->

# Enhancing Threat Detection with YARA & MetaDefender Aether for Core (Adaptive Sandbox)

This article applies to MetaDefender Core 5.14.0 (or higher) and Adaptive Sandbox 2.3.0 (or higher) releases deployed on Windows or Linux systems.

Integrating YARA Scanning with Sandboxing provides a layered approach to threat detection, combining rule-based static analysis for rapid identification of known threats with dynamic sandbox analysis for uncovering advanced, evasive, or zero-day malware.

- **YARA scanning** provides rule-based pattern matching to detect known malware signatures, suspicious behaviors, or file characteristics. It acts as a fast, lightweight pre-filter for identifying potentially malicious files
- **Layered detection**: YARA rules can be tailored to flag specific threat indicators (e.g., obfuscated scripts, known malware families), while sandboxing validates and expands on these findings through behavioral analysis.
- **Improved detection accuracy**: Combining static (YARA) and dynamic (sandbox) techniques reduces false positives and enhances detection of sophisticated threats that may evade one method alone.
- **YARA as a trigger for sandboxing** enables a more efficient workflow: files that match YARA rules are escalated for deeper sandbox analysis, while clean files bypass the sandbox, reducing resource consumption and analysis time.

#### [Why this Matters](/docs/mdcore/v5.21.0/sandbox/enhancing-threat-detection-with-yara---adaptive-sandbox#why-this-matters)

YARA rules are powerful for identifying specific patterns and characteristics of malware. By using YARA, you can detect known threats and suspicious behaviors within files or processes. This initial detection helps in identifying potential attack vectors that might be missed by traditional antivirus solutions.

Combining YARA detection with Sandbox analysis improves the accuracy of threat identification. YARA can flag potential threats based on patterns, while the Sandbox can confirm whether the flagged items exhibit malicious behavior, reducing false positives.

## [Setup Adaptive Sandbox YARA trigger](/docs/mdcore/v5.21.0/sandbox/enhancing-threat-detection-with-yara---adaptive-sandbox#setup-adaptive-sandbox-yara-trigger)

Under **Workflow Management -> Workflows -> (Name of the workflow) -> Adaptive Sandbox -> Advanced configuration,** there is an option "Enable for Adaptive Sandbox YARA rules":

## [Key Takeaway](/docs/mdcore/v5.21.0/sandbox/enhancing-threat-detection-with-yara---adaptive-sandbox#key-takeaway)

Identifying attack vectors with YARA and triggering Sandbox scans based on the results offers a comprehensive approach that enhances threat detection and provides in-depth analysis. To build on this, refer to the [**Attack Vector Detection Coverage**](https://www.opswat.com/docs/mdcore/utilities-engines/attack-vector-detection-coverage) section to see the range of attack vectors the YARA engine can flag early in the threat path, creating an ideal trigger point for deeper Sandbox analysis. It gives a clearer view of how YARA-driven detection strengthens and streamlines the entire analysis workflow.
