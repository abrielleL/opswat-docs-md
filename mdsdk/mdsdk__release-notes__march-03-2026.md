<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/march-03-2026 -->

# March 03rd, 2026

## [Release Note](/docs/mdsdk/release-notes/march-03-2026#release-note)

### [Release Date](/docs/mdsdk/release-notes/march-03-2026#release-date)

- 03/03/2026

### [SDK Version](/docs/mdsdk/release-notes/march-03-2026#sdk-version)

- **Windows**: 4.3.5715.0
- **Linux**: 4.3.4667.0
- **Mac**: 4.3.5156.0

### [Enhancement](/docs/mdsdk/release-notes/march-03-2026#enhancement)

#### [Windows](/docs/mdsdk/release-notes/march-03-2026#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/march-03-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/march-03-2026#mac)

- N/A

### [Bug Fix](/docs/mdsdk/release-notes/march-03-2026#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/march-03-2026#windows)

- Fixed incorrect detection of Office 365 Semi-Annual channel as Current by updating channel identification logic to prioritize the UpdateChannel registry field, ensuring accurate vulnerability reporting and eliminating false CVE alerts for users.
- Fixed failed Zoom x64 installer downloads and installations caused by outdated digital signatures by updating the public key for Zoom EXE and MSI files, ensuring users can reliably download and install the latest certified Zoom versions.

#### [Linux](/docs/mdsdk/release-notes/march-03-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/march-03-2026#mac)

- N/A

### [New Application Support](/docs/mdsdk/release-notes/march-03-2026#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/march-03-2026#windows)

- Windows | Add support detection for Ivanti Application Control
- Windows | Add support detection for Ivanti Environment Manager
- V4 | Windows | Add support for Mozilla Firefox (UWP)
- V4 | Linux | Add support for Cato Client
- V4 | Linux | Add support for Beyond Identity
- V4 | Windows | Add support for Cisco Secure Client Store (Cisco AnyConnect Store)
- Support Detection for Cisco Data Loss Prevention
- V4 | Mac | Add support for Amazon Workspaces

#### [Linux](/docs/mdsdk/release-notes/march-03-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/march-03-2026#mac)

- N/A

### [New Application Version Support](/docs/mdsdk/release-notes/march-03-2026#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/march-03-2026#windows)

- V4 | Windows | Add support for Thunderbird (x86) version 147.0
- V4 | Windows | Add support for Microsoft Office 365 version 16.0.19628.20204
- V4 | Windows | Add support for Google Chrome version 145.0.7632.68
- V4 | Windows | Add support for Microsoft Office 2021 version 16.0.19628.20204
- V4 | Windows | Adobe Acrobat DC Continuous version 25.001.21184
- V4 | Windows | Add support for Microsoft Visual Studio Code version 1.109.2
- V4 | Windows | Add support for Microsoft Visual Studio Code (User) (Arm64) version 1.109.2
- V4 | Windows | Add support for Microsoft Visual Studio Code (Arm64) version 1.109.2
- V4 | Windows | Add support for Mozilla Firefox (arm64) version 147.0.3

#### [Linux](/docs/mdsdk/release-notes/march-03-2026#linux)

- V4 | Linux | Add support for RockyLinux 10 10.1
- V4 | Linux | Add support for AlmaLinux 10.1
- V4 | Linux | Add support for Signal version 7.89.0
- V4 | Linux | Add support for Google Chrome version 145.0.7632.67
- V4 | Linux | Add support for LinuxMint Zena 22.3
- V4 | Linux | Add support for Google Chrome version 144.0.7559.132

#### [Mac](/docs/mdsdk/release-notes/march-03-2026#mac)

- N/A

### [New Method Implementation](/docs/mdsdk/release-notes/march-03-2026#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/march-03-2026#windows)

