<!-- source: https://www.opswat.com/docs/mdicap/release-notes/changelog -->

# Archived Release Notes

## [Version 5.14.0](/docs/mdicap/release-notes/changelog#version-5140)

Enhancement and new features:

- Refreshed UI: Modern, Accessible and Consistent:

  - **Metadefender ICAP Server v5.14.0** adopts OPSWAT's **Blue Line Framework (BLF)** design system, delivering a consistent, modern, and accessible interface.

    - **Unified Visual Language** — Consistent typography, spacing, color palette, and iconography applied across all pages and components for a cohesive look and feel.
    - **Modernized Components** — Buttons, forms, tables, modals, and navigation elements have been rebuilt using BLF-standard components, improving usability and interaction clarity.
    - **Accessibility** — UI components now conform to WCAG 2.1 accessibility standards, featuring enhanced keyboard navigation, visible focus states, and improved color contrast ratios to broaden access for all operators.
    - **Responsive Layout** — The interface adapts fluidly across different screen sizes and resolutions, supporting a consistent experience on various devices.
    - **Consistent Branding** — Visual alignment with other OPSWAT products (MetaDefender Core™, MetaDefender Cloud™, and other OPSWAT products) delivers a unified operator experience across the product suite. If you work across multiple OPSWAT products, the experience will feel immediately familiar.
- Enhanced Support Package Generation:

  - The support package generator has been significantly improved with greater control and flexibility over what gets collected, reducing package size and generation time.

    - **Selective Log Collection** — Choose which logs to include: database logs, system logs, NGINX logs, or ICAP product logs. Collect only what's needed for faster and more targeted diagnostics.
    - **Log File Limit** — Set a maximum number of log files to collect per category. By default, all available log files are included.
    - **Processing History Toggle** — Opt in or out of including processing history. Excluding it can noticeably reduce both the package size and the time required to generate it. By default, this option is disabled.
- Pre-Installation Checks: Port Conflict Detection & Automatic AV Exclusion

  - To streamline deployment and reduce installation issues, two automated checks have been introduced during the installation process.

    - **Port Conflict Detection*(all platforms)*** — Before installation begins, the installer verifies that all required ports are available. If a conflict is detected, installation is blocked and you are notified with enough detail to resolve the issue before retrying — no silent failures, no misconfigured deployments.
    - **Automatic AV Exclusion*(Windows only)*** — On systems running Windows Defender, the ICAP Server process and its working directory are automatically added to the AV exclusion list during installation. No manual post-install configuration required.
- Security Enhancements:

  - Upgraded third-party libraries for improved security:

    - LibXML2 v2.15.3
    - OpenSSL v3.6.2
    - Curl v8.20
    - Nginx v1.30.2
    - Sqlite v3.53.1
    - Zlib v1.3.2
    - ICU for C++ v28.3
    - gRPC v1.78.1

Applied additional security hardening measures across the product to prevent vulnerabilities and strengthen overall protection.

- Usability Improvements:

  - **UTF-8 Encoding for Block Pages** — UTF-8 encoding is now enabled by default for block pages, ensuring proper display of multilingual and special characters without additional configuration.
  - **Broader Password Character Support** — Passwords may now include the `<` and `>` characters, providing greater flexibility when setting credentials.
  - **Higher REST API Body Size Limit** — The default maximum accepted body size for REST API requests has been increased to **2 MB**, accommodating larger payloads without requiring manual configuration changes.
  - **Server Profile Visualization** — A new visual representation of **Server Profiles** makes it easier to understand how scan requests are distributed across MetaDefender Core™ instances. This feature is useful when tuning or troubleshooting multi-instance configurations.

Fixed issues:

- Intermittent Service Crash When Cancelling Scan Requests with Data Trickling Enabled: Resolved an intermittent stability issue introduced in v5.11.0 where the ICAP service could crash if multiple scan requests were cancelled simultaneously while data trickling was enabled.
- Log Rotation Not Functioning on Windows: Resolved an issue introduced in v5.13.0 where log rotation failed to function correctly on Windows systems
- Export CSV of processing history: Fixed an issue where exporting processing history as CSV would fail when multiple filters were combined (regression since v5.13.0
- High CPU load when OCM connection is interrupted: On systems where Metadefender ICAP Server is enrolled and managed by OCM, a dropped connection to OCM could cause abnormally high CPU utilization that persisted until the connection was re-established. This issue has been resolved — CPU usage now remains stable regardless of OCM connection state. This issue introduced in v5.13.0
- Minor Fixes

## [Version 5.13.0](/docs/mdicap/release-notes/changelog#version-5130)

Enhancement and new features:

- Improve capability in handling ICAP messages

  - Enhanced ICAP message handling: Achieved significant performance improvements by doubling the number of ICAP messages processed concurrently, without requiring any changes to existing hardware profiles.
  - Optimized user interface responsiveness: Ensured seamless UI access and interaction even under high load conditions.
  - Reduce the loading of PostgreSQL database by reduce the IO access
- Support Advanced Log Configurations on Web Console

  - Starting with MetaDefender ICAP version 5.13.0, the following advanced log configurations including local time zone, Common Event Format, product logs and syslog settings are supported
- Enhanced authentication experience

  - Implemented Single Logout (SLO) support within Single Sign-On (SAML), allowing users to securely end all active sessions across connected applications with a single action, improving both security and convenience
- Security Enhancements: Upgraded third-party libraries for improved security:

  - PostgreSQL v16.13
  - OpenSSL v3.4.4
  - Angular v19.2.19
  - gRPC v1.71.1
  - Curl v8.18.0

Applied additional security hardening measures across the product to prevent vulnerabilities and strengthen overall protection.

- Usability Improvements:

  - New Configuration Option:

    - **CA path support (Linux):** Added option ***global/curlopt_capth*** to set CA path on Linux, this will enable Docker images running as non-root to instal and use self-sign certitifaces
    - **Skip First Start Page**: Introduced flag ***internal/skip_first_start_page*** to bypass the initial start page, this prevent unnecessary interruptions when Kubernetes PODs are recycled
    - **Handle Non-Standard Content-Encoding**: Added flag ***global/skip_non_standard_encoding_preprocess*** to manage non-standard content-encoding values

      - If a content-encoding type is listed in this flag, the MD ICAP Server will not decode the HTTP body before sending it to MD Core for scanning
      - Example: below ensures that when content-encoding: none is used, the body is passed through without preprocessing
      - global/skip_non_standard_encoding_preprocess = none
    - **Limit URL Storage Length**: Introduced flag ***global/store_first_n_characters_url*** to restrict the number of URL characters stored in the database

      - This will help ensure that sensitive data passed through the URL is not stored in the database
    - **Share SSO Configuration [Linux]**: Add option ***internal/sso_cross_instance_enabled*** to apply a single SSO configuration across all MD ICAP Server instances that use the same Shared Database Mode. This ensures consistency when multiple MD ICAP Server instances are deployed behind a load balancer and accessed via the same URL

Fixed issues:

- Fixed timeout when exporting processing history: Resolved a timeout error that occurred during export of large processing histories
- Fixed crash when deleting a support package via the UI: Fixed an edge case where deleting a support package via the UI could cause the service to crash
- Minor Fixes

## [Version 5.12.0](/docs/mdicap/release-notes/changelog#version-5120)

Enhancement and new features:

- Expanding processing history details: View a complete chronological timeline of each file's journey through the processing pipeline, including precise start and end times for every stage. Quickly identify bottlenecks and optimize performance by visualizing where files spend the most time, enabling faster troubleshooting and process optimization
- Security Hardening for Block Page Content: Strengthen security with an option to disallow scripts and unsafe HTML tags in custom block pages.

  - By default, new installations block these elements to prevent potential vulnerabilities.
  - For upgrades from older versions, if the existing blockpage content contains scripts or unsafe HTML tags, an admin or authorized user will be prompted to review and choose whether to allow or disallow them.
  - *Note: Before applying the* ***“Remove and Block Scripts/Unsafe HTML”*** *option, admins should carefully review the blockpage content, as removing these elements may alter its formatting.*
- Support for CIS Level 1 and 2 for Windows: __MetaDefender ICAP Server now aligns with CIS Level 1 and Level 2 benchmarks for Windows Server 2022. This enhancement supports organizations that require stricter security controls
- Security Enhancements: Upgraded third-party libraries for improved security:

  - Qt v6.9.3
  - PostgreSQL v16.10
  - OpenSSL v3.4.3
  - gRPC v1.71.1
  - NGINX v1.28.0
  - OpenLDAP v2.6.10
  - Brotli v1.2.0
  - Curl v8.16.0

Applied additional security hardening measures across the product to prevent vulnerabilities and strengthen overall protection.

- Usability Improvements:

  - **Prevent Hardware Deployment ID Changes with Teamed NIC:** Ensures stability by preventing deployment ID from changing when network interface cards are teamed.
  - **Configurable Syslog Date Format:** Added a flag option logger/syslog_dateformat to allow customization of the datetime format in syslog entries (refer to [Configuration file](/docs/mdicap/configuration/configuration-file)).
  - **Enhanced Processing History Search:** Supports searching and displaying filenames in processing history if the file can be scanned, even when files are packaged in multipart form
  - **Workflow Optimization: Allow List by File Type** - Introduced an option to allowlist by file type within each workflow, reducing unnecessary scans for extremely small files (e.g., files less than 10–20 bytes).
  - **NGINX Integration Health Check:** Added support for health checks to improve reliability in NGINX-integrated environments.
  - **Simplified ICAP Integration with Numeric Verdicts:** Added an option to return the X-Result-Number header with a numeric value instead of a verdict string, making ICAP client integration simpler for verdict validation. Enable this header by setting the flag global/enable_x_result_number_header (refer to [Configuration file](/docs/mdicap/configuration/configuration-file))
  - Add support for scanning Base64-encoded data embedded within a JSON structure in a URL-encoded format

Fixed issues:

- Random crash issue on Linux: Resolved a rare crash issue on Linux environments that could occur when polling and webhook callbacks were combined
- Slow performance under heavy load in version 5.11.0: In ICAP version 5.11.0, performance may degrade under high load conditions due to an issue with the cURL library. Threads are released slowly, which can result in a large number of parallel threads accumulating. This issue has already been identified and resolved in ICAP version 5.12.0
- Minor Fixes

## [Version 5.11.0](/docs/mdicap/release-notes/changelog#version-5110)

Enhancement and new features:

- Select MetaDefender Core Server Profiles Based on File Attributes
- Dynamic Load Balancing: Introduces a new load balancing mode to address the limitations of Round Robin when MetaDefender Core instances differ in hardware capacity or workload complexity. Scan requests are prioritized and distributed to the least busy MetaDefender Core instance based on the scan queue information
- integration with BeyondTrust's Password Safe: A new option to increase the security for Active Directory configuration. MetaDefender ICAP Server can be integrated with BeyondTrust's Password Safe (Privileged Access Management) for automated credential management. This enables automated credential management for secure access
- Usability Improvements:

  - Support password strength meter
  - Unified login screen experience
  - Default maxstdio value set to 8192 on Windows
  - For SOAP/JSON file in multi-part form uploads of the Content encode feature, the file size limit will be calculated based on the SOAP/JSON file instead of the total size content.
  - Enhancement for SOAP node selector: Now supports XPath syntax for selecting the node
- Security Enhancements: rate limiting for the Test email feature and Upgraded third-party libraries for improved security

  - Qt v6.9.1
  - Angular v19
  - Angular library ag-grid-angular v34.0.0

## [Version 5.10.0](/docs/mdicap/release-notes/changelog#version-5100)

Enhancement and new features:

- Webhook Scanning Out of BETA
- New Operating System Support:

  - Windows Server 2025
  - Oracle Linux 9.5
- User Management via My OPSWAT Central Management API Endpoints
- Email Notification Continuous Enhancement: extended settings for email notifications, including:

  - CPU and RAM usage notifications
  - Certificates expiration notifications
  - Configurable recipient lists based on filters for blocked scan requests
- CIS Level 2 Support for Linux: supports CIS Level 2 system hardening benchmarks for Linux operating systems
- Security Enhancements: Upgraded third-party libraries for improved security

  - Libxml2 v2.14.5
  - Brotli v1.1.0
  - yaml-cpp v0.8.0
  - SQLite v3.50.2
  - **Removed:** 7z library
- Usability Improvements:

  - Added the status of mdicapsrv_engineprocess (for the File Type engine) to health check response
  - Added support to override X-include header in OPTIONS response (specifically for GlobalScape integration)
  - Upgraded the File Type engine bundle to latest version v7.5.0.
  - taDefender Core integration enhancements
  - Added Acknowledgement button in the UI to confirm the clean up of all processing history

## [Version 5.9.0](/docs/mdicap/release-notes/changelog#version-590)

Enhancement and new features:

- Allow List by File Type Per Workflow
- New UI for Downloading Support Packages
- Email Notification Enhancement:

  - MetaDefender Core connectivity with MetaDefender ICAP Server
  - Hard disk usage exceeding defined threshold
- CIS Support for Linux: Supports CIS Level 1 for Ubuntu 22.04, 24.04 and RHEL 9
- Security Enhancements: Upgraded third-party libraries for improved security:

  - `libxml2` 2.13.8
  - `PostgreSQL` 16.8.0
- Usability Improvements

  - Filter workflows based on request body size
  - Support for using Basic Authorization to override usernames in Processing History
  - Enhanced speed for UDP syslog server via DNS name caching
  - Export/import configuration per workflow
  - Automatic license synchronization and updates with Activation Server

## [Version 5.8.0](/docs/mdicap/release-notes/changelog#version-580)

Enhancement and new features:

- New OS support: Rocky Linux 9
- Support user login for nested AD groups
- Email notification: notification about license
- Security enhancements: Upgraded third-party libraries for vulnerability fixes
- Support secure TCP syslog
- Usability enhancements/changes:

  - Support Active Directory Domain Controller
  - Download the User list under User Management
  - Support custom scope and keys for OIDC mapping (prior support mapping was from given keys only)
  - Support the flag to disable revocation server checking in case TLS is enabled on Windows in offline or environment which is protected by firewall/proxy (the flag: global/curlsslopt_revoke_best_effort)
  - Add more options for decoding base64 content encoded (e.g: data is not base64 data), Block/Scan without Decoding or Allow request without scan) - Default option will be Blocked.
