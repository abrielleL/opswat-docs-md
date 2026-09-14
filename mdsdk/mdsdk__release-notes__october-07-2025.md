<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/october-07-2025 -->

# October 07th, 2025

## [Release Note](/docs/mdsdk/release-notes/october-07-2025#release-note)

### [Release Date](/docs/mdsdk/release-notes/october-07-2025#release-date)

- 07/10/2025

### [SDK Version](/docs/mdsdk/release-notes/october-07-2025#sdk-version)

- **Windows**: 4.3.5062.0
- **Linux**: 4.3.4125.0
- **Mac**: 4.3.4523.0

### [Enhancement](/docs/mdsdk/release-notes/october-07-2025#enhancement)

#### [Windows](/docs/mdsdk/release-notes/october-07-2025#windows)

- Patching | Extending InstallFromFiles method by allowing to pass an expected sha256 hash
- [GA Release] Offline support for non-security MS patches

#### [Linux](/docs/mdsdk/release-notes/october-07-2025#linux)

- Patching | Extending InstallFromFiles method by allowing to pass an expected sha256 hash

#### [Mac](/docs/mdsdk/release-notes/october-07-2025#mac)

- N/A

### [Bug Fix](/docs/mdsdk/release-notes/october-07-2025#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/october-07-2025#windows)

- Fix issue GetRealTimeProtectionState method of Kaspersky Small Office Security not working on windows server, and enhance EnableRTP method to enable full option of RTP feature
- Fixed incorrect detection of Mozilla Firefox (x64) when not installed components, ensuring only valid Firefox installations are reported for more accurate application visibility.
- Fixed incorrect reporting of Logi Options+ Windows version by switching to an official source for version data, ensuring users now receive accurate update information for better patch management.
- Fixed inability to update Microsoft Visual C++ Redistributable due to an outdated public key by updating to the new pubkey, ensuring users can seamlessly install the latest version without errors.
- Fixed false positive error codes returned by wa_api_teardown during cache cleanup
- Fixed failed Greenshot upgrades when installed by non-admin users by adding support for user-specific installations, ensuring seamless patching for all user types.
- Fixed outdated Amazon Corretto 8 version information by updating the release note link and data, ensuring users always receive the latest version details for improved accuracy and reliability.

#### [Linux](/docs/mdsdk/release-notes/october-07-2025#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/october-07-2025#mac)

- N/A

### [New Application Support](/docs/mdsdk/release-notes/october-07-2025#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/october-07-2025#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/october-07-2025#linux)

- V4 | Linux | Add detection support for Claude

#### [Mac](/docs/mdsdk/release-notes/october-07-2025#mac)

- N/A

### [New Application Version Support](/docs/mdsdk/release-notes/october-07-2025#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/october-07-2025#windows)

- V4 | Windows | Add support for Mozilla Firefox (x86) version 143.0.1
- V4 | Windows | Add support for WithSecure Elements EDR and EPP for Computers Premium version 25.4
- V4 | Windows | Add support for ESET Endpoint Encryption version 5.4.14.0
- V4 | Windows | Add support for Mozilla Firefox (x64) version 143.0.1
- V4 | Windows | Add support for Bitdefender Antivirus Plus version 27.0.54.271
- V4 | Windows | Add support for WatchGuard EPP version 8.00.25

#### [Linux](/docs/mdsdk/release-notes/october-07-2025#linux)

- V4 | Linux | Add support for Ubuntu LTS 24.04.3
- V4 | Linux | Add support for Google Chrome version 141.0

#### [Mac](/docs/mdsdk/release-notes/october-07-2025#mac)

- N/A

### [New Method Implementation](/docs/mdsdk/release-notes/october-07-2025#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/october-07-2025#windows)

- [Mozilla Firefox] Mozilla Corporation - Update IsDefaultBrowser implementation for Mozilla Firefox (x86)
- [Kaspersky Small Office Security] Kaspersky Lab - Update GetRealTimeProtectionState implementation for Kaspersky Small Office Security
- [Kaspersky Small Office Security] Kaspersky Lab - Update EnableRTP implementation for Kaspersky Small Office Security
- [Mozilla Firefox] Mozilla Corporation - Update GetVersion implementation for Mozilla Firefox (x64)
- [Webex] Cisco Systems, Inc - Update GetVersion implementation for Webex (x86)
- [Mozilla Firefox] Mozilla Corporation - Update IsDefaultBrowser implementation for Mozilla Firefox (x64)

#### [Linux](/docs/mdsdk/release-notes/october-07-2025#linux)

- [Claude] Anthropic PBC - Implement GetRunningState for Claude
- [Claude] Anthropic PBC - Implement TerminateProcesses for Claude
- [Claude] Anthropic PBC - Implement Run for Claude
- [Crowdstrike Falcon] CrowdStrike, Inc. - Update GetAgentState implementation for Crowdstrike Falcon
- [Mozilla Firefox] Mozilla Corporation - Update GetVersion implementation for Mozilla Firefox

#### [Mac](/docs/mdsdk/release-notes/october-07-2025#mac)

- [Software Update] Apple Inc. - Update Run implementation for Software Update
- [Software Update] Apple Inc. - Update TerminateProcesses implementation for Software Update
