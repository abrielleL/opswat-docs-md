<!-- source: https://www.opswat.com/docs/mdss/4.6.0/release-notes/changelog -->

# Changelog

## MetaDefender Storage Security v4.5.2

Release Date: August 19, 2026

Version supported until February 19, 2028

| Maintenance Release |
| ---- |
| - Deep CDR carries dedicated workflow branches for file types it does not sanitize, so you can keep, move, copy or delete them and clear the source folder in one pass. - Workflows validate before a scan runs, and Deep CDR requires an API key on every scan instance in the primary and failover pools. - Reports name the exact outcome per file, including unsupported file types, the sanitization detail returned by MD Core, and the remediation you configured. - Scanning applies a retry budget while MD Core is busy and holds its scaling steady while an instance is unavailable, so throughput stays predictable under load. - Stopping a real-time scan completes in seconds, the report refreshes on its own, and rescan sits in the report actions. - Schedules coordinate so a location runs one scan at a time, consecutive FTP scans run back to back, and real-time scans follow newly created child folders. - The portable package and the offline Docker toolkit deploy on a clean host, and upgrades carry databases holding non-Latin file names. - MDSS runs on the cache you already have, including AWS ElastiCache, and reads CPU and memory from pod limits on Kubernetes. - The NetApp ONTAP Connector ships at 1.0.44 with the full share path, so several SVMs connect to one MDSS. - OPSWAT SAML sign-on, email notifications and telemetry collectors follow your configuration, and inventory tables let you pick the columns you need. **Maintenance Release (v4.5.1)** Release Date: July 30, 2026 Version supported until January 30, 2028 - Real-time protection jobs each apply their own workflow, so multiple policies can run against a single storage unit. - Disk usage in the warning band keeps scanning running, scan health reflects real load, and autoscaling ships enabled on all deployment types with per-instance sizing recommendations. - The NetApp ONTAP Connector delivers files over HTTPS, and you can configure the response it returns to NetApp when a file scan times out. - Real-time protection keeps its status and discovery cycle detail, and partition-based FTP scans resume without reconfiguration. - Stopped jobs report accurately, their files can be rescanned in place, FTP scans run to completion, and event-based scans handle partitioned storage units. - Remediation actions deliver to a second destination, tags follow files moved into folder-based units, and Central Management copy workflows run as configured. - PDF exports honor the filters you applied accurately per storage unit. - The dashboard loads faster against a 10 million file scan with a searchable unit selector, and job schedules support valid month days and 52-week cycles. - Single sign-on from the virtual appliance keeps its identity provider, notification targets are validated, and S3 accounts show the correct region and endpoint fields |
| **Highlights (v4.5.0)** Release Date: July 22, 2026 Version supported until January 22, 2028 MetaDefender Storage Security 4.5.0 introduces a redesigned user interface, centralized management through OPSWAT Central Management (OCM) v10, a new autoscaling engine, significant security enhancements, and multiple platform and storage integration improvements. |
| **New Features (v4.5.0)** **Redesigned User Interface** The application has been rebuilt using the Blue Line design system, delivering a modern user experience with: - Updated Dashboard, Reports, Inventory, Jobs, Workflows, Settings, and Users pages - Improved reporting with dedicated Threats, Sanitization, and Data Loss Prevention views - Guided onboarding for first-time deployments - Dark theme support - Backward-compatible legacy URL redirects **OPSWAT Central Management (OCM) v10 Integration** MetaDefender Storage Security now supports centralized management through OCM v10, including: - Instance enrollment and license management - Remote configuration - Deployment ID synchronization across managed environments **Autoscaling Engine** A new autoscaling engine dynamically adjusts system resources based on workload. Key capabilities include: - CPU, memory, and file throughput monitoring - Scaling recommendations - `/healthz` endpoint for health monitoring - Dashboard visibility into scaling status Supported deployment models include MetaDefender Core, Cloud and Distributed Cluster. **New SMB Service for Windows deployments** The Windows SMB Service is a new, fully in-house SMB client implementation for Windows deployments. Built with no third-party dependencies, it delivers improved reliability and resolves the connection issues found in earlier versions. |
| **Security Improvements (v4.5.0)** This release includes multiple security enhancements, including: - Fixes for OData injection vulnerabilities - License forgery protection - Penetration testing remediations, including JWT secret removal, improved SSO security, and sensitive data protection - Non-root container enforcement for Kubernetes deployments - Improved Windows file permission security |
| **Platform Improvements (v4.5.0)** Platform updates include: - Updated infrastructure components (RabbitMQ, Garnet, Alpine Linux) - Improved job dispatcher with automatic recovery for orphaned scan jobs - Configurable scan result retention policies - Database growth monitoring and protection - Decoupled scanning service architecture for cross-product reuse - Prevention of overlapping scans within storage groups - Optimized scanning and results storage for archives |
| **Storage and Integration Improvements (v4.5.0)** Storage connectors have been enhanced with improved reliability and functionality, including: - Better error reporting for NFS and SFTP - Improved SharePoint Cloud real-time protection - Microsoft Graph connection throttling for OneDrive and SharePoint - NetApp ONTAP enhancements - Autodiscovery support for all S3-compatible storage providers - Updated Diode integration documentation |
| **Telemetry (v4.5.0)** Telemetry has been renamed **Usage Report** and now includes: - Kubernetes containerized collector - Improved usage reporting accuracy |
| **Resolved Issues (v4.5.0)** This release resolves several issues, including: - Scheduled scans starting at incorrect times due to timezone offsets - Recovery of cancelled or stuck scan jobs after service restart - Dashboard threat counts matching report data - Improved stability when scanning large file volumes - RabbitMQ startup synchronization issues - Improved error handling across storage integrations |
| **Known limitation: Remediation counters on reports for scans performed before version 4.0.0 (v4.5.0)** After upgrading from a version earlier than 4.0.0, reports for scans that completed on the older version may display inconsistent remediation counters: - The **Keep** counter may show 0 even when files were kept. - The **Remediated** counter excludes kept files, so it may show 0 when keeping files was the only configured remediation action. All other values on these reports remain accurate, including the allowed and blocked file totals and the **Move**, **Copy**, **Delete**, and **Tagging** counters. This limitation applies only to scans completed before the upgrade. Scans performed after the upgrade display all counters correctly. |

