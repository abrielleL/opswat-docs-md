<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/november-04-2025 -->

# November 04th, 2025

## [Release Note](/docs/mdsdk/release-notes/november-04-2025#release-note)

### [Release Date](/docs/mdsdk/release-notes/november-04-2025#release-date)

- 04/11/2025

### [SDK Version](/docs/mdsdk/release-notes/november-04-2025#sdk-version)

- **Windows**: 4.3.5183.0
- **Linux**: 4.3.4214.0
- **Mac**: 4.3.4613.0

### [Enhancement](/docs/mdsdk/release-notes/november-04-2025#enhancement)

#### [Windows](/docs/mdsdk/release-notes/november-04-2025#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/november-04-2025#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/november-04-2025#mac)

- N/A

### [Bug Fix](/docs/mdsdk/release-notes/november-04-2025#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/november-04-2025#windows)

- Fixed incorrect detection of Mozilla Firefox (x64) GetProductInfo input.detect_user_installed_mode as per-user installed by adding a disable registry check flag to the detection logic, ensuring accurate identification of machine-wide installations and improving compliance reporting for users.
- Fixed a memory leak in libwautils where process handles were not closed after use by updating the SDK to properly release handles, reducing resource consumption and improving stability for users running in non-elevated mode or with WMI disabled.
- Fixed WAAPI_ERROR_INVALID_SIGNATURE when updating LibreOffice 25.8.2.2 by adding the new certificate chain and public key, ensuring seamless updates and reliable patch installations for users.

#### [Linux](/docs/mdsdk/release-notes/november-04-2025#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/november-04-2025#mac)

- N/A

### [New Application Support](/docs/mdsdk/release-notes/november-04-2025#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/november-04-2025#windows)

- Windows | Add support detection for Tomcat 11

#### [Linux](/docs/mdsdk/release-notes/november-04-2025#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/november-04-2025#mac)

- N/A

### [New Application Version Support](/docs/mdsdk/release-notes/november-04-2025#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/november-04-2025#windows)

- V4 | Windows | Add support for Mozilla Firefox (x86) version 144.0.2
- V4 | Windows | Add support for Mozilla Firefox (x64) version 144.0.2
- V4 | Windows | Add support for Trend Micro Apex One Security Agent version 14.0.20315
- V4 | Windows | Add support for Mozilla Firefox (arm64) version 144.0.2

#### [Linux](/docs/mdsdk/release-notes/november-04-2025#linux)

- V4 | Linux | Add support for Signal version 7.77.1
- V4 | Linux | Add support for LibreOffice version 25.8.2
- V4 | Linux | Add support for MySQL Workbench version 8.0.44
- V4 | Linux | Add support for Thunderbird version 144.0.1
- V4 | Linux | Add support for Visual Studio Code version 1.105.1
- V4 | Linux | Add support for Wireshark version 4.6.0
- V4 | Linux | Add support for Fedora 43
- V4 | Linux | Add support for Google Chrome version 142.0.7444.59

#### [Mac](/docs/mdsdk/release-notes/november-04-2025#mac)

- N/A

### [New Method Implementation](/docs/mdsdk/release-notes/november-04-2025#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/november-04-2025#windows)

- [VirIT eXplorer PRO] TG Soft S.a.s. - Implement Run for VirIT eXplorer PRO
- [VirIT eXplorer PRO] TG Soft S.a.s. - Update GetThreats implementation for VirIT eXplorer PRO
- [VirIT eXplorer PRO] TG Soft S.a.s. - Update GetRunningState implementation for VirIT eXplorer PRO
- [VirIT eXplorer PRO] TG Soft S.a.s. - Update GetDefinitionState implementation for VirIT eXplorer PRO
- [VirIT eXplorer PRO] TG Soft S.a.s. - Implement GetVersion for VirIT eXplorer PRO
- [Apache Tomcat] Apache Software Foundation - Implement GetComponents for Apache Tomcat 11
- [Apache Tomcat] Apache Software Foundation - Implement IsAuthentic for Apache Tomcat 11
- [Apache Tomcat] Apache Software Foundation - Implement GetRunningState for Apache Tomcat 11
- [Apache Tomcat] Apache Software Foundation - Implement TerminateProcesses for Apache Tomcat 11
- [Apache Tomcat] Apache Software Foundation - Implement Run for Apache Tomcat 11
- [Apache Tomcat] Apache Software Foundation - Implement GetVersion for Apache Tomcat 11
- [Java SE Development Kit] Oracle Corporation - Update GetVersion implementation for Java SE Development Kit
- [Mozilla Firefox] Mozilla Corporation - Update GetPlugins implementation for Mozilla Firefox (x64)
- [Mozilla Firefox] Mozilla Corporation - Update IsDefaultBrowser implementation for Mozilla Firefox (x64)
- [Mozilla Firefox] Mozilla Corporation - Update IsDefaultBrowser implementation for Mozilla Firefox (x86)
- [Eclipse Temurin JDK with Hotspot 23] Eclipse Foundation, Inc. - Implement GetVersion for Eclipse Temurin JDK with Hotspot 23 (x64)
- [Eclipse Temurin JDK with Hotspot 25] Eclipse Foundation, Inc. - Implement GetVersion for Eclipse Temurin JDK with Hotspot 25 (x64)
- [WinRAR] Alexander Roshal - Implement GetUninstallHive for WinRAR (x86)
- [Foxit Reader] Foxit Software - Implement Run for Foxit PDF Reader

#### [Linux](/docs/mdsdk/release-notes/november-04-2025#linux)

- [Java SE Development Kit] Oracle Corporation - Update GetVersion implementation for Java SE Development Kit
- [Zypper] SUSE LINUX GmbH - Update InstallMissingPatches implementation for Zypper
- [Dandified Yum] Red Hat, Inc. - Update InstallMissingPatches implementation for Dandified Yum
- [Yum] GNU - Update InstallMissingPatches implementation for Yum

#### [Mac](/docs/mdsdk/release-notes/november-04-2025#mac)

- [Microsoft Edge] Microsoft Corporation - Implement GetVersion for Microsoft Edge
- [Java Development Kit] Oracle Corporation - Update GetVersion implementation for Java Development Kit
- [Ivanti Endpoint Manager Agent] Ivanti, Inc. - Implement GetRunningState for Ivanti Endpoint Manager Agent
- [FileVault] Apple Inc. - Update GetEncryptionState implementation for FileVault
