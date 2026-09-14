<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/august-04-2026 -->

# August 4th, 2026

## [Release Note](/docs/mdsdk/release-notes/august-04-2026#release-note)

### [Release Date](/docs/mdsdk/release-notes/august-04-2026#release-date)

- 04/08/2026

### [SDK Version](/docs/mdsdk/release-notes/august-04-2026#sdk-version)

- **Windows**: 4.3.6434.0
- **Linux**: 4.3.5437.0
- **Mac**: 4.3.5821.0

### [Enhancement](/docs/mdsdk/release-notes/august-04-2026#enhancement)

#### [Windows](/docs/mdsdk/release-notes/august-04-2026#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/august-04-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/august-04-2026#mac)

- N/A

### [Bug Fix](/docs/mdsdk/release-notes/august-04-2026#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/august-04-2026#windows)

- Fixed an issue where orphaned Windows user profiles could cause product scans to fail, ensuring complete detection results for all valid users.
- Fixed the .NET Runtime 6.0 installation failure caused by incorrect user impersonation prompts by updating the VAPM patch data to ensure silent, system-wide deployment, improving the reliability of unattended patching for standard users.

#### [Linux](/docs/mdsdk/release-notes/august-04-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/august-04-2026#mac)

- N/A

### [New Application Support](/docs/mdsdk/release-notes/august-04-2026#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/august-04-2026#windows)

- Add product support (detection + AV state) for McAfee+ consumer suite on Windows
- Add product support for Comet Browser v149.x (Windows)
- Add removal support for Sophos Endpoint Agent 2026
- Add product support for VMware Tools v13.x (Windows)

#### [Linux](/docs/mdsdk/release-notes/august-04-2026#linux)

- Linux | Add support for Cisco Secure Client - Endpoint DLP on Linux under the Data Loss Prevention category

#### [Mac](/docs/mdsdk/release-notes/august-04-2026#mac)

- V4 | Mac | Add support for Sophos Endpoint version 2026.1.0.439
- [W:4] macOS | Add support detection for remove.bg Desktop
- [W:4] macOS | Add support detection for Hugging Face
- [W:4] macOS | Add support detection for Circleback
- [W:4] macOS | Add support detection for Copilot (Finance)
- [W:4] macOS | Add support detection for Enchanted

### [New Application Version Support](/docs/mdsdk/release-notes/august-04-2026#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/august-04-2026#windows)

- V4 | Windows | Add support for Windows Update Agent version 1508.2606.17012.0
- V4 | Windows | Add support for Windows Update Agent version 1508.2606.17012.0
- Add product support (detection + AV state) for McAfee+ consumer suite on Windows
- Add product support for Comet Browser v149.x (Windows)
- Add removal support for Sophos Endpoint Agent 2026
- V4 | Windows | Add support for Microsoft Visual Studio Code (User) (Arm64) version 1.131.0
- V4 | Windows | Add support for Microsoft Visual Studio Code (Arm64) version 1.131.0
- V4 | Windows | Add support for Mozilla Firefox (arm64) version 153.0.1
- Add product support for VMware Tools v13.x (Windows)

#### [Linux](/docs/mdsdk/release-notes/august-04-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/august-04-2026#mac)

- V4 | Mac | Add support for Sophos Endpoint version 2026.1.0.439
- [W:4] macOS | Add support detection for remove.bg Desktop
- [W:4] macOS | Add support detection for Hugging Face
- [W:4] macOS | Add support detection for Circleback
- [W:4] macOS | Add support detection for Copilot (Finance)
- [W:4] macOS | Add support detection for Enchanted

### [New Method Implementation](/docs/mdsdk/release-notes/august-04-2026#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/august-04-2026#windows)

- [Red Hat OpenJDK] Red Hat, Inc. - Implement GetRunningState for Red Hat OpenJDK 8
- [Red Hat OpenJDK] Red Hat, Inc. - Implement TerminateProcesses for Red Hat OpenJDK 8
- [Zalo] VNG Corporation - Update GetVersion implementation for Zalo
- [Xerox Workplace Cloud Client] Xerox Corporation - Implement GetRunningState for Xerox Workplace Cloud Client
- [Xerox Workplace Cloud Client] Xerox Corporation - Implement TerminateProcesses for Xerox Workplace Cloud Client
- [CoolUtils Mail Viewer] CoolUtils - Implement GetVersion for CoolUtils Mail Viewer
- [Azul Zulu JRE 21] Azul Systems, Inc. - Implement GetVersion for Azul Zulu JRE 21 (x64)
- [eM Client] eM Client, Inc. - Implement GetVersion for eM Client
- [eM Client] eM Client, Inc. - Implement Run for eM Client
- [Microsoft Visual Studio Code] Microsoft Corporation - Implement IsAuthentic for Microsoft Visual Studio Code (User)
- [Azul Zulu JRE 11] Azul Systems, Inc. - Implement GetVersion for Azul Zulu JRE 11 (x64)
- [PDF-XChange] Tracker Software Products Ltd. - Update GetRunningState implementation for PDF-XChange Editor
- [PDF-XChange] Tracker Software Products Ltd. - Update TerminateProcesses implementation for PDF-XChange Editor

#### [Linux](/docs/mdsdk/release-notes/august-04-2026#linux)

- [Cisco Secure Client - Endpoint Data Loss Prevention] Cisco Systems, Inc. - Implement Run for Cisco Secure Client - Endpoint Data Loss Prevention

#### [Mac](/docs/mdsdk/release-notes/august-04-2026#mac)

- [HuggingFace CLI] HuggingFace Inc. - Implement GetVersion for HuggingFace CLI
- [HuggingFace CLI] HuggingFace Inc. - Implement GetInstallationDirectories for HuggingFace CLI
- [Circleback] Circleback AI, Inc. - Implement GetRunningState for Circleback
