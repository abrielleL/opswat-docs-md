<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/october-07-2026 -->

# October 7th, 2026

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Release Note](/docs/mdsdk/release-notes/october-07-2026#release-note)

### [Release Date](/docs/mdsdk/release-notes/october-07-2026#release-date)

- 07/10/2026

### [SDK Version](/docs/mdsdk/release-notes/october-07-2026#sdk-version)

- **Windows**: 4.3.6706.0
- **Mac**: 4.3.6098.0

### [Enhancement](/docs/mdsdk/release-notes/october-07-2026#enhancement)

#### [Windows](/docs/mdsdk/release-notes/october-07-2026#windows)

- Add change logs for Compliance data (libwaresource)
- Enhancement request to add data_source to products.json

#### [Mac](/docs/mdsdk/release-notes/october-07-2026#mac)

- Add change logs for Compliance data (libwaresource)
- Enhancement request to add data_source to products.json

### [Bug Fix](/docs/mdsdk/release-notes/october-07-2026#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/october-07-2026#windows)

- Resolved a named pipe vulnerability by implementing exclusive pipe ownership and randomized rendezvous names, improving protection against unauthorized process takeovers and ensuring secure communication between the SDK and third-party hosts.
- Resolved Zoom 7.0.6 being incorrectly flagged for vulnerabilities via correcting the fix versions for CVE-2026-53413, CVE-2026-53414, and CVE-2026-53415, improving the accuracy of vulnerability reporting for users on the 7.0.x branch.
- Fixed disk exhaustion caused by accumulated temporary registry transaction files during DetectProducts when detect_all_users_products is enabled. The SDK now cleans up all transaction sidecar files after the operation completes.
- Fixed the incorrect classification of Microsoft Office 365 and Office Click-to-Run applications as manual patching by updating the data rules to recognize download scripts as automatic, ensuring users can accurately identify and leverage automatic patching for these products.
- Fixed missing vulnerability mapping for CVE-2026-16367 on Mozilla Firefox by correcting the version range in the vulnerability data, improving the accuracy of security reporting and patch detection for affected users.

#### [Mac](/docs/mdsdk/release-notes/october-07-2026#mac)

- N/A

### [New Application Support](/docs/mdsdk/release-notes/october-07-2026#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/october-07-2026#windows)

- Add detection support for Cynet EPS 5.x
- Add detection support for OneSEC ThreatBook Agent

#### [Mac](/docs/mdsdk/release-notes/october-07-2026#mac)

- N/A

### [New Application Version Support](/docs/mdsdk/release-notes/october-07-2026#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/october-07-2026#windows)

- V4 | Windows | Add support for Webroot SecureAnywhere version 9.0.46.75
- V4 | Windows | Add support for Malwarebytes Anti-Malware version 5.7.2.358
- V4 | Windows | Add support for Avast Premium Security version 26.8
- V4 | Windows | Add support for ESET Smart Security version 19.2.7.0
- V4 | Windows | Add support for Transmission version 4.1.3
- V4 | Windows | Add support for Microsoft Defender ATP version 10.0.28000.3086
- V4 | Windows | Add support for Bitdefender Total Security version 27.0.55.303
- V4 | Windows | Add support for Bitdefender Internet Security version 27.0.62.355
- V4 | Windows | Add support for Cisco Secure Endpoint version 8.6.2.30642
- Add Support for Trellix Endpoint Security 26.8.0

#### [Mac](/docs/mdsdk/release-notes/october-07-2026#mac)

- V4 | Mac| Add support for The Unarchiver version 4.3.9
- V4 | Mac | Add support for Malwarebytes 4+ version 5.28.3
- V4 | Mac | Add support for Bitdefender Endpoint Security for Mac version 8.26.08.200046
- V4 | Mac | Add support for Xprotect version 5363

### [New Method Implementation](/docs/mdsdk/release-notes/october-07-2026#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/october-07-2026#windows)

- [CynetEPS] Cynet Security LTD - Update TerminateProcesses implementation for CynetEPS
- [CynetEPS] Cynet Security LTD - Update Run implementation for CynetEPS
- [CynetEPS] Cynet Security LTD - Implement GetInstallationDirectories for CynetEPS
- [CynetEPS] Cynet Security LTD - Implement GetRunningState for CynetEPS
- [Git] The Git Development Community - Update GetVersion implementation for Git (x64)
- [QI-ANXIN Tianqing] Qi An Xin Group - Implement GetFirewallState for QI-ANXIN Tianqing
- [QI-ANXIN Tianqing] Qi An Xin Group - Update GetVersion implementation for QI-ANXIN Tianqing
- [Bitdefender Internet Security] Bitdefender - Update GetFirewallState implementation for Bitdefender Internet Security
- [Microsoft .NET SDK 10.0] Microsoft Corporation - Implement GetComponents for Microsoft .NET SDK 10.0 (arm64)
- [Microsoft .NET SDK 10.0] Microsoft Corporation - Implement GetInstallationDirectories for Microsoft .NET SDK 10.0 (arm64)
- [Microsoft .NET SDK 10.0] Microsoft Corporation - Implement GetUninstallString for Microsoft .NET SDK 10.0 (arm64)
- [Microsoft .NET SDK 10.0] Microsoft Corporation - Implement GetComponents for Microsoft .NET SDK 10.0 (x86)
- [Microsoft .NET SDK 10.0] Microsoft Corporation - Implement GetInstallationDirectories for Microsoft .NET SDK 10.0 (x86)
- [Microsoft .NET SDK 10.0] Microsoft Corporation - Implement GetUninstallString for Microsoft .NET SDK 10.0 (x86)
- [Microsoft .NET SDK 10.0] Microsoft Corporation - Implement GetInstallationDirectories for Microsoft .NET SDK 10.0 (x64)
- [Microsoft .NET SDK 10.0] Microsoft Corporation - Implement GetUninstallString for Microsoft .NET SDK 10.0 (x64)
- [Microsoft .NET SDK 10.0] Microsoft Corporation - Implement GetComponents for Microsoft .NET SDK 10.0 (x64)
- [Microsoft Web Deploy] Microsoft Corporation - Implement GetVersion for Microsoft Web Deploy
- [ThreatBook Agent] Beijing ThreatBook Technology Co., Ltd - Implement GetDefinitionState for ThreatBook Agent
- [ThreatBook Agent] Beijing ThreatBook Technology Co., Ltd - Implement GetRealTimeProtectionState for ThreatBook Agent
- [ThreatBook Agent] Beijing ThreatBook Technology Co., Ltd - Implement GetLastScanTime for ThreatBook Agent
- [ThreatBook Agent] Beijing ThreatBook Technology Co., Ltd - Implement GetVersion for ThreatBook Agent
- [ESET Smart Security] ESET - Update SetFirewallState implementation for ESET Smart Security

#### [Mac](/docs/mdsdk/release-notes/october-07-2026#mac)

- [GIMP] Spencer Kimball, Peter Mattis and the GIMP Development Team - Update GetVersion implementation for GIMP
