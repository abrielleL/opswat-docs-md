<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/september-15-2026 -->

# September 15th, 2026

## [Release Note](/docs/mdsdk/release-notes/september-15-2026#release-note)

### [Release Date](/docs/mdsdk/release-notes/september-15-2026#release-date)

- 15/09/2026

### [SDK Version](/docs/mdsdk/release-notes/september-15-2026#sdk-version)

- **Windows**: 4.3.6607.0
- **Linux**: 4.3.5608.0
- **Mac**: 4.3.5996.0

### [Enhancement](/docs/mdsdk/release-notes/september-15-2026#enhancement)

#### [Windows](/docs/mdsdk/release-notes/september-15-2026#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/september-15-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/september-15-2026#mac)

- N/A

### [Bug Fix](/docs/mdsdk/release-notes/september-15-2026#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/september-15-2026#windows)

- Resolved the issue where Microsoft Defender real-time protection was incorrectly reported as disabled by switching to Defender's own status class for version 4.18.26080.3, improving the accuracy of security compliance reporting.
- Resolved excessive blocking during product detection by optimizing the service-list refresh to use a non-blocking swap approach, significantly improving assessment speed on Windows endpoints with slow EDR service queries.
- Resolved a rare host application crash during SDK shutdown by ensuring the background debug-log check stops before its memory is released, improving overall system stability.

#### [Linux](/docs/mdsdk/release-notes/september-15-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/september-15-2026#mac)

- N/A

### [New Application Support](/docs/mdsdk/release-notes/september-15-2026#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/september-15-2026#windows)

- Follow up MDESDK-8260 - Add removal support for Trend Vision One Endpoint Security
- Add patching support for mRemoteNG
- Add patching support for AirSquirrels Reflector
- Add detection support for AirSquirrels Reflector
- Add detection support for Zoom VDI Client, Zoom Meeting SDK, and Zoom Workplace VDI Plugin for Windows
- Add detection support for Yubikey Manager
- Add patching support for Yubikey Manager

#### [Linux](/docs/mdsdk/release-notes/september-15-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/september-15-2026#mac)

- MacOS | Add Detection support for FileWave Client 16.x
- macOS | Add support auto-patching for AppCleaner
- Add support for Safari 27.x on macOS

### [New Application Version Support](/docs/mdsdk/release-notes/september-15-2026#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/september-15-2026#windows)

- Follow up MDESDK-8260 - Add removal support for Trend Vision One Endpoint Security
- V4 | Windows | Add support for FileZilla version 3.71.1
- Add patching support for mRemoteNG
- Add patching support for AirSquirrels Reflector
- V4 | Windows | Add support for Brave version 1.93.138
- V4 | Windows | Add support for Microsoft Edge 80+ version 152.0.4191.53
- V4 | Windows | Add support for Microsoft Visual Studio Code version 1.136.1
- Add detection support for AirSquirrels Reflector
- Add detection support for Zoom VDI Client, Zoom Meeting SDK, and Zoom Workplace VDI Plugin for Windows
- Add detection support for Yubikey Manager
- V4 | Windows | Add support for Windows Update Agent version 1508.2606.17012.0
- Add patching support for Yubikey Manager

#### [Linux](/docs/mdsdk/release-notes/september-15-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/september-15-2026#mac)

- MacOS | Add Detection support for FileWave Client 16.x
- V4 | Mac | Add support for Visual Studio Code version 1.137.0
- Add support for Safari 27.x on macOS

### [New Method Implementation](/docs/mdsdk/release-notes/september-15-2026#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/september-15-2026#windows)

