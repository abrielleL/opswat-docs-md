<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/september-08-2026 -->

# September 8th, 2026

## [Release Note](/docs/mdsdk/release-notes/september-08-2026#release-note)

### [Release Date](/docs/mdsdk/release-notes/september-08-2026#release-date)

- 08/09/2026

### [SDK Version](/docs/mdsdk/release-notes/september-08-2026#sdk-version)

- **Windows**: 4.3.6579.0
- **Linux**: 4.3.5580.0
- **Mac**: 4.3.5968.0

### [Enhancement](/docs/mdsdk/release-notes/september-08-2026#enhancement)

#### [Windows](/docs/mdsdk/release-notes/september-08-2026#windows)

- V4 | Windows | KB5121767 does not appear in patch_system_aggregation.json
- Add skip_connection_check support to method UpdateDefinitions (1003)

#### [Linux](/docs/mdsdk/release-notes/september-08-2026#linux)

- Add skip_connection_check support to method UpdateDefinitions (1003)

#### [Mac](/docs/mdsdk/release-notes/september-08-2026#mac)

- Add skip_connection_check support to method UpdateDefinitions (1003)

### [Bug Fix](/docs/mdsdk/release-notes/september-08-2026#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/september-08-2026#windows)

- Fixed the bypass of pre-install signature and vendor verification in PatchV2 by ensuring the `skip_check_signature` field defaults to 0 instead of NULL, improving security by enforcing mandatory authenticity checks for all installers.
- Fixed the issue where `InstallMissingPatches` incorrectly reported success for failed Windows updates by reworking the result resolution to prioritize specific failure codes from both the update and batch levels, ensuring users receive accurate installation status and reliable patch deployment.
- Fixed an issue on Windows Server 2016 where GetInstalledPatches could fail with an incorrect connection error, improving the reliability of installed patch detection and reporting.
- Fixed an issue where failed or uninstalled Windows updates could be incorrectly reported as installed, improving patch status accuracy and preventing unnecessary remediation attempts.
- Resolved a vulnerability where the Windows App Remover followed symbolic links in its extraction directory via reparse-point-aware path validation and secure file handling, improving system security by preventing unauthorized file deletion or overwriting. The extraction path and directory permissions are unchanged.

#### [Linux](/docs/mdsdk/release-notes/september-08-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/september-08-2026#mac)

- Resolved the issue where macOS application installations sporadically failed with a generic error code by capturing and surfacing detailed rsync error messages in the response, improving troubleshooting speed and accuracy for users.

### [New Application Support](/docs/mdsdk/release-notes/september-08-2026#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/september-08-2026#windows)

- V4 | Windows | Add Support detection for Instalator Szafir

#### [Linux](/docs/mdsdk/release-notes/september-08-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/september-08-2026#mac)

- Add version support — CrowdStrike Falcon 8.10.21306 (macOS)
- macOS | Add support auto-patching for Microsoft Remote Desktop (currently named Windows App)
- macOS | Add support auto-patching for NordLayer
- macOS | Add support auto-patching Okta Verify

### [New Application Version Support](/docs/mdsdk/release-notes/september-08-2026#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/september-08-2026#windows)

- V4 | Windows | Add support for Microsoft Edge 80+ version 151.0.4129.93
- V4 | Windows | Add support for ESET Endpoint Security version 13.0.2044.0

#### [Linux](/docs/mdsdk/release-notes/september-08-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/september-08-2026#mac)

- Add version support — CrowdStrike Falcon 8.10.21306 (macOS)
- V4 | Mac | Add support for Xprotect version 5356
- V4 | Mac | Add support for Visual Studio Code version 1.136.1

### [New Method Implementation](/docs/mdsdk/release-notes/september-08-2026#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/september-08-2026#windows)

