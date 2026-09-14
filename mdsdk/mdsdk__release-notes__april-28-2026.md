<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/april-28-2026 -->

# April 28th, 2026

## [Release Note](/docs/mdsdk/release-notes/april-28-2026#release-note)

### [Release Date](/docs/mdsdk/release-notes/april-28-2026#release-date)

- 28/04/2026

### [SDK Version](/docs/mdsdk/release-notes/april-28-2026#sdk-version)

- **Windows**: 4.3.5973.0
- **Linux**: 4.3.5005.0
- **Mac**: 4.3.5402.0

### [Enhancement](/docs/mdsdk/release-notes/april-28-2026#enhancement)

#### [Windows](/docs/mdsdk/release-notes/april-28-2026#windows)

- Remove the "method_status" from patch_status.json
- Remove "method_status" from analog/server/patch_status.json

#### [Linux](/docs/mdsdk/release-notes/april-28-2026#linux)

- Remove the "method_status" from patch_status.json
- Remove "method_status" from analog/server/patch_status.json
- Support patching multiple instances on Linux
- Linux 3rd party patch data not included in patch_aggregation.json

#### [Mac](/docs/mdsdk/release-notes/april-28-2026#mac)

- N/A

### [Bug Fix](/docs/mdsdk/release-notes/april-28-2026#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/april-28-2026#windows)

- Fixed missing event_type and handler_id in wa_event_handler’s event payload for event_type 10 by including these fields in the callback, enabling users to reliably identify event context and improve integration accuracy.
- Fixed incorrect last_scan_time values sent from Symantec Endpoint Protection clients by updating the GetLastScanTime method to reliably detect completed scans regardless of location changes, ensuring accurate scan status reporting for users and administrators.
- Fixed temp folders not being deleted under Windows\Temp by removing the legacy .sig file validation, allowing the SDK to securely clean up all temporary folders and freeing up disk space for users.

#### [Linux](/docs/mdsdk/release-notes/april-28-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/april-28-2026#mac)

- N/A

### [New Application Support](/docs/mdsdk/release-notes/april-28-2026#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/april-28-2026#windows)

- V4 | Windows | Separate signatures for HeidiSQL installed in All Users and Current User Mode

#### [Linux](/docs/mdsdk/release-notes/april-28-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/april-28-2026#mac)

- N/A

### [New Application Version Support](/docs/mdsdk/release-notes/april-28-2026#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/april-28-2026#windows)

- V4 | Windows | Add support for Google Chrome version 147.0.7727.117
- V4 | Windows | Add support for Cortex XDR version 9.1
- V4 | Windows | Add support for McAfee version 1.38.166.1
- V4 | Windows | Add support for Mozilla Firefox (arm64) version 150.0.0

#### [Linux](/docs/mdsdk/release-notes/april-28-2026#linux)

- V4 | Linux | Add support for Mozilla Firefox version 150.0

#### [Mac](/docs/mdsdk/release-notes/april-28-2026#mac)

- N/A

### [New Method Implementation](/docs/mdsdk/release-notes/april-28-2026#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/april-28-2026#windows)

- [TortoiseGit] https://tortoisegit.org/ - Implement GetUninstallString for TortoiseGit (x64)
- [TortoiseGit] https://tortoisegit.org/ - Implement GetUninstallHive for TortoiseGit (x64)
- [TortoiseGit] https://tortoisegit.org/ - Update GetVersion implementation for TortoiseGit (x64)
- [TortoiseGit] https://tortoisegit.org/ - Implement TerminateProcesses for TortoiseGit (x64)
- [TortoiseGit] https://tortoisegit.org/ - Implement GetRunningState for TortoiseGit (x64)
- [TortoiseGit] https://tortoisegit.org/ - Implement GetVersion for TortoiseGit (x86)
- [TortoiseGit] https://tortoisegit.org/ - Implement TerminateProcesses for TortoiseGit (x86)
- [TortoiseGit] https://tortoisegit.org/ - Implement GetRunningState for TortoiseGit (x86)
- [TortoiseGit] https://tortoisegit.org/ - Implement GetUninstallString for TortoiseGit (x86)
- [TortoiseGit] https://tortoisegit.org/ - Implement GetUninstallHive for TortoiseGit (x86)
- [HeidiSQL] Ansgar Becker - Implement GetUninstallString for HeidiSQL (User)
- [HeidiSQL] Ansgar Becker - Implement GetUninstallHive for HeidiSQL (User)
- [HeidiSQL] Ansgar Becker - Implement GetVersion for HeidiSQL (User)
- [TortoiseGit] https://tortoisegit.org/ - Implement GetRunningState for TortoiseGit (arm64)
- [TortoiseGit] https://tortoisegit.org/ - Implement TerminateProcesses for TortoiseGit (arm64)
- [TortoiseGit] https://tortoisegit.org/ - Implement GetUninstallHive for TortoiseGit (arm64)
- [TortoiseGit] https://tortoisegit.org/ - Implement GetUninstallString for TortoiseGit (arm64)
- [TortoiseGit] https://tortoisegit.org/ - Implement GetVersion for TortoiseGit (arm64)
- [McAfee] McAfee, Inc. - Update GetDefinitionState implementation for McAfee
- [Symantec Endpoint Protection] Symantec Corporation - Update GetLastScanTime implementation for Symantec Endpoint Protection

#### [Linux](/docs/mdsdk/release-notes/april-28-2026#linux)

- [Mozilla Firefox] Mozilla Corporation - Update GetAntiphishingState implementation for Mozilla Firefox

#### [Mac](/docs/mdsdk/release-notes/april-28-2026#mac)
