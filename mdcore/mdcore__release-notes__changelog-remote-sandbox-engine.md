<!-- source: https://www.opswat.com/docs/mdcore/release-notes/changelog-remote-sandbox-engine -->

# Remote Engine

View as Markdown Ask ChatGPT about this page Ask Claude about this page Pro Tip

Keep your MetaDefender Aether (previously know MetaDefender Sandbox) standalone instance up to date for the latest features. See the [release notes](https://docs.opswat.com/filescan/release-notes) for more information.

## [V3.3.1](/docs/mdcore/release-notes/changelog-remote-sandbox-engine#v331)

Release date: 13/10/2026

| **New Features and Improvements** |
| --- |
| - Fixed configuration issues with No Threat Detected verdict |

## [v3.3.0](/docs/mdcore/release-notes/changelog-remote-sandbox-engine#v330)

Release date: 10/10/2026

| **New Features and Improvements** |
| --- |
| - **LLM Scanning**Submit a model to MetaDefender Aether in the same way you submit any other file. Aether runs two analyses: static analysis of the model file and dynamic analysis of the running model. If Aether finds a threat, Core blocks the file.**Static analysis**Aether never loads or runs the model. It reads only the parts of the file that can carry code or configuration and skips over the weights, so memory use stays low even for very large models.Any payload Aether finds inside the file, including data hidden between tensors, is extracted and analysed on its own.**Dynamic analysis**Aether connects to your inference server through its OpenAI-compatible API and runs 38 attack probes against the live model, covering 9 of the OWASP Top 10 for LLM Applications categories. Probes run in order of severity. Each scan plants single-use canary tokens, so if one appears in a response, the leak is confirmed. Every finding shows the prompt, the model's response, the severity, the OWASP category and the rule that flagged it.Static and dynamic analysis are separate options, so you can run either one or both. - **More Evidence from emulation** - **HTTP traffic**: Emulation now records the full request and response for each HTTP call, including headers and body. - **Delayed macros:** VBA emulation now supports Application.OnTime, which malware uses to delay its payload. - **Deeper unpacking** - **Installers**: Better extraction from nested installers and more installer types, including PyInstaller, py2exe, ps2exe and Nuitka files. - **Extended YARA triggers**Adaptive Sandbox scan can be triggered for custom YARA rules |

## [v3.2.0](/docs/mdcore/release-notes/changelog-remote-sandbox-engine#v320)

Release date: 31/07/2026

| **New Features and Improvements** |
| --- |
| - **Implemented instrumented file system within the PE emulator:** The PE emulator now instanciates an instrumented filesystem in which the emulated sample resides. A great step towards the first official version of Filescan's PE emulator. This feature enables proper emulation of any file operation and interaction which would have previously terminated the emulation. This feature brings the flexibility of manually configuring the fake files that "exist" within, so that the emulated sample actually locates any file defined in the configuration file. Hence, this milestone not only enables a new feature, but extends configuration and flexibility of the emulation environment. - **Detection for Emerging Evasion Techniques:** Threat actors keep getting more creative — Sandbox keeps pace. This release adds detection for *etherhiding* (concealing threat actor infrastructure inside blockchain transactions) and intentionally malformed .NET assemblies built to break automated analysis tools. - **Detection for Emerging Evasion Techniques:** Threat actors keep getting more creative — Sandbox keeps pace. This release adds detection for *etherhiding* (concealing threat actor infrastructure inside blockchain transactions) and intentionally malformed .NET assemblies built to break automated analysis tools. - **Smarter Remote Template Detection:** Remote template injection analysis got a full pass this release, aimed at keeping the false-positive rate flat while closing real detection gaps. A rebuilt link-detection and URL-classification pipeline now tells genuine injection attempts apart from ordinary embedded links — fixing two indicators that had been flagging legitimate URLs as malicious, and closing a gap where obfuscated, octal-encoded malicious IP links were going undetected. Fewer false alarms, no loss of coverage. - **Broader Detection & Coverage Improvements:** This release also expands detection coverage on several fronts: new detection engineering for wiper malware, CAPTCHA identification via OCR (including obfuscated but rendered fake CAPTCHAs used in ClickFix attacks), new config extractors for PrivateLoader and Quasar RAT, and expanded IOC coverage in the local reputation database. |

## [v3.1.0](/docs/mdcore/release-notes/changelog-remote-sandbox-engine#v310)

Release date: 31/04/2026

| **New Features and Improvements** |
| --- |
| **What's new**   - **Expanded archive support:** Multiple archive types are now supported with Core 18.1. - **Deep CDR hyperlink trigger:** The hyperlink Deep CDR type can now be used to trigger Sandbox analysis. - **TLS certificate verification:** Added an option to enable TLS certificate validation using the operating system's certificate store.   **Bug Fixes**   - **Improved URL handling:** Fixed URL parsing when the Load Balancer feature is enabled. |

## [v3.0.0](/docs/mdcore/release-notes/changelog-remote-sandbox-engine#v300)

Release date 26/01/2026

| **New Features and Improvements** |
| --- |
| We are excited to announce **MetaDefender Aether 3.0.0**, OPSWAT’s next-generation unified zero-day detection solution. With this release, the proven **MetaDefender Sandbox dynamic analysis engine is now fully integrated into MetaDefender Aether as Layer 2**, strengthening Aether’s multi-layered detection architecture and delivering deeper, faster, and more scalable threat analysis at the perimeter.  **Improvements**   - **E-PUB support** - Added support for EPUB files, to ensure broader compatibility with widely used e‑reading formats. - **Verdict Renaming** – Updated verdicts to provide clearer guidance on how to interpret analysis results and take appropriate actions based on potential threat levels   **Bug Fixes**   - **Duplicate Tags** - Tags originating from multiple sources were being shown repeatedly in the UI. The fix ensures that tags are properly deduplicated so each one appears only once. |

## [v2.5.1](/docs/mdcore/release-notes/changelog-remote-sandbox-engine#v251)

Release date 11/20/2025

| **New Features and Improvements** |
| --- |
| **Improvements**   - **Stability & Security -** Updated core dependencies to enhance performance and security.   **Bug Fixes**   - **Fixed zlib support** – zlib files are now correctly processed by the Archive Engine instead of the Adaptive Sandbox, ensuring proper handling and improved efficiency. |

## [v2.5.0](/docs/mdcore/release-notes/changelog-remote-sandbox-engine#v250)

Release date: 10/30/2025

| **New Features and Improvements** |
| --- |
| **What's New**   - **Full Report Downloading** – Introduced the ability to download generated reports from the Remote Engine directly via the Core UI. |

## [v2.4.0](/docs/mdcore/release-notes/changelog-remote-sandbox-engine#v240)

Release date: 07/31/2025

| **New Features and Improvements** |
| --- |
| **What's New** 🎉   - **Load Balancing / Failover**: Implemented Round Robin load balancing and failover to ensure even traffic distribution and high availability during node failures. |

## [v2.3.0](/docs/mdcore/release-notes/changelog-remote-sandbox-engine#v230)

Release date: 06/05/2025

| **New Features and Improvements** |
| --- |
| - **Scan Execution Profiles**: Users can now select from predefined scan profiles or create custom profiles, enabling a more streamlined and flexible scanning experience tailored to specific needs. - **YARA result triggering:** Sandbox scans can now be automatically initiated based on curated rules embedded within the Adaptive Sandbox’s YARA engine, allowing for intelligent, rule-driven threat escalation. [YARA Trigger](/docs/mdcore/sandbox/enhancing-threat-detection-with-yara---adaptive-sandbox) - **Enhanced file type support:** The file type selector has been updated to more accurately reflect the full range of formats supported by the Adaptive Sandbox engine, improving usability and clarity. - **Result updated with scan preferences:** Selected scan settings are now displayed in the Result tab, making it easier to troubleshoot and understand how each scan was configured and executed. |

## [v2.2.0](/docs/mdcore/release-notes/changelog-remote-sandbox-engine#v220)

Release date: 12/02/2024

| **New Features and Improvements** |
| --- |
| - **Threat Indicator details**: Report is extended with Threat Indicators details, providing better and easier assessment of the file.      - **Updated IOC details**: Improved IOC details UI      - **Dependency handling**: Visual C++ Redistributable is no longer required, making it easier to install and update the engine on the fly. |

## [v2.1.0](/docs/mdcore/release-notes/changelog-remote-sandbox-engine#v210)

Release date: 12/02/2024

| **New Features and Improvements** |
| --- |
| - **Min-Max Analysis timeout changed:** Minimum and Maximum Analysis Timeout changed to 60-86400, for better handling of Large Files. - **.Dll files are signed:** Windows .Dll files are now signed for better security - **Enhanced Archive handling:** Archive File handling improved to reduce Scan times. - **Deep CDR Triggers options added:** New Deep CDR Trigger option is added to Workflow configs for a more granular setup option. - **Improved Error Handling:** More Errors messages are available for easier problem solving. |

Deep CDR Triggers

## [v2.0.1 - Windows](/docs/mdcore/release-notes/changelog-remote-sandbox-engine#v201---windows)

Release date: 09/27/2024

| **New Features and Improvements** |
| --- |
| - Fixed dependency check for Visual Studio Redistributable on Windows |

## [v2.0.0](/docs/mdcore/release-notes/changelog-remote-sandbox-engine#v200)

Release date: 07/23/2024

Backward compatibility

Sandbox standalone version 2.0.0 is not backward compatible with older engine versions

| **New Features and Improvements** |
| --- |
| - Ensured support for Ubuntu 22.04 - Added verdict to IOCs on the UI - Sandbox standalone version 2.0.0 compatibility |

## [v1.7.0](/docs/mdcore/release-notes/changelog-remote-sandbox-engine#v170)

Release date: 04/26/2024

| **New Features and Improvements** |
| --- |
| - Improved error reporting - Added HTTP redirection support |

Improved error reporting

## [v1.6.0](/docs/mdcore/release-notes/changelog-remote-sandbox-engine#v160)

Release date: 01/29/2024

| **New Features and Improvements** |
| --- |
| - Improved engine performance and stability |

## [v1.5.0](/docs/mdcore/release-notes/changelog-remote-sandbox-engine#v150)

Release date: 11/06/2023

| **New Features and Improvements** |
| --- |
| - New IOC types for Crypto wallets |

Crypto Wallets

| **Known issues** |
| --- |
| - Crypto Wallet IOCs will not be displayed on the UI until a new Filescan Standalone version is released |

## [v1.3.3](/docs/mdcore/release-notes/changelog-remote-sandbox-engine#v133)

Release date: 07/07/2023

| **New Features and Improvements** |
| --- |
| - Fixed global config “reset to defaults” feature |

## [v1.3.2](/docs/mdcore/release-notes/changelog-remote-sandbox-engine#v132)

Release date: 06/14/2023

| **New Features and Improvements** |
| --- |
| - Updated logging for MetaDefender Core support package |

## [v1.3.1](/docs/mdcore/release-notes/changelog-remote-sandbox-engine#v131)

Release date: 06/05/2023

| **New Features and Improvements** |
| --- |
| - Fixed global config reset to default values feature - Fixed report generation for files including Email IOCs |

## [v1.3.0](/docs/mdcore/release-notes/changelog-remote-sandbox-engine#v130)

Release date: 05/26/2023

| **New Features and Improvements** |
| --- |
| - YARA matches displayed on MDCore UI |

## [v1.2.0](/docs/mdcore/release-notes/changelog-remote-sandbox-engine#v120)

Release date: 05/17/2023

| **New Features and Improvements** |
| --- |
| - Scan results are extended with the list of IOCs - Private scanning option added, enabled by default - Reputation lookup support added and enabled by default - Reputation lookup verdict improvements |

## [v1.1.0](/docs/mdcore/release-notes/changelog-remote-sandbox-engine#v110)

Release date: 05/08/2023

| **New Features and Improvements** |
| --- |
| - Improved Microsoft Office file handling - Security and performance improvements |

## [v1.0.0](/docs/mdcore/release-notes/changelog-remote-sandbox-engine#v100)

Release date: 04/06/2023

| **New Features and Improvements** |
| --- |
| - First versions of Embedded and Remote engines for MetaDefender Core customers |
