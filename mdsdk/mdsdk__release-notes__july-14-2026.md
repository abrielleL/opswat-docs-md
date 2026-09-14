<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/july-14-2026 -->

# July 14th, 2026

## [Release Note](/docs/mdsdk/release-notes/july-14-2026#release-note)

### [Release Date](/docs/mdsdk/release-notes/july-14-2026#release-date)

- 14/07/2026

### [SDK Version](/docs/mdsdk/release-notes/july-14-2026#sdk-version)

- **Windows**: 4.3.6344.0
- **Linux**: 4.3.5313.0
- **Mac**: 4.3.5703.0

### [Enhancement](/docs/mdsdk/release-notes/july-14-2026#enhancement)

#### [Windows](/docs/mdsdk/release-notes/july-14-2026#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/july-14-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/july-14-2026#mac)

- N/A

### [Bug Fix](/docs/mdsdk/release-notes/july-14-2026#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/july-14-2026#windows)

- Resolved the discrepancy between the Patch Management support chart and analog data by synchronizing Node.js version support for Windows and macOS, improving the accuracy of product patching information for users.

#### [Linux](/docs/mdsdk/release-notes/july-14-2026#linux)

- Resolved the discrepancy between the Patch Management support chart and analog data by synchronizing Node.js version support for Windows and macOS, improving the accuracy of product patching information for users.

#### [Mac](/docs/mdsdk/release-notes/july-14-2026#mac)

- Resolved a hang occurring when users cancel macOS update downloads by implementing a stall-detection mechanism with idle timeouts and terminal output markers, ensuring the SDK remains responsive and provides accurate status reports.
- Resolved the discrepancy between the Patch Management support chart and analog data by synchronizing Node.js version support for Windows and macOS, improving the accuracy of product patching information for users.

### [New Application Support](/docs/mdsdk/release-notes/july-14-2026#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/july-14-2026#windows)

- Add support for Acronis Cyber Protection Agent 26.5.x
- Windows | Add Support detection for Microsoft Copilot
- Windows | Add support detection for Github Copilot

#### [Linux](/docs/mdsdk/release-notes/july-14-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/july-14-2026#mac)

- macOS | Add support auto-patching for Rectangle
- macOS | Add support auto-patching for iTerm2
- V4 | MAC | Request support for FileVault 27.x
- Mac OS X Builtin Gatekeeper 27 - Detection Support
- [W:5] macOS | Add support detection for Pieces (for Developers)
- [W:5] macOS | Add support detection for Cody
- [W:5] macOS | Add support detection for Continue
- [W:5] macOS | Add support detection for GitHub Copilot CLI
- [W:5] macOS | Add support detection for Claude CLI
- Mac OS X Builtin Firewall (mac) ver 27.x

### [New Application Version Support](/docs/mdsdk/release-notes/july-14-2026#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/july-14-2026#windows)

- Add support for Acronis Cyber Protection Agent 26.5.x
- V4 | Windows | Add support for Microsoft Visual Studio Code (Arm64) version 1.128.0
- V4 | Windows | Add support for Microsoft Visual Studio Code (User) (Arm64) version 1.128.0
- V4 | Windows | Add support for 7-Zip (arm64) version 26.02
- V4 | Windows | Add support for Mozilla Firefox (arm64) version 152.0.5

#### [Linux](/docs/mdsdk/release-notes/july-14-2026#linux)

- V4 | Linux | Add support for Mozilla Firefox version 152.0.5
- V4 | Linux | Add support for RockyLinux version 9.8
- V4 | Linux | Add support for RockyLinux version 10.2

#### [Mac](/docs/mdsdk/release-notes/july-14-2026#mac)

- V4 | MAC | Request support for FileVault 27.x
- Mac OS X Builtin Gatekeeper 27 - Detection Support
- Mac OS X Builtin Firewall (mac) ver 27.x

### [New Method Implementation](/docs/mdsdk/release-notes/july-14-2026#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/july-14-2026#windows)