- [Visme] Easy WebContent, LLC - Implement Run for Visme
- [System Center Endpoint Protection] Microsoft Corporation - Update UpdateDefinitions implementation for System Center Endpoint Protection
- [Windows Defender] Microsoft Corporation - Update UpdateDefinitions implementation for Windows Defender
- [Microsoft Intune Endpoint Protection] Microsoft Corporation - Update UpdateDefinitions implementation for Microsoft Intune Endpoint Protection
- [Microsoft Defender ATP] Microsoft Corporation - Update UpdateDefinitions implementation for Microsoft Defender ATP
- [Microsoft Build of OpenJDK with Hotspot 11] Microsoft Corporation - Implement GetInstallationDirectories for Microsoft Build of OpenJDK with Hotspot 11
- [DigiDoc4 Client] RIA - Implement Run for DigiDoc4 Client
- [Instalator Szafir] Krajowa Izba Rozliczeniowa - Implement GetVersion for Instalator Szafir
- [Windows Admin Center (v2)] Microsoft Corporation - CLONE - Implement GetRunningState for Windows Admin Center (v2)
- [Windows Admin Center (v2)] Microsoft Corporation - Implement GetRunningState for Windows Admin Center (v2)
- [Windows Admin Center (v2)] Microsoft Corporation - Implement TerminateProcesses for Windows Admin Center (v2)
- [Windows Admin Center (v2)] Microsoft Corporation - Implement Run for Windows Admin Center (v2)
- [Windows Admin Center (v2)] Microsoft Corporation - Implement GetVersion for Windows Admin Center (v2)
- [Zoom Client for VDI] Zoom Video Communications, Inc. - Implement GetVersion for Zoom Client for VDI
- [Zoom VDI Workplace] Zoom Video Communications, Inc. - Implement GetVersion for Zoom VDI Workplace
- [Microsoft Power BI Report Server] Microsoft Corporation - Implement Run for Microsoft Power BI Report Server
- [Microsoft Power BI Report Server] Microsoft Corporation - Implement TerminateProcesses for Microsoft Power BI Report Server
- [Microsoft Power BI Report Server] Microsoft Corporation - Implement GetRunningState for Microsoft Power BI Report Server
- [Microsoft Power BI Report Server] Microsoft Corporation - Implement GetVersion for Microsoft Power BI Report Server
- [Microsoft Edge] Microsoft Corporation - Update GetPlugins implementation for Microsoft Edge
- [Scribe] Colony Labs, Inc - Update Run implementation for Scribe
- [Scribe] Colony Labs, Inc - Update Run implementation for Scribe
- [Microsoft .NET Runtime 7.0] Microsoft Corporation - Update GetVersion implementation for Microsoft .NET Runtime 7.0 (x64)
- [Microsoft .NET Runtime 7.0] Microsoft Corporation - Update GetVersion implementation for Microsoft .NET Runtime 7.0 (x86)
- [Microsoft .NET Runtime 6.0] Microsoft Corporation - Update GetVersion implementation for Microsoft .NET Runtime 6.0 (x64)
- [Microsoft .NET Runtime 6.0] Microsoft Corporation - Update GetVersion implementation for Microsoft .NET Runtime 6.0 (x86)
- [Trend Vision One Endpoint Security] Trend Micro, Inc. - Implement GetVersion for Trend Vision One Endpoint Security
- [YubiKey Manager CLI] Yubico AB - Implement GetVersion for YubiKey Manager CLI
- [Microsoft Visual Studio] Microsoft Corporation - Update GetRunningState implementation for Visual Studio Enterprise 2017
- [Microsoft Visual Studio] Microsoft Corporation - Update GetRunningState implementation for Visual Studio Professional 2017

#### [Linux](/docs/mdsdk/release-notes/september-08-2026#linux)

- [Advanced Packaging Tool] GNU - Update InstallMissingPatches implementation for Advanced Packaging Tool
- [Rapid7 Insight Agent] Rapid7 - Implement GetDefinitionState for Rapid7 Insight Agent
- [Rapid7 Insight Agent] Rapid7 - Implement GetRealTimeProtectionState for Rapid7 Insight Agent
- [Rapid7 Insight Agent] Rapid7 - Implement TerminateProcesses for Rapid7 Insight Agent
- [Rapid7 Insight Agent] Rapid7 - Implement Run for Rapid7 Insight Agent

#### [Mac](/docs/mdsdk/release-notes/september-08-2026#mac)

- [Xprotect] Apple Inc. - Update GetDefinitionState implementation for Xprotect
- [Xprotect] Apple Inc. - Implement GetInstallationDirectories for Xprotect
- [Xprotect] Apple Inc. - Implement GetRunningState for Xprotect
- [Visual Studio Code] Microsoft Corporation - Implement Run for Visual Studio Code
- [Visual Studio Code] Microsoft Corporation - Implement GetComponents for Visual Studio Code
- [Visual Studio Code] Microsoft Corporation - Implement TerminateProcesses for Visual Studio Code
- [iBoostUp] iBoostUp Pty Ltd - Update GetLastScanTime implementation for iBoostUp
- [iBoostUp] iBoostUp Pty Ltd - Update GetThreats implementation for iBoostUp
