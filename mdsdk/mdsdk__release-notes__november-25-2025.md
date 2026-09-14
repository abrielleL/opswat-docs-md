<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/november-25-2025 -->

# November 25th, 2025

## [Release Note](/docs/mdsdk/release-notes/november-25-2025#release-note)

### [Release Date](/docs/mdsdk/release-notes/november-25-2025#release-date)

- 25/11/2025

### [SDK Version](/docs/mdsdk/release-notes/november-25-2025#sdk-version)

- **Windows**: 4.3.5273.0
- **Linux**: 4.3.4332.0
- **Mac**: 4.3.4732.0

### [Enhancement](/docs/mdsdk/release-notes/november-25-2025#enhancement)

#### [Windows](/docs/mdsdk/release-notes/november-25-2025#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/november-25-2025#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/november-25-2025#mac)

- N/A

### [Bug Fix](/docs/mdsdk/release-notes/november-25-2025#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/november-25-2025#windows)

- Fixed incorrect OpenSSL license information in OSSLicense.json by thoroughly reviewing and updating the file, ensuring accurate license details for seamless customer integration and compliance.
- Fixed incorrect detection of CVE-2023-49147 in PDF24 Creator by updating the vulnerability database and adding manual CVE data, ensuring accurate vulnerability reporting and improved security insights for users.
- Fixed GetVersion returning 0.0 for Elastic Agent by enhance data checks, ensuring accurate version detection and compliance for users.
- Fixed installation failures for Notepad++ updates caused by missing digital signature information by adding the required certificate chain and public key, ensuring seamless patching and improved reliability for users.
- Fixed incorrect definition date reporting for Trend Micro Deep Security Agent by updating the SDK to retrieve the latest modified time from the correct pattern and config files, ensuring users always see accurate and up-to-date definition information.
- Fixed installation failures for WinRAR x64 caused by missing digital signature data by adding the required signing information, ensuring seamless patching and improved reliability for users.

#### [Linux](/docs/mdsdk/release-notes/november-25-2025#linux)

- Fixed incorrect OpenSSL license information in OSSLicense.json by thoroughly reviewing and updating the file, ensuring accurate license details for seamless customer integration and compliance.

#### [Mac](/docs/mdsdk/release-notes/november-25-2025#mac)

- N/A

### [New Application Support](/docs/mdsdk/release-notes/november-25-2025#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/november-25-2025#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/november-25-2025#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/november-25-2025#mac)

- N/A

### [New Application Version Support](/docs/mdsdk/release-notes/november-25-2025#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/november-25-2025#windows)

- V4 | Windows | Add support for Adobe Acrobat DC Continuous version 25.001.20937
- V4 | Windows | Add support for Mozilla Firefox (x86) version 145.0.1
- V4 | Windows | Add support for Mozilla Firefox (x64) version 145.0.1
- V4 | Windows | Add support for Microsoft Visual Studio Code (User) (Arm64) version 1.106.2
- V4 | Windows | Add support for Citrix Workspace version 25.8.10.36
- V4 | Windows | Add support for Dropbox 3+ version 237.4.5655
- V4 | Windows | Add support for Mozilla Firefox (arm64) version 145.0.1
- V4 | Windows | Add support for Microsoft Visual Studio Code (User) (Arm64) version 1.106.0

#### [Linux](/docs/mdsdk/release-notes/november-25-2025#linux)

- V4 | Linux | Add support for Wireshark version 4.6.1
- V4 | Linux | Add support for Signal version 7.80.0
- V4 | Linux | Add support for Visual Studio Code version 1.106.2

#### [Mac](/docs/mdsdk/release-notes/november-25-2025#mac)

- N/A

### [New Method Implementation](/docs/mdsdk/release-notes/november-25-2025#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/november-25-2025#windows)

