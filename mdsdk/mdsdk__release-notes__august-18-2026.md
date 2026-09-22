<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/august-18-2026 -->

# August 18th, 2026

## [Release Note](/docs/mdsdk/release-notes/august-18-2026#release-note)

### [Release Date](/docs/mdsdk/release-notes/august-18-2026#release-date)

- 18/08/2026

### [SDK Version](/docs/mdsdk/release-notes/august-18-2026#sdk-version)

- **Windows**: 4.3.6494.0
- **Linux**: 4.3.5496.0
- **Mac**: 4.3.5884.0

### [Enhancement](/docs/mdsdk/release-notes/august-18-2026#enhancement)

#### [Windows](/docs/mdsdk/release-notes/august-18-2026#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/august-18-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/august-18-2026#mac)

- N/A

### [Bug Fix](/docs/mdsdk/release-notes/august-18-2026#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/august-18-2026#windows)

- Resolved a security vulnerability where predictable temporary directory names and insecure file writes allowed local users to overwrite arbitrary system files via symbolic links by implementing randomized directory naming and strict ownership validation, ensuring the SDK only operates within secure, trusted environments.
- Resolved the misleading `WAAPI_ERROR_SCRIPTING_GENERAL` error for Office 365 downloads via enhanced error reporting, improving visibility by returning a specific `WAAPI_ERROR_ACCESS_DENIED` code when file creation is restricted.

#### [Linux](/docs/mdsdk/release-notes/august-18-2026#linux)

- Resolved a security vulnerability where predictable temporary directory names and insecure file writes allowed local users to overwrite arbitrary system files via symbolic links by implementing randomized directory naming and strict ownership validation, ensuring the SDK only operates within secure, trusted environments.

#### [Mac](/docs/mdsdk/release-notes/august-18-2026#mac)

- Resolved a security vulnerability where predictable temporary directory names and insecure file writes allowed local users to overwrite arbitrary system files via symbolic links by implementing randomized directory naming and strict ownership validation, ensuring the SDK only operates within secure, trusted environments.
- Fixed a memory leak in the macOS SDK's application inventory scan by implementing an autorelease pool for folder alias checks, ensuring stable memory consumption and preventing system performance degradation during extended uptime.

### [New Application Support](/docs/mdsdk/release-notes/august-18-2026#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/august-18-2026#windows)

- Windows | Add detection support for Adobe Acrobat Reader DC Continuous 26.x

#### [Linux](/docs/mdsdk/release-notes/august-18-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/august-18-2026#mac)

- V4| Add support for Mac OS X Builtin Firewall methods GetRunningState
- macOS | Add support auto-patching for GitHub Desktop
- [W:3] macOS | Add support detection for Navi

### [New Application Version Support](/docs/mdsdk/release-notes/august-18-2026#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/august-18-2026#windows)

- Windows | Add detection support for Adobe Acrobat Reader DC Continuous 26.x

#### [Linux](/docs/mdsdk/release-notes/august-18-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/august-18-2026#mac)

- V4| Add support for Mac OS X Builtin Firewall methods GetRunningState
- V4 | Mac | Add support for Xprotect version 5351
- [W:3] macOS | Add support detection for Navi

### [New Method Implementation](/docs/mdsdk/release-notes/august-18-2026#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/august-18-2026#windows)

- [企业微信] 腾讯科技(深圳)有限公司 - Implement TerminateProcesses for 企业微信
- [企业微信] 腾讯科技(深圳)有限公司 - Implement GetRunningState for 企业微信
- [Scribe] Colony Labs, Inc - Implement GetVersion for Scribe
- [Adobe Acrobat Reader DC Continuous] Adobe Systems Inc. - Update Run implementation for Adobe Acrobat Reader DC Continuous
- [Adobe Acrobat Reader DC Continuous] Adobe Systems Inc. - Update Run implementation for Adobe Acrobat Reader DC Continuous MUI
- [Azure Connected Machine Agent] Microsoft Corporation - Implement TerminateProcesses for Azure Connected Machine Agent
- [Azure Connected Machine Agent] Microsoft Corporation - Implement GetRunningState for Azure Connected Machine Agent
- [DBeaver] DBeaver Corp - Implement GetVersion for DBeaver
- [Visual Studio BuildTools 2026] Microsoft Corporation - Implement TerminateProcesses for Visual Studio BuildTools 2026
- [Visual Studio BuildTools 2026] Microsoft Corporation - Implement GetVersion for Visual Studio BuildTools 2026
- [Visual Studio BuildTools 2026] Microsoft Corporation - Implement TerminateProcesses for Visual Studio BuildTools 2026
- [Azure Connected Machine Agent] Microsoft Corporation - Implement GetVersion for Azure Connected Machine Agent
- [Microsoft .NET Runtime 10.0] Microsoft Corporation - Implement GetVersion for Microsoft .NET Runtime 10.0
- [Dialpad] Dialpad - Implement GetRunningState for Dialpad
- [docuPrinter] Neevia Tech - Implement GetInstallationDirectories for docuPrinter
- [Dialpad] Dialpad - Update GetVersion implementation for Dialpad
- [Microsoft Build of OpenJDK with Hotspot 25] Microsoft - Implement GetVersion for Microsoft Build of OpenJDK with Hotspot 25
- [TortoiseHg] Steve Borho and others - Update TerminateProcesses implementation for TortoiseHg
- [Amazon WorkSpaces] Amazon Web Services, Inc - Implement GetRunningState for Amazon WorkSpaces
- [Amazon WorkSpaces] Amazon Web Services, Inc - Implement TerminateProcesses for Amazon WorkSpaces

#### [Linux](/docs/mdsdk/release-notes/august-18-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/august-18-2026#mac)

- [Mac OS X Builtin Firewall] Apple Inc. - Implement GetRunningState for Mac OS X Builtin Firewall
- [Navi] Karl Valencia - Implement GetVersion for Navi
- [Navi] Karl Valencia - Implement Run for Navi
