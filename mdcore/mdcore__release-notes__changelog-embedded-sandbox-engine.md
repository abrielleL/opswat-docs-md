<!-- source: https://www.opswat.com/docs/mdcore/release-notes/changelog-embedded-sandbox-engine -->

# Embedded Engine

## [Known issues](/docs/mdcore/release-notes/changelog-embedded-sandbox-engine#known-issues)

| Issue | Solution |
| --- | --- |
| MSI certificate validation is not supported on Windows OS |  |

## [v3.0.0](/docs/mdcore/release-notes/changelog-embedded-sandbox-engine#v300)

Release date: 26/01/2026

| **New Features and Improvements** |
| --- |
| **What's new**  We are excited to announce the release of **MetaDefender Aether for Core v3.0.0.** With this update, users can now enable dynamic file analysis and behavioral threat detection directly within their Core environment—no additional infrastructure required.   - **Simplified and Enhanced OSINT Lookups** - OSINT lookups were simplified and local reputation results are now visible in the OSINT results as OFFLINE_REPUTATION - **Verdict Renaming** – Updated verdicts to provide clearer guidance on how to interpret analysis results and take appropriate actions based on potential threat levels - **E-PUB support** - Added support for EPUB files, to ensure broader compatibility with widely used e‑reading formats. - **IOC Skip List Migration** - Moved the IOC skip list (allow/blocklist) from the local application database to the separated detection database package to enable frequent updates - **Core Component Hardening** - Hardened core components with additional security safeguards to strengthen the overall defense posture. - **QR Code Detection Improvements** - Improved to allow the scanning of rendered images in documents and emails - **Batch File-Type Detection** - Enhanced to improve accuracy across complex payloads.   **Bug Fixes**   - **BAT Script Classification Fix** - Corrected file-type misclassification for obfuscated BAT scripts, eliminating related false positives.   **Threat Detection 2.0.0 Release Notes**  **MetaDefender Aether for Core supports independent updates to detection logic and threat intelligence**, enabling faster deployment of new protections and a more rapid response to emerging threats. The following updates have been delivered over the past several months.  **What's new**   - **Significant Enhancements to PE Installer Analysis** - Added deep static extraction and analysis for Windows installers: NSIS, Inno, InstallShield, Advanced Installer, Wise, WiX, InstallAnywhere, and Actual Installer. It now extracts prioritized embedded files, analyzes installer scripts, and scores custom installers heuristically. - **AI / ML Model Security Scanning** - Introduced security analysis for Machine Learning models, including multi-serialization parsing and deep static inspection to detect hidden malicious payloads before they impact AI workflows. - **Zero-Day Exploit Detection** - Added detection for recent Windows Explorer LNK vulnerabilities (CVE-2025-50154, CVE-2025-59214) that leak NTLM credentials without user interaction. Also, introduced detection for critical XXE exploitation in Apache Tika (CVE-2025-66516). - **Phishing Campaign Intelligence** - Introduced indicators for seasonal / opportunistic lures (holidays, global events). Improves campaign clustering and early phishing detection. - **Invisible String Obfuscation Detection** - It now detects *GlassWorm*-style obfuscation techniques by identifying invisible and deceptive code constructs used to evade analysis and enable silent execution. This includes detection of homoglyph characters, PUA (Private Use Area) Unicode characters, and hidden or non-printable whitespace that visually alters code without changing execution. - **Advanced Evasion Technique Detection** - Expanded detection for techniques used to evade automated analysis, including meaningless infinite loops, abuse of password-protected in-house macros, .NET PE constant protection and control-flow obfuscation, and deobfuscation of hexadecimal-encoded JavaScript. - **Expanded File Type & Archive Coverage** - Added support for VSIX files, CRX archives, and improved archive file filtering and prioritization. - **HTML Threats & Web Payload Extraction** - It now extracts hidden downloadable payloads from HTML href data blobs and improves detection for abused HTML capabilities (e.g., disabled context menu). - **Detection of IP logging and tracking services** - Added indicators to flag the presence of IP-logging URLs that may be abused by attackers to identify victim location, apply geofencing, or support other reconnaissance and targeting activities, improving visibility into early-stage attack workflows.   **Improvements**   - **Encrypted Documents** - Enhanced decryption for protected Office and PDF documents by introducing a multi-step password recovery with fallback logic for phishing-delivered encrypted files. - **Base64-Encoded Payload Extraction** - Added base64 decoding for dynamically created files during emulation. This improves visibility into malware that reconstructs payloads at runtime to bypass static analysis and hide secondary stages until execution. - **ClickFix Variant Detection** - Improved detection for new ClickFix variants that abuse hex-encoded URLs and msiexec execution. - **Email & Phishing Analysis Accuracy** - Improved EML parsing to correctly associate images with embedded URLs, support text-based attachments, and enhance call-to-action detection across multiple languages. - **Multi-Stage Infection Chain Visibility** - Improved emulation triggering for downloaded scripts, enabling full infection chain analysis when payloads are fetched from an external resource. - **Better Detection Precision & URL Noise Extraction Reduction** - Reduced false positives by refining encryption-related indicators shared by malware and legitimate installers, adapting string-detection heuristics for PE files.   **Bug Fixes**   - **MSI Extraction Reliability** - Fixed multiple issues causing missing or incomplete payload extraction from MSI installers. - **URL Redirection & Download Chain Handling** - Fixed missing redirected URLs, deduplicated download tasks, and added detection for delayed redirections. - **Indicator Stability & Engine Robustness** - Fixed unintended indicator triggers (including PDF-related), skipped unnecessary PE disassembly when packers are detected, and resolved multiple internal indicator bugs. - **Duplicate Tags** - Tags originating from multiple sources were being shown repeatedly in the UI. The fix ensures that tags are properly deduplicated so each one appears only once. |

