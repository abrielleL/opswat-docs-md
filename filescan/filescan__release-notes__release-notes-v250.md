<!-- source: https://www.opswat.com/docs/filescan/release-notes/release-notes-v250 -->

# Release Notes for v2.5.0

## [Date: 27 October, 2025](/docs/filescan/release-notes/release-notes-v250#date-27-october-2025)

Awareness

OPSWAT releases **MetaDefender Sandbox 2.5.0,** enabling faster IOC updates, broader threat coverage of malware families, and deeper visibility.

## [MetaDefender Sandbox 2.5.0 Release Notes](/docs/filescan/release-notes/release-notes-v250#metadefender-sandbox-250-release-notes)

**Sandbox 2.5.0** adds Rocky Linux support, MP3 analysis, offline certificate validation, and enhanced emulation.

### [What's New](/docs/filescan/release-notes/release-notes-v250#whats-new)

- **Periodic Threat Detection Updates -** MetaDefender Sandbox now supports independent updates of detection logic and threat indicators, ensuring faster deployment of new protections and quicker response to emerging threats.
- **Rocky Linux Support** – Added full support for Rocky Linux, including installation pipelines, testing, and release documentation, ensuring reliable Sandbox deployments on this platform.
- **Web Threat Detection** - Enhanced ML-based detection with multi-label classification, advanced content analysis, automated data pipelines, improved false positive handling, and style analysis.

URL Details

- **MP3 Filetype Support** – Expanded filetype coverage with MP3 parsing and analysis.

### [Improvements](/docs/filescan/release-notes/release-notes-v250#improvements)

- **Trends Page Updates** – Redesigned Trends pages with new tabs, filters, charts, and components, improved mobile responsiveness, and connected statistics and backend jobs for better performance.
- **Verdict Renaming** – Implemented UI-only renaming of verdicts with dynamic mapping to maintain backward compatibility in the API and database, including the addition of a SYSTEM_ERROR verdict and support for both old and new verdicts in API responses.
- **Updated Translations** –Refined translations for a smoother, more consistent user experience.
- **Emulation Graph Enhancements** – Updated the emulation graph to highlight processes by threat level, making it easier to identify malicious or suspicious activity.

Improved emulation graph

### [Bug Fixes](/docs/filescan/release-notes/release-notes-v250#bug-fixes)

- **Authentication UX** – Corrected several login and password handling issues, including error placement, unclickable buttons, and empty input handling.
- **Report & UI** – Resolved report duplication, tag sizing, long URL formatting, PDF preview errors, and navigation inconsistencies.
- **Emulation Page** – Fixed 500 error occurring when loading the Emulation page.
- **Incorrect URL Extraction** – Resolved parsing issues causing incomplete or inaccurate URL extraction.
- **Reporting & Metadata** – Corrected metadata keys to ensure consistency.
- **Offline License Activation** – Resolved an issue with offline license activation caused by an unreadable file.

## [PE Emulator (Beta) Release Notes](/docs/filescan/release-notes/release-notes-v250#pe-emulator-beta-release-notes)

- **PE Section Handling** – Improved emulation memory management for emulated PE mapping
- **Covert API Lookups** – Sandbox now reports API lookups directly from the export table (as opposed to conventional GetProcAddress)

## [MetaDefender Sandbox 2.5.0 Threat Detection Release Notes](/docs/filescan/release-notes/release-notes-v250#metadefender-sandbox-250-threat-detection-release-notes)

The latest Threat Detection updates include capability to detect AI-based evasion techniques, advanced installer and filetype support, and improved zero-day defence, empowering organizations with proactive, agile protection against modern threats.

### [What’s new](/docs/filescan/release-notes/release-notes-v250#whats-new)

- **Periodic Threat Detection Updates -** The latest Threat Detection updates include capability to detect AI-based evasion techniques, advanced installer and filetype support, and improved zero-day defence, empowering organizations with proactive, agile protection against modern threats.
- **Double Base64 Decoding** – Detects payloads hidden in multiple layers of Base64 encoding, commonly used by advanced malware to evade security controls.
- **Extended Threat Indicators for Pickle & PyTorch** – Detects weaponized Python serialization and machine learning model files often used for supply chain and AI-related attacks.

Detection of Pickle file capabilities

- **Improved AI Evasion Detection** – Enhanced identification of the **nullifAI evasion technique** and **stack pickle manipulations**, strengthening AI/ML malware defense.

Stacked Pickle trick evasion

- **New Installer Package Support** – Added extraction and analysis for:

  - **Advanced Installer packages**
  - **NSIS (Nullsoft Scriptable Install System) packages**
  - **Inno Setup packages**
  - **Wise Installer packages** - This expands coverage for malware distributed via custom installer frameworks.

Static file extraction for PE installer

Threat indicators detecting actions defined in installer scripts

- **CVE-2018-15982 Detection** – Identifies exploitation of a critical Adobe Flash vulnerability.
- **Equation Editor Exploit Detection** – Detects obfuscated versions of this long-abused Microsoft Office exploit.

Signal group and threat indicator detecting obfuscated and malformed exploit document

- **Extended PDF Threat Indicators** – Better phishing detection in PDF documents, with new heuristics for malicious links and embedded content.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
