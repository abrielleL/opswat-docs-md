<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/july-21-2026 -->

# July 21st, 2026

## [Release Note](/docs/mdsdk/release-notes/july-21-2026#release-note)

### [Release Date](/docs/mdsdk/release-notes/july-21-2026#release-date)

- 21/07/2026

### [SDK Version](/docs/mdsdk/release-notes/july-21-2026#sdk-version)

- **Windows**: 4.3.6375.0
- **Linux**: 4.3.5372.0
- **Mac**: 4.3.5733.0

### [Enhancement](/docs/mdsdk/release-notes/july-21-2026#enhancement)

#### [Windows](/docs/mdsdk/release-notes/july-21-2026#windows)

- Enhance GetRealTimeProtectionState to include information about the 3rd-party product managing Windows Defender Antivirus
- Add a new field in products.json to indicate whether the download link is directly available in patch_aggregation.json.

#### [Linux](/docs/mdsdk/release-notes/july-21-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/july-21-2026#mac)

- N/A

### [Bug Fix](/docs/mdsdk/release-notes/july-21-2026#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/july-21-2026#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/july-21-2026#linux)

- Resolved the issue where LibreOffice updates failed with a generic scripting engine error when disk space was exhausted via improved Lua script error handling and pattern definitions, ensuring users receive clear, actionable feedback such as "insufficient disk space" for smoother troubleshooting.

#### [Mac](/docs/mdsdk/release-notes/july-21-2026#mac)

- Resolved macOS privacy permission popups by applying bundle search restrictions to the live file system watcher, ensuring excluded locations are no longer accessed to maintain user privacy.

### [New Application Support](/docs/mdsdk/release-notes/july-21-2026#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/july-21-2026#windows)

- Add detection support for mRemoteNG
- V4 | Add support method GetMissingPatches for existing product Dell Command | Update
- V4 | Windows | Add support for Microsoft PowerToys
- v4| Add support for existing products McAfee 1.40.x antivirus
- Add support patching for eID Client (Slovakia)

#### [Linux](/docs/mdsdk/release-notes/july-21-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/july-21-2026#mac)

- macOS | Add support auto-patching for BBEdit
- macOS | Add support auto-patching for Yubico Authenticator
- macOS | Add support auto-patching for Fork
- [W:6] macOS | Add support detection for Grain
- [W:7] macOS | Add support detection for MeetGeek
- [W:7] macOS | Add support detection for Limitless
- [W:6] macOS | Add support detection for LanguageTool
- [W:6] macOS | Add support detection for Writer
- [W:7] macOS | Add support detection for Amazon Q
- macOS | Add support auto-patching for Loom

### [New Application Version Support](/docs/mdsdk/release-notes/july-21-2026#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/july-21-2026#windows)

- Add detection support for mRemoteNG
- V4 | Windows | Add support for BitLocker Drive Encryption version 10.0.28000.2336
- V4 | Add support method GetMissingPatches for existing product Dell Command | Update
- v4| Add support for existing products McAfee 1.40.x antivirus

#### [Linux](/docs/mdsdk/release-notes/july-21-2026#linux)

- V4 | Linux | Add support for Visual Studio Code version 1.128.0
- V4 | Linux | Add support for Wireshark version 4.6.7
- V4 | Linux | Add support for Signal version 8.18.0
- V4 | Linux | Add support for Mozilla Firefox version 152.0.6

#### [Mac](/docs/mdsdk/release-notes/july-21-2026#mac)

- [W:6] macOS | Add support detection for Grain
- [W:7] macOS | Add support detection for MeetGeek
- [W:7] macOS | Add support detection for Limitless
- [W:6] macOS | Add support detection for LanguageTool
- [W:6] macOS | Add support detection for Writer
- [W:7] macOS | Add support detection for Amazon Q

### [New Method Implementation](/docs/mdsdk/release-notes/july-21-2026#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/july-21-2026#windows)

- [mRemoteNG] GNU - Implement GetVersion for mRemoteNG
- [Windows Defender] Microsoft Corporation - Update GetRealTimeProtectionState implementation for Windows Defender
- [Dell Command | Update] Dell Inc. - Implement GetMissingPatches for Dell Command | Update (UWP)
- [McAfee] McAfee, Inc. - Update GetDefinitionState implementation for McAfee
- [McAfee] McAfee, Inc. - Update GetUninstallHive implementation for McAfee
- [ExpressVPN] ExpressVPN - Implement GetVersion for ExpressVPN
- [ExpressVPN] ExpressVPN - Implement Run for ExpressVPN
- [ExpressVPN] ExpressVPN - Update TerminateProcesses implementation for ExpressVPN
- [ExpressVPN] ExpressVPN - Implement GetInstallationDirectories for ExpressVPN
- [ExpressVPN] ExpressVPN - Implement GetComponents for ExpressVPN
- [ExpressVPN] ExpressVPN - Implement IsAuthentic for ExpressVPN
- [ExpressVPN] ExpressVPN - Implement GetUninstallString for ExpressVPN
- [PowerToys] Microsoft Corporation - Update GetVersion implementation for PowerToys
- [PowerToys] Microsoft Corporation - Update GetVersion implementation for PowerToys (User)
- [VirtualBox] Oracle Corporation - Update Run implementation for VirtualBox
- [VirtualBox] Oracle Corporation - Implement GetRunningState for VirtualBox
- [VirtualBox] Oracle Corporation - Implement TerminateProcesses for VirtualBox

#### [Linux](/docs/mdsdk/release-notes/july-21-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/july-21-2026#mac)

- [Grain] Grain Intelligence Inc. - Implement Run for Grain
- [Grain] Grain Intelligence Inc. - Implement GetRunningState for Grain
- [Grain] Grain Intelligence Inc. - Implement TerminateProcesses for Grain
- [MeetGeek] MeetGeek AI - Implement Run for MeetGeek
- [Limitless] Limitless - Implement Run for Limitless
- [Amazon Quick] Amazon Web Services, Inc - Implement Run for Amazon Quick
