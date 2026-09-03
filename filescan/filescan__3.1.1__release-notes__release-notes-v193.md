<!-- source: https://www.opswat.com/docs/filescan/3.1.1/release-notes/release-notes-v193 -->

# Release Notes for v1.9.3

---

## [Date: 26 March, 2024](/docs/filescan/3.1.1/release-notes/release-notes-v193#date-26-march-2024)

**Added:**

- Python Unpacking & Decompilation for PyInstaller, Nuitka, and py2exe

- Extended the malware configuration extractor to support the Cobalt Strike malware family

- Included disassembly of exported functions for Windows binaries
- Threat indicator to flag when executable files have two different sections with the same section name
- Extraction of VBA macro code from DWG files (shown as OLE Stream in File Details section)
- Support for MITRE Att&ack technique mapping from Yara rule metadata

- New DotnetInfo tab in the File Details section for .NET executables
- Added the “auditor” role, which functions as a read-only admin role
- MISP integration options in Admin Settings, see details at [MISP](/docs/filescan/3.1.1/integrations/misp)
- Added support for new Sandbox installations on Ubuntu 22.04 (it will be possible to upgrade the OS on older installations with the next major release coming later in 2024)

**Changed:**

- Improved proxy handling and proxy related bug fixes, see configuration details at [Proxy Usage](/docs/filescan/3.1.1/installation/installation-with-proxy)
- Enhanced script language detection using the guesslang library
- Fine-tuned several threat indicators to reduce false positive ratio
- Return "Unknown" verdict if no threat indicators are generated for URL and file submissions
- Improved detection for phishing calendar invites
- Enhanced recursive analysis of active content containers (email, Office documents, PDF, etc.)
- Improved scan process for corrupt OLE2 documents
- Return HTTP 429 responses to new scan requests when the scan queue is full
- Long-running scans are cancelled after user-defined timeout
- Show queue count statistics in Admin Panel/Statistics/Jobs/Scan Health
- Enhanced system resilience by continuing interrupted scans after a queue restart
- Improved URL rendering to bypass simple human verification check boxes (e.g. Cloudflare)
- Improved compatibility for filenames with special characters

**Fixed:**

- Resolved issues with license actions (deactivation, inconsistent states)
- Fixed several issues with existing threat indicators (ELF binaries, URL extraction, EML)
- Enhanced Application Security measures, especially for URL emulation
- Invitation links should work even if the "Sign up" feature is disabled
- Extended functional tests for the Webservice API and resolved potential runtime issues
- Fixed simple search not working for tags, e.g. #html
- URL preview should be displayed automatically on URL details page
- Only execute Similarity Search if the original verdict matches the specified configuration

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
