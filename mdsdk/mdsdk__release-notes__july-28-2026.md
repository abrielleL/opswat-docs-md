<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/july-28-2026 -->

# July 28th, 2026

## [Release Note](/docs/mdsdk/release-notes/july-28-2026#release-note)

### [Release Date](/docs/mdsdk/release-notes/july-28-2026#release-date)

- 28/07/2026

### [SDK Version](/docs/mdsdk/release-notes/july-28-2026#sdk-version)

- **Windows**: 4.3.6404.0
- **Linux**: 4.3.5382.0
- **Mac**: 4.3.5762.0

### [Enhancement](/docs/mdsdk/release-notes/july-28-2026#enhancement)

#### [Windows](/docs/mdsdk/release-notes/july-28-2026#windows)

- [Windows] Regulatory Compliance — Phase 1 (Generic Mode + PCI-DSS 4.0.1)
- Add error_message field to error response

#### [Linux](/docs/mdsdk/release-notes/july-28-2026#linux)

- Add error_message field to error response

#### [Mac](/docs/mdsdk/release-notes/july-28-2026#mac)

- Expose the require_full_disk_access attribute in the SDK server side
- [macOS] Regulatory Compliance — Phase 1 (Generic Mode + PCI-DSS 4.0.1)
- Add error_message field to error response

### [Bug Fix](/docs/mdsdk/release-notes/july-28-2026#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/july-28-2026#windows)

- Fixed a thread handle leak in the internet connectivity check used by {{GetRealTimeProtectionState}}, {{GetDefinitionState}}, and other APIs.
- Resolved OneDrive reporting unreleased Insider versions as available updates by defaulting the update ring to Production when no explicit configuration is found, ensuring users on the production channel only receive stable, released updates.

#### [Linux](/docs/mdsdk/release-notes/july-28-2026#linux)

- Fixed inconsistent JSON types in the `GetLatestInstaller` response by normalizing the `dependencies` field to always return an empty object instead of an array when no dependencies exist, improving compatibility for strict JSON parsers.
- Resolved the issue where `GetVersion` incorrectly reported older LibreOffice versions on Linux when multiple major versions coexisted via an updated detection logic that compares all installed binary paths, ensuring the SDK accurately identifies the latest version for improved compliance reporting.
- Resolved false-positive success reports during Linux patch installations by implementing a pre-flight health probe that detects broken package manager states, improving error reporting accuracy and preventing failed updates from being incorrectly flagged as successful.
- Resolved the issue where Linux patch installations incorrectly returned a generic invalid input error when a package was on hold via apt-mark by implementing specific error code mapping for held packages and other common failure scenarios, improving the accuracy of diagnostic feedback for users.

#### [Mac](/docs/mdsdk/release-notes/july-28-2026#mac)

- N/A

### [New Application Support](/docs/mdsdk/release-notes/july-28-2026#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/july-28-2026#windows)

- Windows | Cortex XDR GetFirewallState (method 1007) unreliable on 9.1.x+ as Cytool no longer a supported/reliable status source
- Add Support patching for NAPS2 (Not Another PDF Scanner 2)
- Add Support patching for KIR Szafir e-Signature Software
- Add Support patching for D.Suite/eIDAS
- AppRemoval| Add removal support for Trend Vision One Endpoint Security

#### [Linux](/docs/mdsdk/release-notes/july-28-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/july-28-2026#mac)

- Mac | Add FIREWALL category support for Cortex XDR on macOS (Signature 100379).
- [W:4] macOS | Add support detection for Luma Dream Machine
- [W:5] macOS | Add support detection for PhotoRoom
- [W:4] macOS | Add support detection for Ideogram
- [W:4] macOS | Add support detection for aider
- [W:4] macOS | Add support detection for Image Playground
- [W:5] macOS | Add support detection for Writing Tools
- [W:4] macOS | Add support detection for HuggingChat
- macOS | Add support detection for Microsoft Remote Desktop (currently named Windows App)

### [New Application Version Support](/docs/mdsdk/release-notes/july-28-2026#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/july-28-2026#windows)

- Windows | Cortex XDR GetFirewallState (method 1007) unreliable on 9.1.x+ as Cytool no longer a supported/reliable status source
- AppRemoval| Add removal support for Trend Vision One Endpoint Security
- V4 | Windows | Add support for Microsoft Teams (work or school) version 26163.405.4842.717
- V4 | Windows | Add support for Mozilla Firefox (arm64) version 152.0.6

#### [Linux](/docs/mdsdk/release-notes/july-28-2026#linux)

