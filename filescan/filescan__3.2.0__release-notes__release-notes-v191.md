<!-- source: https://www.opswat.com/docs/filescan/3.2.0/release-notes/release-notes-v191 -->

# Release Notes for v1.9.1

View as Markdown Ask ChatGPT about this page Ask Claude about this page

---

## [Date: 22 November, 2023](/docs/filescan/3.2.0/release-notes/release-notes-v191#date-22-november-2023)

Warning

This version is not suitable for a clean installation due to breaking changes introduced in Docker 25. Please **use version 1.9.2 or later** for clean installations!

**Added:**

- Integrated OPSWAT Central Management (OCM) into the Web UI: [OCM Registration](/docs/filescan/3.2.0/installation/ocm-registration)

- Automatic email notifications with the original email sender when scanning .eml files: Email Notifications
- Detected and flagged .exe suffixes in URLs to highlight potential downloads of PEs
- Displayed additional Crypto Wallet Indicators of Compromise (IOCs) in scan reports
- Displayed the product's current version in the Web UI footer
- Showcased top malware families in the Trends page
- Identified clickable and non-clickable URLs from documents
- Implemented disassembly of relevant functions in 64-bit executables
- Implemented a parser for .ics files (vCalendar), including the extraction of attached files
- Extended support for JavaScript emulation in Adobe PDF files
- Enabled threat indicator monitoring and statistics support
- Enabled support for all file types when generating an executive summary using OpenAI’s GPT large language model (LLM): [ChatGPT (Executive Summary)](/docs/filescan/3.2.0/integrations/open-ai-executive-summary)

**Changed:**

- Revamped the processing of threat indicators and the methodology behind verdict calculations
- Augmented documentation and introduced an automated system check to verify the utilization of CPUs with AVX support. [Technical Requirements](/docs/filescan/3.2.0/installation/technical-requirements)
- Expanded malware configuration extractors to encompass the latest and most pertinent threats

- Implemented the generation of randomized internal passwords for fsBroker and fsTransform components during the installation process
- Upgraded the detection capabilities to more effectively identify malicious office documents
- Improved the extraction process for Crypto Wallets to ensure a more comprehensive and accurate output
- Fine-tuned the extraction of overlay elements in PDF files for increased precision
- Strengthened the system's capability to handle malformed Microsoft Office documents
- Enhanced heuristic domain identification to minimize false positives
- Improved the identification and parsing of VBA content within PDF files
- Enhanced memory management within the scan engine to boost overall efficiency
- Improved parsing for .NET executables for more accurate analysis
- Enhanced parsing for YARA rules to achieve greater precision in matching
- Improved the reporting mechanism for identifying and handling invalid signatures during certificate validation
- Elevated the capabilities of VBA and PowerShell emulation for heightened security measures
- Incorporated confidence values in phishing detections, influencing the final verdict for URL rendering
- Updated the "Download IOCs" button to selectively download items solely from the current page
- Refreshed the internal FSIO fuzzy hash blocklist to encompass emerging threat clusters

**Fixed:**

- Enhanced Application Security measures
- Improved health check functionality in scan job queues, automatically restarting when required
- Eliminated weak third-party YARA rules to prevent False Positives

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
