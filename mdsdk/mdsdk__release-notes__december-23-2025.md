<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/december-23-2025 -->

# December 23rd, 2025

## [Release Note](/docs/mdsdk/release-notes/december-23-2025#release-note)

### [Release Date](/docs/mdsdk/release-notes/december-23-2025#release-date)

- 23/12/2025

### [SDK Version](/docs/mdsdk/release-notes/december-23-2025#sdk-version)

- **Windows**: 4.3.5405.0
- **Linux**: 4.3.4453.0
- **Mac**: 4.3.4853.0

### [Enhancement](/docs/mdsdk/release-notes/december-23-2025#enhancement)

#### [Windows](/docs/mdsdk/release-notes/december-23-2025#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/december-23-2025#linux)

- Implement splitting of liv.dat per Linux flavors
- Split liv.dat into smaller files based on Linux distros

#### [Mac](/docs/mdsdk/release-notes/december-23-2025#mac)

- N/A

### [Bug Fix](/docs/mdsdk/release-notes/december-23-2025#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/december-23-2025#windows)

- Fixed significant slowdown in GetOSInfo and related methods on Windows by update ESU status check, reducing execution time and improving overall SDK performance for faster API responses.
- Fixed failure to detect Amazon Corretto 15 on Windows by updating the signature and detection methods to ensure accurate identification and compliance reporting for all compatible machines.
- Fixed significant delays in CrowdStrike Falcon detection methods on Windows by optimizing internet connectivity checks, reducing scan times and improving user experience and operational efficiency.

#### [Linux](/docs/mdsdk/release-notes/december-23-2025#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/december-23-2025#mac)

- N/A

### [New Application Support](/docs/mdsdk/release-notes/december-23-2025#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/december-23-2025#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/december-23-2025#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/december-23-2025#mac)

- N/A

### [New Application Version Support](/docs/mdsdk/release-notes/december-23-2025#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/december-23-2025#windows)

- V4 | Windows | Add support for Microsoft Edge 80+ version 143.0.3650.96
- V4 | Windows | Add support for Mozilla Firefox (arm64) version 146.0.1
- V4 | Windows | Add support for Mozilla Firefox (x64) version 146.0.1
- V4 | Windows | Add support for Mozilla Firefox (x86) version 146.0.1
- V4 | Windows | Add support for Google Chrome version 143.0.7499.170
- V4 | Windows | Add support for Malwarebytes Anti-Malware version 5.4.5.226
- V4 | Windows | Add support for Microsoft Office 365 version 16.0.19426.20218
- V4 | Windows | Add support for Microsoft Office version 16.0.19426.20218
- V4 | Windows | Add support for Windows Defender 4.18.25110.5

#### [Linux](/docs/mdsdk/release-notes/december-23-2025#linux)

- V4 | Linux | Add support for Signal version 7.83.0
- V4 | Linux | Add support for Google Chrome version 143.0.7499.169
- V4 | Linux | Add support for Visual Studio Code version 1.107.1
- V4 | Linux | Add support for LibreOffice version 25.8.4
- V4 | Linux | Add support for Thunderbird 146.0.1
- V4 | Linux | Add support for Zoom 6.7.0.6313

#### [Mac](/docs/mdsdk/release-notes/december-23-2025#mac)

- N/A

### [New Method Implementation](/docs/mdsdk/release-notes/december-23-2025#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/december-23-2025#windows)

