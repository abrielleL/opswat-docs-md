<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/october-27-2026 -->

# October 27th, 2026

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
## [Release Note](/docs/mdsdk/release-notes/october-27-2026#release-note)

### [Release Date](/docs/mdsdk/release-notes/october-27-2026#release-date)

- 27/10/2026

### [SDK Version](/docs/mdsdk/release-notes/october-27-2026#sdk-version)

- **Windows**: 4.3.6788.0
- **Linux**: 4.3.5785.0
- **Mac**: 4.3.6181.0

### [Enhancement](/docs/mdsdk/release-notes/october-27-2026#enhancement)

#### [Windows](/docs/mdsdk/release-notes/october-27-2026#windows)

- GetProductVulnerability: support detect_affected_instances on Windows
- Support Vulnerability Assessment for Windows Drivers
- Distinguish OS restart vs application restart in patch reboot metadata (reboot_required is overloaded)

#### [Linux](/docs/mdsdk/release-notes/october-27-2026#linux)

- Distinguish OS restart vs application restart in patch reboot metadata (reboot_required is overloaded)
- Support Compliance module for Ubuntu 26.10

#### [Mac](/docs/mdsdk/release-notes/october-27-2026#mac)

- GetProductVulnerability: support detect_affected_instances on macOS
- Distinguish OS restart vs application restart in patch reboot metadata (reboot_required is overloaded)

### [Bug Fix](/docs/mdsdk/release-notes/october-27-2026#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/october-27-2026#windows)

- Resolved the issue where empty OesisHiveCopies directories were left in C:\Windows\Temp after per-user registry scans via a new approach that creates and deletes a fresh folder for each user's registry copy, improving system cleanliness and preventing temporary file accumulation.
- Fixed the failure of x64 SDK modules to initialize on Windows 11 on Arm by skipping the call-stack self-protection check when emulation is detected, ensuring full compatibility and reliable method execution for x64 applications on Arm devices.
- Fixed the issue where the helper process could load unauthorized WMI COM objects from the user registry by binding WMI client components to their machine-wide registration at startup, improving the security and integrity of signed process execution during system checks.
- Fixed multiple privilege-escalation and hardware-access vulnerabilities in the OESIS V4 Helper Driver by restricting device control permissions to administrators and implementing strict request-size validation, improving overall system security and protecting against unauthorized local access.

#### [Linux](/docs/mdsdk/release-notes/october-27-2026#linux)

- Fixed the failure to delete expired debug logs on XFS filesystems (with ftype = 0 ) by implementing an lstat() fallback for entries with unknown types, ensuring consistent log retention and directory listing for users on older Linux volume formats.

#### [Mac](/docs/mdsdk/release-notes/october-27-2026#mac)

- Fixed the failure to delete expired debug logs on XFS filesystems (with ftype = 0 ) by implementing an lstat() fallback for entries with unknown types, ensuring consistent log retention and directory listing for users on older Linux volume formats.

### [New Application Support](/docs/mdsdk/release-notes/october-27-2026#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/october-27-2026#windows)

- Add support detection for ALYac Enterprise 5.1
- V4 | Update data for vmod-om.dat of some products
- KB_info.json missing Server 2022 and 2025 information
- PatchV2 | Add patch management support for ASCOMP Software Synchredible
- Add Vulnerability detection support for Microsoft NET Runtime 8.0
- Request for Driver/Firmware patching for Latitude 5420 and Precision 5690
- PatchV2 | Add support for Omnissa Horizon Client v8.19

#### [Linux](/docs/mdsdk/release-notes/october-27-2026#linux)

- Add support for CrowdStrike Falcon 8.X Anti-Malware for Linux
- Request for Driver/Firmware patching for Latitude 5420 and Precision 5690

#### [Mac](/docs/mdsdk/release-notes/october-27-2026#mac)

- V4 | Update data for vmod-om.dat of some products
- MacOS | Request support auto patching for Sublime Text 4
- V4| Add support| Trellix Endpoint Security 26.x For MacOS
- Add Support for Kaspersky Endpoint Security for Mac 12.2.1
- MacOS | Request support auto patching for new app Obsidian
- Request for Driver/Firmware patching for Latitude 5420 and Precision 5690
- MacOS | Request support detection for new app Obsidian

### [New Application Version Support](/docs/mdsdk/release-notes/october-27-2026#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/october-27-2026#windows)