- [UltraEdit] IDM Computer Solutions, Inc. - Implement TerminateProcesses for UltraEdit
- [UltraEdit] IDM Computer Solutions, Inc. - Implement Run for UltraEdit
- [UltraEdit] IDM Computer Solutions, Inc. - Implement GetRunningState for UltraEdit
- [SeaTools for Windows] Seagate Technology - Implement Run for SeaTools for Windows
- [SeaTools for Windows] Seagate Technology - Implement GetInstallationDirectories for SeaTools for Windows
- [WinDirStat] Seifert - Implement Run for WinDirStat
- [Absolute Uninstaller] Glarysoft Ltd - Implement GetVersion for Absolute Uninstaller
- [Absolute Uninstaller] Glarysoft Ltd - Implement Run for Absolute Uninstaller
- [JetBrains YouTrack] JetBrains - Implement TerminateProcesses for JetBrains YouTrack
- [JetBrains YouTrack] JetBrains - Implement Run for JetBrains YouTrack
- [JetBrains YouTrack] JetBrains - Implement GetRunningState for JetBrains YouTrack
- [JetBrains YouTrack] JetBrains - Implement GetVersion for JetBrains YouTrack
- [JetBrains YouTrack] JetBrains - Implement GetInstallationDirectories for JetBrains YouTrack
- [JetBrains YouTrack] JetBrains - Implement GetComponents for JetBrains YouTrack
- [JetBrains YouTrack] JetBrains - Implement IsAuthentic for JetBrains YouTrack
- [Azul Zulu JRE 8] Azul Systems, Inc. - Implement GetVersion for Azul Zulu JRE 8 (x64)
- [Azul Zulu JDK 23] Azul Systems, Inc. - Implement GetVersion for Azul Zulu JDK 23 (x64)
- [Auslogics BitReplica] Auslogics - Implement Run for Auslogics BitReplica
- [Auslogics BitReplica] Auslogics - Implement GetVersion for Auslogics BitReplica
- [PDF-XChange] Tracker Software Products Ltd. - Implement GetRunningState for PDF-XChange Editor (Arm64)
- [PDF-XChange] Tracker Software Products Ltd. - Implement TerminateProcesses for PDF-XChange Editor (Arm64)
- [PDF-XChange] Tracker Software Products Ltd. - Implement GetRunningState for PDF-XChange Editor
- [PDF-XChange] Tracker Software Products Ltd. - Implement TerminateProcesses for PDF-XChange Editor
- [PDF-XChange] Tracker Software Products Ltd. - Update Run implementation for PDF-XChange Editor (Arm64)
- [PDF-XChange] Tracker Software Products Ltd. - Update Run implementation for PDF-XChange Editor
- [NVDA] NV Access - Implement GetInstallationDirectories for NVDA (x86)
- [NVDA] NV Access - Update TerminateProcesses implementation for NVDA (x86)
- [NVDA] NV Access - Update Run implementation for NVDA (x86)
- [NVDA] NV Access - Implement GetRunningState for NVDA (x86)
- [NVDA] NV Access - Implement GetComponents for NVDA (x86)
- [NVDA] NV Access - Implement IsAuthentic for NVDA (x86)
- [NVDA] NV Access - Implement GetUninstallHive for NVDA (x86)
- [NVDA] NV Access - Implement GetInstallationDirectories for NVDA (x64)
- [NVDA] NV Access - Implement GetRunningState for NVDA (x64)
- [NVDA] NV Access - Implement Run for NVDA (x64)
- [NVDA] NV Access - Implement TerminateProcesses for NVDA (x64)
- [NVDA] NV Access - Implement GetComponents for NVDA (x64)
- [NVDA] NV Access - Implement IsAuthentic for NVDA (x64)
- [NVDA] NV Access - Implement GetUninstallHive for NVDA (x64)
- [NVDA] NV Access - Implement GetVersion for NVDA (x64)
- [Copilot] Microsoft Corporation - Implement GetRunningState for Copilot
- [Copilot] Microsoft Corporation - Implement GetVersion for Copilot
- [Copilot] Microsoft Corporation - Implement Run for Copilot
- [Copilot] Microsoft Corporation - Implement TerminateProcesses for Copilot
- [Copilot] Microsoft Corporation - Implement GetInstallationDirectories for Copilot
- [GitHub Copilot] GitHub, Inc. - Update Run implementation for GitHub Copilot
- [GitHub Copilot] GitHub, Inc. - Implement GetInstallationDirectories for GitHub Copilot
- [GitHub Copilot] GitHub, Inc. - Implement Run for GitHub Copilot
- [Trellix EDRF] Trellix - Implement GetVersion for Trellix EDRF
- [Trellix EDRF] Trellix - Implement GetRunningState for Trellix EDRF
- [Trellix EDRF] Trellix - Implement GetRealTimeProtectionState for Trellix EDRF
- [Trellix EDRF] Trellix - Implement GetDefinitionState for Trellix EDRF
- [NVDA] NV Access - Update GetVersion implementation for NVDA
- [Copilot] Microsoft Corporation - Implement GetUninstallString for Copilot
- [Copilot] Microsoft Corporation - Update GetUninstallHive implementation for Copilot
- [TreeSize Professional] JAM Software - Implement GetRunningState for TreeSize Professional
- [TreeSize Professional] JAM Software - Implement TerminateProcesses for TreeSize Professional
- [TreeSize Professional] JAM Software - Implement Run for TreeSize Professional
- [TreeSize Professional] JAM Software - Implement GetInstallationDirectories for TreeSize Professional
- [TreeSize Professional] JAM Software - Implement GetUninstallHive for TreeSize Professional
- [TreeSize Professional] JAM Software - Implement GetUninstallString for TreeSize Professional
- [TreeSize Professional] JAM Software - Implement IsAuthentic for TreeSize Professional
- [TreeSize Professional] JAM Software - Update GetVersion implementation for TreeSize Professional
- [Copilot] Microsoft Corporation - Implement GetUninstallHive for Copilot
- [DriverEasy] Easeware - Implement GetVersion for DriverEasy