- V4 | Linux | Add support for Thunderbird version 153.0
- V4 | Linux | Add support for Signal version 8.20.0
- V4 | Linux | Add support for Visual Studio Code version 1.130.0
- V4 | Linux | Add support for LibreOffice version 26.2.5
- V4 | Linux | Add support for Visual Studio Code version 1.129.0
- V4 | Linux | Add support for Signal version 8.19.0
- V4 | Linux | Add support for Zoom version 7.1.5
- V4 | Linux | Add support for Mozilla Firefox version 153.0

#### [Mac](/docs/mdsdk/release-notes/july-28-2026#mac)

- Mac | Add FIREWALL category support for Cortex XDR on macOS (Signature 100379).
- [W:4] macOS | Add support detection for Luma Dream Machine
- [W:5] macOS | Add support detection for PhotoRoom
- [W:4] macOS | Add support detection for Ideogram
- [W:4] macOS | Add support detection for aider
- [W:4] macOS | Add support detection for Image Playground
- [W:5] macOS | Add support detection for Writing Tools
- [W:4] macOS | Add support detection for HuggingChat
- V4 | Mac | Add support for LibreOffice version 26.2.4
- V4 | Mac | Add support for OneDrive version 26.119.0622.0003
- V4 | Mac | Add support for VNC Server version 7.17.0
- V4 | Mac | Add support for Firefox version 153.0
- V4 | Mac | Add support for Webex version 46.7.0.35472
- V4 | Mac | Add support for Microsoft Teams (work or school) version 26183.1901.4874.5228

### [New Method Implementation](/docs/mdsdk/release-notes/july-28-2026#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/july-28-2026#windows)

- [HWMonitor] CPUID - Implement GetVersion for HWMonitor
- [Cortex XDR] Palo Alto Networks, Inc. - Update GetFirewallState implementation for Cortex XDR
- [FlashPeak SlimBrowser] FlashPeak Inc. - Implement GetVersion for SlimBrowser
- [FlashPeak SlimBrowser] FlashPeak Inc. - Implement TerminateProcesses for SlimBrowser
- [FlashPeak SlimBrowser] FlashPeak Inc. - Implement GetRunningState for SlimBrowser
- [FlashPeak SlimBrowser] FlashPeak Inc. - Implement Run for SlimBrowser
- [FlashPeak SlimBrowser] FlashPeak Inc. - Implement GetInstallationDirectories for SlimBrowser
- [Microsoft OneDrive] Microsoft Corporation - Update GetVersion implementation for Microsoft OneDrive
- [Microsoft OneDrive] Microsoft Corporation - Update GetVersion implementation for Microsoft OneDrive (User)

#### [Linux](/docs/mdsdk/release-notes/july-28-2026#linux)

- [LibreOffice] The Document Foundation - Update GetVersion implementation for LibreOffice

#### [Mac](/docs/mdsdk/release-notes/july-28-2026#mac)

- [Cortex XDR] Palo Alto Networks, Inc. - Implement GetFirewallState for Cortex XDR
- [Photoroom] Photoroom, Inc. - Implement GetInstallationDirectories for Photoroom
- [Photoroom] Photoroom, Inc. - Implement TerminateProcesses for Photoroom
- [Photoroom] Photoroom, Inc. - Implement Run for Photoroom
- [Photoroom] Photoroom, Inc. - Implement GetRunningState for Photoroom
- [Photoroom] Photoroom, Inc. - Implement GetVersion for Photoroom
- [Ideogram] Ideogram, Inc. - Implement Run for Ideogram
- [Ideogram] Ideogram, Inc. - Implement GetInstallationDirectories for Ideogram
- [Ideogram] Ideogram, Inc. - Implement TerminateProcesses for Ideogram
- [Ideogram] Ideogram, Inc. - Implement GetRunningState for Ideogram
- [Ideogram] Ideogram, Inc. - Implement GetVersion for Ideogram
- [Aider] Aider AI LLC - Implement GetVersion for Aider
- [Aider] Aider AI LLC - Implement GetInstallationDirectories for Aider
- [Endpoint Security Agent] Broadcom - Implement GetRunningState for Endpoint Security Agent
- [Endpoint Security Agent] Broadcom - Implement GetRealTimeProtectionState for Endpoint Security Agent
- [Endpoint Security Agent] Broadcom - Implement GetFirewallState for Endpoint Security Agent
- [Endpoint Security Agent] Broadcom - Implement GetDefinitionState for Endpoint Security Agent
- [Endpoint Security Agent] Broadcom - Implement UpdateDefinitions for Endpoint Security Agent
- [Endpoint Security Agent] Broadcom - Implement GetLastScanTime for Endpoint Security Agent
- [Endpoint Security Agent] Broadcom - Implement IsAuthentic for Endpoint Security Agent