## [v2.5.1](/docs/mdcore/release-notes/changelog-embedded-sandbox-engine#v251)

Release date: 11/20/2025

| **New Features and Improvements** |
| --- |
| **Improvements**   - **Stability & Security -** Updated core dependencies to enhance performance and security.   **Bug Fixes**   - **Fixed zlib support** – zlib files are now correctly processed by the Archive Engine instead of the Adaptive Sandbox, ensuring proper handling and improved efficiency. |

## [v2.5.0](/docs/mdcore/release-notes/changelog-embedded-sandbox-engine#v250)

Release date: 10/30/2025

| **New Features and Improvements** |
| --- |
| **What's New**   - **Periodic Threat Detection Updates -** MetaDefender Sandbox now supports independent updates to detection logic and threat indicators, enabling faster deployment of new protections and quicker responses to emerging threats. - **Offline Mode Certificate Validation** - Added a transform configuration to whitelist signed files without revocation checks; auto-enabled in air-gapped environments, but can be disabled for maximum security. - **MP3 Filetype Support** – Expanded filetype coverage with MP3 parsing and analysis.   **Bug Fixes**   - **Incorrect URL Extraction** – Resolved parsing issues causing incomplete or inaccurate URL extraction. - **Reporting & Metadata** – Corrected metadata keys to ensure consistency.   **Threat Detection 1.0.0 Release Notes**  **Threat Detection 1.0.0** detects AI-based evasion techniques, advanced installer and filetype support, and improved zero-day defense, empowering organizations with proactive, agile protection against modern threats.  **What's new**   - **Double Base64 Decoding** – Detects payloads hidden in multiple layers of Base64 encoding, commonly used by advanced malware to evade security controls. - **Extended Threat Indicators for Pickle & PyTorch** – Detects weaponized Python serialization and machine learning model files often used for supply chain and AI-related attacks.     Detection of Pickle file capabilities   - **Improved AI Evasion Detection** – Enhanced identification of the **nullifAI evasion technique** and **stack pickle manipulations**, strengthening AI/ML malware defense.     Stacked Pickle trick evasion   - **New Installer Package Support** – Added extraction and analysis for:    - **Advanced Installer packages**   - **NSIS (Nullsoft Scriptable Install System) packages**   - **Wise Installer packages** - This expands coverage for malware distributed via custom installer frameworks.     Static file extraction for PE installer    Threat indicators detecting actions defined in installer scripts   - **CVE-2018-15982 Detection** – Identifies exploitation of a critical Adobe Flash vulnerability. - **Equation Editor Exploit Detection** – Detects obfuscated versions of this long-abused Microsoft Office exploit.     Signal group and threat indicator detecting obfuscated and malformed exploit documents   - **Extended PDF Threat Indicators** – Better phishing detection in PDF documents, with new heuristics for malicious links and embedded content. |
|  |

