<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/february-10-2026 -->

# February 10th, 2026

## [Release Note](/docs/mdsdk/release-notes/february-10-2026#release-note)

### [Release Date](/docs/mdsdk/release-notes/february-10-2026#release-date)

- 10/02/2026

### [SDK Version](/docs/mdsdk/release-notes/february-10-2026#sdk-version)

- **Windows**: 4.3.5626.0
- **Linux**: 4.3.4667.0
- **Mac**: 4.3.5067.0

### [Enhancement](/docs/mdsdk/release-notes/february-10-2026#enhancement)

#### [Windows](/docs/mdsdk/release-notes/february-10-2026#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/february-10-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/february-10-2026#mac)

- N/A

### [Bug Fix](/docs/mdsdk/release-notes/february-10-2026#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/february-10-2026#windows)

- Fixed incorrect Spybot version detection by re-implementing the GetVersion method to ensure the latest installed version is accurately reported, improving reliability for users and integrators.
- Fixed failed Webex (User) (x64) patching—where updates didn’t apply if no active user session existed—by updating the patch logic to correctly return an error or upgrade when appropriate, ensuring reliable and accurate Webex updates for all users.
- Fixed incorrect "installation failed" errors when patching Office without internet by updating the installation script to return a clear "no connection" message, so users now receive accurate feedback and can troubleshoot connectivity issues more easily.

#### [Linux](/docs/mdsdk/release-notes/february-10-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/february-10-2026#mac)

- N/A

### [New Application Support](/docs/mdsdk/release-notes/february-10-2026#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/february-10-2026#windows)

- V4 | Windows | Add Support for Ninjaone software under category Patch Management
- V4 | Windows | Add support for iTunes (UWP)
- Windows | Add support detection for Yubico Authenticator
- V4 | Windows | Add support for AIMP2 Audio Recorder

#### [Linux](/docs/mdsdk/release-notes/february-10-2026#linux)

- V4 | Windows | Add Support for Ninjaone software under category Patch Management

#### [Mac](/docs/mdsdk/release-notes/february-10-2026#mac)

- N/A

### [New Application Version Support](/docs/mdsdk/release-notes/february-10-2026#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/february-10-2026#windows)

- V4 | Windows | Add support for Microsoft Office 365 version 16.0.19628.20166
- V4 | Windows | Add support for Bitdefender Endpoint Security Tools version 8.26.2.607
- V4 | Windows | Add support for Microsoft Office 2021 version 16.0.19628.20166
- V4 | Windows | Add support for Microsoft Edge version 144.0.3719.82
- V4 | Windows | Add support for Microsoft OneDrive version 26.012.0119.0002
- V4 | Windows | Add support for Sophos Endpoint Agent version 2025.2.3.8.0
- V4 | Windows | Add support for Dropbox 3+ version 241.4.4795
- V4 | Windows | Add support for Microsoft OneDrive version 26.007.0112.0002
- V4 | Windows | Add support for Dropbox 3+ version 240.4.8609
- V4 | Windows | Add support for Mozilla Firefox (x86) version 147.0.3

#### [Linux](/docs/mdsdk/release-notes/february-10-2026#linux)

- V4 | Linux | Add support for Signal version 7.87.0
- V4 | Linux | Add support for Mozilla Firefox version 147.0.2
- V4 | Linux | Add support for LibreOffice version 26.2.0
- V4 | Linux | Add support for Signal version 7.88.0
- V4 | Linux | Add support for Debian 13.3

#### [Mac](/docs/mdsdk/release-notes/february-10-2026#mac)

- N/A

### [New Method Implementation](/docs/mdsdk/release-notes/february-10-2026#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/february-10-2026#windows)

- [Microsoft Intune Management Extension] Microsoft Corporation - Implement GetAgentState for Microsoft Intune Management Extension
- [NinjaRMMAgent] NinjaRMM LLC - Implement GetComponents for NinjaRMMAgent
- [NinjaRMMAgent] NinjaRMM LLC - Implement Run for NinjaRMMAgent
- [NinjaRMMAgent] NinjaRMM LLC - Implement TerminateProcesses for NinjaRMMAgent
- [Spybot - Search & Destroy] Safer-Networking Ltd. - Implement GetVersion for Spybot - Search & Destroy
- [Yubico Authenticator] Yubico AB - Implement Run for Yubico Authenticator
- [1Password] AgileBits - Implement TerminateProcesses for 1Password msix
- [1Password] AgileBits - Implement Run for 1Password msix
- [Sophos Endpoint Agent] Sophos Limited - Implement Run for Sophos Endpoint Agent
- [Amazon Corretto] Amazon.com - Update GetRunningState implementation for Amazon Corretto 8 (x64)
- [Amazon Corretto] Amazon.com - Update GetRunningState implementation for Amazon Corretto JRE 8 (x64)
- [Amazon Corretto] Amazon.com - Update GetRunningState implementation for Amazon Corretto JRE 8 (x86)
- [Amazon Corretto] Amazon.com - Update GetRunningState implementation for Amazon Corretto 8 (x86)
- [Yubico Authenticator] Yubico AB - Implement GetUninstallString for Yubico Authenticator (UWP)
- [Yubico Authenticator] Yubico AB - Implement Run for Yubico Authenticator (UWP)
- [Yubico Authenticator] Yubico AB - Implement GetUninstallHive for Yubico Authenticator (UWP)
- [Kaspersky Standard] Kaspersky Lab - Update GetRunningState implementation for Kaspersky Standard
- [Yubico Authenticator] Yubico AB - Implement GetVersion for Yubico Authenticator (UWP)
- [iTunes] Apple Inc. - Implement GetUninstallString for iTunes (UWP)
- [iTunes] Apple Inc. - Implement Run for iTunes (UWP)
- [iTunes] Apple Inc. - Implement GetInstallationDirectories for iTunes (UWP)
- [Actipace Total Security] Actipace Private Limited - Update GetRealTimeProtectionState implementation for Actipace Total Security
- [GridinSoft Anti-Malware] GridinSoft LLC. - Implement Run for GridinSoft Anti-Malware
- [GridinSoft Anti-Malware] GridinSoft LLC. - Update GetRealTimeProtectionState implementation for GridinSoft Anti-Malware
- [GridinSoft Anti-Malware] GridinSoft LLC. - Update GetDefinitionState implementation for GridinSoft Anti-Malware

#### [Linux](/docs/mdsdk/release-notes/february-10-2026#linux)

- [Mozilla Firefox] Mozilla Corporation - Update GetAntiphishingState implementation for Mozilla Firefox
- [Microsoft Defender ATP] Microsoft Corporation - Implement GetAgentState for Microsoft Defender ATP
- [Signal] Signal Messenger, LLC - Update GetVersion implementation for Signal

#### [Mac](/docs/mdsdk/release-notes/february-10-2026#mac)

- [Software Update] Apple Inc. - Update InstallMissingPatches implementation for Software Update
- [Microsoft Defender ATP] Microsoft Corporation - Implement GetAgentState for Microsoft Defender ATP