- [Elastic Agent] Elasticsearch B.V. - Update GetVersion implementation for Elastic Agent
- [Dell Peripheral Manager] Dell Inc. - Implement TerminateProcesses for Dell Peripheral Manager
- [Dell Peripheral Manager] Dell Inc. - Implement GetRunningState for Dell Peripheral Manager
- [Dell Peripheral Manager] Dell Inc. - Implement Run for Dell Peripheral Manager
- [Floating License Manager] Schneider Electric - Implement GetRunningState for Floating License Manager
- [Floating License Manager] Schneider Electric - Implement TerminateProcesses for Floating License Manager
- [Floating License Manager] Schneider Electric - Implement Run for Floating License Manager
- [Dell SupportAssist OS Recovery Plugin for Dell Update] Dell Inc. - Implement GetRunningState for Dell SupportAssist OS Recovery Plugin for Dell Update
- [Dell SupportAssist OS Recovery Plugin for Dell Update] Dell Inc. - Implement TerminateProcesses for Dell SupportAssist OS Recovery Plugin for Dell Update
- [Microsoft SQL Server Express] Microsoft Corporation - Update Run implementation for Microsoft SQL Server Express 2022
- [Microsoft 3D Viewer] Microsoft Corporation - Implement Run for Microsoft 3D Viewer (UWP)
- [Microsoft Paint 3D] Microsoft Corporation - Implement Run for Microsoft Paint 3D (UWP)
- [Trend Micro Deep Security Agent] Trend Micro, Inc. - Update GetDefinitionState implementation for Trend Micro Deep Security Agent
- [Dell ControlVault Driver and Firmware] Broadcom - Implement GetVersion for Dell ControlVault Driver and Firmware
- [GiliSoft USB Stick Encryption] GiliSoft International LLC - Implement GetEncryptionState for GiliSoft USB Stick Encryption
- [GiliSoft USB Stick Encryption] GiliSoft International LLC - Implement GetVersion for GiliSoft USB Stick Encryption
- [GiliSoft USB Stick Encryption] GiliSoft International LLC - Implement Run for GiliSoft USB Stick Encryption
- [Microsoft SQL Server] Microsoft Corporation - Update TerminateProcesses implementation for Microsoft SQL Server 2022
- [Microsoft SQL Server] Microsoft Corporation - Update Run implementation for Microsoft SQL Server 2022
- [Microsoft SQL Server] Microsoft Corporation - Update GetRunningState implementation for Microsoft SQL Server 2022
- [Microsoft Visual Studio Code] Microsoft Corporation - Implement Run for Microsoft Visual Studio Code (User) (Arm64)
- [Microsoft Paint 3D] Microsoft Corporation - Implement GetVersion for Microsoft Paint 3D (UWP)
- [Microsoft ASP.NET Core Runtime 9.0] Microsoft Corporation - Implement GetVersion for Microsoft ASP.NET Core Runtime 9.0 (x86)
- [Microsoft ASP.NET Core Runtime 9.0] Microsoft Corporation - Implement GetVersion for Microsoft ASP.NET Core Runtime 9.0 (x64)
- [ManageEngine Endpoint Central - Agent] ZOHO Corp - Update SetAgentState implementation for ManageEngine Endpoint Central - Agent
- [ManageEngine Endpoint Central - Agent] ZOHO Corp - Update GetInstalledPatches implementation for ManageEngine Endpoint Central - Agent
- [ManageEngine Endpoint Central - Agent] ZOHO Corp - Update GetRunningState implementation for ManageEngine Endpoint Central - Agent
- [ManageEngine Endpoint Central - Agent] ZOHO Corp - Update GetMissingPatches implementation for ManageEngine Endpoint Central - Agent
- [ManageEngine Endpoint Central - Agent] ZOHO Corp - Update TerminateProcesses implementation for ManageEngine Endpoint Central - Agent
- [ManageEngine Endpoint Central - Agent] ZOHO Corp - Update Run implementation for ManageEngine Endpoint Central - Agent
- [ManageEngine Endpoint Central - Agent] ZOHO Corp - Implement GetUninstallString for ManageEngine Endpoint Central - Agent
- [ManageEngine Endpoint Central - Agent] ZOHO Corp - Implement GetUninstallHive for ManageEngine Endpoint Central - Agent
- [CCleaner] Piriform Ltd - Update GetVersion implementation for CCleaner

#### [Linux](/docs/mdsdk/release-notes/november-25-2025#linux)

- [FortiClient] Fortinet Inc. - Update GetInstallationDirectories implementation for FortiClient

#### [Mac](/docs/mdsdk/release-notes/november-25-2025#mac)

- [Kaspersky Endpoint Security] Kaspersky Lab - Update GetDefinitionState implementation for Kaspersky Endpoint Security
- [Time Machine] Apple Inc. - Update GetBackupState implementation for Time Machine
- [Thunderbird ESR] Mozilla Corporation - Implement GetVersion for Thunderbird ESR
- [Thunderbird] Mozilla Corporation - Update GetVersion implementation for Thunderbird