- Bug Fixes:

  - ICAP parser did not allow custom http method on MD ICAP v5.7.0
  - Fixed crash issues in cases: Unenroll to OCM incase very highloading and Receive many empty files when data tricking enable
  - Addressed various UI cosmetics issues and minor bugs

## [Version 5.7.0](/docs/mdicap/release-notes/changelog#version-570)

Enhancement and new features:

- Continuous support for My OPSWAT and Central Management v8 integration: Dashboard and processing history
- Enhance processing of base64 encoded data which is embedded in common data format (SOAP/JSON/Form URLEncoded ):

  - Beside SOAP/JSON format, MD ICAP Server v5.7.0 has already supported extracted and scanned base64 data which is embedded in FORM URL Encoded
  - Able to select the node/path to specific the file name for Base64 data, this will help trace back the scan data at MD Core side more easier
  - Support configure to select scan all base64 data in array at once (use "*"), instead of configure each node one by one
- Upgrade Bundle PostgreSQL to v16.x (need check this document carefully before upgrade: <https://www.opswat.com/docs/mdicap/installation/upgrade-to-version-5-7-0>)
- Override some values of processing history and configurable the metadata send to MD Core
- Security enhancements: Upgraded third-party libraries for vulnerability fixes (Curl, Qt, Npgsql, PostgreSQL, Angular)
- Usability enhancements/changes:

  - Enhance the license management to align with new update of On-Premises License Management Server (OLMS).
  - Added smaller options to Data Retention settings
  - Support 2 new service paths for Globalscape's EFT integration
  - Support new content encoding: zstandard - zstd

## [Version 5.6.0](/docs/mdicap/release-notes/changelog#version-560)

Enhancement and new features:

- Continuous support for My OPSWAT and Central Management v8 integration:

  - Workflow Rules
  - Inventory (Server profiles and block pages configuration)
  - Global Settings
  - Data Retention
- PostgreSQL 15 remote support
- Security enhancements:

  - Upgraded third-party libraries for vulnerability fixes (OpenLDAP, Libxml2, PostgreSQL)
  - Front-end enhancements:

    - Hardened the Strict Transport Security header (HSTS)
    - Disabled auto-fill password on login page
- Docker enhancements: Introduced new settings for the On-Premises License Management Server (OLMS) proxy
- Discontinued support for Windows Server 2012 and Debian 9
- Login banner: Added the ability to display a custom notice during the login process

Fixed issues:

- Product stability improvements:

  - Resolved a memory leak issue in version 5.5.1 when activated by OLMS.
  - Fixed an issue that prevented connection to remote PostgreSQL v14 on Windows.
  - Fixed an issue where the same internal PostgreSQL username was generated for MetaDefender Core when using the same remote PostgreSQL server.
  - Fixed an issue causing the loss of processing history during upgrades on newer versions of Kubernetes (K8S)

## [Version 5.5.1](/docs/mdicap/release-notes/changelog#version-551)

Enhancement and new features:

- MetaDefender ICAP Server now supports users to control proxy setting for the product via UI setting, and also proxy authentication is supported
- Provide a way to filter requests based on request URL
- Security enhancements:

  - Strengthen the product security to use strongest cipher AES_256_GCM to encrypt sensitive data on PostgreSQL database.
  - Increase minimum password length enforcement to 30 characters.
- Logging improvements:

  - New configuration to collect system resource information on server where MetaDefender ICAP Server resides for Splunk integration, instead of using Splunk Universal Forwarder.
- Performance improvements:

  - Improved system resources utilization better.
  - Enhanced scan result polling mechanism against MetaDefender Core.

Fixed issues:

- Fixes on product stability issues:

  - “Scan Server Became Unreachable” setting mistakenly became unchecked after upgrading from MetaDefender ICAP Server version 5.2.0 to 5.5.0.
  - Failed to create SAML user directory.
  - Failed to connect and setup email server when using system proxy configuration (via environmental variable).
  - Base64 decoding could be incorrect when data length is not a multiply of 4
  - Correct decoding for malformed base64 data whose length is not multiple of 4.

## [Version 5.5.0](/docs/mdicap/release-notes/changelog#version-550)

Enhancement and new features:

- Processing files with MetaDefender Cloud
- New high availability option for Server Profile
- Security improvements: Upgraded 3rd party libraries for vulnerabilities (Zlib, PostgreSQL, LibXML, Xerces-c, OpenSSL)
- Logging improvements: More comprehensive logs for Splunk application integration

Fixed issues:

- Failed to integrate with AD FS OpenID Connect due to missing user_endpoint URL.

## [Version 5.4.0](/docs/mdicap/release-notes/changelog#version-540)

Enhancement and new features:

- Block page various enhancements
- Continuous NGINX integration enhancement
- UI Update

Fixed issues:

- Unable export processing history to CSV file
- Some UI cosmetics and minor bugs are addressed.

## [Version 5.3.0](/docs/mdicap/release-notes/changelog#version-530)

Enhancement and new features:

- Support SOAP/JSON message with Base64 embedded data
- Support new OS Version: Ubuntu 22.04, Red Hat/Cent OS 9
- provides a new UI accessibility mode to support accessibility view (disabled by default)
- Upgraded 3rd party libraries for vulnerabilities (NGINX, Curl, Angular, Zlib)

Fixed issues:

- Encountered when multiple AD servers are added, and the first AD server failed to authenticate user
- Some UI cosmetics and minor bugs are addressed.

## [Version 5.2.1](/docs/mdicap/release-notes/changelog#version-521)

Enhancement and new features:

- Integration with My OPSWAT portal
- Host-name based search for the processing history page
- Health check API based on MetaDefender Core workflow
- Other functionality updates

  - Support Deep CDR analysis mode (only when enabled on MetaDefender Core)
  - Like IP addresss, now server domain is also supported for webhook_callback setting
  - Synchronize to display according scan verdict from MetaDefender Core.
- Oher UI updates: Some minor cosmetic UI updates for the processing history page.

Enhancement and new features:

- PostgreSQL data missed in the support package on Windows
- SYSTEM user directory was mistakenly removed

## [Version 5.2.0](/docs/mdicap/release-notes/changelog#version-520)

Enhancement and new features:

- New Database Management System (PostgreSQL) to replace SQLite
- Support to handle Proactive DLP-processed files
- Security enhancements

  - Upgrade 3rd party dependencies: Curl 8.1.2 (formerly 8.0.1)
  - Set default TLS version 1.3
- Support setting to allow traffic if MetaDefender Core is down
- Single Sign On - Azure ODIC enhancement: Use logged-in user information from ID token (in JWT format) from authorization endpoint instead of UserInfo endpoint.
- Options-TTL for OPTIONS method: A new option to enable/disable Options-TTL header in response for OPTIONS command (supported to integrate with Oracle ZFS)
- Licensing with On-prem License Management Server (OLMS): New licensing management model for MetaDefender ICAP to allow On-prem license management server (to be released) to manage the product's license status including activation, deactivation.
- Correct display ICAP duration on UI display

Fixed issues:

- Webhook callback: if respond body from Metadefender Core contain character "< >" then MD ICAP Server will not receive the callback
- Enhancement on ICAP connection with MetaDefender Core: Keep number of sockets steadily while working with MetaDefender Core to allow running out sockets on system.

## [Version 5.1.1](/docs/mdicap/release-notes/changelog#version-511)

Enhancement and new features:

- Security hardening: As a regular security practice, we upgraded 3rd party dependencies and development framework to prevent critical vulnerabilities (Upgraded OpenSSL 3.0.8, Upgraded Curl on Linux 7.88.0, Upgraded Protobuf 3.21.11)
- Add more setting option about Session policies in Setting > Security

  - Toggle (switch on / off) for duplicate sessions enablement.
  - Toggle (switch on / off) for cross IP sessions enablement.
- Add health check API
- Allow search by the user in User Management

Fixed issues:

- MetaDefender ICAP Server v5.1.0 can not connect to MetaDefender Core when enabling TLS secure connection. on Debian OS
- Product stability improvement

  - Improve search users result with special character input (e.g: "+").
  - Import/export feature.

## [Version 5.1.0](/docs/mdicap/release-notes/changelog#version-510)

Enhancement and new features:

- Support NGINX integration: A NGINX dynamic module (OMetaScan NGINX module) to integrate MetaDefender ICAP Server with your existing NGINX web server.
- Enhance the OceanStor integration :
- Support Huawei OceanStor Dorado All-Flash Storage & Huawei OceanStor Hybrid Flash Storage
- New feature: move blocked files to quarantine path
- User Name can be displayed on ICAP History for Filemod
- The exported JSON configuration file can be encrypted and protected with password.
- As a regular security practice, we upgraded 3rd party dependencies and development framework to prevent critical vulnerabilities

Fixed issues:

- fix product UI: Only the fist page of LDAP user list was displayed.
- Log override feature did not work on Windows.
- Database vaccum failed on docker container environment.
- Potential XSS/HTML injection on the product UI features.

## [Version 5.0.0](/docs/mdicap/release-notes/changelog#version-500)

Enhancement and new features:

- A brand-new UI for the management console, which was designed with the focus on the quality and thoughtfulness of the user experience. The new administrative console UI provides an advanced set of MetaDefender ICAP Server features.
- Applicable to local users, support to recover user credentials via a new forgot-password feature
- Import/export config feature improvement (Support for the email configuration setting and Resolved misleading error message under certain circumstance)

Version 4.13.0

Enhancement and new features:

- Docker container support for Linux base environment (CentOS / RedHat, Ubuntu / Debian)
- Helm chart and configuration support on Kubernetes environment
- Supports authentication using SSO with widen integration coverage for most of Identity Providers (IDP) via SAML 2.0 and OpenID Connect 1.0 standard support.
- 3rd party vulnerabilities check and remediation.
- Fixed UI display corresponding the setting.

Fixed issues:

- Prevented Cross-Site Scripting (XSS) attack vulnerability via the blocked page response. Details: CVE-2022-40778
- Under high load circumstance with the local scan mode, temporary files could not be cleaned up properly due to being locked by MetaDefender Core.
- Lookout time and number of failed logins before lookout
- Minor UI fixes

## [Version 4.12.2](/docs/mdicap/release-notes/changelog#version-4122)

Enhancement and new features:

- Update the range input of Idle timeout and absolute session
- Add flag "notify_modified_ custom_header"

Fixed issues:

- Fixed issue of QTcpServer become unresponsive when client which are connected to it ungracefully close the socket repeatedly
- Fixed crash issue when webhook mode is used

## [Version 4.12.1](/docs/mdicap/release-notes/changelog#version-4121)

Enhancement and new features:

- Session timeout setting
- Custom ICAP request header

Fixed issues:

- Security vulnerability: Fixed some security vulnerabilities on the product.

## [Version 4.12.0](/docs/mdicap/release-notes/changelog#version-4120)

Enhancement and new features:

- Official support new OS version (CentOS: 8.x; Red Hat Enterprise Linux 8.x; Debian 10.x, 11.x; Ubuntu 18.04, 20.04)
- Password policy options for the admin UI
- Security enhancement

  - Supported TLS 1.3 for HTTPS connection
  - Enhanced HTTPS with new appended secured headers for the product management console UI: Content-Security-Policy, Strict-Transport-Security, X-Content-Type-Options.
  - Upgrade OpenSSL to 1.0.2u for potential vulnerabilities on Windows.
  - New configuration supported for toggling on certificate's name against host verification.
- Log enhancement

  - Added client IP address info to mdicapsvr.log scan entries.
  - Write to separate file feature coming with log rotation is enabled by default on Windows.
- Startup time improvement: MetaDefender ICAP Server startup is now faster even when its database size is big.

Fixed issues:

- MetaDefender ICAP Server was not working if Nginx installation folder in configured custom path start with "n" character
- MetaDefender Core API key on Core URI configuration was lost when adding MetaDefender Core during ICAP server configuration wizard.

## [Version 4.11.1](/docs/mdicap/release-notes/changelog#version-4111)

Enhancement and new features:

- Import/Export configurations
- UI enhancements

  - In Server Profiles, added warning message when putting a new MetaDefender Core URL address without workflow rule selected.
  - Message polished for unexpected result while adding additional MetaDefender Core server in Server Profiles

Fixed issues:

- In-use HTTPS/ICAPS certificate was removed
- Handling credentials information in log
- New user directory failed to create under certain circumstance
- UI issues fixed

  - Activating wrong license key exposed with misleading error message
  - Only applicable while browsing MetaDefender ICAP server management console in OPSWAT Central Management UI: Server profile data could not be displayed randomly

## [Version 4.11.0](/docs/mdicap/release-notes/changelog#version-4110)

Enhancement and new features:

- Webhook callback mode (BETA)
- Data querying and searching speed improvement
- JSON scan result response back to ICAP client
- New setting for max number of connections accepted by ICAP server
- New setting for unique URI assigned for each ICAP service (REQMOD, RESPMOD)

## [Version 4.10.1](/docs/mdicap/release-notes/changelog#version-4101)

Enhancement and new features:

- Upgrade nginx to version 1.20.1
- Calculate the DURATION more accuracy and add IDLE DURATION

Fixed issues:

- Intermediate certificate stripped out issue
- Missing data in temp file when generate support package

## [Version 4.10.0](/docs/mdicap/release-notes/changelog#version-4100)

Enhancement and new features:

- Database Defragmentation and Optimization

  - When your scan database grows big, it might cause performance degradation (e.g. timeout on client requests). Now MetaDefender ICAP Server administrators can be notified on the UI (also warning logs), and you are supported to perform database defragmentation and optimization including multiple stages to vacuum and defrag your database without loss of actual scan data.
  - As a result, your database file size could be reduced which helps boost processing performance tremendously over usage time.
- New search UI and Improved search performance on MetaDefender ICAP processing history page.

## [Version 4.9.0](/docs/mdicap/release-notes/changelog#version-490)

Enhancement and new features:

- Local scan support
- Upgrading MetaDefender ICAP on Windows (Wizard UI)

Fixed issues:

- MetaDefender ICAP service failed with IP version 6 interface disabled
- UI issue when OPSWAT Central Management denied the access

## [Version 4.8.1](/docs/mdicap/release-notes/changelog#version-481)

Enhancement and new features:

- Nginx web server component upgrade
- IPv6 supported for OPSWAT Central Management v7 integration

Fixed issues:

- Error while configuring MetaDefender Core server profile
- Upgrade ICAP server failed with ICAPS setting missing
- The sanitized data could not be sent back to ICAP client
- Bad request occurred with > 4GB file streaming with Dell EMC Isilon OneFS integration
- CONTINUE status is not changed with big file size processing on Windows

## [Version 4.8.0](/docs/mdicap/release-notes/changelog#version-480)

Enhancement and new features:

- FILEMOD method support
- Nginx log rotation option
- Out-of-box ICAP over TLS
- TLS configuration on the UI

## [Version 4.7.6](/docs/mdicap/release-notes/changelog#version-476)

Enhancement and new features:

- Configurable forced ISTag update frequency

## [Version 4.7.5](/docs/mdicap/release-notes/changelog#version-475)

Enhancement and new features:

- Improved handling of encoded filenames

## [Version 4.7.4](/docs/mdicap/release-notes/changelog#version-474)

Enhancement and new features:

- Verbose logging of processing events
- Tuning for better file upload support

## [Version 4.7.3](/docs/mdicap/release-notes/changelog#version-473)

Enhancement and new features:

- Export ICAP History to CSV
- Placeholder for first violation

Fixed issues:

- Multi-part requests blocked
- Server profile details hidden

## [Version 4.7.2](/docs/mdicap/release-notes/changelog#version-472)

Fixed issues:

- Upgrade failure in version 4.7.1

## [Version 4.7.1](/docs/mdicap/release-notes/changelog#version-471)

Enhancement and new features:

- Support for product sets and groups in Central Management

## [Version 4.7.0](/docs/mdicap/release-notes/changelog#version-470)

Enhancement and new features:

- ICAP Server data trickling

Fixed issues:

- Config wizard loading for ever

## [Version 4.6.1](/docs/mdicap/release-notes/changelog#version-461)

Fixed issues:

- There were some broken links in the user guide page [F5 BIG IP SSL configuration](https://onlinehelp.opswat.com/icap/F5_BIG_IP_SSL_configuration.html)
- *Product schema is invalid* error when adding ICAP Server to Central Management

## [Version 4.6.0](/docs/mdicap/release-notes/changelog#version-460)

Enhancement and new features:

- Permissive parsing to accept space in header names
- Support additional placeholder tokens in the block page
- Rules to support filtering by the ICAP client (proxy)

## [Version 4.5.0](/docs/mdicap/release-notes/changelog#version-450)

Enhancement and new features:

- Added support for ICAP preview functionality
- [Permissive parsing](/docs/mdicap/configuration/other-settings) now accepts HTTP requests/responses without HTTP version
- Syslog messages can be [configured](/docs/mdicap/configuration/configuration-file) to use the server's local timezone
- Added an option to enforce an enhanced password policy to [local user directories](/docs/mdicap/configuration/user-management)
- Number of all and displayed requests are shown in the ICAP history
- Improved history loading and service starting time

Fixed issues:

- Content-Length header was missing from blocked responses
- Fixed some minor issues on the default block page

## [Version 4.4.0](/docs/mdicap/release-notes/changelog#version-440)

Enhancement and new features:

- Added additional pages to wizard for easier setup of the product
- Added a more advanced filtering to the history pages next to the basic [search](/docs/mdicap/operating/history-search)
- Welcome wizard now allows creating user with the name "admin"
- Added a bypass option for general Core errors
- Added an option for requests with not supported encoding or decoding error to be scanned as it is

Fixed issues:

- Decreased severity of " An error occurred during writing response" log message from warning to debug
- Security rules could disappear after service restart if a server profile was deleted which was used in an already deleted security rule
- Updated texts and URLs in the default block page's footnote

## [Version 4.3.1](/docs/mdicap/release-notes/changelog#version-431)

Fixed issues:

- Improved temporary directory creation as it could fail on Windows when there were 256 directories present at the same time

## [Version 4.3.0](/docs/mdicap/release-notes/changelog#version-430)

Important features:

- Introduced welcome wizard
- Batch scanning functionality of MetaDefender Core is used when handling multipart requests

Enhancement and new features:

- Added wildcard (globbing) support for Host and Client IP matching in [Security rules](/docs/mdicap/operating/security-rules-policy)
- Added support for [Layer 7 load balanced Core](https://onlinehelp.opswat.com/corev4/9.5.1._HTTP(S)_-_Layer_7_load_balancing.html)
- Added an [option](/docs/mdicap/configuration/configuration-file) for skipping scanning parts in a multipart request where the Content-Disposition header does not contain a filename parameter

Fixed issues:

- Windows event log source was changed to "Metadefender ICAP Server" from the incorrect "Metadefender ICAP"
- Support package didn't remove every temporary file when cleaning up

## [Version 4.2.3](/docs/mdicap/release-notes/changelog#version-423)

Fixed issues:

- Results were missing from the ICAP history

## [Version 4.2.2](/docs/mdicap/release-notes/changelog#version-422)

New features:

- Parallelized processing of multipart requests

Fixed issues:

- Central Management connectivity fix

## [Version 4.2.1](/docs/mdicap/release-notes/changelog#version-421)

New features:

- Re-interpreted, fresh look and feel
- Central Management connectivity

## [Version 4.2.0](/docs/mdicap/release-notes/changelog#version-420)

New features:

- Support deflate encoding / compression
- Configurable timeout for request scans
- Do not send oversized requests to Core
- Display IPs that are counted for license
- Search for keywords in ICAP history URIs
- Display blocked requests on the chart

Fixed issues:

- Read-only users can't view inventory

## [Version 4.1.1](/docs/mdicap/release-notes/changelog#version-411)

Fixed issues:

- Option to capture traffic of bad requests
- Option to use more permissive parsing

## [Version 4.1.0](/docs/mdicap/release-notes/changelog#version-410)

New features:

- Core load balancing and high availability
- Option to override blocking oversized files
- Detailed error messages in block page
- Detailed error messages in ICAP history

## [Version 4.0.3](/docs/mdicap/release-notes/changelog#version-403)

Fixed issues:

- License option for unlimited number of clients

## [Version 4.0.2](/docs/mdicap/release-notes/changelog#version-402)

Fixed issues:

- Blocking page is not configurable

## [Version 4.0.1](/docs/mdicap/release-notes/changelog#version-401)

Fixed issues:

- Upgrade clears all data

## [Version 4.0.0](/docs/mdicap/release-notes/changelog#version-400)

New features:

- Standalone product offering
- Support for multiple Linux distributions
- Web based user interface for management, configuration and monitoring
- Role based user management with multiple admin users and Active Directory integration
- Multiple ICAP security policies with filters and advanced scan configuration
- Different policy filter settings based on source client, destination host, or any other header
- Multi-part (MIME) sanitization
- Support for base64, brotli and gzip encoding