- [Microsoft .NET SDK 9.0] Microsoft Corporation - Implement GetVersion for Microsoft .NET SDK 9.0 (x64)
- [Microsoft Defender ATP] Microsoft Corporation - Update GetRealTimeProtectionState implementation for Microsoft Defender ATP
- [Windows Defender] Microsoft Corporation - Update GetRealTimeProtectionState implementation for Windows Defender
- [Windows Defender] Microsoft Corporation - Update EnableRTP implementation for Windows Defender
- [Microsoft .NET SDK 10.0] Microsoft Corporation - Implement GetVersion for Microsoft .NET SDK 10.0 (x64)
- [Microsoft .NET SDK 10.0] Microsoft Corporation - Implement GetVersion for Microsoft .NET SDK 10.0 (arm64)
- [Microsoft .NET SDK 10.0] Microsoft Corporation - Implement GetVersion for Microsoft .NET SDK 10.0 (x86)
- [FileZilla] FileZilla Project - Implement GetInstallationDirectories for FileZilla
- [Antigravity] Google - Implement GetVersion for Antigravity
- [Reflector 4] Squirrels - Implement GetVersion for Reflector 4
- [Microsoft .NET Runtime 10.0] Microsoft Corporation - Implement GetVersion for Microsoft .NET Runtime 10.0 (x86)
- [Zoom VDI Plugin Management] Zoom Video Communications, Inc. - Implement TerminateProcesses for Zoom VDI Plugin Management
- [Zoom VDI Plugin Management] Zoom Video Communications, Inc. - Implement Run for Zoom VDI Plugin Management
- [Zoom VDI Plugin Management] Zoom Video Communications, Inc. - Implement GetRunningState for Zoom VDI Plugin Management
- [Zoom VDI Plugin Management] Zoom Video Communications, Inc. - Implement GetComponents for Zoom VDI Plugin Management
- [Zoom VDI Universal Plugin] Zoom Video Communications, Inc. - Implement GetRunningState for Zoom VDI Universal Plugin
- [Zoom VDI Universal Plugin] Zoom Video Communications, Inc. - Implement TerminateProcesses for Zoom VDI Universal Plugin
- [Zoom VDI Workplace] Zoom Video Communications, Inc. - Implement GetRunningState for Zoom VDI Workplace
- [Zoom VDI Workplace] Zoom Video Communications, Inc. - Implement Run for Zoom VDI Workplace
- [Zoom VDI Workplace] Zoom Video Communications, Inc. - Implement TerminateProcesses for Zoom VDI Workplace
- [Zoom Client for VDI] Zoom Video Communications, Inc. - Implement TerminateProcesses for Zoom Client for VDI
- [Zoom Client for VDI] Zoom Video Communications, Inc. - Implement Run for Zoom Client for VDI
- [Zoom Client for VDI] Zoom Video Communications, Inc. - Implement GetRunningState for Zoom Client for VDI
- [Zoom VDI Workplace] Zoom Video Communications, Inc. - Implement GetInstallationDirectories for Zoom VDI Workplace
- [Zoom Client for VDI] Zoom Video Communications, Inc. - Implement GetInstallationDirectories for Zoom Client for VDI
- [Zoom VDI Plugin Management] Zoom Video Communications, Inc. - Implement IsAuthentic for Zoom VDI Plugin Management
- [Visme] Easy WebContent, LLC - Implement TerminateProcesses for Visme
- [Zoom VDI Plugin Management] Zoom Video Communications, Inc. - Implement GetVersion for Zoom VDI Plugin Management
- [Zoom VDI Universal Plugin] Zoom Video Communications, Inc. - Implement GetVersion for Zoom VDI Universal Plugin
- [Zoom Client for VDI] Zoom Video Communications, Inc. - Update GetVersion implementation for Zoom Client for VDI
- [Zoom VDI Workplace] Zoom Video Communications, Inc. - Update GetVersion implementation for Zoom VDI Workplace

#### [Linux](/docs/mdsdk/release-notes/september-15-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/september-15-2026#mac)

- [FileWave Client] FileWave - Implement GetInstallationDirectories for FileWave Client
- [FileWave Client] FileWave - Implement IsAuthentic for FileWave Client
- [FileWave Client] FileWave - Implement GetVersion for FileWave Client
- [Visual Studio Code] Microsoft Corporation - Implement Run for Visual Studio Code
- [Firefox] Mozilla Corporation - Update GetVersion implementation for Firefox
- [npm] Joyent, Inc. - Update GetVersion implementation for npm
- [Firefox] Mozilla Corporation - Update GetVersion implementation for Firefox
