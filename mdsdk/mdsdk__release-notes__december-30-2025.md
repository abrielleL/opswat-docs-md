<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/december-30-2025 -->

# December 30th, 2025

## [Release Note](/docs/mdsdk/release-notes/december-30-2025#release-note)

### [Release Date](/docs/mdsdk/release-notes/december-30-2025#release-date)

- 30/12/2025

### [SDK Version](/docs/mdsdk/release-notes/december-30-2025#sdk-version)

- **Windows**: 4.3.5434.0
- **Linux**: 4.3.4481.0
- **Mac**: 4.3.4881.0

### [Enhancement](/docs/mdsdk/release-notes/december-30-2025#enhancement)

#### [Windows](/docs/mdsdk/release-notes/december-30-2025#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/december-30-2025#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/december-30-2025#mac)

- N/A

### [Bug Fix](/docs/mdsdk/release-notes/december-30-2025#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/december-30-2025#windows)

- Fixed false positive CVE-2024-12797 detections in Python requests library files by removing incorrect hashes from the vulnerability database to ensure accurate scan results and prevent unnecessary security alerts for users.
- Fixed false detection of CVEs for the 'applypatch-msg.sample' file by removing its hash from the production database, ensuring users no longer experience incorrect vulnerability alerts.
- Fixed ESET product feeds not updating due to a changed vendor link by updating the feed retrieval URL, ensuring users always receive the latest antivirus definitions for improved protection and reliability.
- Fixed incorrect Windows Firewall version detection caused by Windows API redirection by updating the SDK to always retrieve version information correctly, ensuring accurate firewall version reporting for improved compliance and security validation.

#### [Linux](/docs/mdsdk/release-notes/december-30-2025#linux)

- Fixed false detection of CVEs for the 'applypatch-msg.sample' file by removing its hash from the production database, ensuring users no longer experience incorrect vulnerability alerts.

#### [Mac](/docs/mdsdk/release-notes/december-30-2025#mac)

- N/A

### [New Application Support](/docs/mdsdk/release-notes/december-30-2025#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/december-30-2025#windows)

- Windows | Add Support detection for ImageMagick version 7.1.x

#### [Linux](/docs/mdsdk/release-notes/december-30-2025#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/december-30-2025#mac)

- N/A

### [New Application Version Support](/docs/mdsdk/release-notes/december-30-2025#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/december-30-2025#windows)

- V4 | Windows | Add support for CrowdStrike Falcon version 7.31.20308.0
- V4 | Windows | Add support for Avast Premium Security version 25.11
- V4 | Windows | Add support for iTools version 4.5.1.9
- V4 | Windows | Add support for Sophos Endpoint Agent version 2025.2.1.709

#### [Linux](/docs/mdsdk/release-notes/december-30-2025#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/december-30-2025#mac)

- N/A

### [New Method Implementation](/docs/mdsdk/release-notes/december-30-2025#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/december-30-2025#windows)

