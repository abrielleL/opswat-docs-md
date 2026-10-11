<!-- source: https://www.opswat.com/docs/filescan/3.2.0/release-notes/release-notes-v240 -->

# Release Notes for v2.4.0

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Date: 30 July, 2025](/docs/filescan/3.2.0/release-notes/release-notes-v240#date-30-july-2025)

Info

This release artifact contains False Positive files (pycdc, upx, nuitka-extractor) that are incorrectly detected by the Cylance and Quick Heal AV engines. If you are scanning the release artifact with MetaDefender Core, please enable the Reputation engine as explained here to avoid these misdetections: <https://www.opswat.com/docs/mdcore/reputation-engine/configuration-reputation-engine>

## [**MetaDefender Sandbox 2.4.0 Release Notes**](/docs/filescan/3.2.0/release-notes/release-notes-v240#metadefender-sandbox-240-release-notes)

Seamless enterprise integration, streamlined user access, and a powerful new interface - MetaDefender Sandbox is now faster to deploy, easier to use, and richer in insight than ever before.

**What's New**

- **Report Overview Redesign**

  - Experience a fully reimagined UI built for clarity and speed - featuring intuitive navigation, dynamic filtering, and rich threat insights all in one streamlined view.

A Newly Designed, High Level Overview of the Report

- **Redesigned Trends Page**

  - Seamlessly navigate the enhanced Trends page featuring a refreshed layout, and intuitive visuals — unlocking deeper visibility with updated charts on scan verdicts, average scan time, IOC generation, and leading threat indicators.

More Insights via the New Trends Page

- **SAML 2.0 Identity provider (IDP) Integration**

  - Effortlessly connect Sandbox to enterprise SSO Solutions like OKTA, Ping, and Active Directory Federation Services (AD FS) with full SAML 2.0 Federation - streamlining user management and strengthening security posture.
- **Red Hat Offline Installation Mode**

  - Deploy Sandbox securely in isolated environments with support for fully offline installation on Red Hat Enterprise Linux 9.
- **Advanced Windows PE Emulator (Beta)**

  - The Beta of the PE emulator already adds high value by unpacking dynamic payloads, hidden IOCs, and enabling new threat indicators.

Scan Without PE Emulation - Malicious Activity Suspected

PE Emulation Boosts Detection Accuracy

**Improvements**

- **Threat-Indicator Overview Counts**

  - Dashboards now surface distinct threat indicators—cutting through signal clutter to deliver clearer, more actionable risk assessments.
- **Input Accessibility & Form Refactor**

  - Revamped form components ensuring consistent labelling, ARIA compliance, and accessible validation—enhancing usability and aligning with accessibility best practices.

---

**Bug Fixes**

- **Improved Account Settings**

  - Resolved faulty password strength checks and a username validation edge case in My Settings, in turn, hardening authentication.
- **Authentication Settings Stability**

  - Previously, external authentication providers could block the *Save* action in validation settings—this has been restored, providing full control over validation configurations.
- **Invite Link Session Handling**

  - Corrected a browser session conflict that caused partial logins where invite links were opened in an active browser session.
- **UI Glitch Cleanup**

  - Addressed user interface anomalies identified through error clustering, leading to a more consistent user experience.

---

## [**MetaDefender Sandbox 2.4.0 Threat Detection Release Notes**](/docs/filescan/3.2.0/release-notes/release-notes-v240#metadefender-sandbox-240-threat-detection-release-notes)

**What's New**

- **Updated YARA & Malware Config Extraction Logic**

  - Updated YARA & Malware Config Extraction Logic for Lumma Stealer (ChaCha), MetaStealer, and Snake Keylogger.
- **.NET Loader Unpacking Enhancements**

  - **.**NET Loader Unpacking for Roboski and ReZer0 loaders.

.NET Loader Deobfuscated - Roboski and ReZer0 Modules Extracted

- **Control Flow Deobfuscation in .NET Files**

  - Added control flow deobfuscation in .NET files to enhance payload unpacking performance.
- **Early Detection for ClickFix Variants**

  - Introduced early detection capabilities for ClickFix and its variants, a trending social engineering technique.

"ClickFix" is a social engineering attack that tricks users into executing malware by manipulating clipboard and presenting fake prompts

- **Automated Decoding of Base64 Commands**

  - Implemented automated decoding of base64-encoded commands for Python and Bash scripts, uncovering deeper layers of obfuscation and enhancing threat detection accuracy.

Cracking Base64: Automated decoding for Python/Bash boosts detection

- **Support for ACCDE File Analysis**

  - Now supporting analysis of ACCDE files—expanding coverage to include Microsoft Access Applications and strengthening visibility into embedded threats.

---

**Improvements**

- **Improved .NET Binary Detection**

  - Improved detection of suspicious .NET binaries by analyzing low-level anomalies - such as oversized static arrays, high-entropy resources, and abnormal call patterns - enabling earlier identification of obfuscated threats.
- **Advanced HTML Analysis**

  - Enhanced HTML analysis with a more resilient parser and expanded threat detection indicators, improving accuracy against evasive or malformed web-based threats.
- **Expanded Threat Coverage**

  - Boosted IOC and MITRE ATT&CK coverage with deeper parsing of LNK files, smarter enrichment of indicators, and more flexible tagging using YARA-derived metadata-sharpening threat correlation and context across reports.

Extended MITRE Mapping reveals obfuscation, evasion, and execution tactics in .NET and PowerShell

- **Smarter File Detection**

  - Updated the DIE (Detect It Easy) Database to improve the identification of file types and packed binaries, boosting classification accuracy across diverse samples.
- **Heuristic Lookup Optimization**

  - Disabled OSINT lookups for heuristically extracted domains - reducing false positives and improving the precision of threat verdicts.

---

**Bug Fixes**

- **Improved Malware Unpacking**

  - Resolved an unpacking issue with downloaded files, improving analysis of second-stage malware.
- **Corrected Hash Validation**

  - Corrected a hash mismatch during PE resource extraction - ensuring accurate file integrity checks.
- **Sharper Verdict Accuracy**

  - Refined detection logic for Office documents, emails, and URLs to minimize false positives, in turn sharpening verdict confidence.
- **Fixed URL Construction**

  - Corrected URL construction logic for absolute paths in Open Directory Scans.
- **Enhanced Extractor Stability**

  - Improved stability of the base64-encoded file extractor, which now handles edge cases that previously caused failures.
- **Smali Parsing Fix**

  - Fixed an error in parsing Smali files within APK packages - improving visibility into APK Packages.

---

## [**MetaDefender Sandbox 2.4.0 Engine Release Notes**](/docs/filescan/3.2.0/release-notes/release-notes-v240#metadefender-sandbox-240-engine-release-notes)

[**Advanced Windows PE Emulator (Beta)**](/docs/filescan/3.2.0/datasheet/pe-emulator--beta-)

**Enhancements**

- **Shellcode Execution:**

  - Support for standalone shell-code and forwarder binding.
- **Event Tracking:**

  - Detect suspicious activity such as memory/disk writes, protection manipulation, DNS resolution, HTTP request and more.
- **Relevant Dumps:**

  - Automatically extracted memory dumps from significant execution points, including PE Files, providing deeper inspection.
- **Integration with Disassembly:**

  - Routing meaningful memory dumps directly to the disassembler for in-depth analysis.
- **Overview and Trace:**

  - Summary stats, versioning and configurable API Log enhancements bringing the detail closer.
- **New Threat Indicators:**

  - PE-specific behavioral threat indicators added to enrich analysis with targeted insight.
- **Additional IOC Extraction:**

  - Dynamically uncover IOCs that are invisible to static scanning, enabled through emulation.
- **Defeating Evasion:**

  - Enhanced simulated fingerprinting checks to avoid evasive malware techniques.

---

**What's New**

- .lnk **Batch Drop Detection**

  - Detects Windows shortcut files that generate and execute batch payloads, closing a visibility gap for “living-off-the-land” techniques.
- **Configurable Indicator-Based Verdict Enforcement**

  - New config allows enforcing MALICIOUS verdict if any selected indicators trigger. Specific indicators can be disabled—set to *unknown* strength—with optional notifications to reflect customer overrides.
- **Clipboard API Emulation (**`write()` **/** `writeText()`**)**

  - Web emulation now understands modern clipboard calls, capturing write events used by phishing kits and droppers.
- **ECMAScript 6 Support in Anesidora**

  - JavaScript emulation upgraded to handle ES6 syntax, broadening coverage of modern malicious scripts.

---

**Improvements**

- **Automated Button/Link Clicks in HTML Emulation**

  - Enhanced coverage of drive-by scripts that hide malicious functions behind UI events.
- **Event Handler Execution on** `onclick`

  - Inline handler bodies now executed, boosting exploit detection in weaponized HTML/JS samples.
- `document.body.append()` **& Self-Read / Stage-Spawn Support**

  - Higher-fidelity DOM simulation and self-analysis behavior handling.
- **HtmlUnit Upgrades**

  - Brings JavaScript engine fixes, improved CSS support, and stability enhancements.

---

**Bug Fixes:**

- Optimized memory usage within JavaScript emulation pipeline to improve reliability under load.
- Filled gaps where emulation-derived threat indicators were missing from final reports.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
