<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/july-07-2026 -->

# July 07th, 2026

## [Release Note](/docs/mdsdk/release-notes/july-07-2026#release-note)

### [Release Date](/docs/mdsdk/release-notes/july-07-2026#release-date)

- 07/07/2026

### [SDK Version](/docs/mdsdk/release-notes/july-07-2026#sdk-version)

- **Windows**: 4.3.6310.0
- **Linux**: 4.3.5313.0
- **Mac**: 4.3.5674.0

### [Enhancement](/docs/mdsdk/release-notes/july-07-2026#enhancement)

#### [Windows](/docs/mdsdk/release-notes/july-07-2026#windows)

- [Phase 2] Patch-centric Patch Management

#### [Linux](/docs/mdsdk/release-notes/july-07-2026#linux)

- [Phase 2] Patch-centric Patch Management

#### [Mac](/docs/mdsdk/release-notes/july-07-2026#mac)

- [Phase 2] Patch-centric Patch Management

### [Bug Fix](/docs/mdsdk/release-notes/july-07-2026#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/july-07-2026#windows)

- Fixed the analog CDN eTag update issue caused by failed {{analog.zip}} generation. The oversized files {{patch_system_aggregation.json}}, {{ap_support_charts.json}}, and {{wuo.dat}} were reviewed and approved as expected, then {{analog.zip}} was regenerated and published to VCR on Jun 26 at 6 PM ICT, restoring normal eTag updates. Follow-up improvements are planned to improve alert routing, report all size validation failures in a single pass, and support partial regeneration for faster recovery.
- Fixed the issue where custom file downloads failed to trigger in customer tools by adding the required "attachment" directive to the Gateway's redirect response, ensuring reliable file downloads and correct naming for users.
- Resolved the failure of Microsoft Visual C++ 2015-2022 Redistributable patching via updating public keys and certificate paths to support the new vendor installer version, improving the reliability of automated software updates for users.

#### [Linux](/docs/mdsdk/release-notes/july-07-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/july-07-2026#mac)

- N/A

### [New Application Support](/docs/mdsdk/release-notes/july-07-2026#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/july-07-2026#windows)

- V4 | All | Add support for rebrand of Trend Micro to TrendAI
- Add support for the Microsoft Edge Extended Stable Channel
- Add support for Trend Micro Deep Security Agent version 20.0.31491
- Add support | Existing product support patch management for Python
- Request add support detection for Codex on Windows
- Request support Node.js versions (Current or LTS lines) in analog for Windows
- Request add support detection for OpenAI's ChatGPT Desktop on Windows

#### [Linux](/docs/mdsdk/release-notes/july-07-2026#linux)

- V4 | All | Add support for rebrand of Trend Micro to TrendAI

#### [Mac](/docs/mdsdk/release-notes/july-07-2026#mac)

- V4 | All | Add support for rebrand of Trend Micro to TrendAI
- macOS | Add support detection for Augment Code
- macOS | Add support detection for GitHub Desktop
- macOS | Add support detection for Loom
- macOS | Add support detection for Yubico Authenticator
- macOS | Add support detection for BBEdit
- macOS | Add support detection for AWS Client VPN
- Add support | Existing product support patch management for Python
- V4 | Add support for existing product Trend Micro Security 3.7.2050 - MacOS
- Add Support for Sentinel Agent 26.x for MacOS

### [New Application Version Support](/docs/mdsdk/release-notes/july-07-2026#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/july-07-2026#windows)

- V4 | All | Add support for rebrand of Trend Micro to TrendAI
- Add support for the Microsoft Edge Extended Stable Channel
- V4 | Windows | Add support for Microsoft Visual Studio Code (User) version 1.123.1
- V4 | Windows | Add support for Microsoft Visual Studio Code version 1.124.0
- Add support for Trend Micro Deep Security Agent version 20.0.31491
- V4 | Windows | Add support for Mozilla Firefox (arm64) version 152.0.4
- Add support | Existing product support patch management for Python
- Request add support detection for Codex on Windows
- Request support Node.js versions (Current or LTS lines) in analog for Windows
- Request add support detection for OpenAI's ChatGPT Desktop on Windows

