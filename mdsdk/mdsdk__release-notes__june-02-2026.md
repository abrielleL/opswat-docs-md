<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/june-02-2026 -->

# June 02nd, 2026

## [Release Note](/docs/mdsdk/release-notes/june-02-2026#release-note)

### [Release Date](/docs/mdsdk/release-notes/june-02-2026#release-date)

- 02/06/2026

### [SDK Version](/docs/mdsdk/release-notes/june-02-2026#sdk-version)

- **Windows**: 4.3.6139.0
- **Linux**: 4.3.5164.0
- **Mac**: 4.3.5555.0

### [Enhancement](/docs/mdsdk/release-notes/june-02-2026#enhancement)

#### [Windows](/docs/mdsdk/release-notes/june-02-2026#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/june-02-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/june-02-2026#mac)

- N/A

### [Bug Fix](/docs/mdsdk/release-notes/june-02-2026#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/june-02-2026#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/june-02-2026#linux)

- Resolved the issue where `InstallMissingPatches` incorrectly returned a "not_found" state on Amazon Linux 2023 via the inclusion of the `--releasever=latest` flag in the update command, ensuring successful package upgrades and accurate patch status reporting for users.

#### [Mac](/docs/mdsdk/release-notes/june-02-2026#mac)

- N/A

### [New Application Support](/docs/mdsdk/release-notes/june-02-2026#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/june-02-2026#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/june-02-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/june-02-2026#mac)

- N/A

### [New Application Version Support](/docs/mdsdk/release-notes/june-02-2026#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/june-02-2026#windows)

- V4 | Windows | Add support for Norton version 26.5.10994
- V4 | Windows | Add support for Bitdefender Antivirus Plus version 27.0.59.334
- V4 | Windows | Add support for Mozilla Firefox (x86) version 150.0.2
- V4 | Windows | Add support for Mozilla Firefox (x64) version 150.0.2
- V4 | Windows | Add support for Adobe Acrobat DC Continuous version 26.001.21563
- V4 | Windows | Add support for AVG Antivirus version 26.5.10994.3659
- V4 | Windows | Add support for Foxit Reader version 2026.1.1.36485
- V4 | Windows | Add support for FortiClient version 7.4.7.2003

#### [Linux](/docs/mdsdk/release-notes/june-02-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/june-02-2026#mac)

- N/A

### [New Method Implementation](/docs/mdsdk/release-notes/june-02-2026#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/june-02-2026#windows)

- [Norton] Gen Digital Inc. - Update GetDefinitionState implementation for Norton
- [Szafir msi] Krajowa Izba Rozliczeniowa - Implement GetVersion for Szafir msi
- [Mozilla Firefox] Mozilla Corporation - Update SetAntiphishingState implementation for Mozilla Firefox (x64)
- [Mozilla Firefox] Mozilla Corporation - Update SetAntiphishingState implementation for Mozilla Firefox (x86)
- [Mozilla Firefox] Mozilla Corporation - Update SetAntiphishingState implementation for Mozilla Firefox (x86)
- [WatchGuard Endpoint Security Basic] WatchGuard Technologies Inc - Implement GetVersion for WatchGuard Endpoint Security Basic
- [WatchGuard Endpoint Security Basic] WatchGuard Technologies Inc - Implement GetDefinitionState for WatchGuard Endpoint Security Basic
- [WatchGuard Endpoint Security 360] WatchGuard Technologies Inc - Implement GetFirewallState for WatchGuard Endpoint Security 360
- [WatchGuard Endpoint Security Basic] WatchGuard Technologies Inc - Implement GetFirewallState for WatchGuard Endpoint Security Basic
- [Kaspersky Premium] Kaspersky Lab - Update GetRealTimeProtectionState implementation for Kaspersky Premium
- [UniAccessLite] Shenzhen Leagsoft Technology Co., Ltd. - Implement GetVersion for UniAccessLite
- [UniAccessLite] Shenzhen Leagsoft Technology Co., Ltd. - Implement GetUninstallString for UniAccessLite
- [UniAccessLite] Shenzhen Leagsoft Technology Co., Ltd. - Implement GetUninstallHive for UniAccessLite
- [UniAccessLite] Shenzhen Leagsoft Technology Co., Ltd. - Implement GetDefinitionState for UniAccessLite
- [UniAccessLite] Shenzhen Leagsoft Technology Co., Ltd. - Implement GetRealTimeProtectionState for UniAccessLite
- [UniAccessLite] Shenzhen Leagsoft Technology Co., Ltd. - Implement GetRunningState for UniAccessLite
- [Mozilla Firefox] Mozilla Corporation - Update GetPlugins implementation for Mozilla Firefox (x86)
- [CrowdStrike Falcon] CrowdStrike, Inc. - Implement GetLastScanTime for CrowdStrike Falcon
- [Adobe Acrobat Pro 2024] Adobe Systems Inc. - Implement GetVersion for Adobe Acrobat Pro 2024
- [Adobe Acrobat Pro 2024] Adobe Systems Inc. - Implement GetRunningState for Adobe Acrobat Pro 2024
- [Adobe Acrobat Pro 2024] Adobe Systems Inc. - Implement TerminateProcesses for Adobe Acrobat Pro 2024
- [Foxit PDF Editor] Foxit Software Inc. - Update TerminateProcesses implementation for Foxit PDF Editor Suite

#### [Linux](/docs/mdsdk/release-notes/june-02-2026#linux)

- [VMware Workstation] VMware, Inc. - Update TerminateProcesses implementation for VMware Workstation
- [VMware Workstation] VMware, Inc. - Update GetAvailableVMs implementation for VMware Workstation
- [VMware Workstation] VMware, Inc. - Update GetRunningState implementation for VMware Workstation
- [Dandified Yum] Red Hat, Inc. - Update InstallMissingPatches implementation for Dandified Yum

#### [Mac](/docs/mdsdk/release-notes/june-02-2026#mac)
