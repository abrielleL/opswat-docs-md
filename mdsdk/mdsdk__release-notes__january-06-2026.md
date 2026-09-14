<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/january-06-2026 -->

# January 06th, 2026

## [Release Note](/docs/mdsdk/release-notes/january-06-2026#release-note)

### [Release Date](/docs/mdsdk/release-notes/january-06-2026#release-date)

- 06/01/2026

### [SDK Version](/docs/mdsdk/release-notes/january-06-2026#sdk-version)

- **Windows**: 4.3.5463.0
- **Linux**: 4.3.4510.0
- **Mac**: 4.3.4910.0

### [Enhancement](/docs/mdsdk/release-notes/january-06-2026#enhancement)

#### [Windows](/docs/mdsdk/release-notes/january-06-2026#windows)

- Add "usable_download_link" to analog/server/products.json

#### [Linux](/docs/mdsdk/release-notes/january-06-2026#linux)

- Add "usable_download_link" to analog/server/products.json

#### [Mac](/docs/mdsdk/release-notes/january-06-2026#mac)

- N/A

### [Bug Fix](/docs/mdsdk/release-notes/january-06-2026#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/january-06-2026#windows)

- Fixed incorrect detection of QI-ANXIN Tianqing when using its marketing name GHUES by updating the detection logic to recognize both names, ensuring accurate identification and compliance reporting for users.
- Fixed temp folders not being deleted on Windows 8.1 by implementing logic to detect and prevent reparse point traversal based on Windows API error codes, ensuring secure cleanup of temporary files and improving system hygiene for all users.
- Fixed failed Webex upgrades when both per-user and per-machine variants were installed by introducing separate detection and patching for each variant, ensuring reliable updates and preventing installation errors for all users.

#### [Linux](/docs/mdsdk/release-notes/january-06-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/january-06-2026#mac)

- N/A

### [New Application Support](/docs/mdsdk/release-notes/january-06-2026#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/january-06-2026#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/january-06-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/january-06-2026#mac)

- N/A

### [New Application Version Support](/docs/mdsdk/release-notes/january-06-2026#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/january-06-2026#windows)

- V4 | Windows | Add support for Trellix Endpoint Security version 10.7.19.13811
- V4 | Windows | Add support for Thunderbird (x86) version 146.0.1
- V4 | Windows | Add support for Thunderbird (x64) version 146.0.1
- V4 | Windows | Add support for BitLocker Drive Encryption version 10.0.26100.7309
- V4 | Windows | Add support for Webroot SecureAnywhere version 9.0.42.38
- V4 | Windows | Add support for Bitdefender Antivirus Plus version 27.0.54.272
- V4 | Windows | Add support for Dropbox 3+ version 238.4.6305
- V4 | Windows | Add support for BitLocker Drive Encryption version 10.0.26100.7019
- V4 | Windows | Add support for Windows Defender version 4.18.25110.6
- V4 | Windows | Add support for Sentinel Agent version 25.2.3.407

#### [Linux](/docs/mdsdk/release-notes/january-06-2026#linux)

- V4 | Linux | Add support for Zoom version 6.7.2.6498

#### [Mac](/docs/mdsdk/release-notes/january-06-2026#mac)

- N/A

### [New Method Implementation](/docs/mdsdk/release-notes/january-06-2026#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/january-06-2026#windows)

- [QI-ANXIN Tianqing] Qi An Xin Group - Implement GetVersion for QI-ANXIN Tianqing
- [Trellix Endpoint Security] Musarubra US LLC. - Update GetScanState implementation for Trellix Endpoint Security
- [Webex] Cisco Systems, Inc - Update GetVersion implementation for Webex (x64)
- [Webex] Cisco Systems, Inc - Update GetRunningState implementation for Webex (x64)
- [Webex] Cisco Systems, Inc - Update TerminateProcesses implementation for Webex (x64)
- [Webex] Cisco Systems, Inc - Implement GetUninstallHive for Webex (x64)
- [Webex] Cisco Systems, Inc - Implement GetUninstallHive for Webex (User) (x64)
- [Webex] Cisco Systems, Inc - Update GetVersion implementation for Webex (User) (x64)
- [Webex] Cisco Systems, Inc - Update GetInstallationDirectories implementation for Webex (User) (x64)
- [Webex] Cisco Systems, Inc - Update GetRunningState implementation for Webex (User) (x64)
- [Webex] Cisco Systems, Inc - Update TerminateProcesses implementation for Webex (User) (x64)
- [MongoDB Community Server] MongoDB, Inc. - Implement GetInstallationDirectories for MongoDB Community Server 7.0
- [MongoDB Community Server] MongoDB, Inc. - Implement GetVersion for MongoDB Community Server 7.0
- [VIPRE Antivirus Plus] VIPRE Security Group, Inc. - Implement GetLastScanTime for VIPRE Antivirus Plus
- [VIPRE Antivirus Plus] VIPRE Security Group, Inc. - Implement GetThreats for VIPRE Antivirus Plus
- [VIPRE Antivirus Plus] VIPRE Security Group, Inc. - Implement GetAntiphishingState for VIPRE Antivirus Plus
- [VIPRE Antivirus Plus] VIPRE Security Group, Inc. - Implement UpdateDefinitions for VIPRE Antivirus Plus
- [VIPRE Antivirus Plus] VIPRE Security Group, Inc. - Implement GetDefinitionState for VIPRE Antivirus Plus
- [VIPRE Antivirus Plus] VIPRE Security Group, Inc. - Implement EnableRTP for VIPRE Antivirus Plus
- [VIPRE Antivirus Plus] VIPRE Security Group, Inc. - Implement GetRealTimeProtectionState for VIPRE Antivirus Plus
- [VIPRE Antivirus Plus] VIPRE Security Group, Inc. - Implement GetRunningState for VIPRE Antivirus Plus
- [VIPRE Antivirus Plus] VIPRE Security Group, Inc. - Implement Run for VIPRE Antivirus Plus
- [VIPRE Antivirus Plus] VIPRE Security Group, Inc. - Implement GetInstallationDirectories for VIPRE Antivirus Plus
- [Nextcloud Desktop Client] Nextcloud GmbH - Implement Run for Nextcloud Desktop Client
- [Nextcloud Desktop Client] Nextcloud GmbH - Implement GetUninstallHive for Nextcloud Desktop Client
- [Nextcloud Desktop Client] Nextcloud GmbH - Update GetBackupState implementation for Nextcloud Desktop Client

#### [Linux](/docs/mdsdk/release-notes/january-06-2026#linux)

- [Mozilla Firefox ESR] Mozilla Corporation - Update GetVersion implementation for Mozilla Firefox ESR
- [Mozilla Firefox] Mozilla Corporation - Update GetVersion implementation for Mozilla Firefox
- [Visual Studio Code] Microsoft Corporation - Update GetVersion implementation for Visual Studio Code
- [VNC Viewer] RealVNC Ltd - Update GetVersion implementation for VNC Viewer
- [RealVNC Server] RealVNC Ltd - Update GetVersion implementation for RealVNC Server
- [Citrix Workspace] Citrix Systems, Inc. - Update GetVersion implementation for Citrix Workspace

#### [Mac](/docs/mdsdk/release-notes/january-06-2026#mac)

- [Kaspersky Endpoint Security] Kaspersky Lab - Update GetRealTimeProtectionState implementation for Kaspersky Endpoint Security
- [Zalo] VNG Corporation - Implement GetVersion for Zalo