- Add support detection for ALYac Enterprise 5.1
- V4 | Windows | Add support for Sophos Endpoint Agent version 2026.3.0.2090.0
- V4 | Windows | Add support for Kaspersky Endpoint Security version 14.2.0.536
- V4 | Windows | Add support for Cisco Secure Endpoint version 8.6.3
- V4 | Windows | Add support for Microsoft Visual Studio Code (User) (Arm64) version 1.141.1
- V4 | Windows | Add support for Microsoft Visual Studio Code (Arm64) version 1.141.1
- KB_info.json missing Server 2022 and 2025 information
- V4 | Windows | Add support for Cortex XDR version 9.4
- V4 | Windows | Add support for Bitdefender Antivirus Plus version 27.0.62.355
- PatchV2 | Add patch management support for ASCOMP Software Synchredible
- Add Vulnerability detection support for Microsoft NET Runtime 8.0
- V4 | Windows | Add support for Microsoft Defender ATP version 10.0.26100.9711
- Request for Driver/Firmware patching for Latitude 5420 and Precision 5690
- PatchV2 | Add support for Omnissa Horizon Client v8.19
- V4 | Windows | Add support for Trend Micro Maximum Security version 17.9
- V4 | Windows | Add support for Check Point Endpoint Security version 89.26.6011
- V4 | Windows | Add support for BitTorrent version 7.11.0.47391
- V4 | Windows | Add support for Bitdefender Endpoint Security Tools version 8.26.10.671
- V4 | Windows | Add support for Microsoft Visual Studio Code (Arm64) version 1.141.0
- V4 | Windows | Add support for Microsoft Visual Studio Code (User) (Arm64) version 1.141.0

#### [Linux](/docs/mdsdk/release-notes/october-27-2026#linux)

- V4 | Linux | Add support for MySQL Server version 26.10.0
- V4 | Linux | Add support for Visual Studio Code version 1.143.0
- V4 | Linux | Add support for Thunderbird version 158.0.1
- Add support for CrowdStrike Falcon 8.X Anti-Malware for Linux
- V4 | Linux | Add support for Google Chrome version 156.0.8078.47
- V4 | Linux | Add support for Signal version 8.32.0
- V4 | Linux | Add support for Advanced Packaging Tool version 3.3.4
- V4 | Linux | Add support for Mozilla Firefox ESR version 153.5.0
- V4 | Linux | Add support for Mozilla Firefox version 158.0
- V4 | Linux | Add support for Signal version 8.31.0
- V4 | Linux | Add support for Thunderbird version 158.0
- V4 | Linux | Add support for Visual Studio Code version 1.142.0
- Request for Driver/Firmware patching for Latitude 5420 and Precision 5690
- V4 | Linux | Add support for Firewalld version 2.5.2
- V4 | Linux | Add support for Mozilla Firefox ESR version 140.17.0
- V4 | Linux | Add support for IPTables version 1.8.13

#### [Mac](/docs/mdsdk/release-notes/october-27-2026#mac)

- MacOS | Request support auto patching for Sublime Text 4
- V4| Add support| Trellix Endpoint Security 26.x For MacOS
- V4 | Mac | Add support for Trend Micro Deep Security Agent version 20.0.0.271
- V4 | Mac | Add support for Webex version 46.10.0.36042
- MacOS | Request support auto patching for new app Obsidian
- Request for Driver/Firmware patching for Latitude 5420 and Precision 5690
- V4 | Mac | Add support for ESET Endpoint Security version 9.1.3100.0
- MacOS | Request support detection for new app Obsidian
- V4 | Mac | Add support for Kaspersky Endpoint Security version 12.2.1.191
- V4 | Mac | Add support for Little Snitch version 6.5

### [New Method Implementation](/docs/mdsdk/release-notes/october-27-2026#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/october-27-2026#windows)

