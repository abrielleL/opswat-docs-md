<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/february-03-2026 -->

# February 03rd, 2026

## [Release Note](/docs/mdsdk/release-notes/february-03-2026#release-note)

### [Release Date](/docs/mdsdk/release-notes/february-03-2026#release-date)

- 03/02/2026

### [SDK Version](/docs/mdsdk/release-notes/february-03-2026#sdk-version)

- **Windows**: 4.3.5588.0
- **Linux**: 4.3.4630.0
- **Mac**: 4.3.5031.0

### [Enhancement](/docs/mdsdk/release-notes/february-03-2026#enhancement)

#### [Windows](/docs/mdsdk/release-notes/february-03-2026#windows)

- Add Gaming software category
- Add AI software category

#### [Linux](/docs/mdsdk/release-notes/february-03-2026#linux)

- Add Gaming software category
- Add AI software category

#### [Mac](/docs/mdsdk/release-notes/february-03-2026#mac)

- N/A

### [Bug Fix](/docs/mdsdk/release-notes/february-03-2026#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/february-03-2026#windows)

- Fixed unexpected revision values in cves.json by updating incorrect CVE entries to use only valid revisions, ensuring accurate vulnerability data and preventing related errors for users.
- Fixed incorrect RealTimeProtection state detection for Carbon Black Cloud Sensor by adding an alternative retrieval method and improved error handling, ensuring accurate protection status reporting for users.

#### [Linux](/docs/mdsdk/release-notes/february-03-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/february-03-2026#mac)

- N/A

### [New Application Support](/docs/mdsdk/release-notes/february-03-2026#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/february-03-2026#windows)

- Add support detection and patching for new product: ImageMagick version 7.1.x
- V4 | Windows | Separate signature for Zoom exe and msi

#### [Linux](/docs/mdsdk/release-notes/february-03-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/february-03-2026#mac)

- N/A

### [New Application Version Support](/docs/mdsdk/release-notes/february-03-2026#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/february-03-2026#windows)

- V4 | Windows | Add support for Spotify version 1.2.82.428
- V4 | Windows | Add support for Microsoft Office 2021 version 16.0.19628.20150
- V4 | Windows | Add support for Microsoft Office 365 version 16.0.19628.20150
- V4 | Mac | Add support for Thunderbird version 147.0
- V4 | Windows | Add support for Mozilla Firefox (arm64) version 147.0.2
- V4 | Windows | Add support for Mozilla Firefox (x64) version 147.0.2
- V4 | Windows | Add support for Mozilla Firefox (x86) version 147.0.2
- V4 | Windows | Add support for CrowdStrike Falcon version 7.33.20504.0
- V4 | Windows | Add support for Adobe Acrobat Reader DC Continuous version 25.001.20997

#### [Linux](/docs/mdsdk/release-notes/february-03-2026#linux)

- V4 | Linux | Add support for Firefox version 147.0.1
- V4 | Linux | Add support for Google Chrome version 144.0.7559.109
- V4 | Linux | Add support for Thunderbird version 147.0.1

#### [Mac](/docs/mdsdk/release-notes/february-03-2026#mac)

- N/A

### [New Method Implementation](/docs/mdsdk/release-notes/february-03-2026#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/february-03-2026#windows)

- [iTunes] Apple Inc. - Implement GetUninstallHive for iTunes (UWP)
- [Webex] Cisco Systems, Inc - Implement GetComponents for Webex (User) (x64)
- [Check Point Endpoint Security] Check Point Software Technologies - Update GetDefinitionState implementation for Check Point Endpoint Security
- [iTunes] Apple Inc. - Implement GetVersion for iTunes (UWP)
- [Zoom] Zoom Video Communications, Inc. - Implement GetUninstallString for Zoom
- [Zoom] Zoom Video Communications, Inc. - Implement GetUninstallHive for Zoom
- [Zoom] Zoom Video Communications, Inc. - Implement GetUninstallString for Zoom msi
- [Zoom] Zoom Video Communications, Inc. - Implement GetUninstallHive for Zoom msi
- [Carbon Black Cloud Sensor] Broadcom - Update GetRealTimeProtectionState implementation for Carbon Black Cloud Sensor 4+
- [QEMU Guest Agent] Red Hat, Inc. - Implement GetRunningState for QEMU Guest Agent
- [QEMU Guest Agent] Red Hat, Inc. - Implement Run for QEMU Guest Agent
- [QEMU Guest Agent] Red Hat, Inc. - Implement TerminateProcesses for QEMU Guest Agent
- [QEMU Guest Agent] Red Hat, Inc. - Implement IsAuthentic for QEMU Guest Agent
- [QEMU Guest Agent] Red Hat, Inc. - Implement GetUninstallHive for QEMU Guest Agent
- [QEMU Guest Agent] Red Hat, Inc. - Implement GetUninstallString for QEMU Guest Agent
- [CrowdStrike Falcon] CrowdStrike, Inc. - Update GetThreats implementation for CrowdStrike Falcon
- [Adobe Acrobat Reader DC Continuous] Adobe Systems Inc. - Update GetUninstallHive implementation for Adobe Acrobat Reader DC Continuous
- [Tungsten Power PDF Standard] Tungsten Automation - Implement GetVersion for Tungsten Power PDF Standard
- [Cortex XDR] Palo Alto Networks, Inc. - Implement GetVersion for Cortex XDR
- [TreeSize Free] JAM Software - Implement GetVersion for TreeSize Free

#### [Linux](/docs/mdsdk/release-notes/february-03-2026#linux)

- [Visual Studio Code] Microsoft Corporation - Update GetVersion implementation for Visual Studio Code
- [Crowdstrike Falcon] CrowdStrike, Inc. - Implement GetFirewallState for Crowdstrike Falcon
- [Mozilla Firefox] Mozilla Corporation - Update GetAntiphishingState implementation for Mozilla Firefox

#### [Mac](/docs/mdsdk/release-notes/february-03-2026#mac)

- [Software Update] Apple Inc. - Update InstallMissingPatches implementation for Software Update
