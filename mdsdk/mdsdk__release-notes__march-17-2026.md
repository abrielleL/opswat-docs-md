<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/march-17-2026 -->

# March 17th, 2026

## [Release Note](/docs/mdsdk/release-notes/march-17-2026#release-note)

### [Release Date](/docs/mdsdk/release-notes/march-17-2026#release-date)

- 17/03/2026

### [SDK Version](/docs/mdsdk/release-notes/march-17-2026#sdk-version)

- **Windows**: 4.3.5778.0
- **Linux**: 4.3.4820.0
- **Mac**: 4.3.5219.0

### [Enhancement](/docs/mdsdk/release-notes/march-17-2026#enhancement)

#### [Windows](/docs/mdsdk/release-notes/march-17-2026#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/march-17-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/march-17-2026#mac)

- N/A

### [Bug Fix](/docs/mdsdk/release-notes/march-17-2026#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/march-17-2026#windows)

- Fixed inconsistent detection of ASP.NET Core 3.1 (x86/x64) by updating the detection logic to distinguish between Shared Framework and Targeting Pack components, preventing false vulnerability alerts and repeated runtime installations for a smoother user experience.

#### [Linux](/docs/mdsdk/release-notes/march-17-2026#linux)

- Fixed incorrect patch detection for Snap packages on Ubuntu by enhancing GetMissingPatches to only list updates available for the current channel using snap refresh --list, ensuring accurate patch availability and preventing failed installations for users.
- Fixed missing patch results when system locale was non-English by forcing command output to English, ensuring accurate patch detection for all users regardless of locale.

#### [Mac](/docs/mdsdk/release-notes/march-17-2026#mac)

- N/A

### [New Application Support](/docs/mdsdk/release-notes/march-17-2026#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/march-17-2026#windows)

- Windows | Add support detection for Ivanti Application Control
- Add Support detection for D.Suite/eIDAS
- V4 | Windows | Add Support detection for NAPS2 (Not Another PDF Scanner 2)
- V4 | Windows | Add support for ClickShare App

#### [Linux](/docs/mdsdk/release-notes/march-17-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/march-17-2026#mac)

- N/A

### [New Application Version Support](/docs/mdsdk/release-notes/march-17-2026#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/march-17-2026#windows)

- V4 | Windows | Add support for Acronis Cyber Protection Agent version 26.2.41858
- V4 | Windows | Add support for Mozilla Firefox ESR version 140.8.0
- V4 | Windows | Add support for Microsoft Visual Studio Code (User) (Arm64) version 1.111.0
- V4 | Windows | Add support for Brave version 1.88.127
- V4 | Windows | Add support for Mozilla Firefox (x64) version 148.0.2
- V4 | Windows | Add support for Microsoft Defender ATP version 10.0.26200.7922

#### [Linux](/docs/mdsdk/release-notes/march-17-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/march-17-2026#mac)

- N/A

### [New Method Implementation](/docs/mdsdk/release-notes/march-17-2026#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/march-17-2026#windows)

- [Postman] Postman - Implement GetRunningState for Postman
- [Postman] Postman - Implement TerminateProcesses for Postman
- [Microsoft OneDrive] Microsoft Corporation - Implement GetInstallationDirectories for Microsoft OneDrive (User)
- [Microsoft OneDrive] Microsoft Corporation - Implement GetUninstallHive for Microsoft OneDrive (User)
- [Ivanti Application Control] Ivanti, Inc. - Implement Run for Ivanti Application Control Web Services
- [Ivanti Application Control] Ivanti, Inc. - Implement TerminateProcesses for Ivanti Application Control Web Services
- [Ivanti Application Control] Ivanti, Inc. - Implement GetRunningState for Ivanti Application Control Web Services
- [Ivanti Application Control] Ivanti, Inc. - Implement Run for Ivanti Application Control Console
- [TreeSize Free] JAM Software - Implement TerminateProcesses for TreeSize Free
- [TreeSize Free] JAM Software - Implement GetInstallationDirectories for TreeSize Free
- [TreeSize Free] JAM Software - Implement GetRunningState for TreeSize Free
- [TreeSize Free] JAM Software - Implement Run for TreeSize Free
- [TreeSize Free] JAM Software - Update GetVersion implementation for TreeSize Free
- [WireGuard] WireGuard LLC - Implement TerminateProcesses for WireGuard
- [Dell SupportAssist] Dell Inc. - Update Run implementation for Dell SupportAssist
- [Dell SupportAssist] Dell Inc. - Update TerminateProcesses implementation for Dell SupportAssist
- [Dell SupportAssist] Dell Inc. - Implement GetAgentState for Dell SupportAssist
- [D.Suite/eIDAS] DITEC, a.s. - Implement GetVersion for D.Suite/eIDAS
- [D.Suite/eIDAS] DITEC, a.s. - Implement GetInstallationDirectories for D.Suite/eIDAS
- [D.Suite/eIDAS] DITEC, a.s. - Implement Run for D.Suite/eIDAS
- [D.Suite/eIDAS] DITEC, a.s. - Implement TerminateProcesses for D.Suite/eIDAS
- [D.Suite/eIDAS] DITEC, a.s. - Implement GetRunningState for D.Suite/eIDAS
- [Notepad++] Notepad++ Team - Update GetVersion implementation for Notepad++
- [NAPS2 - Not Another PDF Scanner] NAPS2 Software - Implement GetVersion for NAPS2 - Not Another PDF Scanner

#### [Linux](/docs/mdsdk/release-notes/march-17-2026#linux)

- [Yum] GNU - Update GetMissingPatches implementation for Yum
- [Dandified Yum] Red Hat, Inc. - Update GetMissingPatches implementation for Dandified Yum
- [Dandified Yum] Red Hat, Inc. - Update GetVersion implementation for Dandified Yum
- [Snap] Canonical Ltd. - Update GetMissingPatches implementation for Snap

#### [Mac](/docs/mdsdk/release-notes/march-17-2026#mac)
