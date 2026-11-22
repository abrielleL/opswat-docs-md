<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/november-10-2026 -->

# November 10th, 2026

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
## Release Note

### Release Date

- 10/11/2026

### SDK Version

- **Windows**: 4.3.6852.0
- **Linux**: 4.3.5843.0
- **Mac**: 4.3.6240.0

### Enhancement

#### Windows

- Windows | Use KB_ID in InstallMissingPatches API for Windows (#1103)

#### Linux

- N/A

#### Mac

- N/A

### Bug Fix

#### Windows

- Resolved the failure to retrieve the version for Symantec Data Loss Prevention Agent on Windows via a corrected regex and updated component file, improving product version detection accuracy for compliance reporting.

#### Linux

- Improved the reliability of security product state reporting on Linux. GetRealTimeProtectionState and DetectProducts now read service state from system commands through a protected channel, so other programs on the device can't affect the results.

#### Mac

- Resolved a security vulnerability (CVE-2026-111497) in the macOS AppRemover module by upgrading the Brotli library to version 1.2.1, improving the overall security posture and protection against potential memory corruption during product uninstallation.

### New Application Support

#### Windows

- Windows | Add Detection Support for Comet Browser 154.x
- Windows | Add Detection Support for Java SE Development Kit 27.x

#### Linux

- N/A

#### Mac

- Add support detection for GlobalProtect on macOS
- MacOS | Request support detection for Sublime Text 4

### New Application Version Support

#### Windows

- Windows | Add Detection Support for Comet Browser 154.x
- Windows | Add Detection Support for Java SE Development Kit 27.x
- V4 | Windows | Add support for FortiClient version 8.0.0

#### Linux

- V4 | Linux | Add support for Signal version 8.34.0
- V4 | Linux | Add support for Google Chrome version 157.0.8103.38
- V4 | Linux | Add support for Mozilla Firefox version 159.0.1
- V4 | Linux | Add support for Advanced Packaging Tool version 3.3.5
- V4 | Linux | Add support for Kaspersky Endpoint Security for Linux version 12.5.0.1569
- V4 | Linux | Add support for Zoom version 7.2.5
- V4 | Linux | Add support for LibreOffice version 26.8.2
- V4 | Linux | Add support for Signal version 8.33.0
- V4 | Linux | Add support for Citrix Workspace version 26.x
- V4 | Linux | Add support for Transmission version 4.1.4
- V4 | Linux | Add support for Mozilla Firefox version 158.0.1
- V4 | Linux | Add support for Thunderbird version 159.0
- V4 | Linux | Add support for Mozilla Firefox ESR version 153.5.1

#### Mac

- Add support detection for GlobalProtect on macOS
- MacOS | Request support detection for Sublime Text 4
- V4 | Mac | Add support for macOS version 14.8.8
- V4 | Mac | Add support for macOS version 27.3 BETA 1 (preview)
- V4 | Mac | Add support for macOS version 15.8.2
- V4 | Mac | Add support for Trellix Endpoint Security for Mac version 26.8.0.217
- V4 | Mac | Add support for macOS version 26.7.2
- V4 | Mac | Add support for macOS version 27.2 BETA 4 (preview)
- V4 | Mac | Add support for macOS version 27.2 BETA 3 (preview)
- V4 | Mac | Add support for macOS version 27.0 BETA 8 (preview)
- V4 | Mac | Add support for macOS version 27.2 RC (preview)

### New Method Implementation

#### Windows

- [Comet] The Comet Authors - Implement GetInstallationDirectories for Comet
- [Mozilla Firefox ESR] Mozilla Corporation - Implement GetPlugins for Mozilla Firefox ESR (User) (x64)
- [Mozilla Firefox ESR] Mozilla Corporation - Implement GetPlugins for Mozilla Firefox ESR (User) (x86)
- [Mozilla Firefox ESR] Mozilla Corporation - Implement GetPlugins for Mozilla Firefox ESR (x64)
- [Mozilla Firefox ESR] Mozilla Corporation - Implement GetPlugins for Mozilla Firefox ESR (x86)
- [Mozilla Firefox ESR] Mozilla Corporation - Implement SetAntiphishingState for Mozilla Firefox ESR (x86)
- [Mozilla Firefox ESR] Mozilla Corporation - Implement GetAntiphishingState for Mozilla Firefox ESR (x86)
- [Mozilla Firefox ESR] Mozilla Corporation - Implement SetAntiphishingState for Mozilla Firefox ESR (x64)
- [Mozilla Firefox ESR] Mozilla Corporation - Implement GetAntiphishingState for Mozilla Firefox ESR (x64)
- [Mozilla Firefox ESR] Mozilla Corporation - Implement SetAntiphishingState for Mozilla Firefox ESR (User) (x64)
- [Mozilla Firefox ESR] Mozilla Corporation - Implement GetAntiphishingState for Mozilla Firefox ESR (User) (x64)
- [Mozilla Firefox ESR] Mozilla Corporation - Implement SetAntiphishingState for Mozilla Firefox ESR (User) (x86)
- [Mozilla Firefox ESR] Mozilla Corporation - Implement GetAntiphishingState for Mozilla Firefox ESR (User) (x86)
- [Mozilla Firefox ESR] Mozilla Corporation - Implement IsDefaultBrowser for Mozilla Firefox ESR (User) (x86)
- [Mozilla Firefox ESR] Mozilla Corporation - Implement GetComponents for Mozilla Firefox ESR (User) (x86)
- [Mozilla Firefox ESR] Mozilla Corporation - Update GetInstallationDirectories implementation for Mozilla Firefox ESR (User) (x86)
- [Mozilla Firefox ESR] Mozilla Corporation - Implement GetUninstallString for Mozilla Firefox ESR (User) (x86)
- [Mozilla Firefox ESR] Mozilla Corporation - Implement GetUninstallHive for Mozilla Firefox ESR (User) (x86)
- [Mozilla Firefox ESR] Mozilla Corporation - Implement IsDefaultBrowser for Mozilla Firefox ESR (User) (x64)
- [Mozilla Firefox ESR] Mozilla Corporation - Implement GetInstallationDirectories for Mozilla Firefox ESR (User) (x64)
- [Mozilla Firefox ESR] Mozilla Corporation - Update GetUninstallHive implementation for Mozilla Firefox ESR (User) (x64)
- [Mozilla Firefox ESR] Mozilla Corporation - Update GetUninstallString implementation for Mozilla Firefox ESR (User) (x64)
- [Mozilla Firefox ESR] Mozilla Corporation - Implement GetComponents for Mozilla Firefox ESR (User) (x64)
- [Mozilla Firefox ESR] Mozilla Corporation - Update IsDefaultBrowser implementation for Mozilla Firefox ESR (x86)
- [Mozilla Firefox ESR] Mozilla Corporation - Update GetComponents implementation for Mozilla Firefox ESR (x86)
- [Mozilla Firefox ESR] Mozilla Corporation - Implement GetUninstallHive for Mozilla Firefox ESR (x86)
- [Mozilla Firefox ESR] Mozilla Corporation - Implement GetUninstallString for Mozilla Firefox ESR (x86)
- [Mozilla Firefox ESR] Mozilla Corporation - Implement GetInstallationDirectories for Mozilla Firefox ESR (x86)
- [Mozilla Firefox ESR] Mozilla Corporation - Update GetComponents implementation for Mozilla Firefox ESR (x64)
- [Mozilla Firefox ESR] Mozilla Corporation - Update IsDefaultBrowser implementation for Mozilla Firefox ESR (x64)
- [Mozilla Firefox ESR] Mozilla Corporation - Update GetUninstallHive implementation for Mozilla Firefox ESR (x64)
- [Mozilla Firefox ESR] Mozilla Corporation - Update GetUninstallString implementation for Mozilla Firefox ESR (x64)
- [Mozilla Firefox ESR] Mozilla Corporation - Update GetInstallationDirectories implementation for Mozilla Firefox ESR (x64)
- [PGP Utility] Gentian Shkembi - Implement GetRunningState for PGP Utility
- [Vegha] VAMC Consulting LLC - Implement GetVersion for Vegha
- [Mozilla Firefox ESR] Mozilla Corporation - Implement IsDefaultBrowser for Mozilla Firefox ESR (x64)
- [Mozilla Firefox ESR] Mozilla Corporation - Implement GetUninstallHive for Mozilla Firefox ESR (x64)
- [Mozilla Firefox ESR] Mozilla Corporation - Implement GetUninstallString for Mozilla Firefox ESR (x64)
- [Mozilla Firefox ESR] Mozilla Corporation - Implement GetInstallationDirectories for Mozilla Firefox ESR (x64)
- [TextLens] ZH-heng - Implement GetVersion for TextLens
- [TextLens] ZH-heng - Implement GetRunningState for TextLens
- [TextLens] ZH-heng - Implement Run for TextLens
- [Angry IP Scanner] Angry IP Scanner - Update GetVersion implementation for Angry IP Scanner
- [Angry IP Scanner] Angry IP Scanner - Implement Run for Angry IP Scanner
- [Angry IP Scanner] Angry IP Scanner - Update GetRunningState implementation for Angry IP Scanner
- [Angry IP Scanner] Angry IP Scanner - Update TerminateProcesses implementation for Angry IP Scanner
- [FortiClient] Fortinet Inc. - Update GetFirewallState implementation for FortiClient
- [ProseFlow] ProseFlow - Implement GetVersion for ProseFlow
- [Google Chrome] Google Inc. - Implement GetVersion for Google Chrome (User)
- [Google Chrome] Google Inc. - Update GetVersion implementation for Google Chrome
- [Mozilla Firefox ESR] Mozilla Corporation - Update GetVersion implementation for Mozilla Firefox ESR (x86)
- [Mozilla Firefox ESR] Mozilla Corporation - Update GetRunningState implementation for Mozilla Firefox ESR (x86)
- [Mozilla Firefox ESR] Mozilla Corporation - Update Run implementation for Mozilla Firefox ESR (x86)
- [Mozilla Firefox ESR] Mozilla Corporation - Update TerminateProcesses implementation for Mozilla Firefox ESR (x86)
- [Mozilla Firefox ESR] Mozilla Corporation - Update TerminateProcesses implementation for Mozilla Firefox ESR (x64)
- [Mozilla Firefox ESR] Mozilla Corporation - Update GetRunningState implementation for Mozilla Firefox ESR (x64)
- [Mozilla Firefox ESR] Mozilla Corporation - Update Run implementation for Mozilla Firefox ESR (x64)
- [Mozilla Firefox ESR] Mozilla Corporation - Update GetVersion implementation for Mozilla Firefox ESR (x64)
- [Mozilla Firefox ESR] Mozilla Corporation - Implement GetVersion for Mozilla Firefox ESR (User) (x64)
- [Mozilla Firefox ESR] Mozilla Corporation - Implement GetRunningState for Mozilla Firefox ESR (User) (x64)
- [Mozilla Firefox ESR] Mozilla Corporation - Implement Run for Mozilla Firefox ESR (User) (x64)
- [Mozilla Firefox ESR] Mozilla Corporation - Implement TerminateProcesses for Mozilla Firefox ESR (User) (x64)
- [Mozilla Firefox ESR] Mozilla Corporation - Update GetVersion implementation for Mozilla Firefox ESR (x86)
- [Mozilla Firefox ESR] Mozilla Corporation - Implement GetVersion for Mozilla Firefox ESR (User) (x86)
- [Mozilla Firefox ESR] Mozilla Corporation - Implement GetRunningState for Mozilla Firefox ESR (User) (x86)
- [Mozilla Firefox ESR] Mozilla Corporation - Implement Run for Mozilla Firefox ESR (User) (x86)
- [Mozilla Firefox ESR] Mozilla Corporation - Implement TerminateProcesses for Mozilla Firefox ESR (User) (x86)
- [Angry IP Scanner] Angry IP Scanner - Update GetInstallationDirectories implementation for Angry IP Scanner
- [DBX] t8y2 - Update GetVersion implementation for DBX

#### Linux

- [Mozilla Firefox] Mozilla Corporation - Update GetAntiphishingState implementation for Mozilla Firefox
- [Mozilla Firefox] Mozilla Corporation - Update TerminateProcesses implementation for Mozilla Firefox
- [Mozilla Firefox] Mozilla Corporation - Update GetInstallationDirectories implementation for Mozilla Firefox
- [Mozilla Firefox] Mozilla Corporation - Update GetRunningState implementation for Mozilla Firefox
- [Mozilla Firefox] Mozilla Corporation - Update GetComponents implementation for Mozilla Firefox
- [Mozilla Firefox ESR] Mozilla Corporation - Update SetAntiphishingState implementation for Mozilla Firefox ESR
- [Mozilla Firefox ESR] Mozilla Corporation - Update Run implementation for Mozilla Firefox ESR
- [Transmission] The Transmission Project - Update Run implementation for Transmission
- [Mozilla Firefox ESR] Mozilla Corporation - Update GetPlugins implementation for Mozilla Firefox ESR

#### Mac

- [Trellix EDRF] Trellix - Implement IsAuthentic for Trellix EDRF
- [Trellix EDRF] Trellix - Implement GetInstallationDirectories for Trellix EDRF
- [Trellix EDRF] Trellix - Implement Run for Trellix EDRF
- [Trellix EDRF] Trellix - Implement GetVersion for Trellix EDRF
- [Trellix EDRF] Trellix - Implement GetDefinitionState for Trellix EDRF
- [Trellix EDRF] Trellix - Implement GetRealTimeProtectionState for Trellix EDRF
- [Sublime Text] Sublime HQ Pty Ltd - Implement GetRunningState for Sublime Text 4
- [GlobalProtect] Palo Alto Networks, Inc. - Implement GetRunningState for GlobalProtect
- [GlobalProtect] Palo Alto Networks, Inc. - Implement TerminateProcesses for GlobalProtect
- [GlobalProtect] Palo Alto Networks, Inc. - Implement Run for GlobalProtect
- [GlobalProtect] Palo Alto Networks, Inc. - Implement GetVersion for GlobalProtect
- [1Password] AgileBits - Update GetVersion implementation for 1Password
- [Box Sync] Box, Inc. - Update GetBackupState implementation for Box Sync
