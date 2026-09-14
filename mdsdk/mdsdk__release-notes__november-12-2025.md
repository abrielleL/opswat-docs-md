<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/november-12-2025 -->

# November 12th, 2025

## [Release Note](/docs/mdsdk/release-notes/november-12-2025#release-note)

### [Release Date](/docs/mdsdk/release-notes/november-12-2025#release-date)

- 12/11/2025

### [SDK Version](/docs/mdsdk/release-notes/november-12-2025#sdk-version)

- **Windows**: 4.3.5218.0
- **Linux**: 4.3.4278.0
- **Mac**: 4.3.4677.0

### [Enhancement](/docs/mdsdk/release-notes/november-12-2025#enhancement)

#### [Windows](/docs/mdsdk/release-notes/november-12-2025#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/november-12-2025#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/november-12-2025#mac)

- N/A

### [Bug Fix](/docs/mdsdk/release-notes/november-12-2025#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/november-12-2025#windows)

- Fixed failed Dell SupportAssist patch installations caused by vendor data changes by updating the download and installation scripts to verify file sufficiency, ensuring reliable patching and smoother user experience.
- Fixed OpenOffice download failures caused by invalid signature errors by updating the pubkey, ensuring users can successfully download and install version 4.1.16 without interruptions.
- Fixed incorrect detection of Symantec Endpoint Protection's last scan time by updating the logic to retrieve the actual Location value from the registry and refining the scan type matching, ensuring accurate scan time reporting for all configurations.
- Fixed out-of-memory errors during registry data collection by temporarily disabling debug log collection for the affected registry path, ensuring stable installations and preventing failures when updating multiple products.

#### [Linux](/docs/mdsdk/release-notes/november-12-2025#linux)

- Fixed memory leaks detected by AddressSanitizer during runtime when loading patch databases by adding a virtual destructor to the base class, ensuring proper cleanup and improving SDK stability for seamless Linux integrations.

#### [Mac](/docs/mdsdk/release-notes/november-12-2025#mac)

- N/A

### [New Application Support](/docs/mdsdk/release-notes/november-12-2025#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/november-12-2025#windows)

- Window | Add support signature for Eclipse Temurin JDK 23

#### [Linux](/docs/mdsdk/release-notes/november-12-2025#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/november-12-2025#mac)

- N/A

### [New Application Version Support](/docs/mdsdk/release-notes/november-12-2025#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/november-12-2025#windows)

- V4 | Windows | Add support for Brave version 1.84.132
- V4 | Windows | Add support for 7-Zip (arm64) version 25.01
- V4 | Windows | Add support for Microsoft Visual Studio Code (User) (Arm64) version 1.105.1
- V4 | Windows | Add support for Dropbox 3+ version 236.4.5918
- V4 | Windows | Add support for Google Chrome version 142.0.7444.135

#### [Linux](/docs/mdsdk/release-notes/november-12-2025#linux)

- V4 | Linux | Add support for Signal version 7.78.0
- V4 | Linux | Add support for GIMP version 3.0.6
- V4 | Linux | Add support for RealVNC Server version 7.15.0

#### [Mac](/docs/mdsdk/release-notes/november-12-2025#mac)

- N/A

### [New Method Implementation](/docs/mdsdk/release-notes/november-12-2025#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/november-12-2025#windows)

- [Dell Display Manager] Dell Inc. - Implement GetVersion for Dell Display Manager
- [Sophos Home] Sophos Limited - Update UpdateDefinitions implementation for Sophos Home
- [Eclipse Temurin JDK with Hotspot 23] Eclipse Foundation, Inc. - Implement GetVersion for Eclipse Temurin JDK with Hotspot 23 (arm64)
- [7-Zip] Igor Pavlov - Implement Run for 7-Zip (arm64)
- [Symantec Endpoint Protection] Symantec Corporation - Update GetLastScanTime implementation for Symantec Endpoint Protection
- [Microsoft Office MSI] Microsoft Corporation - Update GetVersion implementation for Microsoft Office 2016
- [Apache Tomcat] Apache Software Foundation - Update GetVersion implementation for Apache Tomcat 9
- [Apache Tomcat] Apache Software Foundation - Implement IsAuthentic for Apache Tomcat 9
- [Apache Tomcat] Apache Software Foundation - Implement GetUninstallHive for Apache Tomcat 9
- [Apache Tomcat] Apache Software Foundation - Implement GetComponents for Apache Tomcat 9
- [Apache Tomcat] Apache Software Foundation - Implement GetInstallationDirectories for Apache Tomcat 9
- [Apache Tomcat] Apache Software Foundation - Update Run implementation for Apache Tomcat 9
- [Microsoft Exchange Server] Microsoft Corporation - Update GetVersion implementation for Microsoft Exchange Server
- [Microsoft SQL Server Express] Microsoft Corporation - Update GetVersion implementation for Microsoft SQL Server Express 2016
- [Microsoft SQL Server] Microsoft Corporation - Update GetVersion implementation for Microsoft SQL Server 2016

#### [Linux](/docs/mdsdk/release-notes/november-12-2025#linux)

- [Advanced Packaging Tool] GNU - Update GetMissingPatches implementation for Advanced Packaging Tool
- [Eclipse Temurin JDK with Hotspot 23] Eclipse Foundation, Inc. - Update GetVersion implementation for Eclipse Temurin JDK with Hotspot 23
- [Eclipse Temurin JDK with Hotspot 22] Eclipse Foundation, Inc. - Update GetVersion implementation for Eclipse Temurin JDK with Hotspot 22
- [Eclipse Temurin JDK with Hotspot 21] Eclipse Foundation, Inc. - Update GetVersion implementation for Eclipse Temurin JDK with Hotspot 21
- [Eclipse Temurin JDK with Hotspot 20] Eclipse Foundation, Inc. - Update GetVersion implementation for Eclipse Temurin JDK with Hotspot 20
- [Eclipse Temurin JDK with Hotspot 17] Eclipse Foundation, Inc. - Update GetVersion implementation for Eclipse Temurin JDK with Hotspot 17
- [Eclipse Temurin JDK with Hotspot 11] Eclipse Foundation, Inc. - Update GetVersion implementation for Eclipse Temurin JDK with Hotspot 11
- [Eclipse Temurin JDK with Hotspot 8] Eclipse Foundation, Inc. - Update GetVersion implementation for Eclipse Temurin JDK with Hotspot 8
- [GIMP] Spencer Kimball, Peter Mattis and the GIMP Development Team - Update Run implementation for GIMP
- [RealVNC Server] RealVNC Ltd - Implement GetVersion for RealVNC Server

#### [Mac](/docs/mdsdk/release-notes/november-12-2025#mac)

- [CleanMyMac X] MacPaw Inc. - Update GetRealTimeProtectionState implementation for CleanMyMac X
