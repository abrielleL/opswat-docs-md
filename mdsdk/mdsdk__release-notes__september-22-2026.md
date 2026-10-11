<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/september-22-2026 -->

# September 22nd, 2026

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Release Note](/docs/mdsdk/release-notes/september-22-2026#release-note)

### [Release Date](/docs/mdsdk/release-notes/september-22-2026#release-date)

- 22/09/2026

### [SDK Version](/docs/mdsdk/release-notes/september-22-2026#sdk-version)

- **Windows**: 4.3.6637.0
- **Linux**: 4.3.5637.0
- **Mac**: 4.3.6028.0

### [Enhancement](/docs/mdsdk/release-notes/september-22-2026#enhancement)

#### [Windows](/docs/mdsdk/release-notes/september-22-2026#windows)

- Enhancement Request: Microsoft Teams (3799) UWP Identification

#### [Linux](/docs/mdsdk/release-notes/september-22-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/september-22-2026#mac)

- N/A

### [Bug Fix](/docs/mdsdk/release-notes/september-22-2026#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/september-22-2026#windows)

- Fixed the absence of Microsoft out-of-band patch KB5129195 by manually importing the data into WSUS and triggering the WUO pipeline, ensuring users have access to the latest security updates and installer files.
- Update the patching method for Docker Desktop to return versioned installer URLs instead of version-less links, improving download reliability and hash verification accuracy for users.
- Support patching method for signatures of Wireshark (211, 3592) on older Windows OS. Drop support patching for Webex (3268, 4103) on older Windows OS

#### [Linux](/docs/mdsdk/release-notes/september-22-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/september-22-2026#mac)

- Resolved the issue where ManageEngine UEMS was not detected on macOS via a re-implementation of the detection logic using both product code and server IP address, improving product visibility and compliance reporting for on-premise deployments.
- Resolved the issue where ManageEngine Patch Manager Plus Agent was not detected on macOS via a re-implementation of the detection logic using product codes and server IP addresses, improving SDK reliability and product visibility across all compatible machines.

### [New Application Support](/docs/mdsdk/release-notes/september-22-2026#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/september-22-2026#windows)

- Add detection support for Camtasia Studio
- [New Product Support] Add detection for ESET Small Business Security
- Windows | Add NinjaRMMAgent (ID 2917) to Remote Control category also

#### [Linux](/docs/mdsdk/release-notes/september-22-2026#linux)

- V4 | Linux | Add support for a new product version ClamAV 1.5.3

#### [Mac](/docs/mdsdk/release-notes/september-22-2026#mac)

- macOS | Add support auto-patching for Stats

### [New Application Version Support](/docs/mdsdk/release-notes/september-22-2026#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/september-22-2026#windows)

- V4 | Windows | Add support for Bitdefender Endpoint Security Tools version 8.26.9.668
- V4 | Windows | Add support for Trend Micro Apex One Security Agent version 14.0.20958
- V4 | Windows | Add support for Acronis Cyber Protection Agent version 26.03
- V4 | Windows | Add support for Sophos Endpoint Agent version 2026.2.1.3.0
- V4 | Windows | Add support for Kaspersky Endpoint Security version 14.1.0.423
- V4 | Windows | Add support for CrowdStrike Falcon version 8.10.21408.0
- V4 | Windows | Add support for Bitdefender Antivirus Free version 27.0.60.337
- V4 | Windows | Add support for Google Chrome version 153.0.8010.53
- Add detection support for Camtasia Studio
- V4 | Windows | Add support for Windows Defender version 4.18.26070.9
- [New Product Support] Add detection for ESET Small Business Security
- Windows | Add NinjaRMMAgent (ID 2917) to Remote Control category also

#### [Linux](/docs/mdsdk/release-notes/september-22-2026#linux)

- V4 | Linux | Add support for a new product version ClamAV 1.5.3

#### [Mac](/docs/mdsdk/release-notes/september-22-2026#mac)

- V4 | Mac | Add support for Microsoft Teams (work or school) version 26213.1006.5011.1671
- V4 | Mac | Add support for Spotify version 1.2.87.410
- V4 | Mac | Add support for Adobe Acrobat Reader DC Continuous version 26.002.21869
- V4 | Mac | Add support for Firefox version 153.0.3

### [New Method Implementation](/docs/mdsdk/release-notes/september-22-2026#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/september-22-2026#windows)

- [avast! Free Antivirus] AVAST Software a.s. - Implement GetLastScanTime for avast! Free Antivirus
- [Chromium-Gost] The Chromium-Gost Authors - Implement GetInstallationDirectories for Chromium-Gost
- [Camtasia Studio] TechSmith Corporation - Update GetVersion implementation for Camtasia Studio 2025
- [Camtasia Studio] TechSmith Corporation - Update GetVersion implementation for Camtasia Studio 2026
- [Camtasia Studio] TechSmith Corporation - Implement GetInstallationDirectories for Camtasia Studio 2025
- [Camtasia Studio] TechSmith Corporation - Implement Run for Camtasia Studio 2025
- [Camtasia Studio] TechSmith Corporation - Implement Run for Camtasia Studio 2026
- [Camtasia Studio] TechSmith Corporation - Implement GetInstallationDirectories for Camtasia Studio 2026
- [Windows Subsystem for Linux] Microsoft Corporation - Implement Run for Windows Subsystem for Linux
- [Windows Subsystem for Linux] Microsoft Corporation - Update TerminateProcesses implementation for Windows Subsystem for Linux
- [Windows Subsystem for Linux] Microsoft Corporation - Update GetRunningState implementation for Windows Subsystem for Linux
- [ESET Small Business Security] ESET - Implement GetRunningState for ESET Small Business Security
- [ESET Small Business Security] ESET - Implement GetRealTimeProtectionState for ESET Small Business Security
- [ESET Small Business Security] ESET - Implement GetDefinitionState for ESET Small Business Security
- [ESET Small Business Security] ESET - Implement GetFirewallState for ESET Small Business Security
- [ESET Small Business Security] ESET - Implement SetFirewallState for ESET Small Business Security
- [ESET Small Business Security] ESET - Implement UpdateDefinitions for ESET Small Business Security
- [ESET Small Business Security] ESET - Implement GetLastScanTime for ESET Small Business Security
- [Microsoft .NET SDK 9.0] Microsoft Corporation - Implement GetVersion for Microsoft .NET SDK 9.0 (x86)

#### [Linux](/docs/mdsdk/release-notes/september-22-2026#linux)

- [Zoom] Zoom Video Communications, Inc. - Update GetInstallationDirectories implementation for Zoom

#### [Mac](/docs/mdsdk/release-notes/september-22-2026#mac)

- [ManageEngine Endpoint Central Agent] ZOHO Corp - Update Run implementation for ManageEngine Endpoint Central Agent
- [ManageEngine Endpoint Central Agent] ZOHO Corp - Update TerminateProcesses implementation for ManageEngine Endpoint Central Agent
- [ManageEngine Endpoint Central Agent] ZOHO Corp - Implement IsAuthentic for ManageEngine Endpoint Central Agent
- [ManageEngine Endpoint Central Agent] ZOHO Corp - Update GetRunningState implementation for ManageEngine Endpoint Central Agent
- [ManageEngine Patch Manager Plus Agent] ZOHO Corp - Implement IsAuthentic for ManageEngine Patch Manager Plus Agent
- [ESET Endpoint Security] ESET - Update GetDefinitionState implementation for ESET Endpoint Security
- [Microsoft Teams] Microsoft Corporation - Implement GetRunningState for Microsoft Teams (work or school)
- [Microsoft Teams] Microsoft Corporation - Implement TerminateProcesses for Microsoft Teams (work or school)
- [Adobe Acrobat Reader DC Continuous] Adobe Systems Inc. - Implement IsAuthentic for Adobe Acrobat Reader DC Continuous
- [Adobe Acrobat Reader DC Continuous] Adobe Systems Inc. - Update TerminateProcesses implementation for Adobe Acrobat Reader DC Continuous
- [Adobe Acrobat Reader DC Continuous] Adobe Systems Inc. - Update GetRunningState implementation for Adobe Acrobat Reader DC Continuous
- [Adobe Acrobat Reader DC Continuous] Adobe Systems Inc. - Update GetVersion implementation for Adobe Acrobat Reader DC Continuous