- [Windows Firewall] Microsoft Corporation - Update GetVersion implementation for Windows Firewall
- [Trellix Endpoint Security (HX) Agent] FireEye, Inc. - Implement GetAgentState for Trellix Endpoint Security (HX) Agent
- [Workspace ONE Intelligent Hub] Omnissa, LLC - Implement GetVersion for Workspace ONE Intelligent Hub 25+
- [Workspace ONE Intelligent Hub] Omnissa, LLC - Implement Run for Workspace ONE Intelligent Hub 25+
- [Workspace ONE Intelligent Hub] Omnissa, LLC - Implement GetRunningState for Workspace ONE Intelligent Hub 25+
- [Avast Premium Security] AVAST Software a.s. - Update GetDefinitionState implementation for Avast Premium Security
- [Ollama] Ollama - Implement GetRunningState for Ollama
- [Ollama] Ollama - Implement TerminateProcesses for Ollama
- [Ollama] Ollama - Implement Run for Ollama
- [Ollama] Ollama - Implement GetUninstallHive for Ollama
- [Ollama] Ollama - Implement IsAuthentic for Ollama
- [Ollama] Ollama - Implement GetUninstallString for Ollama
- [Ollama] Ollama - Implement GetComponents for Ollama
- [Ollama] Ollama - Implement GetInstallationDirectories for Ollama
- [Stormshield SSL VPN Client] Stormshield - Update GetComponents implementation for Stormshield SSL VPN Client
- [Stormshield SSL VPN Client] Stormshield - Implement GetUninstallHive for Stormshield SSL VPN Client
- [Stormshield SSL VPN Client] Stormshield - Update GetInstallationDirectories implementation for Stormshield SSL VPN Client
- [Stormshield SSL VPN Client] Stormshield - Update Run implementation for Stormshield SSL VPN Client
- [Microsoft Defender ATP] Microsoft Corporation - Implement GetAgentState for Microsoft Defender ATP
- [Webex] Cisco Systems, Inc - Update Run implementation for Webex (x86)
- [Webex] Cisco Systems, Inc - Update GetInstallationDirectories implementation for Webex (x64)
- [Webex] Cisco Systems, Inc - Update IsAuthentic implementation for Webex (x64)
- [Webex] Cisco Systems, Inc - Update Run implementation for Webex (x64)
- [Webex] Cisco Systems, Inc - Update GetRunningState implementation for Webex (User) (x64)
- [Webex] Cisco Systems, Inc - Update Run implementation for Webex (User) (x64)
- [Webex] Cisco Systems, Inc - Update TerminateProcesses implementation for Webex (User) (x64)
- [Webex] Cisco Systems, Inc - Update GetRunningState implementation for Webex (User) (x86)
- [Webex] Cisco Systems, Inc - Update Run implementation for Webex (User) (x86)
- [Webex] Cisco Systems, Inc - Update TerminateProcesses implementation for Webex (User) (x86)
- [ImageMagick Q8] ImageMagick Studio LLC - Implement GetInstallationDirectories for ImageMagick Q8 (arm64)
- [ImageMagick Q8] ImageMagick Studio LLC - Implement GetComponents for ImageMagick Q8 (arm64)
- [ImageMagick Q8] ImageMagick Studio LLC - Implement GetUninstallString for ImageMagick Q8 (arm64)
- [ImageMagick Q8] ImageMagick Studio LLC - Implement IsAuthentic for ImageMagick Q8 (arm64)
- [ImageMagick Q8] ImageMagick Studio LLC - Implement GetRunningState for ImageMagick Q8 (arm64)
- [ImageMagick Q8] ImageMagick Studio LLC - Implement TerminateProcesses for ImageMagick Q8 (arm64)
- [ImageMagick Q16-HDRI] ImageMagick Studio LLC - Implement GetInstallationDirectories for ImageMagick Q16-HDRI (arm64)
- [ImageMagick Q16-HDRI] ImageMagick Studio LLC - Implement GetComponents for ImageMagick Q16-HDRI (arm64)
- [ImageMagick Q16-HDRI] ImageMagick Studio LLC - Implement GetUninstallString for ImageMagick Q16-HDRI (arm64)
- [ImageMagick Q16-HDRI] ImageMagick Studio LLC - Implement IsAuthentic for ImageMagick Q16-HDRI (arm64)
- [ImageMagick Q16-HDRI] ImageMagick Studio LLC - Implement GetRunningState for ImageMagick Q16-HDRI (arm64)
- [ImageMagick Q16-HDRI] ImageMagick Studio LLC - Implement TerminateProcesses for ImageMagick Q16-HDRI (arm64)
- [ImageMagick Q16] ImageMagick Studio LLC - Implement GetInstallationDirectories for ImageMagick Q16 (arm64)
- [ImageMagick Q16] ImageMagick Studio LLC - Implement GetComponents for ImageMagick Q16 (arm64)
- [ImageMagick Q16] ImageMagick Studio LLC - Implement GetUninstallString for ImageMagick Q16 (arm64)
- [ImageMagick Q16] ImageMagick Studio LLC - Implement IsAuthentic for ImageMagick Q16 (arm64)
- [ImageMagick Q16] ImageMagick Studio LLC - Implement GetRunningState for ImageMagick Q16 (arm64)
- [ImageMagick Q16] ImageMagick Studio LLC - Implement TerminateProcesses for ImageMagick Q16 (arm64)
- [Webex] Cisco Systems, Inc - Update GetVersion implementation for Webex (User) (x86)
- [Webex] Cisco Systems, Inc - Update GetUninstallString implementation for Webex (User) (x86)
- [Webex] Cisco Systems, Inc - Update GetInstallationDirectories implementation for Webex (User) (x86)
- [Webex] Cisco Systems, Inc - Update GetVersion implementation for Webex (User) (x64)
- [Webex] Cisco Systems, Inc - Update GetInstallationDirectories implementation for Webex (User) (x64)
- [Webex] Cisco Systems, Inc - Update GetUninstallString implementation for Webex (User) (x64)
- [ImageMagick Q8] ImageMagick Studio LLC - Implement GetInstallationDirectories for ImageMagick Q8 (x86)
- [ImageMagick Q8] ImageMagick Studio LLC - Implement GetComponents for ImageMagick Q8 (x86)
- [ImageMagick Q8] ImageMagick Studio LLC - Implement GetUninstallString for ImageMagick Q8 (x86)
- [ImageMagick Q8] ImageMagick Studio LLC - Implement IsAuthentic for ImageMagick Q8 (x86)
- [ImageMagick Q8] ImageMagick Studio LLC - Implement GetRunningState for ImageMagick Q8 (x86)
- [ImageMagick Q8] ImageMagick Studio LLC - Implement TerminateProcesses for ImageMagick Q8 (x86)
- [ImageMagick Q16-HDRI] ImageMagick Studio LLC - Implement GetInstallationDirectories for ImageMagick Q16-HDRI (x86)
- [ImageMagick Q16-HDRI] ImageMagick Studio LLC - Implement GetComponents for ImageMagick Q16-HDRI (x86)
- [ImageMagick Q16-HDRI] ImageMagick Studio LLC - Implement GetUninstallString for ImageMagick Q16-HDRI (x86)
- [ImageMagick Q16-HDRI] ImageMagick Studio LLC - Implement IsAuthentic for ImageMagick Q16-HDRI (x86)
- [ImageMagick Q16-HDRI] ImageMagick Studio LLC - Implement GetRunningState for ImageMagick Q16-HDRI (x86)
- [ImageMagick Q16-HDRI] ImageMagick Studio LLC - Implement TerminateProcesses for ImageMagick Q16-HDRI (x86)
- [ImageMagick Q16] ImageMagick Studio LLC - Implement GetComponents for ImageMagick Q16 (x86)
- [ImageMagick Q16] ImageMagick Studio LLC - Implement GetInstallationDirectories for ImageMagick Q16 (x86)
- [ImageMagick Q16] ImageMagick Studio LLC - Implement GetUninstallString for ImageMagick Q16 (x86)
- [ImageMagick Q16] ImageMagick Studio LLC - Implement IsAuthentic for ImageMagick Q16 (x86)
- [ImageMagick Q16] ImageMagick Studio LLC - Implement GetRunningState for ImageMagick Q16 (x86)
- [ImageMagick Q16] ImageMagick Studio LLC - Implement TerminateProcesses for ImageMagick Q16 (x86)
- [Workspace ONE Intelligent Hub] Omnissa, LLC - Implement Run for Workspace ONE Intelligent Hub 25+
- [Workspace ONE Intelligent Hub] Omnissa, LLC - Implement GetVersion for Workspace ONE Intelligent Hub 25+

#### [Linux](/docs/mdsdk/release-notes/december-30-2025#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/december-30-2025#mac)

- [Android Studio] Google Inc. - Implement GetVersion for Android Studio
- [Zalo] VNG Corporation - Implement GetInstallationDirectories for Zalo
- [Zalo] VNG Corporation - Implement Run for Zalo
