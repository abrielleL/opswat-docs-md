<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/march-31-2026 -->

# March 31st, 2026

## [Release Note](/docs/mdsdk/release-notes/march-31-2026#release-note)

### [Release Date](/docs/mdsdk/release-notes/march-31-2026#release-date)

- 31/03/2026

### [SDK Version](/docs/mdsdk/release-notes/march-31-2026#sdk-version)

- **Windows**: 4.3.5842.0
- **Linux**: 4.3.4881.0
- **Mac**: 4.3.5280.0

### [Enhancement](/docs/mdsdk/release-notes/march-31-2026#enhancement)

#### [Windows](/docs/mdsdk/release-notes/march-31-2026#windows)

- Introduce v2mod-vuln-oft-extra.dat

#### [Linux](/docs/mdsdk/release-notes/march-31-2026#linux)

- Introduce v2mod-vuln-oft-extra.dat
- Delta file architecture for liv.dat

#### [Mac](/docs/mdsdk/release-notes/march-31-2026#mac)

- N/A

### [Bug Fix](/docs/mdsdk/release-notes/march-31-2026#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/march-31-2026#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/march-31-2026#linux)

- Fixed patch installation failures for the "kernel" package on RHEL 10 by adding a mechanism to handle required system reboots during patching, ensuring accurate status reporting and smoother updates for users.

#### [Mac](/docs/mdsdk/release-notes/march-31-2026#mac)

- N/A

### [New Application Support](/docs/mdsdk/release-notes/march-31-2026#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/march-31-2026#windows)

- Windows | Add support for Miniforge3
- Windows | Add support detection for FabaSoft Folio Client

#### [Linux](/docs/mdsdk/release-notes/march-31-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/march-31-2026#mac)

- N/A

### [New Application Version Support](/docs/mdsdk/release-notes/march-31-2026#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/march-31-2026#windows)

- V4 | Windows | Add support for Mozilla Firefox (x86) version 149.0
- V4 | Windows | Add support for Windows Defender version 4.18.26010.5
- V4 | Windows | Add support for CrowdStrike Falcon version 7.34.20610.0

#### [Linux](/docs/mdsdk/release-notes/march-31-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/march-31-2026#mac)

- N/A

### [New Method Implementation](/docs/mdsdk/release-notes/march-31-2026#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/march-31-2026#windows)

- [Atera Agent] Atera Networks - Implement GetVersion for Atera Agent
- [Atera Agent] Atera Networks - Implement GetRunningState for Atera Agent
- [Atera Agent] Atera Networks - Implement Run for Atera Agent
- [Atera Agent] Atera Networks - Implement TerminateProcesses for Atera Agent
- [Atera Agent] Atera Networks - Implement GetUninstallString for Atera Agent
- [Atera Agent] Atera Networks - Implement GetUninstallHive for Atera Agent
- [Mozilla Firefox] Mozilla Corporation - Update SetAntiphishingState implementation for Mozilla Firefox (x86)
- [1Password] AgileBits - Update TerminateProcesses implementation for 1Password msix
- [Miniforge3] conda-forge - Implement GetComponents for Miniforge3 25
- [Miniforge3] conda-forge - Implement GetUninstallString for Miniforge3 25
- [Miniforge3] conda-forge - Update TerminateProcesses implementation for Miniforge3 24
- [TreeSize Professional] JAM Software - Update GetVersion implementation for TreeSize Professional
- [TreeSize Professional] JAM Software - Implement GetVersion for TreeSize Professional
- [TikTok] Bytedance Pte. Ltd. - Implement GetVersion for TikTok
- [SimpleHelp Support Server] SimpleHelp Ltd - Implement Run for SimpleHelp Support Server
- [SimpleHelp Support Server] SimpleHelp Ltd - Implement TerminateProcesses for SimpleHelp Support Server
- [ngrok] ngrok Inc. - Implement Run for ngrok

#### [Linux](/docs/mdsdk/release-notes/march-31-2026#linux)

- [Yum] GNU - Update GetMissingPatches implementation for Yum
- [Snap] Canonical Ltd. - Update GetMissingPatches implementation for Snap
- [Snap] Canonical Ltd. - Update GetInstalledPatches implementation for Snap
- [Zypper] SUSE LINUX GmbH - Update GetMissingPatches implementation for Zypper
- [Dandified Yum] Red Hat, Inc. - Update GetInstalledPatches implementation for Dandified Yum
- [Dandified Yum] Red Hat, Inc. - Update GetMissingPatches implementation for Dandified Yum
- [Yum] GNU - Update GetInstalledPatches implementation for Yum

#### [Mac](/docs/mdsdk/release-notes/march-31-2026#mac)

- [Software Update] Apple Inc. - Update InstallMissingPatches implementation for Software Update
- [ClamXav] ClamWin Pty Ltd - Implement Run for ClamXav
- [ClamXav] ClamWin Pty Ltd - Implement GetRealTimeProtectionState for ClamXav
- [ClamXav] ClamWin Pty Ltd - Implement GetVersion for ClamXav
- [ClamXav] ClamWin Pty Ltd - Implement GetInstallationDirectories for ClamXav
- [ClamXav] ClamWin Pty Ltd - Update GetDefinitionState implementation for ClamXav
- [Rapid7 Insight Agent] Rapid7 - Implement GetVersion for Rapid7 Insight Agent
