<!-- source: https://www.opswat.com/docs/filescan/3.2.0/datasheet/zero-day-threat-identification -->

# Zero-Day Threat Identification

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [What is Zero-Day Malware?](/docs/filescan/3.2.0/datasheet/zero-day-threat-identification#what-is-zero-day-malware)

Zero-day malware is malicious software that is **not yet known** to security vendors. It has **no signatures**, **no reputation**, and often bypasses traditional detection engines.

Modern malware is designed to evade static defenses. It uses techniques such as environment checks, execution delays, and sandbox awareness to hide its malicious intent. These threats are built to exploit gaps in traditional tools before signatures or heuristics are updated.

Aether focuses on what matters most: **behavior and attack patterns**, using **advanced emulation** that exposes malicious logic without giving the malware a real environment to adapt to or escape from. This allows Aether to reliably identify previously unseen malware while avoiding common sandbox evasion techniques.

Zero-day tagging helps customers proactively detect and hunt unknown threats that bypass reputation checks and up-to-date AV signatures, providing early and clear visibility into emerging malware campaigns before they spread—without relying on signatures or reputation alone.

## [Requirements to Enable Zero-Day Tagging](/docs/filescan/3.2.0/datasheet/zero-day-threat-identification#requirements-to-enable-zero-day-tagging)

To accurately tag a file as zero-day, Aether needs to confirm that the sample is **truly unknown** at analysis time. For this reason, AV multi-scanning is required.

You must integrate Aether with either **MetaDefender Core** or **MetaDefender Cloud**. This integration allows Aether to submit the file for scanning across multiple AV engines and verify that **there is no detection** when the analysis is performed.

Zero-day tagging is only applied when strong malicious behavior is observed and reputation data confirms the sample is previously unseen. This prevents mislabeling known or commodity malware as zero-day.

## [Showcase: Early Detection in a Real-World Phishing Campaign](/docs/filescan/3.2.0/datasheet/zero-day-threat-identification#showcase-early-detection-in-a-real-world-phishing-campaign)

In this campaign, attackers used a phishing email to deliver a multi-stage attack chain designed to evade traditional defenses. The email contained a JavaScript attachment that appeared benign but acted as the real entry point of the attack.

Through emulation, Aether removed the JavaScript obfuscation and revealed its true behavior. The script executed PowerShell code that downloaded a seemingly harmless PNG file, that apart of the image data, it embedded a Base64-encoded .NET loader.

Aether emulated the PowerShell stage and exposed how the loader was extracted, decoded, and executed. At the time of delivery, scripts and loader had no reputation and no AV detections, allowing it to bypass reputation-based and signature-based controls.

This detection provided early and clear visibility into the campaign before AV engines reacted, enabling defenders to understand the complete infection chain and proactively hunt for related samples and infrastructure.

This example shows how zero-day tagging in Aether exposes real threats hidden behind clean reputation, allowing security teams to detect and respond to new malware campaigns at their earliest stage.

Link to the sample

<https://www.filescan.io/uploads/696895793827c9e1249f3112/reports/be200eab-be4e-43dc-a7f6-7ebe49a323af/emulation_data>

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
