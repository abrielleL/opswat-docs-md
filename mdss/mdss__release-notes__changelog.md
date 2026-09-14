<!-- source: https://www.opswat.com/docs/mdss/release-notes/changelog -->

# Changelog

## [MetaDefender Storage Security v4.4.2](/docs/mdss/release-notes/changelog#metadefender-storage-security-v442)

Release Date: May 14, 2026

Version supported until November 14, 2027

| Maintenance Release |
| --- |
| - **SFTP scan reliability.** Fixed an issue where SFTP scans could fail with repeated connection errors against servers that limit concurrent sessions. - **Windows upgrade from v3.6.1 and v4.4.0.** Fixed a crash during the MongoDB migration step that blocked Windows upgrades to the latest version. - **Offline toolkit package.** Fixed the offline installer so air-gapped deployments include all required components and the platform service starts as expected.   **Maintenance Release (v4.4.1)**   - **NGINX security update.** Updated NGINX to 1.31.0, which patches [CVE-2026-42945](https://nvd.nist.gov/vuln/detail/CVE-2026-42945). Previous MDSS versions are not affected by this CVE; the update ships as a precaution. - **RTP validation for circular remediations.** Real-time scans now reject workflows whose move or copy remediation targets the same storage unit being scanned, preventing the retry loop seen previously. - **Additional S3 region.** Added the New Zealand (ap-southeast-6) region to the AWS S3 and S3-compatible storage selectors. - **Reduced error log noise.** Cleaned up spurious error log entries from background job cleanups and certain file-download failure paths. |
| **Highlights**   - **New Storage Integration: Scality RING -** Added native integration for Scality RING S3-compatible object storage, with full coverage for multiscanning, CDR, DLP, file tagging, and remediation actions. - **Azure Blob storage autodiscovery.** Azure Blob accounts can now automatically discover and onboard new containers as they are created. Container selection can be fully automatic or scoped to a manual subset, and the feature can be toggled per account. - **Access Control (ABAC Phase I).** New Settings → Access Control tab showing default roles and their permissions. - **Real-Time Processing start date.** Added an optional "Pick files modified since" date picker to the RTP scan modal, so older files (e.g., OneDrive uploads that retain their original `LastModified`) can be included in the scan. - **Scan size visibility.** Individual scan reports and active scans now show `Total Files Size` and `Processed Files Size`, and `Total Files Count` is back in the report view. - **Users included in config export/import.** Configuration export can now optionally include MDSS users (local and SSO), with matching users reconciled on import. |
| **Improvements**   - **Scan reliability and gRPC performance.** Reused gRPC channels across NFS/SFTP discovery, object operations, and telemetry to prevent port exhaustion; added watchdog timeouts and retries to prevent stuck scans and stuck remediations; fixed timing edge cases that could mark instant scans complete prematurely; and added parallel consumers on non-priority RPC queues for better authentication throughput. - **Logging and diagnostics.** Added a separate error/warning log file with its own rotation, persisted PostgreSQL/Redis/RabbitMQ logs across container restarts, identified the specific MD Core instance in API key failure logs, and clarified the support package export error around `LOGS_PER_SERVICE`. - **Cancel on-demand scans from Reports.** On-demand scans can now be cancelled directly from the Reports tab, matching the existing RTP cancel behavior. - **Persistent service scaling.** Extra service instances can now be configured in `customer.env` and survive upgrades. - **Discovery throttling for Discovery-Only scans.** Added configurable queue-depth-aware throttling so Discovery-Only workflows back off when downstream queues are saturated and resume once they drain. - **Scan reliability guardrails.** Scans no longer get stuck on slow storage or remediation, and instant scans now wait for discovery to actually finish before reporting completion. - **Workflow display in scan details and reports.** Active scan details now show only the currently running workflow, while reports keep the full workflow history with a clearer "current vs. previously used" layout. - **Adaptive Analysis status accuracy.** Adaptive Analysis and Sandbox now show "Skipped" (not "Failed") when MD Core skipped the file, and clean verdicts display a green badge. - **Adding storage no longer auto-starts a full RTP scan.** New storage units are created without an automatic RTP scan, so the Reports view stays clean until you explicitly start one. - **Delete RTP scans from Reports.** RTP scans (including partition scans) can now be deleted from the Reports page, not just cleaned, with support for bulk and mixed-type deletion. - **Timestamps and cleaner messages on RTP errors.** Expanded error details now show when each error occurred and present a friendlier message without raw stack traces. - **Upgrade reliability.** Fixed Windows upgrades silently overwriting `customer.env`, and restored RTP partition scans that stopped working after upgrading to 4.3.0. - **Stability at scale.** Reduced Garnet memory usage on Windows and fixed a service crash triggered by a large number of scans in the database. - **Integration fixes.** Resolved a SharePoint Online issue where slow Graph subscription creation prevented RTP from starting, and blocked the same GCP bucket from being added twice through different credential types (ADC vs. keys). - **Dependency upgrades.** Upgraded RabbitMQ to 4.2.4, Redis to 8.6.0, and Garnet to 1.0.99. |

Info - Upgrades from v4.3.0 or earlier

**RTP behavior during upgrade.***This applies when upgrading from any version older than v4.3.1. Customers already on v4.3.1 or later are not affected.*

Active RTP scans are paused during the upgrade and resume automatically once it completes. Files added or modified during the upgrade window can be picked up by running an RTP report cleanup afterward with [RTP Handling with Comprehensive Detection](/docs/mdss/configuration/real-time-processing-configuration-for-nas) enabled. On NAS storage units this cleanup reprocesses all files and may take some time depending on volume.

## [MetaDefender Storage Security v4.3.2](/docs/mdss/release-notes/changelog#metadefender-storage-security-v432)

**Release Date: April 03, 2026**

**Version supported until: October 03, 2027**

**Highlights**

**Workflow Cards: Storage Unit Destination**

- Workflow cards now show which storage units are set as destinations for remediation actions, so you can quickly see where your data ends up.
- **How to enable:** Navigate to Workflows and select Extended View from the top right.

**Improvements**

- Certificates are now picked up automatically after a machine restart, without requiring a product restart separately.
- Fixed a race condition during Podman restarts that previously caused orphaned containers running in the background.

## [MetaDefender Storage Security v4.3.1](/docs/mdss/release-notes/changelog#metadefender-storage-security-v431)

**Release Date: March 06, 2026**

**Version supported until: September 06, 2027**

**Improvements**

- Resolved issue that malformed scanning paths for active RTP scans and Scheduled Scans, that target partitions, on FTP, NFS, SFTP, SMB, and SharePoint On-Premise storage units
- Resolved issue that forced RTP scans on NAS storage units to reprocess files processed before upgrade

## [**MetaDefender Storage Security v4.3.0**](https://www.opswat.com/docs/mdss/release-notes/changelog#metadefender-storage-security-v430)

**Release Date: March 05, 2026**

**Version supported until: September 05, 2027**

This release introduces Microsoft Teams support for enhanced collaboration security, auto-discovery for SharePoint Online to streamline setup, a new reprocess failed files feature for easier remediation, stability improvements, and concurrent scanning scenarios.

**Highlights**

- **Multitenancy (MDSS Cloud)**

  - Support for multiple tenants within a single MDSS Cloud deployment
- **OpenTelemetry (Initial Release)**

  - Collect and export telemetry data for monitoring and observability
- **Microsoft Teams Scanning**

  - Scan and sanitize file attachments shared in Microsoft 365 Teams channels and chats
- **SharePoint Online Auto-Discovery**

  - Automatically discover and connect SharePoint Online sites—no manual configuration required
- **Reprocess Failed Files**

  - Create new scans targeting only previously failed files, with the flexibility to apply any workflow
- **Flexible Scan Scheduling**

  - Schedule scans down to the minute for precise timing control
- **Real-Time Protection Limits (Cloud)**

  - Configure scan limits for MDSS Cloud deployments to manage resource usage

**Improvements**

- **Scan Priority UX**

  - Added tooltips and reordered priority options for clearer configuration
- **Storage Unit Display**

  - Storage unit name now visible in scan configuration for easier identification
- **Sanitization Workflow Control**

  - Original files deleted only after successful sanitization. New option to configure delete behavior separately for allowed and blocked files—enabling workflows like Deep CDR for blocked files only while leaving clean files untouched
- **Connection Reliability**

  - Automatic retry on temporary connection failures
- **Performance**

  - Loading indicator on download button when generating large scan reports
- **Report Export UX**

  - Faster remediation processing for large-scale deployments
- **SMTP Configuration**

  - Input validation for host field with helpful error messages for invalid entries
- **SharePoint Storage Units**

  - Cloud and On-Prem storage units now use Site URL and Document Library URL fields. Existing configurations remain compatible, with a post-upgrade prompt to update
- **Bug Fixes & Documentation**

  - Fixed authentication failures when running multiple SMB scans simultaneously
  - Resolved partition scan errors across all users
  - Reports now correctly deleted only after retention period expires and only for completed scans
  - Notification imports now save valid settings even when some notification types fail validation
  - Updated documentation to reflect recent changes that include UI, windows installs, API keys, and scan reprocess actions.

## [**MetaDefender Storage Security v4.2.0**](https://www.opswat.com/docs/mdss/release-notes/changelog#metadefender-storage-security-v420)

**Release Date: December 15, 2025**

**Version supported until: May 25, 2026**

MetaDefender Storage Security 4.2.0 delivers significant enhancements to cloud integration, identity scanning capabilities, and workflow automation, alongside critical stability improvements and bug fixes.

**Highlights**

- **GCP Autodiscovery**

  - Automated bucket discovery for Google Cloud Platform
- **Oracle Cloud Enhancements**

  - Improved support for Oracle Native while keeping its S3-compatible storage configurations
- **Cross Domain**

  - Compliant data transfer across classification domains for high-security environments of workloads with isolated toxic handling, RabbitMQ-orchestrated processing, and webhook-based discovery
- **Identity Detection**

  - Identity detection across backup filesystems with PDF reporting and remediation integration. Supports on-demand and scheduled scans with intelligent incremental scanning. Real-time processing (RTP) not supported.
- **PDF Report Enhancements**

  - Improved file distribution visualization, enhanced tooltips, and identity scan results inclusion
- **PostgreSQL Optimization**

  - Resolved stability and performance issues for large-scale deployments

**Improvements**

- Discovery workflow execution and event-based scanning capabilities
- Advanced file versioning support and remediation workflow performance
- Optimized FTP connection pooling and file discovery mechanisms
- Enhanced MDSS Cloud rate limiting and tenant administrator access controls
- Improved SharePoint OnPrem workflow persistence
- Robust storage account validation and credential management
- Advanced password security in account management interfaces
- Refined form validation for account creation and RabbitMQ configuration
- Improved UI responsiveness and rendering performance across viewing contexts
- Streamlined onboarding experience and intelligent default behaviors
- Enhanced file distribution visualization and reporting accuracy
- Comprehensive RabbitMQ validation, audit logging, and notification delivery
- Refined SMTP lifecycle management
- Improved webhook configuration interface and user guidance
- Optimized database operation efficiency during export operations

## [**MetaDefender Storage Security v4.1.0**](https://www.opswat.com/docs/mdss/release-notes/changelog#metadefender-storage-security-v410)

**Release Date: September 23, 2025**

**Version supported until March 23, 2027**

**Highlights**

- **Sandbox Analysis Integration**

  - Full sandbox analysis capabilities with MITRE technique mapping and threat intelligence dashboard integrated with MD Cloud and MD Core deployments for advanced threat detection.
- **Storage Management Redesign**

  - New dual view modes (Groups and Accounts) for organizing storage units with comprehensive account-level operations including editing, deletion, and bulk scanning capabilities.
- **HTTPS Configuration**

  - Enable HTTPS directly through the Security settings interface with real-time certificate validation and clear error messages, eliminating lengthy timeout periods.
- **Enhanced Real-Time Protection**

  - Configure multiple RTP scans for different partitions within the same storage unit for all scanning configurations per partition.
- **SharePoint Historical Versions**

  - Scan all historical versions of SharePoint files, not just the latest version, ensuring comprehensive security coverage across file version history.
- **Multiple Workflow Destinations**

  - Configure up to 5 copy/move destinations in workflow remediations

**Improvements**

- **User Interface**

  - Form consistency across SMB/SFTP and FTP configurations with interactive guided tour for new users
  - Enhanced inline notifications with auto-scroll functionality and completely rebuilt audit system with improved filtering
- **Integration & Connectivity**

  - FTP storage protocol support
  - Enhanced SFTP ports beyond port 22
  - Individual file webhooks for real-time integration and secure syslog transmission with TLS support
- **Security & Platform**

  - Streamlined licensing without legacy SKUs
  - Workflow processing without multiscanning requirements
- **Reporting & Analytics**

  - Enhanced PDF reports with new file statistics and detailed remediation information
  - Proper handling of files with successful scans but failed remediations
- **Bug Fixes & Documentation**

  - Resolved audit expand functionality, filtering issues, and file path handling improvements
  - Comprehensive API documentation updates and myOPSWAT setup instructions

This release focuses on advanced threat detection capabilities and storage management flexibility while enhancing security and user experience across the platform.

## [**MetaDefender Storage Security v4.0.1 (Hotfix)**](/docs/mdss/release-notes/changelog#metadefender-storage-security-v401-hotfix)

**Release Date: August 25, 2025**

**Version supported until February 25, 2027**

- SMTP Re-activation Issue

  - Fixed a critical functionality bug where SMTP service could not be re-activated after being deactivated, rendering email notifications permanently unusable until system intervention.
- Database Migration Report Recovery

  - Resolved issues where scan reports became inaccessible after upgrading from previous versions (3.5.1/3.6.1), particularly affecting canceled scans and PDF export functionality during database migration processes.
- **Multi-tenancy Filter Disabled for MDSS Cloud**

  - Temporarily disabled PostgreSQL tenant ID filtering for cloud deployments as the multitenancy feature is not yet complete, preventing authentication and permission issues for Tenant Admin users until proper tenant configuration is implemented.

## [**MetaDefender Storage Security v4.0.0**](/docs/mdss/release-notes/changelog#metadefender-storage-security-v400)

**Release Date: August 12, 2025**

**Version supported until February 12, 2027**

**Highlights**

- Migrated from MongoDB to **PostgreSQL 17** to align with MetaDefender Core and ICAP Server. This simplifies deployments and improves performance for complex queries and large datasets.
- The new **Workflows** feature creates an automated security processing pipeline:

  - 5-stage security processing: Scan Configuration → Advanced Threats → Vulnerabilities → Sanitization → File Tagging
  - Automatically sorts files into Original, Allowed, Blocked, and Sanitized categories
  - Executes automated actions (Copy, Move, Delete) based on scan results
  - Process thousands of files without manual intervention
- **Security Updates**

  - New account creation and login flows
  - Enhanced encryption key handling and secure key rotation
  - Security patches for known vulnerabilities

**Improvements**

- **Performance**

  - Upgraded RabbitMQ to version 4.1
  - Enhanced SharePoint Cloud real-time processing
  - Custom date range functionality in Dashboard
- **Integration**

  - Upgraded Microsoft Graph SDK to version 5.79.0
  - Added automatic file tagging for Google Cloud Platform
  - Extended AWS regional support
- **Platform**

  - Updated PostgreSQL documentation
  - Improved Azure AD configuration guide
  - Better error handling

This release focuses on database modernization and workflow automation while maintaining platform stability.

---

## [**MetaDefender Storage Security v3.6.1**](/docs/mdss/release-notes/changelog#metadefender-storage-security-v361)

Release Date: May 20, 2025

Version supported until November 20, 2026

**Highlights**

- Streamlined Autodiscovery of S3 Buckets so users can now easily add S3 storage by providing AWS credentials. MetaDefender Storage Security can now automatically discover available buckets, allowing you to enable continuous discovery or manually select buckets for integration via a simplified interface.
- Advanced Remediation Options

  - Configure 'Empty Folder Cleanup' to preserve specific subfolders during parent folder deletion, preventing critical data loss.
- Expanded SharePoint Support

  - Integrate with SharePoint Online Government Cloud (GCC) using a simple configuration checkbox for correct authentication.
  - Discover, scan, and manage content within SharePoint On-Premises subsites, providing comprehensive coverage for hierarchical structures.
- Granular File Rescan so users can rescan individual files directly from scan reports without needing to rescan the entire storage unit or move files, significantly improving efficiency for addressing specific issues.

**Improvements**

- My OPSWAT Central Management Integration: Access My OPSWAT Central Management settings (SMTP, Notifications, License, Data Retention, Syslog) more easily within MetaDefender Storage Security and utilize integrated read-only user roles, including permissions for managing user invitations.
- Improved Error Handling & Feedback: Enhanced API error handling provides more specific, actionable messages (distinguishing connection, permission, config issues) in a standardized format, improving troubleshooting and UI feedback. Added a clearer error message when attempting to add storage without existing scan configurations.
- UI & UX Refinements

  - The MetaDefender Storage Security Cloud UI now hides unavailable integration options for better clarity.
  - Dashboard charts have an improved "no data" state visualization.
  - User Management features backend-powered search with input validation and minor bug fixes.
  - File remediation details are displayed more comprehensively in the UI.
  - The "Manage Storage Unit" interface now allows separate editing of storage settings and underlying account credentials.
- API & Backend Improvements

  - Real-Time Processing (RTP) scan reports now have a default, non-null name for consistent API identification.
  - API key security is enhanced: copying is restricted to the moment of generation, and GET requests for keys are disallowed.
  - The 'Scan Folder' API now prevents conflicts with 'Delete Empty Folders' remediation by returning a `400 Bad Request`.
- Deployment & Scalability

  - The MongoDB database name used by MetaDefender Storage Security is now configurable, supporting external MongoDB instances with predefined names.
  - Improved reliability for scanning large SharePoint On-Premises deployments by managing request rates and using retry mechanisms.
  - Enhanced internal component version identification for cross-platform consistency.
- More Reliable Windows Deployments by reducing failures and simplified setup through preemptive port validation and improved installation configuration.
- Stronger Security & Data Accuracy by ensuring secured MetaDefender Core connectivity (HTTPS) and corrected S3 file tagging for dependable security verdicts.
- Faster Windows Performance & Simpler Stack by improving speed and streamlined dependencies by migrating Windows caching to Garnet.

## [MetaDefender Storage Security v3.6.0](/docs/mdss/release-notes/changelog#metadefender-storage-security-v360)

Release Date: March 31, 2025

Version supported until September 30, 2026

**Highlights**

- MDSS has undergone a major overhaul, featuring a redesigned UI and achieving feature parity with previous versions.
- Users now control scanning priority (performance or thoroughness) for storage unit scans, allowing for tailored resource allocation.
- A real-time processing overview provides immediate monitoring of storage scan activity and a detailed On-Demand Scan Report.
- Users can now cancel the scanning of individual files, optimizing resource management and preventing unnecessary processing.
- Introduced dedicated permissions for Tenant Admins in MetaDefender Storage Security Cloud, enabling granular tenant management without full admin access.
- Users can now specify a OneDrive group, user, and folder location for scanning. This allows for granular security policies and targeted scanning within OneDrive groups. Remediation actions are updated to accommodate group and user specifications.
- The configuration options that are irrelevant (My OPSWAT Central Management integration) are hidden in MetaDefender Storage Security Cloud deployments, simplifying the UI.
- A "Destination Storage for Remediations" section is added to the dashboard, centralizing remediation action visibility.
- Implemented a configurable debouncing mechanism for RTP scans of productivity files (.docx, .xlsx, .pptx) to prevent exceeding MetaDefender Cloud API limits during high-volume live document editing. This applies to the SharePoint Online Integration and provides configurable debounce settings (interval) and information on MDCloud API request limits.
- Storage Units are now editable in My OPSWAT Central Management. My OPSWAT Central Management configuration is simplified with a dedicated modal and active/inactive/loading states, and user management now features sorting and ordering capabilities.
- Remediation data is included in scan details, providing a comprehensive remediation overview.
- The /file API endpoint is updated to retrieve file lists with filtering options. File remediation history is improved by including remediation information in API responses.
- An optional "Delete empty folders after remediation" setting is added for SMB/NFS/SFTP shares, with audit logging of deleted folders.
- Password security is enhanced to Level 1 compliance, the old password requirement is enforced, existing users migrate on change, and strong authentication is maintained.
- Expanded syslog messages now include Data ID, threat details, and comprehensive scan results for improved SIEM integration.

**Improvements**

- The shutdown process for all services is improved for a clean and controlled shutdown.
- Authorization issues with Box Webhooks are resolved with a dedicated endpoint.
- A non-dismissible warning/error message is displayed if the database version is less than MongoDB 6.
- The `privateprocessing` header is added to MetaDefender Cloud scan requests by default, ensuring immediate file deletion from MetaDefender Cloud servers after scanning.

## [MetaDefender Storage Security v3.5.3](/docs/mdss/release-notes/changelog#metadefender-storage-security-v353)

Release Date: 23 January 2025

Version supported until 23 July 2026

This release of MetaDefender Storage Security focuses on enhanced functionality, improved performance, and bug fixes to provide a more robust and efficient security solution for your storage environments.

**Highlights**

- Manage storage units (read-only) remotely via OPSWAT Cloud Management (OCM) with vPack integration.
- Preserve AWS checksum metadata during file transfers between storage locations, including S3-compatible integrations.
- Added support for Hitachi S3, including object deletion without version ID.

**Improvements**

- Significantly reduced scan times for small files on S3.
- Resolved issues impacting S3 scanning, audit log accuracy, and OCM integration.
- Refined the storage unit management interface in OCM for better usability.

## [MetaDefender Storage Security v3.5.2](/docs/mdss/release-notes/changelog#metadefender-storage-security-v352)

Release Date: 18 December 2024

Version supported until 18 June 2026

**Highlights**

- MDSS can now connect with ADFS servers that utilize larger OpenID tokens (over 4KB).
- Windows deployments can now leverage SharePoint OnPrem for storage and remediation actions.
- Move existing storage units between groups with the updated Storage Units API.
- Integrate MDSS with Kafka to streamline external logging, including audit events.

**Improvements**

- The offline package now includes Docker binaries and a dedicated package for seamless offline MongoDB upgrades.
- JSON formatting for console logs allows easier integration with popular log management tools like Corallogix.
- MDSS Cloud now efficiently retrieves sanitized files from MetaDefender Cloud scan pools.
- Database Retention settings documentation has been updated to provide comprehensive information on data segregation, isolation, retention policies, and file handling in S3 and EC2 environments.
- Windows Upgrade Enhancements:

  - MDSS automatically clears RabbitMQ queues upon restart after upgrading from version 3.4.2.
  - The upgrade process now seamlessly handles MongoDB database upgrades from version 6 to 7.

## [MetaDefender Storage Security v3.5.1](/docs/mdss/release-notes/changelog#metadefender-storage-security-v351)

Release Date: 19 November 2024

Version supported until 19 May 2026

**Highlights**

- We've boosted security for cloud deployments with support for AWS PrivateLink, allowing users to connect to MetaDefender Storage Security securely within their Amazon Virtual Private Cloud (VPC)
- Significantly improved performance for remediation tasks, enabling quicker responses to security threats.
- Single Sign-On (SSO) via SAML 2.0 - Business network administrators can now easily integrate with their existing identity providers using SAML 2.0 protocol. This allows for streamlined user authentication and authorization, enhancing security and simplifying access management.

**Improvements**

- We've addressed stability issues affecting SMB on Windows environments
- Users can now use custom URLs for S3 integration, enabling secure access to S3 buckets via AWS PrivateLink.
- We've improved the OPSWAT Cloud Management (OCM) synchronization job to reduce unnecessary configuration downloads and ensure the latest version of the vPack package is always available.
- To improve performance and scalability, we've added data retention settings for real-time processing for large datasets.
- We've added PIN functionality to OPSWAT Cloud Management, ensuring only authorized users can access and modify your configurations.

## [MetaDefender Storage Security v3.5.0](/docs/mdss/release-notes/changelog#metadefender-storage-security-v350)

Release Date: 23 October 2024

Version supported until 23 April 2026

**Highlights**

New Integration: Native NetApp Storage

- New Integration: Native NetApp Storage using the ONTAP connector.
- New Integration: OPSWAT MetaDefender Managed File Transfer (MFT)
- New Integration: Cubbit Storage
- Support for PingFederate as an SSO (single sign-on) provider via OpenID Connect
- Scan management now includes balanced priority queues for real-time processing and instant scans

**Improvements**

- Improved API documentation for some API endpoints.
- Updated the Serilog package to version 4.0.1 to enhance integration capabilities and security.
- Documentation is now available describing the usage of MetaDefender Core and MetaDefender Cloud APIs, including required roles and permissions for correct access.
- Upgraded multiple node packages to enhance security and reliability.

## [MetaDefender Storage Security v3.4.4](/docs/mdss/release-notes/changelog#metadefender-storage-security-v344)

Release Date: 12 September 2024

Version supported until 12 March 2026

This release brings significant enhancements and bug fixes to improve the overall user experience and security of the system. We've focused on enhancing SSO integration and resolved several critical issues, including security vulnerabilities and database errors. We're committed to continuously improving our product and addressing user needs.

**Highlights**

- SSO Integration Enhancements
- Enhanced discovery error handling for improved system stability

**Improvements**

- Resolved stuck files issue where files wouldn't be marked as Failed.
- Addressed NFS issue with non-ascii folder/filenames causing slow scans.
- Restricted services ports accessibility to localhost only, enhancing security.
- Fixed assigned role issue where role changes weren't reflected correctly.
- Resolved issue preventing adding SMB units across network domains.
- Investigated and addressed "Database Operation Failed" errors appearing in logs.
- Upgraded Webpack to version 5.91.0
- Made updates to our licensing system to further strengthen its security and reliability.

## [MetaDefender Storage Security v3.4.3](/docs/mdss/release-notes/changelog#metadefender-storage-security-v343)

Release Date: 21 August 2024

Version supported until 21 August 2026

This release brings major improvements and fixes, enhancing security, integrations, automation, data management, and user experience. Key updates include strengthened security for encrypted files and user-controlled decryption, enhanced integration process with Box, automated folder scanning and webhook notifications for streamlined workflows, improved data management with import/export enhancements, and a more user-friendly experience with onboarding validation and NFS discovery refinements.

**Highlights**

- Added backend APIs for password-protected files, enabling secure scanning and access control.
- Users can now directly enter passwords for encrypted files within the MDSS interface.
- Configurable real-time push notifications for new Box files through Event-Based Real-Time Processing.
- Introducing REST APIs for automating folder scanning and storage management (S3, EFS), enabling users to initiate on-demand scans of any desired folder within their storage.
- Webhook notifications for scan completion, eliminating polling.
- Improved inter-service communication efficiency with enhanced caching.
- Data retention settings are now included in the export configuration.
- Extended filter options for scan reports (by start date).
- Workflow rule validation during onboarding for compatibility.
- Hidden files and folders can now be skipped during NFS discovery.

## [MetaDefender Storage Security v3.4.2](/docs/mdss/release-notes/changelog#metadefender-storage-security-v342)

Release Date: 17 July 2024

Version supported until 17 January 2026

This release brings major improvements and fixes, enhancing performance and usability across the system. Key updates include better configuration handling, storage licensing enforcement, and SMB service stability. We've improved installation messaging, disk space management, and security with Grpc.Core migration. User management and event logging are more robust, and new features like event-based SMB/NFS setup and Mongo 6.0 deployment are included.

**Highlights**

- Database: We deploy Mongo 6.0 database on new installations.
- SMB Service: We fixed out-of-range file descriptors, and addressed files remaining in "Pending" status when moving sanitized files while also ensuring file logging works as expected.
- Windows Native: Fixed the inability to import configuration during onboarding and parametrized the API Gateway port for better support.
- Licensing: Users can no longer add storage if the license is expired or missing.
- Installation and DevOps: Improved clarity of installation failure messages, prevented rapid disk space usage by ensuring that resources are not being consumed while the service is idle.
- Security and User Management: Migrated from the Grpc.Core library and ensured container configuration in production compose files.
- RTP and Scanning: Fixed errors post-upgrade during file processing for RTP (Event-based) and Corrected error messages returned from the scanning API.
- Audit: Corrected double scan delete event records and properly displayed applied post-action information.
- Logging and Notifications: Added logging for error responses in the Storage Service platform and updated email notifications.
- SSO admins can now successfully enable the SMTP server
- Event Based RTP: Introduced event-based SMB/NFS and implemented the Download Connector post-storage setup

## [MetaDefender Storage Security v3.4.1](/docs/mdss/release-notes/changelog#metadefender-storage-security-v341)

Release Date: 14 June 2024

Version supported until 14 December 2025

**Highlights**

- API Key Functionality Expanded Across All REST APIs: We have extended the API Key functionality, initially exclusive to event-based RTP, to cover our entire application. This enhancement allows users to generate and utilize an API Key for all available REST API endpoints, facilitating long-term integrations. We recommend periodically rotating the API Key to maintain security.
- As part of our ongoing rebranding to MetaDefender Storage Security, we have updated the default rule to MetaDefender Storage Security inside MetaDefender Core in all new installations. This change ensures that new users start with the latest configuration tailored to MetaDefender Storage Security.
- We have introduced a new field in the report to clearly mark discovery errors. This field will capture and display all errors when discovery fails due to a general issue, improving transparency and troubleshooting capabilities.
- We have boosted our integration with myOPSWAT by introducing an advanced health status report for our product MetaDefender Storage Security. This new feature enables myOPSWAT to effectively diagnose and report problems within our product, enhancing overall functionality and user experience.
- SSO administrators now have the ability to accept or decline new user invitations, aligning their permissions with those of local administrators. This update ensures greater control and parity in user management across our platform.

**Performance, Security, and Usability Enhancements**

- Discovery Service: We've implemented a fix for the multithreaded access issue in our Redis cache, ensuring enhanced stability and performance for the discovery service.
- We have upgraded RabbitMQ to version 3.13, enhancing performance and stability.
- Box Integration: Improved validation when the specified location does not exist on the remote storage.
- Windows Native: We have made quality of life improvements and enhanced error messaging for Windows Native, aiming to streamline user experience and provide clearer feedback during install operations. Also, we now include the Visual C++ Redistributable (`vc_redist`) with our product, enabling full installation on offline Windows systems without the need for additional downloads. This enhancement simplifies setup and improves accessibility.
- Database Migrations: We've improved the logging mechanisms in `mongo-migrations` to ensure more detailed and effective troubleshooting.
- Added robust error handling for pre and post-process events in remediations, ensuring smoother operation and improved reliability during critical workflows.

## [MetaDefender Storage Security v3.4.0](/docs/mdss/release-notes/changelog#metadefender-storage-security-v340)

Release date: 13 May 2024

Version supported until 13 November 2025

Introducing Windows Native Compatibility for Our Application

**Highlights**

- Windows Native Support
- We are announcing a new integration capability with Oracle Cloud Object Storage (OCI) via AWS SDK: This integration employs path-based access to connect to OCI, accommodating the platform's limitation on not supporting virtual hosted access.
- We've introduced Single Sign-On support for MDSS using Active Directory Federation Services and OpenID Connect, streamlining login processes and enhancing security and user experience for seamless authentication and easier access management.
- Strengthened API Security Enhancements against various security vulnerabilities, ensuring a more secure and reliable environment for our users: Enhanced HTTPS Enforcement, Strict-Transport-Security (HSTS) Implementation, X-Content-Type-Options Header Upgrade, Mandatory Operation Security Field

**Bug fixes/Enhancements**

- Stress Testing Enhancements: Conducted stress tests under heavy load on a machine with 8 cores and 16GB of RAM, where RabbitMQ and MongoDB utilized 25% of RAM, in both AWS and SMB environments.
- Improved Real-Time Processing for NFS: Enhanced Real-Time Protection with Deep Content Disarm and Reconstruction for NFS on Windows shares, improving security performance.
- Streamlined Command-Line Upgrading for MDSS: Updated the command-line upgrade process to consistently display the EULA page, particularly when using clean commands or exporting support packages, enhancing user compliance and experience during upgrades.
- Event Limitation and Scaling Guidance: Implemented an event limitation in the discovery process; the system will pause when it reaches 5,000 events. Users are encouraged to scale up their systems to maintain continuous operation.
- DocumentDB Integration: Successfully integrated our system with DocumentDB, enhancing our database management capabilities.
- Storage Limitation and UI Enhancements for Simpler Deployments: Introduced a storage limitation per instance to prevent overload and added UI warnings for excessive CPU usage, along with a sizing guide to help customers effectively scale their systems.

## [MetaDefender Storage Security v3.3.4](/docs/mdss/release-notes/changelog#metadefender-storage-security-v334)

Release date: 28 March 2024

Version supported until 28 September 2025

Introducing the Wasabi storage integration, Copy Functionality for duplicating files in place, seamless preservation of tags during storage transfers, and enhanced High Availability and Disaster Recovery options for uninterrupted data access across regions.

**Highlights**

- We're pleased to announce that Wasabi is now a supported storage type! Whether you're in search of cost-effective cloud storage solutions or high-performance storage options, integrating Wasabi provides you with a robust and dependable choice for storing your data.
- Introducing Copy Functionality: Now, you can duplicate files while keeping them in their original location, providing enhanced flexibility and control over your data management compared to the previous method of removing files from the source.
- With our latest update, tags remain intact when files are moved between storage locations, safeguarding valuable metadata and ensuring a seamless experience across storage movements.
- We improved the support for High Availability and Disaster Recovery (HA/DR) that enables the selection of a failover scan pool. In the event of downtime in one region's assigned pool, a backup pool from another region seamlessly assumes control, guaranteeing uninterrupted access to your data.

**Bug fixes/Enhancements**

- The Scan Report now includes comprehensive details regarding Document Library and Folder Location within SharePoint, ensuring complete information coverage.
- You can now effortlessly delete duplicated scan configurations after importing them.
- Now, it's no longer possible to remove a scan configuration that is in use, as this issue has been resolved.
- Efficient handling of key name collisions during storage discovery ensures the continuity of the ongoing scan, facilitating completion without hindrance.
- The scan would be efficiently completed within an appropriate timeframe.
- The display of stop time for RTP reports is accurate when the RTP scan has been initiated, ensuring precision in data presentation.

For further details on the steps involved in integrating Wasabi you can access this link [Add A Wasabi Storage](https://www.opswat.com/docs/mdss/integrations/add-a-wasabi-storage).

## [MetaDefender Storage Security v3.3.3](/docs/mdss/release-notes/changelog#metadefender-storage-security-v333)

Release date: 14 February 2024

Version supported until 14 August 2025

With this release, we're introducing NFS storage integration, offering functionality similar to SMB storage.

**Highlights**

- Add, edit, and delete NFS from the Storage unit, with the addition only possible from the onboarding page.
- Validate and add unique units, preventing duplicates, and properly import and export NFS units.
- Start, stop, and restart RTP and retrieve files once while creating/moving/modifying files after starting RTP.
- Initiate, cancel, or modify multiple instant scans, with updated reports for empty files, small files (1K - 1MB), medium files (100MB), and large files (1GB).
- Ensure file scan results display correctly, reflecting MDCore's response and post-actions applied.
- Perform post-actions such as DeepCDR (Keep/Encrypt/Delete original files), moving sanitized/allowed/blocked files to another storage (S3/Box/Azure Blobs), receiving files from another storage (sanitized files from Box/Azure Blobs), and deleting blocked files.
- Implement logging mechanisms to audit NFS-related actions and include NFS services in the logs.
- Improved logging support by allowing extensive configuration and rotation.
- Polling time intervals support configuration.

**Bug fixes/Enhancements**

- Preventing duplicated folder structure for Box.
- Improving the orchestration of the scanning process to address instances of scans becoming stuck.
- Additional checks on the Windows docker service before starting MDSS

You can find more information on the [Add an NFS Storage](https://www.opswat.com/docs/mdss/integrations/add-a-nfs-storage) steps by accessing the hyperlink.

## [MetaDefender Storage Security v3.3.2](/docs/mdss/release-notes/changelog#metadefender-storage-security-v332)

Release date: 21 December 2023

Version supported until 21 June 2025

**Highlights**

- AWS GovCloud (US)
- Client-Side Encryption for S3 buckets
- Performance improvements
- Native Podman support for RHEL 8
- Removed import functionality post-onboarding

  - This change addresses conflicts that occurred when an import was applied to partially configured instances, leading to unexpected behavior and bugs. Import functionality is now restricted to after onboarding, which remains available for use.

**Bug fixes/Enhancements**

- File location on retry
- SMB Connection Caching
- Outdated UI Reports

## [MetaDefender Storage Security v3.3.1](/docs/mdss/release-notes/changelog#metadefender-storage-security-v331)

Release date: 9 October 2023

Version supported until: 9 April 2025

**Highlights**

- Integration with My OPSWAT portal
- Microsoft SharePoint Integration
- Scan Configuration History
- Azure Gov Storage Integration
- MongoDB v6 Migration Guide
- Amazon S3 URL Validity Control
- UI Session Expiration Customization

**Bug fixes**

- Onboarding: Users can now successfully add an MD Cloud instance
- SMB Storage Integration: Resolved an issue by adding an alternative method to check for file uploads in the SMB storage integration
- Addressed an issue related to queries when utilizing Cosmos DB
- Resolved an issue where scans appeared as stuck when processing spanned multiple days

## [MetaDefender Storage Security v3.3.0](/docs/mdss/release-notes/changelog#metadefender-storage-security-v330)

Release date: 13 July 2023

Version supported until: 13 January 2025

**Highlights**

- SFTP Storage integration now available under Network Attached Storage section
- Transitioned Core Pool settings from the storage level to the scan level to enhance flexibility
- Simplified the licensing. With a valid license, access to all storage integrations is now granted.
- Mark unavailable storage units, based on ENABLED_MODULES from environments variable file

**Bug fixes**

- Better Failure Handling**:** We've made improvements to how the system manages failures.
- Introducing an option to set the interval for flagging a file as failed if it gets stuck during processing. Adjust this with the `MARK_STUCK_FILE_AS_FAILED_HOURS` environment variable in the configuration file.
- Significant performance improvements in file discovery.

## [MetaDefender Storage Security v3.2.0](/docs/mdss/release-notes/changelog#metadefender-storage-security-v320)

Release date: 18 May 2023

Version supported until: 18 November 2024

**Highlights**

- Flexible deployments - User has now the ability to deploy only storage services that will be used. This can be done through an environment variable.
- Generic API for storage units - Exposed a generic API (api/storage/) to handle the Add/Edit/Delete operations on storage units.
- Processing indicator improvements - Showing a single progress bar which indicates the overall processing (discovery, scanning and remediations) progress
- Angular 15 update - Migrated the UI to Angular 15. We suggest to clear the browser cache before upgrading
- API for Offline Activation - Removed content encoding when calling /api/settings/admin/license/activate/offline
- System Checks - Added RabbitMQ and Redis details

**Bug fixes**

- Reports Performance improvements - Improved the scan report performance. Added the option to filter by date, improved the search and pagination. Added Refresh button to the Real-Time Processing report.
- Fixed the issue with Keep folder Structure for SMB remediations
- Import settings Fix for empty destination on Remediations
- Remediation actions Remediation Actions resilience improvement
- Fixed Document DB integration
- S3 compatible file download Fixed the download error for some S3 Compatible providers

## [MetaDefender Storage Security v3.1.4](/docs/mdss/release-notes/changelog#metadefender-storage-security-v314)

Release date: 21 February 2023

Version supported until: 21 August 2024

**Highlights**

- SMB integration SMB integration refactoring for high availability and scalability. Removed discovery debounce time
- OneDrive integration refactoring for high availability and scalability
- Real-time data display on the Dashboard
- Event-based Real-Time processing Moved from Blob-trigger to eventgrid and documented the setup
- RAM authentication option for Alibaba Cloud storage unit
- Terraform example for configuring MDSS

**Bug fixes**

- Fixed the issue with Box storage unit set as a remediation destination
- Improved UI for showing blocked files
- More reliable mechanism to download files from the storage

## [MetaDefender Storage Security v3.1.3](/docs/mdss/release-notes/changelog#metadefender-storage-security-v313)

Release date: 22 December 2022

Version supported until: 22 June 2024

**Highlights**

- SSO integration - Added SSO capability using OIDC (Open ID Connect) for Azure AD identity provider
- Azure Files refactoring - Refactored Azure Files storage unit integration to use Azure Files SDK
- Windows Server 2022 - Added Windows Server 2022 to the list of supported operating systems
- Google Cloud Provider Authentication - IAM role authentication option for a GCP storage unit
- Alibaba Cloud Authentication - RAM authentication option for Alibaba Cloud storage unit
- Terraform resources configuration - Terraform example for configuring MDSS

**Bug fixes**

- Amazon S3/Alibaba Cloud/Google Cloud Provider event based real-time - Improved event-based real-time validation and events tracking mechanism
- Decrypt logging - Added logs when a file is decrypted
- Box - Revert encryption mechanism bug fixes
- Report bug fixes - Date filter and user name bug fixes

**Known limitations**

- Windows 11 installation with Docker 4.15.0 - As a workaround, please downgrade Docker

## [MetaDefender Storage Security v3.1.2](/docs/mdss/release-notes/changelog#metadefender-storage-security-v312)

Release date: 27 October 2022

Version supported until: 27 April 2024

**Highlights**

- Event-Based Real-time processing - Enhanced the MetaDefender Storage Security Real-Time processing by adding the option to process notifications when a new object is added to an Amazon S3, Azure Blob, Alibaba Cloud and Google Cloud Provider storage.
- UI improvements - Consistency changes for input controls
- Amazon S3/ S3 Compatible Added the option to keep the folder structure when moving files to an Amazon S3/ S3 Compatible storage unit
- Vulnerabilities display - Enhanced the vulnerabilities details table with a new CVSS 3 section

**Bug Fixes**

- Remediations action rollback Improved rollback mechanism when applying remediations
- Decrypt logging Added logs when a file is decrypted

## [MetaDefender Storage Security v3.1.1](/docs/mdss/release-notes/changelog#metadefender-storage-security-v311)

Release date: 06 October 2022

Version supported until: 06 April 2024

**Highlights**

- Box storage migration - Discover, scan and apply remediation actions on objects from Box.
- Logs improvements - Added the same logging system to all micro-services
- Documented environment variables - Provided information about the usage of each environment variable

**Bug Fixes**

- Reduced number of requests for license validation
- Reset Password page UI fixes

## [MetaDefender Storage Security v3.1.0](/docs/mdss/release-notes/changelog#metadefender-storage-security-v310)

Release date: 31 August 2022

Version supported until: March 2, 2024

**Highlights**

- Alibaba Cloud storage integration - Discover, scan and apply remediation actions on objects from Alibaba Cloud
- Google Cloud storage integration - Discover, scan and apply remediation actions on objects from Google Cloud
- Job dispatcher service improvements - High-availability improvements for the job dispatcher service
- Log aggregation and persistence - Logs created inside the containers will now persist when restarting MetaDefender Storage Security

**Bug fixes**

- Real-Time Processing handling type display- The handling type can now be seen on the dashboard as well
- Improve validation of move remediation actions - Fixed validation for same type of move remediation action, when having a possible circular dependency between storages
- Audit filter - The filter is now resetting when moving to another page
- Date picker validation improvement - Improved filtering reports based on date
