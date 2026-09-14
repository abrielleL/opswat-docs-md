<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/january-20-2026 -->

# January 20th, 2026

## [Release Note](/docs/mdsdk/release-notes/january-20-2026#release-note)

### [Release Date](/docs/mdsdk/release-notes/january-20-2026#release-date)

- 20/01/2026

### [SDK Version](/docs/mdsdk/release-notes/january-20-2026#sdk-version)

- **Windows**: 4.3.5526.0
- **Linux**: 4.3.4572.0
- **Mac**: 4.3.4943.0

### [Enhancement](/docs/mdsdk/release-notes/january-20-2026#enhancement)

#### [Windows](/docs/mdsdk/release-notes/january-20-2026#windows)

- Include the "date added" for new patches

#### [Linux](/docs/mdsdk/release-notes/january-20-2026#linux)

- Include the "date added" for new patches

#### [Mac](/docs/mdsdk/release-notes/january-20-2026#mac)

- N/A

### [Bug Fix](/docs/mdsdk/release-notes/january-20-2026#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/january-20-2026#windows)

- Fixed failed Adobe Acrobat Reader DC Continuous patch installations caused by invalid digital signature errors by updating the public key and certificate data, ensuring reliable and seamless updates for offline hosts.

#### [Linux](/docs/mdsdk/release-notes/january-20-2026#linux)

- Fixed duplicate patches appearing in GetMissingPatches for dnf by removing redundant data from multiple command sources to ensure users receive accurate and non-repetitive patch information.

#### [Mac](/docs/mdsdk/release-notes/january-20-2026#mac)

- N/A

### [New Application Support](/docs/mdsdk/release-notes/january-20-2026#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/january-20-2026#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/january-20-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/january-20-2026#mac)

- N/A

### [New Application Version Support](/docs/mdsdk/release-notes/january-20-2026#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/january-20-2026#windows)

- V4 | Windows | Add support for Mozilla Firefox (x64) version 147.0.1
- V4 | Windows | Add support for Microsoft Office 365 version 16.0.19530.20144
- V4 | Windows | Add support for Webex (x64) version 46.1.0.33913
- V4 | Windows | Add support for Mozilla Firefox (x86) version 147.0.1
- V4 | Windows | Add support for Microsoft Edge 80+ version 144.0.3719.82
- V4 | Windows | Add support for McAfee Total Protection version 16.0 R54
- V4 | Windows | Add support for McAfee LiveSafe – Internet Security version 16.0 R54
- V4 | Windows | Add support for Kaspersky Plus version 21.23.6.614
- V4 | Windows | Add support for Adobe Acrobat DC Continuous version 25.001.21078
- V4 | Windows | Add support for Foxit PDF Reader version 2025.3.0.35737
- V4 | Windows | Add support for McAfee version 1.35.148.1
- V4 | Windows | Add support for Mozilla Firefox (x64) version 147.0
- V4 | Windows | Add support for Mozilla Firefox (x86) version 147.0
- V4 | Windows | Add support for Sophos Home version 2024.3.3.1.0

#### [Linux](/docs/mdsdk/release-notes/january-20-2026#linux)

- V4 | Linux | Add support for VLC media player version 3.0.23
- V4 | Linux | Add support for Wireshark version 4.6.3
- V4 | Linux | Add support for Signal version 7.85.0
- V4 | Linux | Add support for Google Chrome version 144.0.7559.59

#### [Mac](/docs/mdsdk/release-notes/january-20-2026#mac)

- N/A

### [New Method Implementation](/docs/mdsdk/release-notes/january-20-2026#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/january-20-2026#windows)

- [NVDA] NV Access - Implement GetVersion for NVDA
- [McAfee Total Protection] McAfee, Inc. - Update GetThreats implementation for McAfee Total Protection
- [Kaspersky Plus] Kaspersky Lab - Update GetDefinitionState implementation for Kaspersky Plus
- [Kaspersky Plus] Kaspersky Lab - Update GetLastScanTime implementation for Kaspersky Plus

#### [Linux](/docs/mdsdk/release-notes/january-20-2026#linux)

- [Google Chrome] Google Inc. - Update IsDefaultBrowser implementation for Google Chrome
- [Google Chrome] Google Inc. - Update GetAntiphishingState implementation for Google Chrome
- [Dandified Yum] Red Hat, Inc. - Update GetMissingPatches implementation for Dandified Yum

#### [Mac](/docs/mdsdk/release-notes/january-20-2026#mac)

- [Cortex XDR] Palo Alto Networks, Inc. - Implement GetAgentState for Cortex XDR