## MetaDefender Storage Security v4.4.2

Release Date: May 14, 2026

Version supported until November 14, 2027

| Maintenance Release |
| ---- |
| - **SFTP scan reliability.** Fixed an issue where SFTP scans could fail with repeated connection errors against servers that limit concurrent sessions. - **Windows upgrade from v3.6.1 and v4.4.0.** Fixed a crash during the MongoDB migration step that blocked Windows upgrades to the latest version. - **Offline toolkit package.** Fixed the offline installer so air-gapped deployments include all required components and the platform service starts as expected. **Maintenance Release (v4.4.1)** - **NGINX security update.** Updated NGINX to 1.31.0, which patches [CVE-2026-42945](https://nvd.nist.gov/vuln/detail/CVE-2026-42945). Previous MDSS versions are not affected by this CVE; the update ships as a precaution. - **RTP validation for circular remediations.** Real-time scans now reject workflows whose move or copy remediation targets the same storage unit being scanned, preventing the retry loop seen previously. - **Additional S3 region.** Added the New Zealand (ap-southeast-6) region to the AWS S3 and S3-compatible storage selectors. - **Reduced error log noise.** Cleaned up spurious error log entries from background job cleanups and certain file-download failure paths. |
| **Highlights** - **New Storage Integration: Scality RING -** Added native integration for Scality RING S3-compatible object storage, with full coverage for multiscanning, CDR, DLP, file tagging, and remediation actions. - **Azure Blob storage autodiscovery.** Azure Blob accounts can now automatically discover and onboard new containers as they are created. Container selection can be fully automatic or scoped to a manual subset, and the feature can be toggled per account. - **Access Control (ABAC Phase I).** New Settings → Access Control tab showing default roles and their permissions. - **Real-Time Processing start date.** Added an optional "Pick files modified since" date picker to the RTP scan modal, so older files (e.g., OneDrive uploads that retain their original `LastModified`) can be included in the scan. - **Scan size visibility.** Individual scan reports and active scans now show `Total Files Size` and `Processed Files Size`, and `Total Files Count` is back in the report view. - **Users included in config export/import.** Configuration export can now optionally include MDSS users (local and SSO), with matching users reconciled on import. |
| **Improvements** - **Scan reliability and gRPC performance.**  Reused gRPC channels across NFS/SFTP discovery, object operations, and telemetry to prevent port exhaustion; added watchdog timeouts and retries to prevent stuck scans and stuck remediations; fixed timing edge cases that could mark instant scans complete prematurely; and added parallel consumers on non-priority RPC queues for better authentication throughput. - **Logging and diagnostics.** Added a separate error/warning log file with its own rotation, persisted PostgreSQL/Redis/RabbitMQ logs across container restarts, identified the specific MD Core instance in API key failure logs, and clarified the support package export error around `LOGS_PER_SERVICE`. - **Cancel on-demand scans from Reports.** On-demand scans can now be cancelled directly from the Reports tab, matching the existing RTP cancel behavior. - **Persistent service scaling.** Extra service instances can now be configured in `customer.env` and survive upgrades. - **Discovery throttling for Discovery-Only scans.** Added configurable queue-depth-aware throttling so Discovery-Only workflows back off when downstream queues are saturated and resume once they drain. - **Scan reliability guardrails.** Scans no longer get stuck on slow storage or remediation, and instant scans now wait for discovery to actually finish before reporting completion. - **Workflow display in scan details and reports.** Active scan details now show only the currently running workflow, while reports keep the full workflow history with a clearer "current vs. previously used" layout. - **Adaptive Analysis status accuracy.** Adaptive Analysis and Sandbox now show "Skipped" (not "Failed") when MD Core skipped the file, and clean verdicts display a green badge. - **Adding storage no longer auto-starts a full RTP scan.** New storage units are created without an automatic RTP scan, so the Reports view stays clean until you explicitly start one. - **Delete RTP scans from Reports.** RTP scans (including partition scans) can now be deleted from the Reports page, not just cleaned, with support for bulk and mixed-type deletion. - **Timestamps and cleaner messages on RTP errors.** Expanded error details now show when each error occurred and present a friendlier message without raw stack traces. - **Upgrade reliability.** Fixed Windows upgrades silently overwriting `customer.env`, and restored RTP partition scans that stopped working after upgrading to 4.3.0. - **Stability at scale.** Reduced Garnet memory usage on Windows and fixed a service crash triggered by a large number of scans in the database. - **Integration fixes.** Resolved a SharePoint Online issue where slow Graph subscription creation prevented RTP from starting, and blocked the same GCP bucket from being added twice through different credential types (ADC vs. keys). - **Dependency upgrades.** Upgraded RabbitMQ to 4.2.4, Redis to 8.6.0, and Garnet to 1.0.99. |

> **Info - Upgrades from v4.3.0 or earlier**
>
> **RTP behavior during upgrade.***This applies when upgrading from any version older than v4.3.1. Customers already on v4.3.1 or later are not affected.*
>
> Active RTP scans are paused during the upgrade and resume automatically once it completes. Files added or modified during the upgrade window can be picked up by running an RTP report cleanup afterward with [RTP Handling with Comprehensive Detection](https://www.opswat.com/docs/mdss/configuration/real-time-processing-configuration-for-nas) enabled. On NAS storage units this cleanup reprocesses all files and may take some time depending on volume.

## MetaDefender Storage Security v4.3.2

**Release Date: April 03, 2026**

**Version supported until: October 03, 2027**

**Highlights**

**Workflow Cards: Storage Unit Destination**

- Workflow cards now show which storage units are set as destinations for remediation actions, so you can quickly see where your data ends up.
- **How to enable:** Navigate to Workflows and select Extended View from the top right.

**Improvements**

- Certificates are now picked up automatically after a machine restart, without requiring a product restart separately.
- Fixed a race condition during Podman restarts that previously caused orphaned containers running in the background.

## MetaDefender Storage Security v4.3.1

**Release Date: March 06, 2026**

**Version supported until: September 06, 2027**

**Improvements**

- Resolved issue that malformed scanning paths for active RTP scans and Scheduled Scans, that target partitions, on FTP, NFS, SFTP, SMB, and SharePoint On-Premise  storage units
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

## **MetaDefender Storage Security v4.0.1 (Hotfix)**

**Release Date: August 25, 2025**

**Version supported until February 25, 2027**

- SMTP Re-activation Issue
  - Fixed a critical functionality bug where SMTP service could not be re-activated after being deactivated, rendering email notifications permanently unusable until system intervention.
- Database Migration Report Recovery
  - Resolved issues where scan reports became inaccessible after upgrading from previous versions (3.5.1/3.6.1), particularly affecting canceled scans and PDF export functionality during database migration processes.
- **Multi-tenancy Filter Disabled for MDSS Cloud**
  - Temporarily disabled PostgreSQL tenant ID filtering for cloud deployments as the multitenancy feature is not yet complete, preventing authentication and permission issues for Tenant Admin users until proper tenant configuration is implemented.

## **MetaDefender Storage Security v4.0.0**

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

## **MetaDefender Storage Security v3.6.1**

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

## MetaDefender Storage Security v3.6.0

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

## MetaDefender Storage Security v3.5.3

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

## MetaDefender Storage Security v3.5.2

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

## MetaDefender Storage Security v3.5.1

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

## MetaDefender Storage Security v3.5.0

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

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