- [Thunderbird] Mozilla Corporation - Implement Run for Thunderbird (x86)
- [Thunderbird] Mozilla Corporation - Update GetInstallationDirectories implementation for Thunderbird (x86)
- [Thunderbird] Mozilla Corporation - Update GetUninstallHive implementation for Thunderbird (x86)
- [Ivanti Application Control Agent] Ivanti, Inc. - Update TerminateProcesses implementation for Ivanti Application Control Agent
- [Ivanti Application Control Agent] Ivanti, Inc. - Update Run implementation for Ivanti Application Control Agent
- [Ivanti Environment Manager Agent] Ivanti, Inc. - Update Run implementation for Ivanti Environment Manager Agent
- [Ivanti Environment Manager Agent] Ivanti, Inc. - Update TerminateProcesses implementation for Ivanti Environment Manager Agent
- [Microsoft Defender ATP] Microsoft Corporation - Update GetDefinitionState implementation for Microsoft Defender ATP
- [Microsoft Defender ATP] Microsoft Corporation - Implement UpdateDefinitions for Microsoft Defender ATP
- [Ivanti Application Control Agent] Ivanti, Inc. - Implement Run for Ivanti Application Control Agent
- [Ivanti Application Control Agent] Ivanti, Inc. - Implement GetRunningState for Ivanti Application Control Agent
- [Ivanti Application Control Agent] Ivanti, Inc. - Implement TerminateProcesses for Ivanti Application Control Agent
- [Ivanti Environment Manager Agent] Ivanti, Inc. - Implement Run for Ivanti Environment Manager Agent
- [Ivanti Environment Manager Agent] Ivanti, Inc. - Implement TerminateProcesses for Ivanti Environment Manager Agent
- [Mozilla Firefox] Mozilla Corporation - Implement GetUninstallString for Mozilla Firefox (UWP)
- [Mozilla Firefox] Mozilla Corporation - Implement GetUninstallHive for Mozilla Firefox (UWP)
- [Comet] The Comet Authors - Implement Run for Comet
- [Cisco Secure Client (UWP)] Cisco Systems, Inc. - Implement GetVersion for Cisco Secure Client (UWP)
- [Cisco Secure Client (UWP)] Cisco Systems, Inc. - Implement GetUninstallString for Cisco Secure Client (UWP)
- [Cisco Secure Client (UWP)] Cisco Systems, Inc. - Implement GetUninstallHive for Cisco Secure Client (UWP)
- [Cisco Secure Client (UWP)] Cisco Systems, Inc. - Implement Run for Cisco Secure Client (UWP)
- [Endpoint Protector Client] CoSoSys Ltd. - Implement GetUninstallHive for Endpoint Protector Client
- [Endpoint Protector Client] CoSoSys Ltd. - Implement GetRunningState for Endpoint Protector Client
- [Endpoint Protector Client] CoSoSys Ltd. - Implement GetUninstallString for Endpoint Protector Client
- [SecureDoc] WinMagic Inc. - Implement GetRunningState for SecureDoc
- [Browser Operator] The Browser Operator Authors - Implement IsDefaultBrowser for Browser Operator
- [Browser Operator] The Browser Operator Authors - Implement GetAntiphishingState for Browser Operator
- [Browser Operator] The Browser Operator Authors - Implement GetPlugins for Browser Operator
- [Cisco Secure Client - Endpoint Data Loss Prevention] Cisco Systems, Inc. - Implement GetRunningState for Cisco Secure Client - Endpoint Data Loss Prevention
- [Cisco Secure Client - Endpoint Data Loss Prevention] Cisco Systems, Inc. - Implement Run for Cisco Secure Client - Endpoint Data Loss Prevention
- [Microsoft Office 365] Microsoft Corporation - Update GetVersion implementation for Microsoft Office 365
- [Miniforge3] conda-forge - Implement TerminateProcesses for Miniforge3 25
- [Miniforge3] conda-forge - Implement GetRunningState for Miniforge3 25
- [Miniforge3] conda-forge - Implement TerminateProcesses for Miniforge3 24
- [Miniforge3] conda-forge - Implement GetRunningState for Miniforge3 24
- [Miniforge3] conda-forge - Implement GetVersion for Miniforge3 25
- [Miniforge3] conda-forge - Implement GetVersion for Miniforge3 24

#### [Linux](/docs/mdsdk/release-notes/march-03-2026#linux)

- [Beyond Identity] Beyond Identity, Inc. - Implement GetRunningState for Beyond Identity
- [Beyond Identity] Beyond Identity, Inc. - Implement TerminateProcesses for Beyond Identity
- [Cato Client] Cato Networks - Implement Run for Cato Client
- [Cato Client] Cato Networks - Implement GetVersion for Cato Client

#### [Mac](/docs/mdsdk/release-notes/march-03-2026#mac)

- [Endpoint Protector Client] CoSoSys Ltd. - Implement GetRunningState for Endpoint Protector Client
- [Browser Operator] The Browser Operator Authors - Implement GetAntiphishingState for Browser Operator
- [Browser Operator] The Browser Operator Authors - Implement IsDefaultBrowser for Browser Operator
- [Browser Operator] The Browser Operator Authors - Implement GetPlugins for Browser Operator
- [Comet] The Comet Authors - Implement IsDefaultBrowser for Comet
- [Comet] The Comet Authors - Implement GetAntiphishingState for Comet
- [Comet] The Comet Authors - Implement GetPlugins for Comet
- [Comet] The Comet Authors - Implement GetVersion for Comet
- [Comet] The Comet Authors - Implement Run for Comet
- [Dia] The Browser Company of New York - Implement GetPlugins for Dia
- [Firefox] Mozilla Corporation - Update GetVersion implementation for Firefox
- [FileVault] Apple Inc. - Update GetEncryptionState implementation for FileVault
- [Amazon WorkSpaces] Amazon Web Services, Inc - Implement IsAuthentic for Amazon WorkSpaces
