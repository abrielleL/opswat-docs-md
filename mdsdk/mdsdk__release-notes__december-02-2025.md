<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/december-02-2025 -->

# December 02nd, 2025

## [Release Note](/docs/mdsdk/release-notes/december-02-2025#release-note)

### [Release Date](/docs/mdsdk/release-notes/december-02-2025#release-date)

- 02/12/2025

### [SDK Version](/docs/mdsdk/release-notes/december-02-2025#sdk-version)

- **Windows**: 4.3.5302.0
- **Linux**: 4.3.4361.0
- **Mac**: 4.3.4761.0

### [Enhancement](/docs/mdsdk/release-notes/december-02-2025#enhancement)

#### [Windows](/docs/mdsdk/release-notes/december-02-2025#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/december-02-2025#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/december-02-2025#mac)

- N/A

### [Bug Fix](/docs/mdsdk/release-notes/december-02-2025#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/december-02-2025#windows)

- Fixed compliance being incorrectly passed when the Elastic Agent service was disabled by updating GetRealtimeProtectionState to require both Elastic Agent and Elastic Defend services running with internet connectivity, ensuring accurate protection status and compliance reporting for users.
- Fixed the inability to uninstall CrowdStrike Falcon when a maintenance token is required by adding support for token input and returning a clear error if the product is upgrading, enabling seamless and reliable uninstallation for users.
- Fixed the removal of KeePass desktop and Start-menu shortcuts after upgrading to version 2.60 by updating patching scripts to support all available fix versions, ensuring shortcuts remain accessible for a smoother user experience.
- Fixed incorrect version reporting for Elasticsearch by implementing the GetVersion method, enabling accurate version detection to improve vulnerability assessment and compliance for users.

#### [Linux](/docs/mdsdk/release-notes/december-02-2025#linux)

- Fixed memory leaks at process exit in libwavmodapi by adding a virtual destructor to the base class and ensuring singleton objects are properly destroyed, significantly reducing resource leaks and improving stability for Linux, Mac, and Windows users.
- Fixed incorrect version reporting for Elasticsearch by implementing the GetVersion method, enabling accurate version detection to improve vulnerability assessment and compliance for users.

#### [Mac](/docs/mdsdk/release-notes/december-02-2025#mac)

- N/A

### [New Application Support](/docs/mdsdk/release-notes/december-02-2025#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/december-02-2025#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/december-02-2025#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/december-02-2025#mac)

- N/A

### [New Application Version Support](/docs/mdsdk/release-notes/december-02-2025#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/december-02-2025#windows)

- V4 | Windows | Add support for Microsoft Edge 80+ version 142.0.3595.94
- V4 | Windows | Add support for Google Chrome version 142.0.7444.176
- V4 | Windows | Add support for Avast One Essential version 25.11.10580.419
- V4 | Windows | Add support for ESET Smart Security version 19.0.11.0
- V4 | Windows | Add support for Cortex XDR version 9.0.0.16757

#### [Linux](/docs/mdsdk/release-notes/december-02-2025#linux)

- V4 | Linux | Add support for FileZilla version 3.69.5
- V4 | Linux | Add support for Kaspersky Endpoint Security for Linux version 12.1.0.1297
- V4 | Linux | Add support for Signal version 7.80.1
- V4 | Linux | Add support for Visual Studio Code version 1.106.3
- V4 | Linux | Add support for MySQL Workbench version 8.0.45

#### [Mac](/docs/mdsdk/release-notes/december-02-2025#mac)

- N/A

### [New Method Implementation](/docs/mdsdk/release-notes/december-02-2025#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/december-02-2025#windows)

- [Comet] The Comet Authors - Implement IsDefaultBrowser for Comet
- [Comet] The Comet Authors - Implement GetPlugins for Comet
- [Comet] The Comet Authors - Implement GetAntiphishingState for Comet
- [Comet] The Comet Authors - Implement GetVersion for Comet
- [Elastic Agent] Elasticsearch B.V. - Update GetRealTimeProtectionState implementation for Elastic Agent
- [ESET Smart Security] ESET - Update SetFirewallState implementation for ESET Smart Security
- [ESET Smart Security] ESET - Update EnableRTP implementation for ESET Smart Security
- [Microsoft SQL Server Express] Microsoft Corporation - Update Run implementation for Microsoft SQL Server Express 2022
- [Elasticsearch] Elasticsearch B.V. - Implement GetVersion for Elasticsearch
- [Cortex XDR] Palo Alto Networks, Inc. - Update GetFirewallState implementation for Cortex XDR
- [Cortex XDR] Palo Alto Networks, Inc. - Update GetLastScanTime implementation for Cortex XDR
- [Cortex XDR] Palo Alto Networks, Inc. - Update GetDefinitionState implementation for Cortex XDR

#### [Linux](/docs/mdsdk/release-notes/december-02-2025#linux)

- [Kaspersky Endpoint Security for Linux] Kaspersky Lab - Update GetScanState implementation for Kaspersky Endpoint Security for Linux
- [Kaspersky Endpoint Security for Linux] Kaspersky Lab - Implement GetRunningState for Kaspersky Endpoint Security for Linux
- [Kaspersky Endpoint Security for Linux] Kaspersky Lab - Update Run implementation for Kaspersky Endpoint Security for Linux

#### [Mac](/docs/mdsdk/release-notes/december-02-2025#mac)

- [Sentinel Agent] SentinelOne - Implement GetLastScanTime for Sentinel Agent
- [Software Update] Apple Inc. - Update InstallMissingPatches implementation for Software Update
