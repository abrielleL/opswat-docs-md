<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/january-27-2026 -->

# January 27th, 2026

## [Release Note](/docs/mdsdk/release-notes/january-27-2026#release-note)

### [Release Date](/docs/mdsdk/release-notes/january-27-2026#release-date)

- 27/01/2026

### [SDK Version](/docs/mdsdk/release-notes/january-27-2026#sdk-version)

- **Windows**: 4.3.5558.0
- **Linux**: 4.3.4601.0
- **Mac**: 4.3.5002.0

### [Enhancement](/docs/mdsdk/release-notes/january-27-2026#enhancement)

#### [Windows](/docs/mdsdk/release-notes/january-27-2026#windows)

- Add Vulnerability Management software category

#### [Linux](/docs/mdsdk/release-notes/january-27-2026#linux)

- Add Vulnerability Management software category

#### [Mac](/docs/mdsdk/release-notes/january-27-2026#mac)

- N/A

### [Bug Fix](/docs/mdsdk/release-notes/january-27-2026#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/january-27-2026#windows)

- Fixed application crashes during wa_api_setup when previous log files persist by initializing NtApi before starting log monitoring, ensuring stable setup and smoother user experience.
- Fixed incorrect Citrix Workspace installer download link by updating to the correct version URL, ensuring users always receive the latest version as reported, improving reliability and reducing installation mismatches.
- Fixed SDK crashes caused by a race condition during log cleanup by initializing NtApi before starting log monitoring, ensuring stable setup and smoother user experience.
- Fixed an issue where Office 2019 installers failed with a signature error by adding public keys as a fallback, ensuring reliable downloads and smoother patch management for users.

#### [Linux](/docs/mdsdk/release-notes/january-27-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/january-27-2026#mac)

- N/A

### [New Application Support](/docs/mdsdk/release-notes/january-27-2026#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/january-27-2026#windows)

- Windows | Add Support detection for axesWord
- Windows | Add support detection for NVDA
- Add support detection for eID Client (Slovakia)

#### [Linux](/docs/mdsdk/release-notes/january-27-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/january-27-2026#mac)

- N/A

### [New Application Version Support](/docs/mdsdk/release-notes/january-27-2026#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/january-27-2026#windows)

- V4 | Windows | Add support for Microsoft Office 2021 version 16.0.19530.20184
- V4 | Windows | Add support for Microsoft Office 365 version 16.0.19530.20184
- V4 | Windows | Add support for Dropbox 3+ version 240.4.8493
- V4 | Windows | Add support for Mozilla Firefox ESR version 140.7.0
- V4 | Windows | Add support for Java SE Development Kit version 25.0.2.0
- V4 | Windows | Add support for Brave version 1.86.139
- V4 | Windows | Add support for Microsoft OneDrive version 25.243.1211.0001

#### [Linux](/docs/mdsdk/release-notes/january-27-2026#linux)

- V4 | Linux | Add support for Thunderbird version 147.0
- V4 | Linux | Add support for Visual Studio Code version 1.108.1
- V4 | Linux | Add support for Google Chrome version 144.0.7559.96
- V4 | Linux | Add support for MySQL Workbench version 8.0.46
- V4 | Linux | Add support for MySQL Server version 9.6.0
- V4 | Linux | Add support for Signal version 7.86.0
- V4 | Linux | Add support for GIMP version 3.0.8
- V4 | Linux | Add support for Visual Studio Code version 1.108.2

#### [Mac](/docs/mdsdk/release-notes/january-27-2026#mac)

- N/A

### [New Method Implementation](/docs/mdsdk/release-notes/january-27-2026#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/january-27-2026#windows)

- [Microsoft Visual Studio Code] Microsoft Corporation - Implement IsAuthentic for Microsoft Visual Studio Code
- [Adobe Acrobat Reader DC Continuous] Adobe Systems Inc. - Implement GetUninstallHive for Adobe Acrobat Reader DC Continuous
- [Zoom] Zoom Video Communications, Inc. - Update GetVersion implementation for Zoom exe
- [Zoom] Zoom Video Communications, Inc. - Implement GetVersion for Zoom msi
- [NVDA] NV Access - Implement Run for NVDA
- [NVDA] NV Access - Implement TerminateProcesses for NVDA

#### [Linux](/docs/mdsdk/release-notes/january-27-2026#linux)

- [Thunderbird] Mozilla Corporation - Update GetVersion implementation for Thunderbird
- [FileZilla] FileZilla Project - Implement GetVersion for FileZilla
- [FoxitReader] Foxit Software Inc. - Update GetVersion implementation for FoxitReader
- [TeamViewer] TeamViewer GmbH - Implement GetVersion for TeamViewer
- [TeamViewer Host] TeamViewer GmbH - Implement GetVersion for TeamViewer Host
- [MySQL Server] Oracle Corporation - Update GetVersion implementation for MySQL Server

#### [Mac](/docs/mdsdk/release-notes/january-27-2026#mac)

- [Software Update] Apple Inc. - Update InstallMissingPatches implementation for Software Update
- [Avast One] AVAST Software a.s. - Implement GetVersion for Avast One
- [Avast One] AVAST Software a.s. - Implement Run for Avast One
- [Thunderbird] Mozilla Corporation - Implement Run for Thunderbird
- [Workspace ONE Intelligent Hub] Omnissa, LLC - Implement GetVersion for Workspace ONE Intelligent Hub 24.07+
- [Workspace ONE Intelligent Hub] Omnissa, LLC - Implement GetRunningState for Workspace ONE Intelligent Hub 24.07+
- [Workspace ONE Intelligent Hub] Omnissa, LLC - Implement Run for Workspace ONE Intelligent Hub 24.07+
- [Workspace ONE Intelligent Hub] Omnissa, LLC - Implement GetInstallationDirectories for Workspace ONE Intelligent Hub 24.07+