- [Tera Term] TeraTerm Project T. Teranishi - Implement GetVersion for Tera Term (User)
- [Arduino IDE] Arduino s.r.l. - Implement GetVersion for Arduino IDE msi
- [Arduino IDE] Arduino s.r.l. - Implement GetVersion for Arduino IDE exe
- [Arduino IDE] Arduino s.r.l. - Implement GetVersion for Arduino IDE exe (User)
- [Kaspersky Endpoint Security] Kaspersky Lab - Update Scan implementation for Kaspersky Endpoint Security
- [OpenPencil] dannote - Implement GetUninstallString for OpenPencil
- [OpenPencil] dannote - Implement GetInstallationDirectories for OpenPencil
- [OpenPencil] dannote - Implement GetUninstallHive for OpenPencil
- [OpenPencil] dannote - Implement GetVersion for OpenPencil
- [Sophos Endpoint Agent] Sophos Limited - Update GetRealTimeProtectionState implementation for Sophos Endpoint Agent
- [GitHub Desktop] GitHub, Inc. - Implement GetVersion for GitHub Desktop
- [GitHub Desktop] GitHub, Inc. - Implement GetRunningState for GitHub Desktop
- [OpenWorker] AndrewNg - Implement Run for OpenWorker
- [NextAI Translator] yetone - Update GetVersion implementation for NextAI Translator
- [ThreatBook Agent] Beijing ThreatBook Technology Co., Ltd - Update GetRealTimeProtectionState implementation for ThreatBook Agent
- [ThreatBook Agent] Beijing ThreatBook Technology Co., Ltd - Update GetDefinitionState implementation for ThreatBook Agent
- [ESET Endpoint Security] ESET - Update GetDefinitionState implementation for ESET Endpoint Security
- [Internet Download Manager] Tonec Inc. - Implement GetVersion for Internet Download Manager
- [Microsoft Visual Studio] Microsoft Corporation - Implement GetRunningState for Visual Studio Community 2017
- [Visual Studio BuildTools 2026] Microsoft Corporation - Update GetVersion implementation for Visual Studio BuildTools 2026
- [AdoptOpenJDK JRE 11] AdoptOpenJDK - Implement GetVersion for AdoptOpenJDK JRE with Hotspot 11 (x86)
- [AdoptOpenJDK JRE 11] AdoptOpenJDK - Update GetVersion implementation for AdoptOpenJDK JRE with Hotspot 11 (x64)
- [Webex] Cisco Systems, Inc - Update GetVersion implementation for Webex (User) (x64)
- [Webex] Cisco Systems, Inc - Update GetVersion implementation for Webex (x64)
- [ALYac Enterprise] ESTsoft Corp. - Implement GetRunningState for ALYac Enterprise
- [ALYac Enterprise] ESTsoft Corp. - Implement GetVersion for ALYac Enterprise
- [MalwareFox] MalwareFox - Implement GetVersion for MalwareFox
- [MalwareFox] MalwareFox - Implement GetRunningState for MalwareFox
- [MalwareFox] MalwareFox - Implement GetDefinitionState for MalwareFox
- [MalwareFox] MalwareFox - Implement GetRealTimeProtectionState for MalwareFox

#### [Linux](/docs/mdsdk/release-notes/october-27-2026#linux)

- [Mozilla Firefox ESR] Mozilla Corporation - Update GetInstallationDirectories implementation for Mozilla Firefox ESR
- [Mozilla Firefox ESR] Mozilla Corporation - Update GetComponents implementation for Mozilla Firefox ESR
- [Visual Studio Code] Microsoft Corporation - Update Run implementation for Visual Studio Code
- [Mozilla Firefox] Mozilla Corporation - Update Run implementation for Mozilla Firefox
- [Mozilla Firefox ESR] Mozilla Corporation - Update GetAntiphishingState implementation for Mozilla Firefox ESR
- [Mozilla Firefox ESR] Mozilla Corporation - Update GetInstallationDirectories implementation for Mozilla Firefox ESR
- [Mozilla Firefox ESR] Mozilla Corporation - Update GetComponents implementation for Mozilla Firefox ESR
- [Thunderbird] Mozilla Corporation - Update Run implementation for Thunderbird
- [Thunderbird] Mozilla Corporation - Update GetInstallationDirectories implementation for Thunderbird
- [Thunderbird] Mozilla Corporation - Update GetComponents implementation for Thunderbird

#### [Mac](/docs/mdsdk/release-notes/october-27-2026#mac)

- [ThreatBook Agent] Beijing ThreatBook Technology Co., Ltd - Implement GetVersion for ThreatBook Agent
- [ThreatBook Agent] Beijing ThreatBook Technology Co., Ltd - Implement GetDefinitionState for ThreatBook Agent
- [ThreatBook Agent] Beijing ThreatBook Technology Co., Ltd - Implement GetRealTimeProtectionState for ThreatBook Agent
- [ThreatBook Agent] Beijing ThreatBook Technology Co., Ltd - Implement Run for ThreatBook Agent
- [ThreatBook Agent] Beijing ThreatBook Technology Co., Ltd - Implement GetRunningState for ThreatBook Agent
- [Kaspersky Endpoint Security] Kaspersky Lab - Update GetDefinitionState implementation for Kaspersky Endpoint Security
- [Kaspersky Endpoint Security] Kaspersky Lab - Update GetInstallDirectories implementation for Kaspersky Endpoint Security
- [ESET Endpoint Security] ESET - Update GetLastScanTime implementation for ESET Endpoint Security
- [Trend Micro Deep Security Agent] Trend Micro, Inc. - Update GetRealTimeProtectionState implementation for Trend Micro Deep Security Agent
- [Kaspersky Endpoint Security] Kaspersky Lab - Update GetScanState implementation for Kaspersky Endpoint Security
- [Kaspersky Endpoint Security] Kaspersky Lab - Update GetAntiphishingState implementation for Kaspersky Endpoint Security
