<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/september-29-2026 -->

# September 29th, 2026

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Release Note](/docs/mdsdk/release-notes/september-29-2026#release-note)

### [Release Date](/docs/mdsdk/release-notes/september-29-2026#release-date)

- 29/09/2026

### [SDK Version](/docs/mdsdk/release-notes/september-29-2026#sdk-version)

- **Windows**: 4.3.6669.0
- **Linux**: 4.3.5670.0
- **Mac**: 4.3.6063.0

### [Enhancement](/docs/mdsdk/release-notes/september-29-2026#enhancement)

#### [Windows](/docs/mdsdk/release-notes/september-29-2026#windows)

- Improve RTP status handling to distinguish “disabled” vs “not yet initialized” states

#### [Linux](/docs/mdsdk/release-notes/september-29-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/september-29-2026#mac)

- N/A

### [Bug Fix](/docs/mdsdk/release-notes/september-29-2026#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/september-29-2026#windows)

- Fixed Greenshot update failures on non-domain Windows endpoints by switching the per-user install task to an interactive logon type, ensuring successful patching for workgroup and Entra-ID-only users.
- Resolved the issue where BitLocker encryption status was incorrectly reported as unknown when no user was signed in by implementing the Get-BitLockerVolume command for administrative processes, ensuring accurate encryption reporting regardless of the logon context.
- Fixed the issue where signed-out user profiles with uncommitted registry logs were incorrectly reported as corrupt by copying the associated recovery journals during scans, ensuring complete product detection across all users on an endpoint ( DetectProducts with detect_all_users_products flag enabled).

#### [Linux](/docs/mdsdk/release-notes/september-29-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/september-29-2026#mac)

- N/A

### [New Application Support](/docs/mdsdk/release-notes/september-29-2026#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/september-29-2026#windows)

- Trend Vision One Endpoint Security rebranding name to TrendAI Vision One™ Endpoint Security
- Windows | Add Detection Support for Node.js Current 26.x
- Windows | Add Detection Support for Comet Browser 152.x
- Windows | Add detection support for Cybereason ActiveProbe Antimalware (24.x)
- V4 | Windows | Add patching support for TeamViewer Host 15 MSI
- Windows | Add detection support for Adobe Acrobat Reader DC Continuous MUI 26.x
- Add support detection for SnapAgent (signature 3986) version 2.17.1.0

#### [Linux](/docs/mdsdk/release-notes/september-29-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/september-29-2026#mac)

- N/A

### [New Application Version Support](/docs/mdsdk/release-notes/september-29-2026#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/september-29-2026#windows)

- V4 | Windows | Add support for avast! Free Antivirus version 26.9.11171.3829
- Trend Vision One Endpoint Security rebranding name to TrendAI Vision One™ Endpoint Security
- Windows | Add Detection Support for Node.js Current 26.x
- Windows | Add Detection Support for Comet Browser 152.x
- V4 | Windows | Add support for Microsoft Visual Studio Code (Arm64) version 1.139.1
- V4 | Windows | Add support for Microsoft Visual Studio Code (User) (Arm64) version 1.139.1
- V4 | Windows | Add support for Avast One Essential version 26.9.11171.1011
- V4 | Windows | Add support for BitLocker Drive Encryption version 10.0.28000.2804
- Windows | Add detection support for Cybereason ActiveProbe Antimalware (24.x)
- V4 | Windows | Add support for Malwarebytes Anti-Malware version 5.7.0.328
- V4 | Windows | Add support for Mozilla Firefox ESR (x86) version 140.16.0
- V4 | Windows | Add patching support for TeamViewer Host 15 MSI
- V4 | Windows | Add support for PuTTY (Arm64) version 0.83.0.0
- V4 | Windows | Add support for Microsoft Visual Studio Code (Arm64) version 1.139.0
- V4 | Windows | Add support for Microsoft Visual Studio Code (User) (Arm64) version 1.139.0
- V4 | Windows | Add support for Mozilla Firefox (arm64) version 155.0.1
- Windows | Add detection support for Adobe Acrobat Reader DC Continuous MUI 26.x
- V4 | Windows | Add support for 7-Zip (arm64) version 26.03
- V4 | Windows | Add support for Sentinel Agent version 26.2.2.155
- V4 | Windows | Add support for Webroot SecureAnywhere version 9.0.45.66
- Add support detection for SnapAgent (signature 3986) version 2.17.1.0

#### [Linux](/docs/mdsdk/release-notes/september-29-2026#linux)

- V4 | Linux | Add support for Transmission version 4.0.6.
- V4 | Linux | Add support for Visual Studio Code version 1.139.1
- V4 | Linux | Add support for Signal version 8.28.0
- V4 | Linux | Add support for FileZilla version 3.71.1
- V4 | Linux | Add support for Signal version 8.25.0
- V4 | Linux | Add support for GIMP version 3.2.6
- V4 | Linux | Add support for Wireshark version 4.6.9
- V4 | Linux | Add support for VLC media player version 3.0.24
- V4 | Linux | Add support for FileZilla version 3.71.0
- V4 | Linux | Add support for Thunderbird version 156.0.1
- V4 | Linux | Add support for Mozilla Firefox version 156.0.1
- V4 | Linux | Add support for RealVNC Server version 7.17.0
- V4 | Linux | Add support for Mozilla Firefox version 156.0
- V4 | Linux | Add support for Visual Studio Code version 1.136.0
- V4 | Linux | Add support for Thunderbird version 155.0
- V4 | Linux | Add support for MySQL Server version 26.7.0
- V4 | Linux | Add support for Google Chrome version 154.0.8037.57
- V4 | Linux | Add support for LibreOffice version 26.8.0.3
- V4 | Linux | Add support for Wireshark version 4.6.8
- V4 | Linux | Add support for Zoom version 7.2.0

#### [Mac](/docs/mdsdk/release-notes/september-29-2026#mac)

- V4 | Mac | Add support for Trend Micro Deep Security Agent version 20.0.0.252
- V4 | Mac | Add support for Xprotect version 5360

### [New Method Implementation](/docs/mdsdk/release-notes/september-29-2026#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/september-29-2026#windows)

- [avast! Free Antivirus] AVAST Software a.s. - Update GetLastScanTime implementation for avast! Free Antivirus
- [iDescriptor] iDescriptor - Implement GetVersion for iDescriptor
- [Trend Micro Apex One Security Agent] Trend Micro, Inc. - Update GetRealTimeProtectionState implementation for Trend Micro Apex One Security Agent
- [Apex One Security Agent] Trend Micro, Inc. - Update GetRealTimeProtectionState implementation for Apex One Security Agent
- [Anaconda3] Anaconda, Inc. - Implement GetVersion for Anaconda (User)
- [Anaconda3] Anaconda, Inc. - Implement GetVersion for Anaconda
- [Anaconda3] Anaconda, Inc. - Implement Run for Anaconda
- [Anaconda3] Anaconda, Inc. - Implement Run for Anaconda (User)
- [TrendAI Vision One™ Endpoint Security] Trend Micro, Inc. - Implement GetRunningState for TrendAI Vision One™ Endpoint Security
- [TrendAI Vision One™ Endpoint Security] Trend Micro, Inc. - Implement Run for TrendAI Vision One™ Endpoint Security
- [TrendAI Vision One™ Endpoint Security] Trend Micro, Inc. - Implement TerminateProcesses for TrendAI Vision One™ Endpoint Security
- [BitLocker Drive Encryption] Microsoft Corporation - Update GetEncryptionState implementation for BitLocker Drive Encryption
- [prem-down] lucuma13 - Implement GetRunningState for prem-down
- [Malwarebytes Anti-Malware] Malwarebytes Corporation - Update GetDefinitionState implementation for Malwarebytes Anti-Malware
- [Chromium] The Chromium Authors - Implement TerminateProcesses for Chromium
- [SnapAgent] Blackpoint Cyber - Update GetDefinitionState implementation for SnapAgent
- [SnapAgent] Blackpoint Cyber - Update GetRealTimeProtectionState implementation for SnapAgent
- [Chromium-Gost] The Chromium-Gost Authors - Implement TerminateProcesses for Chromium-Gost
- [Chromium-Gost] The Chromium-Gost Authors - Update GetRunningState implementation for Chromium-Gost
- [Chromium] The Chromium Authors - Implement GetRunningState for Chromium
- [Microsoft SQL Server Express] Microsoft Corporation - Implement GetRunningState for Microsoft SQL Server Express 2025
- [Microsoft SQL Server Express] Microsoft Corporation - Implement TerminateProcesses for Microsoft SQL Server Express 2025
- [Microsoft SQL Server Express] Microsoft Corporation - Implement Run for Microsoft SQL Server Express 2025
- [HashiCorp Terraform] HashiCorp - Implement GetRunningState for HashiCorp Terraform

#### [Linux](/docs/mdsdk/release-notes/september-29-2026#linux)

- [Visual Studio Code] Microsoft Corporation - Update Run implementation for Visual Studio Code
- [Signal] Signal Messenger, LLC - Update Run implementation for Signal
- [VLC media player] VideoLAN - Update GetInstallationDirectories implementation for VLC media player
- [WatchGuard Endpoint Security Prime] WatchGuard Technologies Inc - Implement GetVersion for WatchGuard Endpoint Security Prime
- [WatchGuard Endpoint Security Prime] WatchGuard Technologies Inc - Implement GetDefinitionState for WatchGuard Endpoint Security Prime
- [WatchGuard Endpoint Security Prime] WatchGuard Technologies Inc - Implement GetRealTimeProtectionState for WatchGuard Endpoint Security Prime
- [WatchGuard Endpoint Security 360] WatchGuard Technologies Inc - Implement GetVersion for WatchGuard Endpoint Security 360
- [WatchGuard Endpoint Security 360] WatchGuard Technologies Inc - Implement GetDefinitionState for WatchGuard Endpoint Security 360
- [WatchGuard Endpoint Security 360] WatchGuard Technologies Inc - Implement GetRealTimeProtectionState for WatchGuard Endpoint Security 360
- [Zoom] Zoom Video Communications, Inc. - Update GetComponents implementation for Zoom

#### [Mac](/docs/mdsdk/release-notes/september-29-2026#mac)

- [Iru Agent] Iru, Inc. - Implement GetRealTimeProtectionState for Iru Agent
- [Iru Agent] Iru, Inc. - Implement GetDefinitionState for Iru Agent
- [Iru Agent] Iru, Inc. - Implement IsAuthentic for Iru Agent