## [v2.4.0](/docs/mdcore/release-notes/changelog-embedded-sandbox-engine#v240)

Release date: 07/31/2025

| **New Features and Improvements** |
| --- |
| **What's New**   - **Updated YARA & Malware Config Extraction Logic**    - Updated YARA & Malware Config Extraction Logic for Lumma Stealer (ChaCha), MetaStealer, and Snake Keylogger. - **.NET Loader Unpacking Enhancements**    - **.**NET Loader Unpacking for Roboski and ReZer0 loaders.      - **Control Flow Deobfuscation in .NET Files**    - Added control flow deobfuscation in .NET files to enhance payload unpacking performance. - **Early Detection for ClickFix Variants**    - Introduced early detection capabilities for ClickFix and its variants, a trending social engineering technique.      - **Automated Decoding of Base64 Commands**    - Implemented automated decoding of base64-encoded commands for Python and Bash scripts, uncovering deeper layers of obfuscation and enhancing threat detection accuracy.      - **Support for ACCDE File Analysis**    - Now supporting analysis of ACCDE files—expanding coverage to include Microsoft Access Applications and strengthening visibility into embedded threats.  ---   **Improvements**   - **Improved .NET Binary Detection**    - Improved detection of suspicious .NET binaries by analysing low-level anomalies - such as oversized static arrays, high-entropy resources, and abnormal call patterns - enabling earlier identification of obfuscated threats. - **Expanded Threat Coverage**    - Boosted IOC and MITRE ATT&CK coverage with deeper parsing of LNK files, smarter enrichment of indicators, and more flexible tagging using YARA-derived metadata-sharpening threat correlation and context across reports. - **Smarter File Detection**    - Updated the DIE (Detect It Easy) Database to improve the identification of file types and packed binaries, boosting classification accuracy across diverse samples. - **Heuristic Lookup Optimization**    - Disabled OSINT lookups for heuristically extracted domains - reducing false positives and improving the precision of threat verdicts.  ---   **Bug Fixes**   - **Improved Malware Unpacking**    - Resolved an unpacking issue with downloaded files, improving analysis of second-stage malware. - **Corrected Hash Validation**    - Corrected a hash mismatch during PE resource extraction - ensuring accurate file integrity checks. - **Sharper Verdict Accuracy**    - Refined detection logic for Office documents, emails, and URLs to minimize false positives, in turn sharpening verdict confidence. - **Fixed URL Construction**    - Corrected URL construction logic for absolute paths in Open Directory Scans. - **Enhanced Extractor Stability**    - Improved stability of the base64-encoded file extractor, which now handles edge cases that previously caused failures. - **Smali Parsing Fix**    - Fixed an error in parsing Smali files within APK packages - improving visibility into APK Packages. |

## [v2.3.0](/docs/mdcore/release-notes/changelog-embedded-sandbox-engine#v230)

Release date: 06/05/2025

