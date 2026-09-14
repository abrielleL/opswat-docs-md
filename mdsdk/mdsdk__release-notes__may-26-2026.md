<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/may-26-2026 -->

# May 26th, 2026

## [Release Note](/docs/mdsdk/release-notes/may-26-2026#release-note)

### [Release Date](/docs/mdsdk/release-notes/may-26-2026#release-date)

- 26/05/2026

### [SDK Version](/docs/mdsdk/release-notes/may-26-2026#sdk-version)

- **Windows**: 4.3.6110.0
- **Linux**: 4.3.5094.0
- **Mac**: 4.3.5495.0

### [Enhancement](/docs/mdsdk/release-notes/may-26-2026#enhancement)

#### [Windows](/docs/mdsdk/release-notes/may-26-2026#windows)

- Version-specific patching for 3rd-party application
- Support Patching for Windows Drivers

#### [Linux](/docs/mdsdk/release-notes/may-26-2026#linux)

- Version-specific patching for 3rd-party application

#### [Mac](/docs/mdsdk/release-notes/may-26-2026#mac)

- N/A

### [Bug Fix](/docs/mdsdk/release-notes/may-26-2026#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/may-26-2026#windows)

- Resolved the issue where Norton and Symantec product feeds were not updating via vmod-om.dat by updating the deprecated retrieval links to the active Broadcom security center source, ensuring users receive the most up-to-date virus definitions.
- Fixed incorrect vulnerability flagging for OpenVPN 2.7.0 stable by adding a conditional check to prevent false-positive entries from the update field, ensuring users receive accurate security assessments without erroneous alerts.

#### [Linux](/docs/mdsdk/release-notes/may-26-2026#linux)

- Resolved the issue where a broken dpkg state incorrectly returned a generic "download_failed" error via a new detection mechanism and an optional auto-repair parameter, improving error clarity and enabling seamless automated recovery for Linux patch installations.
- Fixed the failure of KVM vulnerability scans on SLES 16 by updating the version extraction logic in the compliance method to correctly identify kernel module paths, ensuring accurate vulnerability reporting for users.
- Resolved the issue where Norton and Symantec product feeds were not updating via vmod-om.dat by updating the deprecated retrieval links to the active Broadcom security center source, ensuring users receive the most up-to-date virus definitions.

#### [Mac](/docs/mdsdk/release-notes/may-26-2026#mac)

- N/A

### [New Application Support](/docs/mdsdk/release-notes/may-26-2026#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/may-26-2026#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/may-26-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/may-26-2026#mac)

- N/A

### [New Application Version Support](/docs/mdsdk/release-notes/may-26-2026#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/may-26-2026#windows)

- V4 | Windows | Add support for Trend Micro Apex One Security Agent version 14.0.20790
- V4 | Windows | Add support for CrowdStrike Falcon version 7.37.20907.0
- V4 | Windows | Add support for ESET Endpoint Antivirus version 12.0.2062.0
- V4 | Windows | Add support for Sentinel Agent version 26.1.1.163
- V4 | Windows | Add support for Microsoft Teams version 26106.1906.4665.7308

#### [Linux](/docs/mdsdk/release-notes/may-26-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/may-26-2026#mac)

- N/A

### [New Method Implementation](/docs/mdsdk/release-notes/may-26-2026#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/may-26-2026#windows)

- [WatchGuard Endpoint Security 360] WatchGuard Technologies Inc - Implement GetVersion for WatchGuard Endpoint Security 360
- [WatchGuard Endpoint Security 360] WatchGuard Technologies Inc - Implement GetDefinitionState for WatchGuard Endpoint Security 360
- [WatchGuard Endpoint Security 360] WatchGuard Technologies Inc - Implement GetRealTimeProtectionState for WatchGuard Endpoint Security 360
- [Panda Dome] Panda Security, S.L. - Implement GetVersion for Panda Dome
- [Rapid7 Insight Agent] Rapid7 - Update TerminateProcesses implementation for Rapid7 Insight Agent
- [Rapid7 Insight Agent] Rapid7 - Update GetRunningState implementation for Rapid7 Insight Agent
- [Trend Micro Apex One Security Agent] Trend Micro, Inc. - Update GetVersion implementation for Trend Micro Apex One Security Agent
- [Microsoft Teams] Microsoft Corporation - Implement Run for Microsoft Teams (work or school)

#### [Linux](/docs/mdsdk/release-notes/may-26-2026#linux)

- [Advanced Packaging Tool] GNU - Update InstallMissingPatches implementation for Advanced Packaging Tool
- [KVM] KVM - Update GetVersion implementation for KVM

#### [Mac](/docs/mdsdk/release-notes/may-26-2026#mac)
