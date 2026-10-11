<!-- source: https://www.opswat.com/docs/filescan/3.2.0/release-notes/release-notes-v190 -->

# Release Notes for v1.9.0

View as Markdown Ask ChatGPT about this page Ask Claude about this page

---

## [Date: 14 September, 2023](/docs/filescan/3.2.0/release-notes/release-notes-v190#date-14-september-2023)

Warning

This version is not suitable for a clean installation due to breaking changes introduced in Docker 25. Please **use version 1.9.2 or later** for clean installations!

Added:

- New License Management interface added to the Web UI: [License Activation](/docs/filescan/3.2.0/installation/license-activation)
- Automatically generate an executive summary with OpenAI’s GPT large language model (LLM): [ChatGPT (Executive Summary)](/docs/filescan/3.2.0/integrations/open-ai-executive-summary)

- Support different retention periods for different verdicts
- The /api/scan/file API endpoint accepts base64-encoded file content in the JSON request body
- Support filenames with various unicode characters
- Support unpacking of 64-bit executables
- Integrated "[Detect It Easy](https://github.com/horsicq/Detect-It-Easy)" to identify characteristics of executable files related to compilation and packing
- Support malicious documents embedded in PDF files hidden as ActiveMime objects in MHTML format
- New threat indicators to detect the WikiLoader malware family (Microsoft Office files)
- Detection and extraction of embedded RTF files in Office documents, as described in [CVE-2023-36884](https://msrc.microsoft.com/update-guide/vulnerability/CVE-2023-36884)
- Detect XOR decoding routine near the executable entry point
- Enhance Threat Indicator for [Mavinject](https://lolbas-project.github.io/lolbas/Binaries/Mavinject/)

Adversaries may abuse mavinject.exe to proxy execution of malicious code. Mavinject.exe is the Microsoft Application Virtualization Injector, a Windows utility that can inject code into external processes as part of Microsoft Application Virtualization (App-V) See example and new threat indicator.
<https://attack.mitre.org/techniques/T1218/013/>

Changed:

- Faster scan processing time
- Enhanced logging to provide more relevant information
- Improved VBA emulation to support additional features
- Refined emulation error handling for higher success ratio
- Enhanced threat indicators and verdict calculation
- Improved string analysis
- Optimized disk space utilization & clean-up mechanisms
- Enhanced MITRE mapping for user clarity
- Enhanced flagging for suspicious imported APIs and modules

Fixed:

- Added version locks for dependencies in various emulator components
- Improved application security
- Incorrect detection of zip bombs
- Incorrect condition for the emulation of ActiveMime files
- Improved processing of large sample files

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