| **New Features and Improvements** |
| --- |
| - **Scan Execution Profiles**: Users can now select from predefined scan profiles or create custom profiles, enabling a more streamlined and flexible scanning experience tailored to specific needs. - **YARA result triggering:** Sandbox scans can now be automatically initiated based on curated rules embedded within the Adaptive Sandbox’s YARA engine, allowing for intelligent, rule-driven threat escalation. [YARA Trigger](/docs/mdcore/sandbox/enhancing-threat-detection-with-yara---adaptive-sandbox) - **Enhanced file type support:** The file type selector has been updated to more accurately reflect the full range of formats supported by the Adaptive Sandbox engine, improving usability and clarity. - **Result updated with scan preferences:** Selected scan settings are now displayed in the Result tab, making it easier to troubleshoot and understand how each scan was configured and executed. - **Classify Threat Indicators based on sandbox capabilities**: Improved classification and visibility of threat indicators derived from sandbox behavior. Enhancements include better translation, risk categorization, and filtering to support faster triage. - **HTML URL Parsing:** Integrated a new parser for analyzing URLs embedded within HTML content in emails and web threats, improving detection precision in phishing and redirection scenarios. - **Offline URL Model Update:** The model has been retrained using a newly compiled set of URLs to enhance detection accuracy. - **Performance Optimizations:** Improved threat detection performance by enhancing domain resolution speed, scan performance, and reducing memory usage. - **String Extraction:** Improved string extraction logic, including better UTF-8 handling and efficiency. - **URL Handling:** Fixed issues with multi-redirected URLs, reputation lookups, and file type misdetection. - **New Malware Family Detection:** Added config extractors for XWorm, Stealc, and new Lumma Stealer variants, boosting coverage of active campaigns. Also extended detection rules for emerging loaders and RAT such as PrivateLoader and Millenium RAT. - **Short-Lived Certificate Whitelist Bypass Detection:** Prevents whitelisting of malware signed with short-lived certificates - a tactic used to bypass detection mechanisms. - **API Hashing Detection:** Flags obfuscated API calls using hashing, being critical for catching stealthy malware. - **Phishing DKIM Replay Abuse Detection:** Flags spoofed DKIM attempts, enhancing phishing resilience against recent campaigns that abuse Google Sites and DKIM replay to send valid-signed emails, bypassing filters and stealing credentials. - **Enhanced PE Anomaly Detection:** Added 40+ signatures to detect PE structure anomalies, such as significant discrepancies between virtual size and raw size in PE headers. - **APK Certificate Signer Validation:** Added validation and whitelisting of APK certificate signers to improve trust assessment and reduce false positives in mobile threat detection. - **Improved File Extraction From Base64 Artifacts:** Now supports extraction of embedded Base64-encoded files, including reverse cases seen in malware. - **Script-Based Threat Detection Enhancements:** Improved detection of malicious JavaScript, VBA, and PowerShell behavior - including decoding, decryption, and suspicious cmdlet abuse. Emulated PowerShell code is now extracted as readable strings, enhancing visibility and analysis. - **Disassembly Code Extraction Improvements:** Fixed issues with disassembly functions on RET instructions, implemented string annotation for immediate strings, and enhanced filtering to avoid disassembling junk code, improving the accuracy of extracted disassembly data. - **Adaptive Indicator Tuning for Signed PEs:** Fine-tuned context-aware indicators for signed PE files in offline environments, reducing false positives by improving detection accuracy when certificate validation is unavailable. - **Certificate Validation Process Fix:** Resolved the issue where edge-case certificates, which are technically valid, were incorrectly detected as invalid. |

## [v2.2.0](/docs/mdcore/release-notes/changelog-embedded-sandbox-engine#v220)

Release date: 02/17/2025

