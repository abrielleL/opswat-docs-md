<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/june-23-2026 -->

# June 23rd, 2026

## [Release Note](/docs/mdsdk/release-notes/june-23-2026#release-note)

### [Release Date](/docs/mdsdk/release-notes/june-23-2026#release-date)

- 23/06/2026

### [SDK Version](/docs/mdsdk/release-notes/june-23-2026#sdk-version)

- **Windows**: 4.3.6246.0
- **Linux**: 4.3.5255.0
- **Mac**: 4.3.5645.0

### [Enhancement](/docs/mdsdk/release-notes/june-23-2026#enhancement)

#### [Windows](/docs/mdsdk/release-notes/june-23-2026#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/june-23-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/june-23-2026#mac)

- N/A

### [Bug Fix](/docs/mdsdk/release-notes/june-23-2026#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/june-23-2026#windows)

- Resolved the inconsistency in the definition date and detection for Trend Micro Deep Security Agent by refining the timestamp logic to prioritize pattern file release dates and expanding product name matching, ensuring accurate compliance reporting and reliable product detection for users.
- Resolved missing CVE detection for Windows 10 22H2 ESU devices via adding the "ESU" product family to the mapping configuration, improving vulnerability reporting accuracy for licensed systems.
- Resolved incorrect version reporting for pgAdmin4 and Remote Desktop Client via updated GetVersion methods, improving the accuracy of installation status and patching results for users.
- Resolved slow and stalling Foxit PDF Reader downloads via a broader download link approach, improving installation reliability and speed for users.

#### [Linux](/docs/mdsdk/release-notes/june-23-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/june-23-2026#mac)

- N/A

### [New Application Support](/docs/mdsdk/release-notes/june-23-2026#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/june-23-2026#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/june-23-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/june-23-2026#mac)

- N/A

### [New Application Version Support](/docs/mdsdk/release-notes/june-23-2026#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/june-23-2026#windows)

- V4 | Windows | Add support for Mozilla Firefox (arm64) version 152.0.0

#### [Linux](/docs/mdsdk/release-notes/june-23-2026#linux)

- V4 | Linux | Add support for Mozilla Firefox version 152.0
- V4 | Linux | Add support for Mozilla Firefox version 152.0.1

#### [Mac](/docs/mdsdk/release-notes/june-23-2026#mac)

- N/A

### [New Method Implementation](/docs/mdsdk/release-notes/june-23-2026#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/june-23-2026#windows)

- [NoMachine] NoMachine - Implement Run for NoMachine
- [NoMachine] NoMachine - Implement TerminateProcesses for NoMachine
- [NoMachine] NoMachine - Implement GetRunningState for NoMachine
- [NoMachine] NoMachine - Implement GetVersion for NoMachine
- [Azul Zulu JDK 8] Azul Systems, Inc. - Implement GetVersion for Azul Zulu JDK 8 (x64)
- [Trend Micro Apex One Security Agent] Trend Micro, Inc. - Update GetThreats implementation for Trend Micro Apex One Security Agent
- [Microsoft Edge] Microsoft Corporation - Update GetVersion implementation for Microsoft Edge 80+
- [Trend Micro Deep Security Agent] Trend Micro, Inc. - Update GetDefinitionState implementation for Trend Micro Deep Security Agent
- [Trend Micro Apex One Security Agent] Trend Micro, Inc. - Update UpdateDefinitions implementation for Trend Micro Apex One Security Agent
- [Fireflies] Fireflies.ai - Implement Run for Fireflies
- [Fireflies] Fireflies.ai - Implement GetVersion for Fireflies
- [Mozilla Firefox] Mozilla Corporation - Update SetAntiphishingState implementation for Mozilla Firefox (arm64)
- [Remote Desktop Client] Microsoft Corporation - Update GetVersion implementation for Remote Desktop Client
- [Remote Desktop Client] Microsoft Corporation - Implement GetUninstallString for Remote Desktop Client

#### [Linux](/docs/mdsdk/release-notes/june-23-2026#linux)

#### [Mac](/docs/mdsdk/release-notes/june-23-2026#mac)

- [Trellix Endpoint Security for Mac] Musarubra US LLC. - Update EnableRTP implementation for Trellix Endpoint Security for Mac
- [Carbon Black Cloud] VMware, Inc. - Update EnableRTP implementation for Carbon Black Cloud
- [AppCleaner] FreeMacSoft - Implement GetRunningState for AppCleaner
