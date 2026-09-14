<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/april-21-2026 -->

# April 21st, 2026

## [Release Note](/docs/mdsdk/release-notes/april-21-2026#release-note)

### [Release Date](/docs/mdsdk/release-notes/april-21-2026#release-date)

- 21/04/2026

### [SDK Version](/docs/mdsdk/release-notes/april-21-2026#sdk-version)

- **Windows**: 4.3.5939.0
- **Linux**: 4.3.4973.0
- **Mac**: 4.3.5341.0

### [Enhancement](/docs/mdsdk/release-notes/april-21-2026#enhancement)

#### [Windows](/docs/mdsdk/release-notes/april-21-2026#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/april-21-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/april-21-2026#mac)

- N/A

### [Bug Fix](/docs/mdsdk/release-notes/april-21-2026#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/april-21-2026#windows)

- Fixed an issue where method GetRealTimeProtectionState of Microsoft Defender ATP incorrectly returned a false status.
- Fixed inconsistent Windows Firewall version reporting in 32-bit processes by updating the GetVersion script to access FirewallAPI.dll via \Sysnative, ensuring reliable and consistent version results for smoother remediation workflows.

#### [Linux](/docs/mdsdk/release-notes/april-21-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/april-21-2026#mac)

- N/A

### [New Application Support](/docs/mdsdk/release-notes/april-21-2026#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/april-21-2026#windows)

- V4 | Mac | Add support for Cato Client

#### [Linux](/docs/mdsdk/release-notes/april-21-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/april-21-2026#mac)

- N/A

### [New Application Version Support](/docs/mdsdk/release-notes/april-21-2026#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/april-21-2026#windows)

- V4 | Windows | Add support for Google Chrome version 147.0.7727.102

#### [Linux](/docs/mdsdk/release-notes/april-21-2026#linux)

- V4 | Linux | Add support for GIMP version 3.2.2
- V4 | Linux | Add support for Zoom version 6.7.5
- V4 | Linux | Add support for Google Chrome version 147.0.7727.101
- V4 | Linux | Add support for Visual Studio Code version 1.109.0
- V4 | Linux | Add support for LibreOffice version 26.2.2

#### [Mac](/docs/mdsdk/release-notes/april-21-2026#mac)

- N/A

### [New Method Implementation](/docs/mdsdk/release-notes/april-21-2026#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/april-21-2026#windows)

- [Stormshield SSL VPN Client] Stormshield - Implement TerminateProcesses for Stormshield SSL VPN Client
- [Avira Security] Avira Operations GmbH & Co. KG - Implement GetAntiphishingState for Avira Security
- [Avira Security] Avira Operations GmbH & Co. KG - Update GetLastScanTime implementation for Avira Security
- [Avira Security] Avira Operations GmbH & Co. KG - Update GetFirewallState implementation for Avira Security
- [Stormshield SSL VPN Client] Stormshield - Implement GetRunningState for Stormshield SSL VPN Client
- [BitLocker Drive Encryption] Microsoft Corporation - Update GetRunningState implementation for BitLocker Drive Encryption
- [OpenSSL] OpenSSL Software Foundation Inc - Implement GetComponents for OpenSSL Light msi (x64)
- [OpenSSL] OpenSSL Software Foundation Inc - Implement IsAuthentic for OpenSSL Light msi (x64)
- [OpenSSL] OpenSSL Software Foundation Inc - Implement GetInstallationDirectories for OpenSSL Light msi (x64)
- [OpenSSL] OpenSSL Software Foundation Inc - Implement GetInstallationDirectories for OpenSSL msi (x64)
- [OpenSSL] OpenSSL Software Foundation Inc - Implement GetComponents for OpenSSL msi (x64)
- [OpenSSL] OpenSSL Software Foundation Inc - Implement IsAuthentic for OpenSSL msi (x64)
- [Python 3.14] Python Software Foundation - Implement Run for Python 3.14 Arm64
- [Python 3.14] Python Software Foundation - Implement TerminateProcesses for Python 3.14 Arm64
- [Python 3.14] Python Software Foundation - Implement GetRunningState for Python 3.14 Arm64
- [Python 3.14] Python Software Foundation - Implement GetUninstallHive for Python 3.14 Arm64
- [Python 3.14] Python Software Foundation - Implement GetUninstallString for Python 3.14 Arm64
- [Python 3.14] Python Software Foundation - Implement GetInstallationDirectories for Python 3.14 Arm64
- [TikTok] Bytedance Pte. Ltd. - Implement GetUninstallString for TikTok
- [TikTok] Bytedance Pte. Ltd. - Implement GetUninstallHive for TikTok
- [Sophos Connect] Sophos Limited - Update Run implementation for Sophos Connect
- [Microsoft Defender ATP] Microsoft Corporation - Update GetRealTimeProtectionState implementation for Microsoft Defender ATP
- [Windows Firewall] Microsoft Corporation - Update GetVersion implementation for Windows Firewall
- [Microsoft OneNote] Microsoft Corporation - Implement GetVersion for OneNote for Windows 10 (UWP)
- [Microsoft OneNote] Microsoft Corporation - Implement Run for OneNote for Windows 10 (UWP)
- [Microsoft OneNote] Microsoft Corporation - Implement GetUninstallString for OneNote for Windows 10 (UWP)
- [Python 3.14] Python Software Foundation - Implement GetInstallationDirectories for Python 3.14 32-bit
- [Python 3.14] Python Software Foundation - Implement GetUninstallString for Python 3.14 32-bit
- [Python 3.14] Python Software Foundation - Implement GetUninstallHive for Python 3.14 32-bit

#### [Linux](/docs/mdsdk/release-notes/april-21-2026#linux)

- [Dandified Yum] Red Hat, Inc. - Update GetMissingPatches implementation for Dandified Yum
- [Google Chrome] Google Inc. - Update GetAntiphishingState implementation for Google Chrome

#### [Mac](/docs/mdsdk/release-notes/april-21-2026#mac)

- [SnapAgent] Blackpoint Cyber - Implement GetInstallationDirectories for SnapAgent
- [SnapAgent] Blackpoint Cyber - Implement TerminateProcesses for SnapAgent
- [SnapAgent] Blackpoint Cyber - Implement GetVersion for SnapAgent
- [SnapAgent] Blackpoint Cyber - Implement Run for SnapAgent
- [SnapAgent] Blackpoint Cyber - Implement GetRunningState for SnapAgent
- [Visual Studio Code] Microsoft Corporation - Update GetRunningState implementation for Visual Studio Code
