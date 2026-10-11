<!-- source: https://www.opswat.com/docs/filescan/3.2.0/release-notes/release-notes-v200 -->

# Release Notes for v2.0.0

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Date: 18 July, 2024](/docs/filescan/3.2.0/release-notes/release-notes-v200#date-18-july-2024)

Warning

This version is not suitable for a clean Sandbox installation. Please **use version 2.1.0 or later** for clean installations!

**Added:**

- New Streamlined Design for the User Interface

- Support for the installation of MetaDefender Sandbox on offline systems: [Offline Installation](/docs/filescan/3.2.0/installation/offline-installation)
- Audit Logger framework for admin settings and user authentication events: [Audit Logging for Admin Settings and User Authentication](/docs/filescan/3.2.0/configuration/audit-logger)

- Support for AutoIT script files, including compiled AutoIT Portable Executables

- Parsing of MSI metadata and actions, including implementation for filtered file extraction
- Parsing of ODF files and macro extraction
- Parsing of Python pickle files, including implementation for malicious Threat Indicators
- Capability to identify potential obfuscation for extracted macro code
- New Threat Indicator for deceptive filenames commonly used for phishing files
- New Threat Indicator for undetected Equation Editor RTF exploit
- New single configuration option for offline mode
- Introduced a Machine Learning model to identify suspicious URLs even in offline mode (this experimental feature is only enabled by default in offline mode): auto$

**Changed:**

- **Potentially Breaking API change:** The **INFORMATIONAL** verdict was renamed to **NO_THREAT** in the API results to be consistent with the “No Threat” verdict shown on the UI
- Changed the required operating system to Ubuntu 22.04 LTS. Existing Sandbox installations on Ubuntu 20.04 must be upgraded to 22.04 before installing Sandbox 2.0.0: [Operating System Upgrade](/docs/filescan/3.2.0/installation/operating-system-upgrade)
- Modified the system architecture to run all Sandbox components in Docker containers. This change improves application security and reduces the overall installation time to about 20 minutes
- Upgraded to Java 17 and Python 3.10 for all relevant Sandbox components
- Renamed the `fsiolog` command to `sblog` (used to watch Sandbox logs in real time)
- Enhanced parsing of LNK metadata and actions, including new Threat Indicators
- Improved Python-specific Threat Indicators
- Added context info to strings originating from extracted files
- Include proper tags for Golang, Rust and compiled-Python Portable Executables
- Improved processing for nested extracted files
- Enhanced Threat Indicators for imported APIs and emulation respectively
- Improved OSINT lookup workflow
- Changed the default verdict to NO_THREAT if no Threat Indicators are found
- Disabled the ClamAV task by default for improved performance
- Improved URL analysis performance and stability
- Reduced the scan time overhead associated with the webservice component

**Fixed:**

- Fixed minor bugs and misdetections
- Improved application security
- Improved emulation efficacy
- Improved application performance and stability
- Resolved file upload issue in the MetaDefender Core MultiScanning integration
- Fixed an issue causing the remaining daily scan count decreasing without actual scans
- Scan reports are marked as finished if a non-essential subtask reaches a timeout

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
