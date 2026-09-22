<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/august-25-2026 -->

# August 25th, 2026

## [Release Note](/docs/mdsdk/release-notes/august-25-2026#release-note)

### [Release Date](/docs/mdsdk/release-notes/august-25-2026#release-date)

- 25/08/2026

### [SDK Version](/docs/mdsdk/release-notes/august-25-2026#sdk-version)

- **Windows**: 4.3.6525.0
- **Linux**: 4.3.5526.0
- **Mac**: 4.3.5914.0

### [Enhancement](/docs/mdsdk/release-notes/august-25-2026#enhancement)

#### [Windows](/docs/mdsdk/release-notes/august-25-2026#windows)

- Revert (rollback) to previous Application version — Phase 1: InstallFromFiles + enable_rollback

#### [Linux](/docs/mdsdk/release-notes/august-25-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/august-25-2026#mac)

- Revert (rollback) to previous Application version — Phase 1: InstallFromFiles + enable_rollback
- macOS | Support GetVersion languages

### [Bug Fix](/docs/mdsdk/release-notes/august-25-2026#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/august-25-2026#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/august-25-2026#linux)

- Fixed Debian vulnerability false positives by updating the ingestion script to correctly capture fixed package versions, improving the accuracy of security reporting for already-patched systems.

#### [Mac](/docs/mdsdk/release-notes/august-25-2026#mac)

- Resolved the exposure of sensitive credentials in decrypted v4Debug logs by implementing a global redaction sweep that masks all sensitive values across every log entry, ensuring user data privacy and security during diagnostic operations.
- Fixed intermittent crashes and high CPU usage during SDK shutdown on macOS by ensuring child processes are reaped synchronously and terminal exit statuses are handled correctly, improving system stability and resource efficiency.
- Resolved missing vulnerability mappings for Microsoft Office on macOS by updating the detection script to include Office Suite products, ensuring comprehensive CVE detection and accurate patch mapping for users.
- [public] Fixed Software Update's GetMissingPatches method returning incorrect patches.type for OS patches.
- Fixed GetPowerOptions (M30007) on macOS reporting the default screen saver timeout instead of the active user's configured value. screen_saver.timeout is now omitted with WAAPI_PARTIAL_SUCCESS when the value can't be read, rather than reported as a default; a user who never changed the setting still gets the macOS default. required_password_timeout now follows the documented contract on macOS: 0 means never, -1 means immediate.

### [New Application Support](/docs/mdsdk/release-notes/august-25-2026#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/august-25-2026#windows)

- V4 | Add support for new product eScan Elite for Business 22.x
- Add AppRemover support for AVG AntiVirus v25.x (Windows)

#### [Linux](/docs/mdsdk/release-notes/august-25-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/august-25-2026#mac)

- [ER] GetInstallPatches to return the the correct amount of information as the results given from GetMissingPatches

### [New Application Version Support](/docs/mdsdk/release-notes/august-25-2026#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/august-25-2026#windows)

- V4 | Add support for new product eScan Elite for Business 22.x
- Add AppRemover support for AVG AntiVirus v25.x (Windows)

#### [Linux](/docs/mdsdk/release-notes/august-25-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/august-25-2026#mac)

- [ER] GetInstallPatches to return the the correct amount of information as the results given from GetMissingPatches

### [New Method Implementation](/docs/mdsdk/release-notes/august-25-2026#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/august-25-2026#windows)

- [eScan Elite for Business] MicroWorld Technologies Inc. - Implement Scan for eScan Elite for Business
- [eScan Elite for Business] MicroWorld Technologies Inc. - Implement GetDefinitionState for eScan Elite for Business
- [eScan Elite for Business] MicroWorld Technologies Inc. - Implement GetRealTimeProtectionState for eScan Elite for Business
- [eScan Elite for Business] MicroWorld Technologies Inc. - Implement GetLastScanTime for eScan Elite for Business
- [eScan Elite for Business] MicroWorld Technologies Inc. - Implement GetScanState for eScan Elite for Business
- [eScan Elite for Business] MicroWorld Technologies Inc. - Implement GetThreats for eScan Elite for Business
- [eScan Elite for Business] MicroWorld Technologies Inc. - Implement UpdateDefinitions for eScan Elite for Business
- [eScan Elite for Business] MicroWorld Technologies Inc. - Implement GetInstallationDirectories for eScan Elite for Business
- [eScan Elite for Business] MicroWorld Technologies Inc. - Implement Run for eScan Elite for Business
- [eScan Elite for Business] MicroWorld Technologies Inc. - Implement GetVersion for eScan Elite for Business
- [eScan Elite for Business] MicroWorld Technologies Inc. - Implement GetRunningState for eScan Elite for Business
- [npm] Joyent, Inc. - Implement GetVersion for npm
- [npm] Joyent, Inc. - Implement GetUninstallHive for npm
- [Camtasia Studio] TechSmith Corporation - Implement TerminateProcesses for Camtasia Studio 2025
- [Camtasia Studio] TechSmith Corporation - Implement GetRunningState for Camtasia Studio 2025
- [Camtasia Studio] TechSmith Corporation - Implement GetVersion for Camtasia Studio 2025
- [Camtasia Studio] TechSmith Corporation - Implement TerminateProcesses for Camtasia Studio 2026
- [Camtasia Studio] TechSmith Corporation - Implement GetRunningState for Camtasia Studio 2026
- [Camtasia Studio] TechSmith Corporation - Implement GetVersion for Camtasia Studio 2026
- [Java] Oracle Corporation - Update GetUninstallString implementation for Java 7
- [Java] Oracle Corporation - Update GetUninstallHive implementation for Java 6
- [Java] Oracle Corporation - Update GetUninstallString implementation for Java 6
- [Java] Oracle Corporation - Update GetUninstallHive implementation for Java 7
- [PDF-XChange] Tracker Software Products Ltd. - Implement GetInstallationDirectories for PDF-XChange Editor (Arm64)

#### [Linux](/docs/mdsdk/release-notes/august-25-2026#linux)

- [npm] Joyent, Inc. - Implement GetVersion for npm
- [npm] Joyent, Inc. - Implement GetComponents for npm
- [npm] Joyent, Inc. - Implement GetInstallationDirectories for npm

#### [Mac](/docs/mdsdk/release-notes/august-25-2026#mac)

- [npm] Joyent, Inc. - Implement GetVersion for npm
- [npm] Joyent, Inc. - Implement GetInstallationDirectories for npm
- [npm] Joyent, Inc. - Implement IsAuthentic for npm
- [Thunderbird] Mozilla Corporation - Update GetVersion implementation for Thunderbird
- [Thunderbird] Mozilla Corporation - Update GetVersion implementation for Thunderbird
- [Software Update] Apple Inc. - Update GetInstalledPatches implementation for Software Update
- [Software Update] Apple Inc. - Update GetMissingPatches implementation for Software Update
