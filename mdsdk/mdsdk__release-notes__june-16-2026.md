<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/june-16-2026 -->

# June 16th, 2026

## [Release Note](/docs/mdsdk/release-notes/june-16-2026#release-note)

### [Release Date](/docs/mdsdk/release-notes/june-16-2026#release-date)

- 16/06/2026

### [SDK Version](/docs/mdsdk/release-notes/june-16-2026#sdk-version)

- **Windows**: 4.3.6211.0
- **Linux**: 4.3.5226.0
- **Mac**: 4.3.5615.0

### [Enhancement](/docs/mdsdk/release-notes/june-16-2026#enhancement)

#### [Windows](/docs/mdsdk/release-notes/june-16-2026#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/june-16-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/june-16-2026#mac)

- N/A

### [Bug Fix](/docs/mdsdk/release-notes/june-16-2026#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/june-16-2026#windows)

- Resolved the issue where Kaspersky Endpoint Security 12.x could not be uninstalled when incompatible applications like Seqrite were present by implementing the SKIPPRODUCTCHECK=1 parameter and refactoring the removal method, ensuring a successful and silent uninstallation for users.
- Resolved the issue where Microsoft Teams version retrieval incorrectly returned the Meeting Add-in version via the implementation of a squirrel script for version detection, improving the accuracy of product version reporting for users.

#### [Linux](/docs/mdsdk/release-notes/june-16-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/june-16-2026#mac)

- N/A

### [New Application Support](/docs/mdsdk/release-notes/june-16-2026#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/june-16-2026#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/june-16-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/june-16-2026#mac)

- N/A

### [New Application Version Support](/docs/mdsdk/release-notes/june-16-2026#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/june-16-2026#windows)

- V4 | Windows | Add support for Avast One Essential version 26.5.10994.833
- V4 | Windows | Add support for Windows Defender version 4.18.26050.15
- V4 | Windows | Add support for Transmission version 4.1.2
- V4 | MacOS | Add support for Trellix Endpoint Security for Mac version 10.7.12

#### [Linux](/docs/mdsdk/release-notes/june-16-2026#linux)

- V4 | Linux | Add support for Zoom version 7.0.5
- V4 | Linux | Add support for Wireshark version 4.6.6
- V4 | Linux | Add support for Visual Studio Code version 1.123.2
- V4 | Linux | Add support for Mozilla Firefox version 151.0.4
- V4 | Linux | Add support for AlmaLinux version 9.8
- V4 | Linux | Add support for AlmaLinux version 10.2

#### [Mac](/docs/mdsdk/release-notes/june-16-2026#mac)

- N/A

### [New Method Implementation](/docs/mdsdk/release-notes/june-16-2026#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/june-16-2026#windows)

- [Comet] The Comet Authors - Implement GetUninstallString for Comet
- [Comet] The Comet Authors - Implement GetUninstallHive for Comet
- [Comet] The Comet Authors - Update GetAntiphishingState implementation for Comet
- [Comet] The Comet Authors - Update Run implementation for Comet
- [Comet] The Comet Authors - Update GetPlugins implementation for Comet
- [Comet] The Comet Authors - Update GetVersion implementation for Comet
- [Avast One Essential] Avast Software s.r.o. - Update GetLastScanTime implementation for Avast One Essential
- [VMware Workstation] VMware, Inc. - Update ListSnapshots implementation for VMware Workstation
- [VMware Workstation] VMware, Inc. - Update ManageVM implementation for VMware Workstation
- [Windows Defender] Microsoft Corporation - Update SetRansomwareProtection implementation for Windows Defender
- [ALYac] ESTsecurity Corp. - Implement GetVersion for ALYac Public
- [ALYac] ESTsecurity Corp. - Implement GetRunningState for ALYac Public
- [ALYac] ESTsecurity Corp. - Implement GetUninstallString for ALYac Public
- [ALYac] ESTsecurity Corp. - Implement GetUninstallHive for ALYac Public
- [ALYac] ESTsecurity Corp. - Implement GetDefinitionState for ALYac Public
- [GridinSoft Anti-Malware] GridinSoft LLC. - Update EnableRTP implementation for GridinSoft Anti-Malware
- [GridinSoft Anti-Malware] GridinSoft LLC. - Update UpdateDefinitions implementation for GridinSoft Anti-Malware
- [GridinSoft Anti-Malware] GridinSoft LLC. - Update Scan implementation for GridinSoft Anti-Malware
- [GridinSoft Anti-Malware] GridinSoft LLC. - Update GetLastScanTime implementation for GridinSoft Anti-Malware
- [eID Client] MV SR - Implement GetUninstallString for eID Client (x86)
- [eID Client] MV SR - Implement GetUninstallHive for eID Client (x86)
- [eID Client] MV SR - Implement GetUninstallString for eID Client (x64)
- [eID Client] MV SR - Implement GetUninstallHive for eID Client (x64)
- [eID Client] MV SR - Implement GetVersion for eID Client (x64)
- [eID Client] MV SR - Implement GetVersion for eID Client (x86)
- [NAPS2 - Not Another PDF Scanner] NAPS2 Software - Implement GetVersion for NAPS2 - Not Another PDF Scanner msi
- [Microsoft Teams] Microsoft Corporation - Implement GetVersion for Microsoft Teams

#### [Linux](/docs/mdsdk/release-notes/june-16-2026#linux)

- [Mozilla Firefox] Mozilla Corporation - Update GetRunningState implementation for Mozilla Firefox
- [FileZilla] FileZilla Project - Implement GetInstallationDirectories for FileZilla
- [FileZilla] FileZilla Project - Implement Run for FileZilla
- [FileZilla] FileZilla Project - Implement GetRunningState for FileZilla

#### [Mac](/docs/mdsdk/release-notes/june-16-2026#mac)

- [Postman] Postman - Implement GetRunningState for Postman
- [Trellix Endpoint Security for Mac] Musarubra US LLC. - Implement IsAuthentic for Trellix Endpoint Security for Mac