- [ImageMagick Q16-HDRI] ImageMagick Studio LLC - Implement TerminateProcesses for ImageMagick Q16-HDRI (x64)
- [ImageMagick Q16-HDRI] ImageMagick Studio LLC - Implement GetRunningState for ImageMagick Q16-HDRI (x64)
- [ImageMagick Q16-HDRI] ImageMagick Studio LLC - Implement IsAuthentic for ImageMagick Q16-HDRI (x64)
- [ImageMagick Q16-HDRI] ImageMagick Studio LLC - Implement GetUninstallString for ImageMagick Q16-HDRI (x64)
- [ImageMagick Q16-HDRI] ImageMagick Studio LLC - Implement GetComponents for ImageMagick Q16-HDRI (x64)
- [ImageMagick Q16-HDRI] ImageMagick Studio LLC - Implement GetInstallationDirectories for ImageMagick Q16-HDRI (x64)
- [ImageMagick Q8] ImageMagick Studio LLC - Implement GetInstallationDirectories for ImageMagick Q8 (x64)
- [ImageMagick Q8] ImageMagick Studio LLC - Implement GetComponents for ImageMagick Q8 (x64)
- [ImageMagick Q8] ImageMagick Studio LLC - Implement GetUninstallString for ImageMagick Q8 (x64)
- [ImageMagick Q8] ImageMagick Studio LLC - Implement IsAuthentic for ImageMagick Q8 (x64)
- [ImageMagick Q8] ImageMagick Studio LLC - Implement GetRunningState for ImageMagick Q8 (x64)
- [ImageMagick Q8] ImageMagick Studio LLC - Implement TerminateProcesses for ImageMagick Q8 (x64)
- [ImageMagick Q16] ImageMagick Studio LLC - Implement GetRunningState for ImageMagick Q16 (x64)
- [ImageMagick Q16] ImageMagick Studio LLC - Implement TerminateProcesses for ImageMagick Q16 (x64)
- [ImageMagick Q16] ImageMagick Studio LLC - Implement GetInstallationDirectories for ImageMagick Q16 (x64)
- [ImageMagick Q16] ImageMagick Studio LLC - Implement GetComponents for ImageMagick Q16 (x64)
- [ImageMagick Q16] ImageMagick Studio LLC - Implement GetUninstallString for ImageMagick Q16 (x64)
- [ImageMagick Q16] ImageMagick Studio LLC - Implement IsAuthentic for ImageMagick Q16 (x64)
- [Rapid7 Insight Agent] Rapid7 - Implement GetVersion for Rapid7 Insight Agent
- [Rapid7 Insight Agent] Rapid7 - Implement GetRunningState for Rapid7 Insight Agent
- [Rapid7 Insight Agent] Rapid7 - Implement Run for Rapid7 Insight Agent
- [Rapid7 Insight Agent] Rapid7 - Implement TerminateProcesses for Rapid7 Insight Agent
- [Rapid7 Insight Agent] Rapid7 - Implement GetRealTimeProtectionState for Rapid7 Insight Agent
- [Rapid7 Insight Agent] Rapid7 - Implement GetDefinitionState for Rapid7 Insight Agent
- [iTools] ThinkSky Technology Co., Ltd - Implement GetUninstallHive for iTools
- [iTools] ThinkSky Technology Co., Ltd - Implement Run for iTools
- [Microsoft OneDrive] Microsoft Corporation - Update GetInstallationDirectories implementation for Microsoft OneDrive
- [Amazon Corretto] Amazon.com - Update TerminateProcesses implementation for Amazon Corretto 15 (x64)
- [Amazon Corretto] Amazon.com - Update GetVersion implementation for Amazon Corretto 15 (x64)
- [Amazon Corretto] Amazon.com - Update GetRunningState implementation for Amazon Corretto 15 (x64)
- [G Data Security Client] G Data Software AG - Update GetDefinitionState implementation for G Data Security Client
- [G Data Security Client] G Data Software AG - Implement GetUninstallHive for G Data Security Client
- [Malwarebytes Anti-Malware] Malwarebytes Corporation - Update GetLastScanTime implementation for Malwarebytes Anti-Malware
- [Trend Micro Deep Security Agent] Trend Micro, Inc. - Implement UpdateDefinitions for Trend Micro Deep Security Agent
- [CrowdStrike Falcon] CrowdStrike, Inc. - Update GetRealTimeProtectionState implementation for CrowdStrike Falcon
- [CrowdStrike Falcon] CrowdStrike, Inc. - Update GetDefinitionState implementation for CrowdStrike Falcon
- [Webex] Cisco Systems, Inc - Update GetUninstallString implementation for Webex (x64)
- [ArcGIS Pro] Environmental Systems Research Institute, Inc. - Implement TerminateProcesses for ArcGIS Pro
- [ArcGIS Pro] Environmental Systems Research Institute, Inc. - Implement Run for ArcGIS Pro
- [Cortex XDR] Palo Alto Networks, Inc. - Implement GetAgentState for Cortex XDR
- [Google Chrome] Google Inc. - Update GetInstallationDirectories implementation for Google Chrome
- [Webex] Cisco Systems, Inc - Implement IsAuthentic for Webex (x64)
- [Webex] Cisco Systems, Inc - Update GetUninstallString implementation for Webex (x64)
- [Webex] Cisco Systems, Inc - Update GetInstallationDirectories implementation for Webex (x64)

#### [Linux](/docs/mdsdk/release-notes/december-23-2025#linux)

- [Cortex] Palo Alto Networks, Inc. - Implement GetAgentState for Cortex

#### [Mac](/docs/mdsdk/release-notes/december-23-2025#mac)

- [Microsoft Teams] Microsoft Corporation - Implement GetVersion for Microsoft Teams (work or school)
- [Cybereason ActiveProbe] Cybereason - Update GetDefinitionState implementation for Cybereason ActiveProbe
- [Cybereason ActiveProbe] Cybereason - Update GetRealTimeProtectionState implementation for Cybereason ActiveProbe
- [Visual Studio Code] Microsoft Corporation - Implement Run for Visual Studio Code
