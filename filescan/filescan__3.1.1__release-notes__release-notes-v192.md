<!-- source: https://www.opswat.com/docs/filescan/3.1.1/release-notes/release-notes-v192 -->

# Release Notes for v1.9.2

---

## [Date: 24 January, 2024](/docs/filescan/3.1.1/release-notes/release-notes-v192#date-24-january-2024)

**Added:**

- New indicators for Windows APIs related to specific activities
- Implemented flagging for LSASS dump using minidump
- Extracted remote templates inside xTable struct in MS Office documents
- Implemented parser for Debian packages

**Changed:**

- Renamed OPSWAT Filescan Sandbox to [**MetaDefender Sandbox**](https://www.opswat.com/products/metadefender/sandbox)
- Expanded malware configuration extractors to encompass the latest and most pertinent threats
- Improved detection of dynamic syscalls using the HellsGate bypass technique
- Enhanced Quishing and Phishing email detection
- Improved the capabilities of Batch, CSV, HTA, JavaScript, LNK, PowerShell, VBA, and VBScript emulation and fine-tuned timeout handling
- Extended log messages to provide better traceability across various system components

**Fixed:**

- Pinned the installed Docker version to 24 due to the breaking changes introduced in Docker 25
- Enhanced Application Security measures, especially for PowerShell emulation
- Fixed incomplete invitation URLs in User Management
- Resolved file scanning issue when file content was sent to the API in JSON body
- Fixed the MISP format when exporting scan reports
- Refactored functional tests for the Webservice API and resolved potential runtime issues
- Fixed several UTF-8 parsing issues in content parsers (related to HTML & OLE files)
- Ensured that all whitelisted submissions get the Benign verdict
- Improved the stability of concurrent OSINT lookup tasks

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