| **New Features and Improvements** |
| --- |
| - **Daily Scan limit**: Daily scan limit is enforced based on User license, [Licensing](/docs/mdcore/sandbox/licensing) - **Threat Indicator details**: Report is extended with Threat Indicators details, providing better and easier assessment of the file.      - **Updated IOC details**: Improved IOC details UI      - **Dependency handling**: Visual C++ Redistributable is no longer required, making it easier to install and update the engine on the fly. - **URL Parsing**: Embedded engine will no longer try to parse Remote URL, fixing false Error messages in Engine logs - **Property File**: Property files are no longer overridden - **Embedded File extraction**: Embedded file extraction is now correctly working on Windows instances, improving the amount of data available for scans. - **Embedded File Yara**: Yara rules are now correctly applied to Embedded files on Windows, ensuring better static analysis of files. - **Zero-Day Office Document Support**: We now support the analysis of broken Office documents, including those used in zero-day attacks. This helps detect previously evasive threats targeting Office file vulnerabilities. - **Mitigation for Bloated Executables**: A new mitigation feature identifies intentionally bloated executables that attempt to bypass sandbox environments. This enhances the platform's ability to analyze suspicious files that may try to evade detection. - **New Malware Family Detection**: Detection capabilities have been extended to include notable malware families such as WezRat, Remcos, Lumma Stealer, among others. This expands our database and improves detection across a wider array of threats. [Supported malware families via YARA](Supported malware families via YARA) - **JavaScript-Compiled PE File Support**: We’ve added unpacking and decompilation support for JavaScript-compiled PE files, enabling better analysis of malicious payloads that may be delivered through JavaScript. - **Malicious Techniques Detection**: MetaDefender now identifies and flags malicious techniques such as disabling Data Execution Prevention (DEP), Authenticode evasion (SigFlip), and misleading script encoding. This enhances the platform's ability to spot sophisticated attack vectors. - **WebDAV Communications Identification**: MetaDefender can now identify WebDAV communications, improving the detection of network-based attacks that use this protocol. - **Support for Password-Protected Office Documents**: MetaDefender now supports the analysis of password-protected Office documents, improving its ability to handle encrypted files during analysis. - **UNC Paths on IOCs Page**: The IOCs (Indicators of Compromise) page now supports UNC path display, providing easier access to file locations in network environments. - **Enhanced File Type Analysis**: Analysis for APK, RDP, Shell Script, and CHM files has been expanded, improving detection capabilities across these file formats. - **Heuristic Enhancements for Packed Executables**: The heuristic engine has been upgraded to better detect packed executables, which are commonly used to obfuscate malware. - **Extended .NET Obfuscation Detection**: We’ve improved detection for obfuscated .NET assemblies and added better handling for unmanaged .NET functions, making it easier to detect threats hiding in .NET-based applications. - **XOR Decryption Improvements**: XOR decryption capabilities have been enhanced for PE files and URLs, increasing the platform’s ability to analyze encrypted malware. - **Extended Adaptive Context for Executables and Emails**: The adaptive context feature has been expanded to include deeper analysis of executables and email files, improving detection of hidden threats. - **Extended Base64 Decoding for Downloaded Files**: The platform now supports extended base64 decoding for downloaded files, enhancing its ability to analyze encrypted or obfuscated content. - **Blacklist for Abused Certificates**: We’ve extended the blacklist for abused certificates and bootloaders, improving protection against threats using known malicious certificates. - **Whitelist Accuracy**: The file whitelisting process has been fine-tuned for greater accuracy, ensuring only trusted files are excluded from scans. - **Improved Emulation Support**: Emulation for JavaScript coming from email attachments has been extended, improving detection of email-borne JavaScript threats. - **Polyglot Detection**: The ability to detect polyglot files has been improved, increasing the platform’s ability to identify files that contain multiple formats. - **Enhanced Emulation for Common Threats**: Emulation for VBA, JavaScript, PowerShell, Microsoft Equation, and shellcode has been improved, providing deeper analysis for common attack techniques. - **Improved PE Signature Validation**: PE file signature validation has been enhanced, improving detection of malicious files and ensuring more accurate assessments. - **Improved QR Code Analysis**: Enhancements to QR code analysis allow for better identification of hidden threats and malicious links within QR codes. - **VBA Macro Signature Detection**: A bug in the VBA macro signature detection has been resolved, ensuring more accurate detection of malicious macros in Office files. - **Oledump Tool Update**: The oledump tool has been updated to reduce the incorrect extraction of strings, improving the analysis of OLE files. |

## [v2.1.0](/docs/mdcore/release-notes/changelog-embedded-sandbox-engine#v210)

Release date: 12/02/2024

| **New Features and Improvements** |
| --- |
| - **Min-Max Analysis timeout changed:** Minimum and Maximum Analysis Timeout changed to 60-86400, for better handling of Large Files. - **.Dll files are signed:** Windows .Dll files are now signed for better security - **Enhanced Archive handling:** Archive File handling improved to reduce Scan times.      - **Java Dependency checking is fixed:** Fixed Java dependency checking to no longer mismatch some Java versions - **Deep CDR Triggers options added:** New Deep CDR Trigger option is added to Workflow configs for a more granular setup option. - **Removed Scan modes from configuration:** Scan mode workflow config is no longer supported. - **Context-Aware Threat Indicators:** Improved threat indicators by factoring in the context of the analysis, leading to more accurate threat assessments. - **Reduced False Positives**: Lowered false positive rates for heuristically detected or non-clickable IP addresses and URLs, improving the accuracy of threat analysis. - **Malicious Document Detection**: Improved the detection of malicious documents, adding new indicators and reducing the risk of document-based attacks. - **Enhanced Emulation**: Increased emulation success rates, particularly through better recognition of file content types eligible for emulation. - **Python Script Detection**: Improved detection of malicious Python scripts, a growing vector for attacks. - **Better XOR Decryption**: Extended XOR decryption capabilities, improving analysis of encrypted malware. - **Improved IOC Extraction**: Enhanced the extraction of indicators of compromise (IOC) from emulation for a more comprehensive report. - **YARA Rule Updates**: Reviewed and vetted third-party YARA rules. By default, YARA rules are loaded with priority from the OPSWAT repository. - **Symantec Quarantine Repair**: Implemented a repair function for files restored from Symantec quarantine, ensuring files can be analysed post-restoration. - **MSC File Support**: Added the ability to identify and parse Microsoft Management Console (MSC) files, further broadening threat detection capabilities. - **JPHP Support**: Enhanced malware detection with the ability to parse and decompile JPHP files, expanding the range of supported file types and languages. - **.NET API Call Detection**: Added detection of unmanaged .NET API references, improving analysis of .NET-based malware. - **OT Malware Detection**: Introduced a YARA ruleset specifically for OT (Operational Technology) malware, expanding protection to critical infrastructure systems. - **LNK File Threat Indicators**: Strengthened detection for LNK icon smuggling and LNK-MOTW (Mark of the Web) bypass attacks, both common techniques in modern malware. - **Ransomware Detection Enhancement**: Added severity Yara rule matches related to ransomware, helping to prioritize and respond to ransomware threats more effectively. |