#### [Linux](/docs/mdsdk/release-notes/july-07-2026#linux)

- V4 | Linux | Add support for MySQL Workbench version 8.0.47
- V4 | Linux | Add support for Firebird SQL Server version 5.0.4
- V4 | Linux | Add support for Thunderbird version 152.0.1
- V4 | Linux | Add support for MySQL Server version 9.7.1
- V4 | All | Add support for rebrand of Trend Micro to TrendAI
- V4 | Linux | Add support for Signal version 8.16.0
- V4 | Linux | Add support for Mozilla Firefox version 152.0.4
- V4 | Linux | Add support for Visual Studio Code version 1.127.0
- V4 | Linux | Add support for Signal version 8.17.0

#### [Mac](/docs/mdsdk/release-notes/july-07-2026#mac)

- V4 | All | Add support for rebrand of Trend Micro to TrendAI
- V4 | Mac | Add support for macOS version 26.5.2
- Add support | Existing product support patch management for Python
- V4 | Mac | Add support for Dropbox version 258.4.3749
- V4 | Add support for existing product Trend Micro Security 3.7.2050 - MacOS
- Add Support for Sentinel Agent 26.x for MacOS

### [New Method Implementation](/docs/mdsdk/release-notes/july-07-2026#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/july-07-2026#windows)

- [ESET Endpoint Antivirus] ESET - Update GetRealTimeProtectionState implementation for ESET Endpoint Antivirus
- [Auslogics File Recovery] Auslogics - Implement TerminateProcesses for Auslogics File Recovery
- [Auslogics File Recovery] Auslogics - Implement GetRunningState for Auslogics File Recovery
- [Auslogics File Recovery] Auslogics - Implement GetVersion for Auslogics File Recovery
- [HP Support Assistant] HP Development Company, L.P. - Update GetVersion implementation for HP Support Assistant
- [Duplicate Cleaner Free] DigitalVolcano Software Ltd - Implement GetVersion for Duplicate Cleaner Free
- [Softros LAN Messenger] Softros Systems, Inc. - Implement TerminateProcesses for Softros LAN Messenger
- [Softros LAN Messenger] Softros Systems, Inc. - Implement GetRunningState for Softros LAN Messenger
- [Softros LAN Messenger] Softros Systems, Inc. - Implement Run for Softros LAN Messenger
- [Softros LAN Messenger] Softros Systems, Inc. - Implement GetVersion for Softros LAN Messenger
- [Doxygen] Dimitri van Heesch - Implement TerminateProcesses for Doxygen
- [Doxygen] Dimitri van Heesch - Implement GetRunningState for Doxygen
- [Doxygen] Dimitri van Heesch - Implement Run for Doxygen
- [Advanced SystemCare] IObit - Implement TerminateProcesses for Advanced SystemCare
- [Advanced SystemCare] IObit - Implement GetRunningState for Advanced SystemCare
- [Advanced SystemCare] IObit - Implement GetVersion for Advanced SystemCare
- [Wise Disk Cleaner] WiseCleaner - Implement GetVersion for Wise Disk Cleaner
- [Wise Program Uninstaller] WiseCleaner - Implement GetVersion for Wise Program Uninstaller
- [IObit Uninstaller] IObit - Implement TerminateProcesses for IObit Uninstaller
- [IObit Uninstaller] IObit - Implement GetRunningState for IObit Uninstaller
- [IObit Uninstaller] IObit - Implement GetVersion for IObit Uninstaller
- [DiskDefrag] Auslogics - Implement TerminateProcesses for Disk Defrag
- [DiskDefrag] Auslogics - Implement GetRunningState for Disk Defrag
- [DiskDefrag] Auslogics - Implement GetVersion for Disk Defrag
- [Microsoft Visual Studio Code] Microsoft Corporation - Update Run implementation for Microsoft Visual Studio Code
- [Microsoft Visual Studio Code] Microsoft Corporation - Update Run implementation for Microsoft Visual Studio Code (User)
- [Trend Micro Deep Security Agent] Trend Micro, Inc. - Update GetRunningState implementation for Trend Micro Deep Security Agent
- [Codex] OpenAI - Implement GetVersion for Codex
- [Codex] OpenAI - Implement TerminateProcesses for Codex
- [Codex] OpenAI - Implement GetRunningState for Codex
- [Codex] OpenAI - Implement Run for Codex
- [Codex] OpenAI - Implement GetUninstallString for Codex
- [Codex] OpenAI - Implement GetUninstallHive for Codex
- [Codex] OpenAI - Implement GetInstallationDirectories for Codex
- [Codex] OpenAI - Implement GetComponents for Codex
- [Codex] OpenAI - Implement IsAuthentic for Codex
- [WatchGuard Endpoint Security Prime] WatchGuard Technologies Inc - Implement GetDefinitionState for WatchGuard Endpoint Security Prime
- [WatchGuard Endpoint Security Prime] WatchGuard Technologies Inc - Implement GetVersion for WatchGuard Endpoint Security Prime
- [ChatGPT] OpenAI - Implement GetVersion for ChatGPT
- [ChatGPT] OpenAI - Implement Run for ChatGPT
- [ChatGPT] OpenAI - Implement GetUninstallHive for ChatGPT
- [ChatGPT] OpenAI - Implement GetUninstallString for ChatGPT
- [Azul Zulu JDK 11] Azul Systems, Inc. - Implement GetVersion for Azul Zulu JDK 11 (x64)

