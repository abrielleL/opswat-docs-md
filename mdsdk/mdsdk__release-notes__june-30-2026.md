<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/june-30-2026 -->

# June 30th, 2026

## [Release Note](/docs/mdsdk/release-notes/june-30-2026#release-note)

### [Release Date](/docs/mdsdk/release-notes/june-30-2026#release-date)

- 30/06/2026

### [SDK Version](/docs/mdsdk/release-notes/june-30-2026#sdk-version)

- **Windows**: 4.3.6280.0
- **Linux**: 4.3.5284.0
- **Mac**: 4.3.5645.0

### [Enhancement](/docs/mdsdk/release-notes/june-30-2026#enhancement)

#### [Windows](/docs/mdsdk/release-notes/june-30-2026#windows)

- Support Human-Readable Logs with multi-level support
- Plaintext Log | File Header / Self-Contained Context per log file
- Bulletin Support for Patching
- Windows | Request for BIOS/firmware updates for Dell and Lenovo

#### [Linux](/docs/mdsdk/release-notes/june-30-2026#linux)

- Support Human-Readable Logs with multi-level support
- Plaintext Log | File Header / Self-Contained Context per log file
- Bulletin Support for Patching

#### [Mac](/docs/mdsdk/release-notes/june-30-2026#mac)

- N/A

### [Bug Fix](/docs/mdsdk/release-notes/june-30-2026#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/june-30-2026#windows)

- Resolved the issue where the `lc.dat` cache file failed to inherit parent folder permissions by implementing a cross-platform solution that explicitly copies the parent directory's access control list (DACL) or mode bits to the file after every write, ensuring consistent security compliance and file accessibility for users.
- Resolved a local privilege escalation vulnerability by implementing mutual PID verification and explicit access control lists on named pipes, improving system security by preventing unauthorized code execution.
- Resolved system crashes (BSOD) during application updates by implementing a multi-layered process guard that prevents the accidental termination of critical Windows system processes, improving overall system stability and reliability for end users.
- Fixed the issue where a default `rm.log` file was created even when a custom logging path was configured by making logging opt-in and ensuring no log files are produced unless explicitly requested, improving system security by preventing the creation of predictable and potentially exploitable log files.
- Resolved a race condition during SDK shutdown that caused intermittent process crashes by implementing an early stop for the debug monitor thread, improving stability and ensuring a crash-free teardown process for users.
- Resolved the failure of Office 365 installation directory detection in Slovak language environments via an updated regex pattern to match localized display names, improving compatibility and detection accuracy for international users.

#### [Linux](/docs/mdsdk/release-notes/june-30-2026#linux)

- Resolved the issue where the `lc.dat` cache file failed to inherit parent folder permissions by implementing a cross-platform solution that explicitly copies the parent directory's access control list (DACL) or mode bits to the file after every write, ensuring consistent security compliance and file accessibility for users.

#### [Mac](/docs/mdsdk/release-notes/june-30-2026#mac)

- N/A

### [New Application Support](/docs/mdsdk/release-notes/june-30-2026#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/june-30-2026#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/june-30-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/june-30-2026#mac)

- N/A

### [New Application Version Support](/docs/mdsdk/release-notes/june-30-2026#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/june-30-2026#windows)

- V4 | Windows | Add support for Malwarebytes Anti-Malware Premium version 5.6.1.257
- V4 | Windows | Add support for Malwarebytes Anti-Malware version 5.6.1.257
- V4 | Windows | Add support for VeraCrypt version 1.26.29
- V4 | Windows | Add support for ESET Internet Security version 19.1.12.0
- V4 | Windows | Add support for Mozilla Firefox (arm64) version 152.0.3
- V4 | Windows | Add support for Avast Premium Security version 26.5.10994.3655
- V4 | Windows | Add support for Sentinel Agent version 26.1.2.175

#### [Linux](/docs/mdsdk/release-notes/june-30-2026#linux)

- V4 | Linux | Add support for Mozilla Firefox version 152.0.3

#### [Mac](/docs/mdsdk/release-notes/june-30-2026#mac)

- N/A

### [New Method Implementation](/docs/mdsdk/release-notes/june-30-2026#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/june-30-2026#windows)

- [Malwarebytes Anti-Malware] Malwarebytes Corporation - Update GetDefinitionState implementation for Malwarebytes Anti-Malware

#### [Linux](/docs/mdsdk/release-notes/june-30-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/june-30-2026#mac)
