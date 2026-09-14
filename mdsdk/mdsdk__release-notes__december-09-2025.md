<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/december-09-2025 -->

# December 09th, 2025

## [Release Note](/docs/mdsdk/release-notes/december-09-2025#release-note)

### [Release Date](/docs/mdsdk/release-notes/december-09-2025#release-date)

- 09/12/2025

### [SDK Version](/docs/mdsdk/release-notes/december-09-2025#sdk-version)

- **Windows**: 4.3.5336.0
- **Linux**: 4.3.4392.0
- **Mac**: 4.3.4792.0

### [Enhancement](/docs/mdsdk/release-notes/december-09-2025#enhancement)

#### [Windows](/docs/mdsdk/release-notes/december-09-2025#windows)

- Rebrand our SDK docs to OESIS Framework

#### [Linux](/docs/mdsdk/release-notes/december-09-2025#linux)

- Rebrand our SDK docs to OESIS Framework

#### [Mac](/docs/mdsdk/release-notes/december-09-2025#mac)

- N/A

### [Bug Fix](/docs/mdsdk/release-notes/december-09-2025#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/december-09-2025#windows)

- Ensure {{wa_api_teardown}} cleans up cache files correctly in all cases and that no allocated resources remain on the endpoint.
- Fixed incorrect patch status reporting for Microsoft Office 2007 MSI by creating a dedicated feed and updating detection signatures, ensuring GetProductPatchLevel now accurately reflects the latest version so users see correct patch status after updates.
- Fixed incorrect reporting of Elastic Agent virus signatures as up-to-date by requiring admin permission, verifying both Elastic Agent and ElasticEndpoint services are running, and using agent status and fleet connectivity checks, ensuring users receive accurate compliance and protection status.

#### [Linux](/docs/mdsdk/release-notes/december-09-2025#linux)

- Fixed the issue where GetProductVulnerability returned errors due to dnf version command timeouts by enhancing the GetVersion method, ensuring reliable vulnerability detection and accurate results for users on RHEL 10.

#### [Mac](/docs/mdsdk/release-notes/december-09-2025#mac)

- N/A

### [New Application Support](/docs/mdsdk/release-notes/december-09-2025#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/december-09-2025#windows)

- Add support for Comet AI based browser

#### [Linux](/docs/mdsdk/release-notes/december-09-2025#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/december-09-2025#mac)

- N/A

### [New Application Version Support](/docs/mdsdk/release-notes/december-09-2025#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/december-09-2025#windows)

- V4 | Windows | Add support for Microsoft OneDrive version 25.222.1112.0002
- V4 | Windows | Add support for Sentinel Agent version 25.2.2.380
- V4 | Windows | Add support for FileZilla version 3.69.5
- V4 | Windows | Add support for Adobe Acrobat DC Continuous version 25.001.20982
- V4 | Windows | Add support for Brave version 1.85.111
- V4 | Windows | Add support for Microsoft Visual Studio Code (User) (Arm64) version 1.106.3
- V4 | Windows | Add support for Microsoft Visual Studio Code (Arm64) version 1.106.3
- V4 | Windows | Add support for Microsoft OneDrive version 25.216.1104.0002

#### [Linux](/docs/mdsdk/release-notes/december-09-2025#linux)

- V4 | Linux | Add support for Signal version 7.81.0
- V4 | Linux | Add support for Wireshark version 4.6.2
- V4 | Linux | Add support for Zoom version 6.6.11

#### [Mac](/docs/mdsdk/release-notes/december-09-2025#mac)

- N/A

### [New Method Implementation](/docs/mdsdk/release-notes/december-09-2025#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/december-09-2025#windows)

- [Wise Folder Hider] WiseCleaner - Implement GetRunningState for Wise Folder Hider
- [Wise Folder Hider] WiseCleaner - Implement TerminateProcesses for Wise Folder Hider
- [MongoDB Community Server] MongoDB, Inc. - Implement GetInstallationDirectories for MongoDB Community Server 8.0
- [Elastic Agent] Elasticsearch B.V. - Update GetDefinitionState implementation for Elastic Agent
- [Microsoft Office 365] Microsoft Corporation - Implement GetRunningState for Microsoft Office 365
- [Microsoft Office 365] Microsoft Corporation - Implement TerminateProcesses for Microsoft Office 365
- [Microsoft Office 365] Microsoft Corporation - Implement GetComponents for Microsoft Office 365
- [Microsoft Office 365] Microsoft Corporation - Update GetInstallationDirectories implementation for Microsoft Office 365
- [Acronis Cyber Protection Agent] Acronis - Implement Run for Acronis Cyber Protection Agent
- [Acronis Cyber Protection Agent] Acronis - Update GetLastScanTime implementation for Acronis Cyber Protection Agent
- [pgAdmin 4] The pgAdmin Development Team - Update GetRunningState implementation for pgAdmin 4 v4
- [Symantec Endpoint Encryption] Symantec Corporation - Update GetEncryptionState implementation for Symantec Endpoint Encryption
- [Microsoft Visual Studio Code] Microsoft Corporation - Implement Run for Microsoft Visual Studio Code (Arm64)
- [Microsoft Visual Studio Code] Microsoft Corporation - Implement TerminateProcesses for Microsoft Visual Studio Code (Arm64)
- [Microsoft Visual Studio Code] Microsoft Corporation - Update TerminateProcesses implementation for Microsoft Visual Studio Code (User) (Arm64)
- [ArcGIS Pro] Environmental Systems Research Institute, Inc. - Implement GetVersion for ArcGIS Pro
- [Heimdal Thor Agent] Heimdal Security - Update GetRealTimeProtectionState implementation for Heimdal Thor Agent
- [Heimdal Thor Agent] Heimdal Security - Update GetDefinitionState implementation for Heimdal Thor Agent

#### [Linux](/docs/mdsdk/release-notes/december-09-2025#linux)

- [Dandified Yum] Red Hat, Inc. - Update GetVersion implementation for Dandified Yum

#### [Mac](/docs/mdsdk/release-notes/december-09-2025#mac)

- [ManyCam] ManyCam ULC. - Update GetVersion implementation for ManyCam
- [CleanMyMac X] MacPaw Inc. - Update GetDefinitionState implementation for CleanMyMac X
- [CleanMyMac X] MacPaw Inc. - Update GetRealTimeProtectionState implementation for CleanMyMac X