#### [Linux](/docs/mdsdk/release-notes/july-07-2026#linux)

- [Proxmox Virtual Environment] Proxmox Server Solutions GmbH - Implement GetVersion for Proxmox Virtual Environment
- [Proxmox Virtual Environment] Proxmox Server Solutions GmbH - Implement GetRunningState for Proxmox Virtual Environment
- [Proxmox Virtual Environment] Proxmox Server Solutions GmbH - Implement TerminateProcesses for Proxmox Virtual Environment
- [Proxmox Virtual Environment] Proxmox Server Solutions GmbH - Implement Run for Proxmox Virtual Environment
- [Proxmox Virtual Environment] Proxmox Server Solutions GmbH - Implement GetAvailableVMs for Proxmox Virtual Environment
- [Proxmox Virtual Environment] Proxmox Server Solutions GmbH - Implement ManageVM for Proxmox Virtual Environment
- [Proxmox Virtual Environment] Proxmox Server Solutions GmbH - Implement GetVMState for Proxmox Virtual Environment
- [WatchGuard Endpoint Security Basic] WatchGuard Technologies Inc - Implement GetVersion for WatchGuard Endpoint Security Basic
- [WatchGuard Endpoint Security Basic] WatchGuard Technologies Inc - Implement GetRealTimeProtectionState for WatchGuard Endpoint Security Basic
- [WatchGuard Endpoint Security Basic] WatchGuard Technologies Inc - Implement GetDefinitionState for WatchGuard Endpoint Security Basic

#### [Mac](/docs/mdsdk/release-notes/july-07-2026#mac)

- [Auggie] Augment Code - Implement GetVersion for Auggie
- [Auggie] Augment Code - Implement GetInstallationDirectories for Auggie
- [GitHub Desktop] GitHub, Inc. - Implement Run for GitHub Desktop
- [Loom] Atlassian - Implement Run for Loom
- [Yubico Authenticator] Yubico AB - Implement Run for Yubico Authenticator
- [BBEdit] Bare Bone Software, Inc. - Implement Run for BBEdit
- [AWS VPN Client] Amazon Web Services, Inc - Implement Run for AWS VPN Client