Deep CDR Triggers

## [v2.0.0](/docs/mdcore/release-notes/changelog-embedded-sandbox-engine#v200)

Release date: 08/28/2024

| **New Features and Improvements** |
| --- |
| - Upgraded to Java 17 and Python 3.10 for all relevant Sandbox components - Support for AutoIT script files, including compiled AutoIT Portable Executables - Parsing of MSI metadata and actions, including implementation for filtered file extraction - Parsing of ODF files and macro extraction - Parsing of Python pickle files, including implementation for malicious Threat Indicators - Capability to identify potential obfuscation for extracted macro code - New Threat Indicator for deceptive filenames commonly used for phishing files - New Threat Indicator for undetected Equation Editor RTF exploit - Enhanced parsing of LNK metadata and actions, including new Threat Indicators - Improved Python-specific Threat Indicators - Include proper tags for Golang, Rust and compiled-Python Portable Executables - Improved processing for nested extracted files - Enhanced Threat Indicators for imported APIs and emulation respectively   Fixes and improvements:   - Fixed minor bugs and misdetections - Improved emulation efficacy - Improved application security |

## [v1.7.1](/docs/mdcore/release-notes/changelog-embedded-sandbox-engine#v171)

Release date: 05/24/2024

| **New Features and Improvements** |
| --- |
| - Ensured support for Ubuntu 22.04 - Added new threat indicators - Disabled IP address OSINT lookups to avoid false positive findings - Added verdict to IOCs on the UI - Reduced false positive / false negative detection - Updated YARA rule-set - Fixed office file emulation errors |

Verdict for IOCs

## [v1.7.0](/docs/mdcore/release-notes/changelog-embedded-sandbox-engine#v170)

Release date: 04/26/2024

| **New Features and Improvements** |
| --- |
| - Malware config extraction support - Python Unpacking & Decompilation for PyInstaller, Nuitka, and py2exe - Improved error reporting - Added long path support on Windows - Added HTTP redirection support - Included disassembly of exported functions for Windows binaries - Threat indicator to flag when executable files have two different sections with the same section name - Extraction of VBA macro code from DWG files (shown as OLE Stream in File Details section) - Enhanced script language detection using the guesslang library - Fine-tuned several threat indicators to reduce false positive ratio - Improved detection for phishing calendar invites - Enhanced recursive analysis of active content containers (email, Office documents, PDF, etc.) - Improved scan process for corrupt OLE2 documents - Fixed several issues with existing threat indicators (ELF binaries, URL extraction, EML) |

Improved error reporting

## [v1.6.0](/docs/mdcore/release-notes/changelog-embedded-sandbox-engine#v160)

Release date: 01/29/2024

