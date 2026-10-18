<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/october-02-2026 -->

# October 2nd, 2026

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## Release Note

### Release Date

- 02/10/2026

### SDK Version

- **Windows**: 4.3.6685.0
- **Linux**: 4.3.5684.0
- **Mac**: 4.3.6077.0

### Enhancement

#### Windows

- N/A

#### Linux

- N/A

#### Mac

- N/A

### Bug Fix

#### Windows

- Resolved the issue where the SDK automatically re-created deleted debug-log folders with restricted permissions via a fix that ensures the folder is only created when a log file is actively opened, improving the reliability of application uninstallation and preventing unexpected folder permission changes.

#### Linux

- Resolved the issue where the SDK automatically re-created deleted debug-log folders with restricted permissions via a fix that ensures the folder is only created when a log file is actively opened, improving the reliability of application uninstallation and preventing unexpected folder permission changes.

#### Mac

- Resolved the issue where the SDK automatically re-created deleted debug-log folders with restricted permissions via a fix that ensures the folder is only created when a log file is actively opened, improving the reliability of application uninstallation and preventing unexpected folder permission changes.

### New Application Support

#### Windows

- V4 | Windows | Add support for Carbon Black Cloud Sensor version 4.2.0.3361
- Add support detection and patching OneSEC ThreatBook Agent on Windows

#### Linux

- N/A

#### Mac

- macOS | Add support auto-patching for Firefox Beta
- Add support detection and patching OneSEC ThreatBook Agent on macOS

### New Application Version Support

#### Windows

- V4 | Windows | Add support for ESET NOD32 Antivirus version 19.2.7.0
- V4 | Windows | Add support for ESET Internet Security version 19.2.10.0
- V4 | Windows | Add support for Carbon Black Cloud Sensor version 4.2.0.3361
- Add support detection and patching OneSEC ThreatBook Agent on Windows
- V4 | Windows | Add support for Microsoft Visual Studio Code (User) (Arm64) version 1.140.0
- V4 | Windows | Add support for Microsoft Visual Studio Code (Arm64) version 1.140.0
- V4 | Windows | Add support for Microsoft Visual Studio Code version 1.140.0
- V4 | Windows | Add support for Acronis Cyber Protection Agent version 26.9.43144

#### Linux

- V4 | Linux | Add support for Mozilla Firefox version 157.0
- V4 | Linux | Add support for Visual Studio Code version 1.140.0
- V4 | Linux | Add support for Thunderbird version 157.0

#### Mac

- V4 | Mac | Update version format for Malwarebytes 4+
- Add support detection and patching OneSEC ThreatBook Agent on macOS
- V4 | Mac | Add support for Check Point Endpoint Security version 89.40.7522
- V4 | Mac | Add support for Trend Micro Deep Security Agent version 20.0.0.271
- V4 | Mac | Add support for Check Point Endpoint Security version 89.30.7380
- V4 | Mac | Add support for Xprotect version 5362

### New Method Implementation

#### Windows

- [ESET Internet Security] ESET - Implement SetFirewallState for ESET Internet Security
- [Carbon Black Cloud Sensor] Broadcom - Implement GetInstallationDirectories for Carbon Black Cloud Sensor 4+
- [Carbon Black Cloud Sensor] Broadcom - Update GetDefinitionState implementation for Carbon Black Cloud Sensor 4+
- [Acronis Cyber Protection Agent] Acronis - Update GetRealTimeProtectionState implementation for Acronis Cyber Protection Agent

#### Linux

- [Mozilla Firefox] Mozilla Corporation - Update GetInstallationDirectories implementation for Mozilla Firefox
- [Mozilla Firefox] Mozilla Corporation - Update IsDefaultBrowser implementation for Mozilla Firefox
- [Thunderbird] Mozilla Corporation - Implement GetComponents for Thunderbird
- [Thunderbird] Mozilla Corporation - Update GetInstallationDirectories implementation for Thunderbird
- [Trellix EDRF] Musarubra US LLC. - Implement GetRunningState for Trellix EDRF
- [Trellix EDRF] Musarubra US LLC. - Implement GetVersion for Trellix EDRF
- [Trellix EDRF] Musarubra US LLC. - Implement GetDefinitionState for Trellix EDRF
- [Trellix EDRF] Musarubra US LLC. - Implement GetRealTimeProtectionState for Trellix EDRF
- [Trellix EDRF] Musarubra US LLC. - Implement GetVersion for Trellix EDRF

#### Mac

- [Firefox Developer Edition] Mozilla Corporation - Implement GetVersion for Firefox Developer Edition
- [Check Point Endpoint Security] Check Point Software Technologies - Update GetRealTimeProtectionState implementation for Check Point Endpoint Security
- [Check Point Endpoint Security] Check Point Software Technologies - Update GetRealTimeProtectionState implementation for Check Point Endpoint Security
- [Check Point Endpoint Security] Check Point Software Technologies - Update GetInstallationDirectories implementation for Check Point Endpoint Security
- [Sunbird] Cybereason - Implement GetRealTimeProtectionState for Sunbird
- [Sunbird] Cybereason - Implement GetDefinitionState for Sunbird
- [Sunbird] Cybereason - Implement IsAuthentic for Sunbird
