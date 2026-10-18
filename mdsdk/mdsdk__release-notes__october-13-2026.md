<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/october-13-2026 -->

# October 13th, 2026

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## Release Note

### Release Date

- 13/10/2026

### SDK Version

- **Windows**: 4.3.6729.0
- **Linux**: 4.3.5726.0
- **Mac**: 4.3.6120.0

### Enhancement

#### Windows

- N/A

#### Linux

- All platforms | Add change logs for Compliance data (libwaresource)
- Enhancement request to add data_source to products.json

#### Mac

- N/A

### Bug Fix

#### Windows

- Resolved the issue where GetProductVulnerability returned superseded remediation KBs by ensuring a full Windows Update scan is performed when skip_extra_installed_os_patches_checks is enabled, improving the accuracy of automated remediation.
- Resolved the issue where the OESIS SDK unnecessarily created the `__PSLockDownPolicy` registry key on legacy Windows versions by updating the helper to only modify the key if it already exists, preventing Remote Desktop Session Host (RDS) server conflicts and improving system stability.

#### Linux

- N/A

#### Mac

- Fixed the issue where macOS updates incorrectly reported success despite failing due to invalid credentials or installer crashes by implementing a pre-execution credential validation gate and stricter success-pattern matching, ensuring accurate patch status reporting and improved reliability for Apple silicon devices.

### New Application Support

#### Windows

- Windows | Add detection and auto-patching support for Microsoft .NET SDK 10.0
- Windows | Need to add GetRealTimeProtectionState and GetDefinitionState for Trend Micro Apex One Security Agent 14.0.x
- Add patching support for Microsoft NET Runtime 8.0

#### Linux

- N/A

#### Mac

- N/A

### New Application Version Support

#### Windows

- Windows | Add detection and auto-patching support for Microsoft .NET SDK 10.0
- Windows | Need to add GetRealTimeProtectionState and GetDefinitionState for Trend Micro Apex One Security Agent 14.0.x
- V4 | Windows | Add support for Quest KACE Agent version 14.1
- Add patching support for Microsoft NET Runtime 8.0
- V4 | Windows | Add support for Trend Micro Full Disk Encryption version 6.0.0.4013
- V4 | Windows | Add support for Microsoft Defender ATP version 10.0.26100.9457
- V4 | Windows | Add support for Opera version 137.0.6036.39
- V4 | Windows | Add support for 7-Zip (arm64) version 26.04
- V4 | Windows | Add support for Mozilla Firefox (arm64) version 157.0.1

#### Linux

- V4 | Linux | Add support for Transmission version 4.1.3.
- V4 | Linux | Add support for Firewalld version 2.3.1
- V4 | Linux | Add support for Signal version 8.30.0
- V4 | Linux | Add support for Mozilla Firefox version 157.0.1
- V4 | Linux | Add support for Advanced Packaging Tool version 3.3.2
- V4 | Linux | Add support for Visual Studio Code version 1.141.0
- V4 | Linux | Add support for Thunderbird version 157.0.1
- V4 | Linux | Add support for Signal version 8.29.0
- V4 | Linux | Add support for LibreOffice version 26.8.1
- V4 | Linux | Add support for Advanced Packaging Tool version 2.9.23

#### Mac

- V4 | Mac | Add support for ESET Cyber Security version 9.0.6700.0
- V4 | Mac | Add support for FileVault version 27.2
- V4 | Mac | Add support for Xprotect version 5366

### New Method Implementation

#### Windows

- [Sentinel Agent] SentinelOne - Update GetRealTimeProtectionState implementation for Sentinel Agent
- [MalwareFox] MalwareFox - Implement GetDefinitionState for MalwareFox
- [MalwareFox] MalwareFox - Implement GetRealTimeProtectionState for MalwareFox
- [MalwareFox] MalwareFox - Implement GetRunningState for MalwareFox
- [MalwareFox] MalwareFox - Implement GetVersion for MalwareFox
- [Xerox Workplace Cloud Client] Xerox Corporation - Update GetVersion implementation for Xerox Workplace Cloud Client
- [ESET Endpoint Security] ESET - Update GetDefinitionState implementation for ESET Endpoint Security
- [ESET Endpoint Security] ESET - Update GetVersion implementation for ESET Endpoint Security
- [Anaconda3] Anaconda, Inc. - Update GetRunningState implementation for Anaconda
- [Anaconda3] Anaconda, Inc. - Implement TerminateProcesses for Anaconda
- [Anaconda3] Anaconda, Inc. - Implement GetRunningState for Anaconda (User)
- [Anaconda3] Anaconda, Inc. - Implement TerminateProcesses for Anaconda (User)
- [Tableau Reader] Tableau Software - Implement GetVersion for Tableau Reader
- [Git] The Git Development Community - Update GetRunningState implementation for Git (x64)
- [Git] The Git Development Community - Update TerminateProcesses implementation for Git (x64)
- [Git] The Git Development Community - Implement Run for Git (x64)
- [Microsoft .NET SDK 10.0] Microsoft Corporation - Implement GetUninstallHive for Microsoft .NET SDK 10.0 (x64)
- [Microsoft .NET SDK 10.0] Microsoft Corporation - Implement GetUninstallHive for Microsoft .NET SDK 10.0 (x86)
- [Microsoft .NET SDK 10.0] Microsoft Corporation - Implement GetUninstallHive for Microsoft .NET SDK 10.0 (arm64)
- [Microsoft .NET SDK 10.0] Microsoft Corporation - Implement IsAuthentic for Microsoft .NET SDK 10.0 (x64)
- [Microsoft .NET SDK 10.0] Microsoft Corporation - Implement IsAuthentic for Microsoft .NET SDK 10.0 (x86)
- [Microsoft .NET SDK 10.0] Microsoft Corporation - Implement IsAuthentic for Microsoft .NET SDK 10.0 (arm64)

#### Linux

- [Transmission] The Transmission Project - Implement GetInstallationDirectories for Transmission
- [Transmission] The Transmission Project - Implement TerminateProcesses for Transmission
- [Transmission] The Transmission Project - Implement Run for Transmission
- [Transmission] The Transmission Project - Implement GetRunningState for Transmission
- [Transmission] The Transmission Project - Implement GetVersion for Transmission
- [Firewalld] Red Hat, Inc. - Implement GetVersion for Firewalld
- [Mozilla Firefox] Mozilla Corporation - Update GetComponents implementation for Mozilla Firefox
- [Advanced Packaging Tool] GNU - Implement GetInstallationDirectories for Advanced Packaging Tool
- [Dandified Yum] Red Hat, Inc. - Update GetMissingPatches implementation for Dandified Yum

#### Mac

- [Software Update] Apple Inc. - Update InstallMissingPatches implementation for Software Update
- [ESET Cyber Security] ESET - Update GetLastScanTime implementation for ESET Cyber Security