#### [Linux](/docs/mdsdk/release-notes/july-14-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/july-14-2026#mac)

- [iCloud] Apple Inc. - Implement GetComponents for iCloud
- [iCloud] Apple Inc. - Implement IsAuthentic for iCloud
- [Software Update] Apple Inc. - Update InstallMissingPatches implementation for Software Update
- [WatchGuard Endpoint Security Basic] WatchGuard Technologies Inc - Implement GetDefinitionState for WatchGuard Endpoint Security Basic
- [WatchGuard Endpoint Security Basic] WatchGuard Technologies Inc - Implement GetRealTimeProtectionState for WatchGuard Endpoint Security Basic
- [WatchGuard Endpoint Security Basic] WatchGuard Technologies Inc - Implement IsAuthentic for WatchGuard Endpoint Security Basic
- [FileVault] Apple Inc. - Implement Run for FileVault
- [GitHub Copilot CLI] GitHub, Inc. - Implement GetInstallationDirectories for GitHub Copilot CLI
- [GitHub Copilot CLI] GitHub, Inc. - Implement GetVersion for GitHub Copilot CLI
- [Continue CLI] Anysphere, Inc. - Implement GetInstallationDirectories for Continue CLI
- [Continue CLI] Anysphere, Inc. - Implement GetVersion for Continue CLI
- [Claude] Anthropic PBC - Implement GetVersion for Claude CLI
- [Claude] Anthropic PBC - Implement GetInstallationDirectories for Claude CLI
- [Cody] Sourcegraph - Implement GetVersion for Cody
- [Cody] Sourcegraph - Implement GetInstallationDirectories for Cody
- [Pieces] Mesh Intelligent Technologies, Inc. - Implement Run for Pieces