| **New Features and Improvements** |
| --- |
| - Improved engine performance and stability - Implemented configurable OPSWAT Reputation secret in engine global config - New indicators for Windows APIs related to specific activities - Implemented flagging for LSASS dump using minidump - Extracted remote templates inside xTable struct in MS Office documents - Implemented parser for Debian packages - Expanded malware configuration extractors to encompass the latest and most pertinent threats - Improved detection of dynamic syscalls using the HellsGate bypass technique - Enhanced Quishing and Phishing email detection - Improved the capabilities of Batch, CSV, HTA, JavaScript, LNK, PowerShell, VBA, and VBScript emulation and fine-tuned timeout handling - Fixed several UTF-8 parsing issues in content parsers (related to HTML & OLE files) - Ensured that all whitelisted submissions get the Benign verdict - Improved the stability of concurrent OSINT lookup tasks |

## [v1.5.0](/docs/mdcore/release-notes/changelog-embedded-sandbox-engine#v150)

Release date: 11/06/2023

| **New Features and Improvements** |
| --- |
| - Updated Threat Indicators - Improved office file emulation - Improved PE file analysis - Updated YARA rule-set - Improved disassembly for x64 architecture - Improved file type detection - New IOC types for Crypto wallets - New Executive Summary (ChatGPT report) |

Executive Summary

Crypto Wallets

| **Known issues** |
| --- |
| - Crypto Wallets IOCs sometimes parsed and displayed incorrectly on the UI |

## [v1.4.0](/docs/mdcore/release-notes/changelog-embedded-sandbox-engine#v140)

Release date: 09/22/2023

| **New Features and Improvements** |
| --- |
| - Support filenames with various Unicode characters - Support unpacking of 64-bit executables - Support malicious documents embedded in PDF files hidden as ActiveMime objects in MHTML format - New threat indicators to detect the WikiLoader malware family (Microsoft Office files) - Detection and extraction of embedded RTF files in Office documents, as described in [CVE-2023-36884](https://msrc.microsoft.com/update-guide/vulnerability/CVE-2023-36884) - Enhance Threat Indicator for [Mavinject](https://lolbas-project.github.io/lolbas/Binaries/Mavinject/) - Improved office file emulation - Improved application security - Improved large file processing |

## [v1.3.4](/docs/mdcore/release-notes/changelog-embedded-sandbox-engine#v134)

Release date: 08/02/2023

| **New Features and Improvements** |
| --- |
| - Updated Threat Indicators - Improved office file emulation - Improved verdict calculation |

## [v1.3.3](/docs/mdcore/release-notes/changelog-embedded-sandbox-engine#v133)

Release date: 07/07/2023

| **New Features and Improvements** |
| --- |
| - Fixed global config “reset to defaults” feature - Improved office file emulation - Updated YARA ruleset - Updated Threat Indicators - Updated verdict calculation |

## [v1.3.2](/docs/mdcore/release-notes/changelog-embedded-sandbox-engine#v132)

Release date: 06/14/2023

| **New Features and Improvements** |
| --- |
| - Updated logging for MetaDefender Core support package - Improved handling of embedded JavaScript files |

## [v1.3.1](/docs/mdcore/release-notes/changelog-embedded-sandbox-engine#v131)

Release date: 06/05/2023

| **New Features and Improvements** |
| --- |
| - Enabled XML file support by default - Updated reputation sources - Improved verdict calculation - Fixed global config reset to default values feature - Fixed report generation for files including Email IOCs |

## [v1.3.0](/docs/mdcore/release-notes/changelog-embedded-sandbox-engine#v130)

Release date: 05/26/2023

| **New Features and Improvements** |
| --- |
| - Updated YARA rule database - YARA matches displayed on MDCore UI - Dependency check on startup |

## [v1.2.0](/docs/mdcore/release-notes/changelog-embedded-sandbox-engine#v120)

Release date: 05/17/2023

| **New Features and Improvements** |
| --- |
| - Scan results are extended with the list of IOCs - Rapid mode support added and enabled by default - Reputation lookup support added and enabled by default - Reputation lookup verdict improvements - Improved embedded engine performance |

## [v1.1.0](/docs/mdcore/release-notes/changelog-embedded-sandbox-engine#v110)

Release date: 05/08/2023

| **New Features and Improvements** |  |
| --- | --- |
| - Improved Microsoft Office file handling - Security and performance improvements |  |

## [v1.0.0](/docs/mdcore/release-notes/changelog-embedded-sandbox-engine#v100)

Release date: 04/06/2023

| **New Features and Improvements** |
| --- |
| - First versions of Embedded and Remote engines for MetaDefender Core customers |
