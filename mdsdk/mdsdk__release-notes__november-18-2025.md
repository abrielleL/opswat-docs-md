<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/november-18-2025 -->

# November 18th, 2025

## [Release Note](/docs/mdsdk/release-notes/november-18-2025#release-note)

### [Release Date](/docs/mdsdk/release-notes/november-18-2025#release-date)

- 18/11/2025

### [SDK Version](/docs/mdsdk/release-notes/november-18-2025#sdk-version)

- **Windows**: 4.3.5244.0
- **Linux**: 4.3.4303.0
- **Mac**: 4.3.4677.0

### [Enhancement](/docs/mdsdk/release-notes/november-18-2025#enhancement)

#### [Windows](/docs/mdsdk/release-notes/november-18-2025#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/november-18-2025#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/november-18-2025#mac)

- N/A

### [Bug Fix](/docs/mdsdk/release-notes/november-18-2025#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/november-18-2025#windows)

- Fixed inconsistent minimum_version reporting in GetLatestInstaller, which previously returned the OS version instead of the application version, by aligning the field to reflect the detected product version for non-OS updates—ensuring accurate version information and improving consistency for users.
- Fixed failure to retrieve last scan time for Trend Micro Deep Security Agent caused by a broken vendor CLI by implementing a region-based API URL workaround and updating the Chinese version signature, enabling accurate detection and scan time reporting for improved compliance visibility.

#### [Linux](/docs/mdsdk/release-notes/november-18-2025#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/november-18-2025#mac)

- N/A

### [New Application Support](/docs/mdsdk/release-notes/november-18-2025#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/november-18-2025#windows)

- Window | Add support signature for Eclipse Temurin JDK 25

#### [Linux](/docs/mdsdk/release-notes/november-18-2025#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/november-18-2025#mac)

- N/A

### [New Application Version Support](/docs/mdsdk/release-notes/november-18-2025#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/november-18-2025#windows)

- V4 | Windows | Add support for Mozilla Firefox (arm64) version 145.0
- V4 | Windows | Add support for Mozilla Firefox (x86) version 145.0
- V4 | Windows | Add support for Mozilla Firefox (x64) version 145.0
- V4 | Windows | Add support for Adobe Acrobat DC Continuous version 25.001.20844
- V4 | Windows | Add support for iTunes version 12.13.9.1
- V4 | Windows | Add support for Node.js LTS version 24.10.0

#### [Linux](/docs/mdsdk/release-notes/november-18-2025#linux)

- V4 | Linux | Add support for Visual Studio Code version 1.106.1
- V4 | Linux | Add support for LibreOffice version 25.8.3.2
- V4 | Linux | Add support for Thunderbird version 145.0
- V4 | Linux | Add support for Signal version 7.79.0
- V4 | Linux | Add support for Visual Studio Code version 1.106.0
- V4 | Linux | Add support for MySQL Server version 9.5.0

#### [Mac](/docs/mdsdk/release-notes/november-18-2025#mac)

- N/A

### [New Method Implementation](/docs/mdsdk/release-notes/november-18-2025#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/november-18-2025#windows)

- [Mozilla Firefox] Mozilla Corporation - Update GetPlugins implementation for Mozilla Firefox (x86)
- [Trend Micro Deep Security Agent] Trend Micro, Inc. - Update GetLastScanTime implementation for Trend Micro Deep Security Agent
- [Microsoft .NET Runtime 9.0] Microsoft Corporation - Implement GetVersion for Microsoft .NET Runtime 9.0 (x64)
- [Microsoft .NET Runtime 9.0] Microsoft Corporation - Implement GetVersion for Microsoft .NET Runtime 9.0 (x86)
- [VMware Workstation] VMware, Inc. - Update GetVersion implementation for VMware Workstation
- [iTunes] Apple Inc. - Implement Run for iTunes

#### [Linux](/docs/mdsdk/release-notes/november-18-2025#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/november-18-2025#mac)

- N/A
