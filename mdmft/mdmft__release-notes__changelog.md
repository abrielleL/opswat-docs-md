<!-- source: https://www.opswat.com/docs/mdmft/release-notes/changelog -->

# Changelog

Summarize Page    Connect to Cursor Connect to VS Code
## [Version 3.11.4](/docs/mdmft/release-notes/changelog#version-3114)

**Highlights**

- One-Time Upload Token, generate a single-use token for file upload authorization, enabling controlled external upload access without exposing user credentials or persistent sharing links.
- SSO Admin Role Assignment, assign Readonly Administrator and Helpdesk Administrator roles to users via SSO group claims, extending automatic role provisioning to administrative role types.
- SSO Group as Supervisor Approver, assign an SSO group as the supervisor for approval workflows, enabling approval responsibility to follow group membership without per-user manual configuration.
- User Group Access Controls, configure folder, sharing, and Trash permissions at the group level, restricting actions for specific user groups without per-user configuration — covering folder creation, folder renaming, file and folder sharing, and Trash access.
- External User Interface Restrictions, hide the Sharing panel and My Files section for External Users, presenting a scoped interface limited to their permitted access areas.
- Ad Hoc Guest Sharing Reliability, guest accounts created on-the-fly during file sharing are processed through a consolidated creation flow, reducing edge cases in shared space provisioning.
- Path-Based Transfer Filtering, filter file transfer operations by path patterns to restrict, allow, or redirect transfers based on source or destination path criteria.
- MFT-to-MFT TCP Connection Limit, configure the maximum number of concurrent TCP connections for MFT-to-MFT transfers over one-way network diodes, preventing connection exhaustion in high-throughput environments.
- Guest Sharing Email Template, invitation emails sent to guest users created during file sharing use a dedicated template, providing clear first-access context separate from standard sharing notifications.
- File Deletion Email Notification, receive an email notification when a file is moved to Trash, keeping users informed of deletions affecting shared or monitored content.
- HA Controller Live Configuration Apply, configuration changes saved in the HA Controller are applied to the cluster immediately without requiring a service restart, reducing planned downtime for HA updates.
- SQL HA Connection String Reconfiguration, reconfigure the SQL connection string for MFT in an HA deployment without running the installer, reducing downtime when updating database connection settings.
- LibreOffice Preview Engine Update, preview Office documents using LibreOffice 26.2.1, incorporating upstream security fixes and improved compatibility with recent document formats.
- HA Configuration Tool UI Refinements, the HA Configuration Tool incorporates design updates for improved clarity and visual consistency with the MFT administrative interface.
- File Status on Post-Action Failure, files processed successfully but with a failed post-action display an accurate availability status, distinguishing a completed transfer from a post-processing error.
- Login Page Announcement, configure a custom announcement message that displays on the MFT login page, communicating maintenance windows or access notices to all users before authentication.
- Column-Level Table Filtering, filter table data at the column level across MFT list views, enabling targeted searches by specific field values without affecting other column displays.
- SharePoint Add-in Removal, the legacy SharePoint Add-in option is removed from the MFT interface, directing SharePoint integration to the supported SharePoint connector path.
- Usage Report, report aggregated, anonymized statistics, measures, and usage information as defined in the OPSWAT Terms of Service, to help OPSWAT improve its products.
- Flexible File Download Format, download multiple files as a single ZIP archive or as individual files, choosing the format best suited to the recipient's workflow at the time of download.

**Fixed**

- Security Fixes, the SSO configuration Update button is disabled for Readonly Administrators; the MFT REST API applies rate limiting and input validation to close a Denial of Service exposure path; and the SFT Database Configuration Tool enforces SQL Server certificate validation in SQL authentication mode instead of trusting self-signed certificates.
- Stability Fixes, Next service memory usage returns to baseline after prolonged automation job execution; the MFT login page loads correctly when both the HA Controller and MFT nodes run in HTTPS mode; archive download jobs complete without initialization errors; upload request streams are disposed correctly after transfer completion; automation jobs recover from a transient SQL connectivity loss instead of remaining stuck; and the SFT Database Configuration Tool completes installation, upgrade, and rollback operations reliably across Windows and SQL authentication modes.
- Reliability Improvements, pull jobs with file classification report accurate completion status; permanent file deletions no longer generate repeated error log entries and their audit records are removed correctly; MFT-to-MFT transfers emit detailed log entries for each step; SMB Pull jobs no longer report false disconnection failures; database query performance is optimized for high-frequency operations; expired OTP authentication attempts are recorded in the audit log; and shared content, including Shared With Me downloads and ad hoc guest access, is reliably accessible across all sharing configurations.
- Behavior Corrections, resolved issues across sharing endpoint error handling, Setup Wizard rate limit configuration, SFTP key-only authentication messaging, HA Controller upgrade path enforcement, external user sharing permissions, CSV recipient parsing, email notification display, secure web form behavior, file scan error states, Trash-disabled deletion, email warning list scope, and SFT Database Configuration Tool and File Security Report filter accuracy.
- UI and Usability Fixes, resolved display, validation, and interaction issues across approval dropdowns, automation job configuration fields, upload questionnaires, Audit filters, Email OTP authentication UI, AD notification emails, and the SFT Database Configuration Tool's CLI help and validation messaging; Secure Web Forms is now generally available with the BETA designation removed.

## [Version 3.11.3](/docs/mdmft/release-notes/changelog#version-3113)

**Highlights**

- SAML 2.0 SSO Integration, configure SSO with any SAML 2.0-compliant identity provider alongside existing OIDC, extending enterprise authentication compatibility to EntraID, Okta, and other SAML-based IdPs.
- Email-Based OTP Authentication, configure email-delivered one-time passwords as a secondary MFA factor, supporting users without SMS or authenticator apps.
- Cross-Tenant Entra ID User Mapping, map users across different Entra ID tenants in MFT-to-MFT deployments, resolving cross-tenant identity mismatches for organizations with separate high-side and low-side directories.
- 3DES Cipher Removal from TLS, remove DES-CBC3-SHA (3DES) from the default non-FIPS nginx configuration, eliminating the SWEET32 vulnerability (CVE-2016-2183) without requiring manual customer changes.
- Granular Folder Sharing Roles, share folders with five distinct roles — Owner, Editor, Downloader, Uploader, and Viewer — for precise control over collaborator permissions beyond the previous binary share model.
- Random Password Enforcement for External Users, enforce automatically generated passwords for External User accounts, keeping passwords hidden from the creating user and delivering them via invite email.
- Group Upload Identity Restriction, configure a per-group toggle to control whether users can upload files as members of that group, removing restricted groups from the upload identity dropdown.
- Q&A Conditional Question Branching in Secure Web Forms, define conditional questions in upload questionnaires where the answer to one question determines which follow-up questions appear, enabling branching multi-step approval workflows.
- Discovered MFT Nomination in Orchestration, nominate a Discovered MFT as a Destination MFT directly from the Visual Orchestration node action menu, without navigating away from the automation view.
- SPOP Jobs in Visual Orchestration, view and filter SPOP Automated Jobs in the Visual Orchestration page with integration details consistent with other job types.
- MFT-to-MFT Manual Transfer Mode, configure MFT-to-MFT connections to hold uploaded files until an administrator manually approves forwarding, enabling controlled transfers in data diode and air-gap environments.
- MFT-to-MFT Hash Verification, enable automatic hash verification on every MFT-to-MFT transfer to confirm data integrity, with mismatches flagged in the audit trail.
- MFT-to-MFT Full Destination Sync, configure MFT-to-MFT connections to sync all existing files to the destination regardless of upload time, giving administrators complete control over the destination content state.
- HA Cluster Configuration Tool, manage HA Controller cluster members, MFT node connections, and peer settings through a cross-platform desktop UI application, replacing manual JSON configuration editing.
- HA Configurator Enhancements, access the HA Configurator application from the HA Controller installer package, with several usability additions in this release.
- HA Load Balancer Health Endpoint, query the public /health/ready endpoint on each MFT node without authentication so load balancers can automatically detect and route to active nodes.
- HA Reverse Proxy Port Toggle, disable the HA Controller reverse proxy port in two-site deployments where the proxy is not needed, reducing the exposed attack surface.
- HA Installer Configuration Migration, migrate HA Controller configuration properties automatically during upgrade, adding required fields while preserving all existing settings.
- Configurable Audit Export Timezone, export audit logs in the server's configured timezone instead of UTC, aligning exported report timestamps with timestamps displayed in the MFT UI.
- Geographic Location in Audit Trails, view City and Country columns in the system Audit Trail, resolved from client IP addresses, for faster event origin identification without manual IP lookups.
- IP Location in File Activity Trails, view City and Country columns in the file-level Audit Trail with tooltip details on hover, exported automatically when generating audit reports.
- City-Level IP Location Management, define IP-to-location mappings at city and country granularity using CIDR ranges or IP ranges on the IP Location page, enabling precise geographic identification of file transfer origins.
- Outbreak Prevention Rescan Period Picker, configure the outbreak prevention rescan period in hours, days, or weeks using a time span picker, removing the need to calculate total minutes manually.
- Custom Dashboard Widget Layout, rearrange, remove, and restore widgets on the System and File Security dashboards using drag-and-drop, with layout changes auto-saved per user and reset-to-default available.

**Fixed**

- Security Fixes, user session tokens and OAuth client secrets are stored and transmitted encrypted, resolving cleartext exposure in logs, the database, and API responses; SSO login attempts by disabled third-party users are blocked and recorded as failed; SFTP Pull and MFT-to-MFT group transfers apply correct permission scoping; restricted and read-only administrator access to settings pages restored.
- Stability Fixes, unsharing files shared with large user groups, MFT-to-MFT transfers of large files behind HA Controller, and MFT admin tools post-upgrade all operate correctly.
- Reliability Improvements, over 60 reliability fixes across Audit Trail, Dashboard, SFTP Pull, MFT-to-MFT integration, file sharing emails, DFS Share jobs, and OCM registration.
- Behavior Corrections, resolved issues across MFT-to-MFT config visibility, SSO credential handling after upgrade, file management (deleted files, encryption key changes, shared views), and automation job history visibility.
- UI and Usability Fixes, resolved display, validation, and interaction issues across File Classification, Visual Orchestration, SSO settings, Groups, and Dashboard widgets.

## [Version 3.11.2](/docs/mdmft/release-notes/changelog#version-3112)

**Highlights**

- Configurable File Expiration by User and Group, admins can define file expiration days for users and groups, overriding the system default based on priority, enabling more precise policy control.
- Extended Audit Logs with File Path and Tags, admins can enable extended audit logging to include file path and tags, improving traceability while maintaining control over database usage.
- Introduce 'Skipped' Approval State for Supervision, a new “Skipped” approval state is introduced when supervision is bypassed, providing clearer and more informative status visibility.
- Updated Toast Notifications, toast notifications now feature a refreshed design, improving clarity and consistency across the application.
- New System and File Security Widgets, the dashboard now includes new widgets for file security and login activity, enhancing visibility into blocked files, vulnerabilities, and invalid login attempts.
- Redundant HA Controller for Fault Tolerance, the HA Controller is now fully redundant and fault-tolerant, supporting multiple instances, leader-based node control, trusted forwarders, HTTPS between peers, and health checks, improving cluster reliability and eliminating single points of failure.
- Role Assignment Using Immutable Claims, roles can now be assigned using immutable claims, allowing more secure and flexible SSO-based user role management.
- SharePoint Add-in Support, a new SharePoint Add-in lets users send files directly to MFT from SharePoint, enabling seamless integration into their workflows.
- Configurable Group File Sharing, admins can now enable or disable file and folder sharing for individual AD groups, providing more control over group-level sharing permissions.
- Sortable and Filterable Columns, all columns in the File Security Report page are now sortable and filterable, improving data navigation and analysis.
- Automated Deployment Support, MFT now supports automated post-install configuration using a json file, enabling fully unattended deployments and simplifying large-scale or scripted installations.
- Integrations Module in OPSWAT Central Management, OPSWAT Central Management's MFT configuration now includes an Integrations module, providing centralized management of external system connections with a consistent experience aligned with MFT.

**Fixed**

- File Processing and Upload Stability Improvements, improved file status handling and upload processing to prevent incorrect states, unexpected interruptions, and performance degradation, enhancing overall system reliability.
- File Status and UI Label Corrections, resolved inconsistencies in default file status handling and updated interface labels for improved accuracy and clarity across the application.
- Improved Unauthorized Page Navigation, enhanced unauthorized page behavior to ensure proper browser back-button handling, preventing users from getting stuck and improving overall navigation experience.
- UI Improvements, minor UI glitches have been resolved.

## [Version 3.11.1](/docs/mdmft/release-notes/changelog#version-3111)

**Highlights**

- Visual Status Indicators for MFT-to-MFT Connection Events, audit log entries for MFT-to-MFT connection status changes now display clear success and failure icons in the Outcome column, enabling faster recognition of connection issues and improved filtering of critical events.
- Okta SSO Group Claims Support, MFT now supports Okta group claims via a new *SSO Group* type, usable anywhere groups are referenced and behaving like Active Directory groups for access control and workflow configuration.
- View Upload Question Answers in My Files, users can now view the upload questions and their submitted answers directly from the file actions menu in My Files via a new *View Upload Questions* option, providing quick review of file-related metadata when available.
- Detailed Views for Metascan and Utilities Modules, administrators can now open dedicated detail pages for the Metascan and Utilities modules, providing an expanded view of each module's status
- Processing Queue Filter, a new *Processing Queue* filter is available in My Files and Processing History, allowing users to quickly view only files that are currently under processing, improving visibility and workflow focus.
- DFS Share Mapping Support for Automated Jobs, MFT now supports DFS share mapping for job integrations, allowing customers to specify and resolve the appropriate server per automated job when using DFS paths, ensuring reliable job execution in distributed file system environments.
- API Key Generation for All Users, non-admin users, including automation coordinators and regular users, can now generate and manage their own API keys via a dedicated *My Credentials* section, enabling easier and more secure access to MFT APIs.
- Timestamp-Based Renaming for Duplicate Files, pull jobs can now automatically append a timestamp to incoming files with duplicate names, preventing overwrites and ensuring all versions are preserved for clear tracking and auditing.
- Cancel Ongoing File Scans from Processing History, administrators can now cancel ongoing file scans directly from Processing History, either individually or in bulk. Cancelled scans are marked as *Scan Cancelled*, preventing automatic rescans and giving admins better control over resource-heavy or misuploaded files.
- Username Search in Processing History, processing history now supports searching by username, including partial and full matches, enabling faster filtering of records while preserving existing filters and pagination.
- Security and Audit Settings in OPSWAT Central Management, OPSWAT Central Management now includes *Security* and *Audit Settings* modules, replicating the MFT experience for managing security configurations and audit logging.
- Manage Notification Emails for All User Types, administrators can now view and edit notification emails for all user types directly on user pages. CSV uploads can add or update these emails, improving communication management across the platform.
- SharePoint Subsite Support, MFT now allows SharePoint On-Premises automated jobs using subsite URLs, enabling file transfers and library operations scoped directly to the specified subsite.
- Event-Based Automated Jobs Trigger, MFT now supports event-based triggers for automated jobs, when files are created, modified, deleted, or renamed. This ensures faster, more reliable file processing with minimal manual intervention.
- Enhanced Sorting and Filtering, the file security report has been improved with broader column sorting and filtering capabilities, making it easier to organize, search, and analyze file security data for faster investigations and better visibility.
- Aether and AI Engine Results in Scan Results Page, MFT now presents Aether and AI engine results within the Scan Results page, ensuring advanced analysis outcomes are handled and displayed consistently with other scanning engines.
- Starred Files and Folders, users can now mark files and folders as favorites using a star icon and filter My Files to show only starred items, making it easier to quickly access frequently used content.
- Dashboard Widgets and Navigation Improvements, new widgets have been added to the File Security and System dashboards to improve visibility into security trends and file composition, and the Dashboard entry has been moved to the top of the sidebar for quicker access.
- Pause, Resume, and Auto-Retry for SMB Automation Jobs, SMB automation jobs now support pause and resume, along with automatic retry using exponential backoff on interruptions. Transfers can continue from the point of failure, preserving progress, improving reliability, and reducing the need to restart large jobs.
- MFT-to-MFT Connection Alerts, MFT now provides automated monitoring and alerting for MFT-to-MFT connections. Administrators are notified via in-app banners and optional email when a connection goes down or is restored, ensuring timely awareness and faster remediation of sync issues.
- Context Menus Across Key Modules, contextual menus are now available in modules such as User Management, Groups, Approval workflows, Files, and File Security Reports, offering consistent row-specific actions and improved usability throughout the platform.
- Enhance SSO Group Handling, SSO groups are treated as a distinct type with read-only membership and fixed names, ensuring consistent management while preventing unintended changes or removals.
- Redundant High Availability Controllers, the high availability controller now supports multiple instances in an active-passive setup, removing the single point of failure and improving fault tolerance for critical operations.

**Fixed**

- File Processing Improvements, enhance the file processing workflow logic to improve efficiency, reliability, and maintainability.
- Installer Reliability and Usability Enhancements, the installer now reliably handles service states, applies correct permissions, shows database upgrade progress, provides clear uninstall feedback, and generates support packages in accessible locations, improving overall installation, upgrade, and uninstall reliability while giving users clearer guidance and reducing failures.
- Visual Orchestration Usability Improvements, enhancements to the automation section now allow users to skip the Wizard Tour by clicking outside the active step, filter Automated Jobs by owner, and pause/resume jobs directly from the orchestration view. These changes improve navigation, control, and efficiency for administrators and job owners.
- Improve Subsite Connection Feedback, enhance SPOP messages during subsite connection tests to clearly indicate connection status and provide informative, actionable feedback to the user.
- SFTP Pull Job Connectivity Handling, improve SFTP Pull jobs to automatically recover from temporary connectivity issues, preventing stalled jobs and reducing manual intervention.
- UI Improvements, minor UI glitches have been resolved.

## [Version 3.11.0](/docs/mdmft/release-notes/changelog#version-3110)

**Highlights**

- Processing History Page Upgrade, the Processing History page now features a summary chart, giving users a clear visual overview of file trends and making it easier to track processing activity over time.
- Expanded Visual Orchestration Capabilities, Visual Orchestration now supports all automated jobs, along with MFT-to-MFT routing and pause/resume functionality, making automation management more intuitive, efficient, and transparent.
- Proxy Support with User/Password Authentication, MFT now support HTTP proxies with optional user/password authentication, enabling secure and flexible connectivity for all network environments.
- SSO Phone Number Visibility, admins can now display phone numbers received from SSO by the new “Phone Number” column in the user list.
- Q&A questionnaires, administrators can now define Q&A questionnaires for file uploads, capturing metadata that guides routing and supervisor approvals, ensuring more accurate and efficient file handling.
- Password Reset Email Template, a customizable password reset email template has been added, allowing administrators to edit the subject, branding, and content just like other notification templates.
- Guest Users List Sorting, guest Users can now be sorted by username, expiration date, or registration date, with preferences persisting across pages. This makes monitoring and managing large guest user lists easier and more efficient.
- RTL Layout Support, MFT now supports right-to-left layouts, ensuring correct text direction, alignment, and component behavior for RTL-language users.
- Pause & Auto-Resume for SMB Automation Jobs, SMB Automation Jobs can now be paused and resumed from the point of interruption, with automatic retries on failure, ensuring data integrity and saving time during large file transfers.
- FTPS Connector for Automated Jobs, a new FTPS connector is now available for Automated Jobs, enabling secure and reliable file uploads and downloads.
- SharePoint On-Premise Connector for Automated Jobs, MFT now supports SharePoint On-Premise as a source and destination in Automated Jobs, enabling fully automated workflows with internal document repositories without manual intervention.
- Admin-Enforced File Classification, administrators can now enforce file classification for all uploads, ensuring consistent data handling and compliance across the organization.
- Enhanced File Security & System Dashboards, the System and File Security dashboards now feature dynamic widgets for scanned and blocked files, threats prevented, and data loss protection. Admins can view real-time and historical data, export dashboards to PDF, with actionable security insights displayed clearly and concisely.
- Full Admin Control Over Automation Jobs, administrators can now view and manage all Automation Jobs, while Automation Coordinators continue to see only their own, improving oversight and collaboration across teams.
- Retain Credentials When Editing Automation Jobs, automation Jobs now preserve existing credentials during edits, so users can update schedules or settings without re-entering usernames and passwords, improving efficiency and reducing errors.
- Real-Time Progress & Estimated Time Remaining for File Transfers, file transfer jobs now update progress based on actual data moved and display an estimated time remaining, giving operators a smoother, more accurate view of job status and helping them plan their next actions with confidence.
- File Hash Added to “File Uploaded” Email Template, the “File Uploaded” email now includes the file hash by default, giving recipients clearer file integrity details and improving trust in file verification.
- External & Guest User Support in Custom Groups, custom Groups now support adding External and Guest users, making shared folder access simpler and more flexible.
- HA Controller Support Package Tool, a new CLI tool is now included with the HA Controller, allowing users to generate a support package containing configuration, logs, and installation details for easier troubleshooting and support.

**Fixed**

- Improved OPSWAT Central Management Communication, improved OPSWAT Central Management ensures timely license updates and better visibility across all MFT instances.
- Display Canceled Scans in MFT, MFT now clearly shows when a scan has been canceled on the Core side, updating the file status to “Cancelled” to keep administrators informed of interrupted analyses.
- Installer Database Upgrade Progress Feedback, the installer now provides detailed progress feedback during database upgrades, including the percentage of migrations completed.
- MFT to MFT bidirectional: Improve file querying, MFT-to-MFT file status lookups are optimized with batch processing, making queries approximately twice as fast.
- Installer Support Package Location, the installer now generates support packages next to the launched installer by default making troubleshooting easier.
- On-Demand Automation Wizard Tour, admins can now start the Automation Wizard Tour on-demand, with the tutorial video featured as the first step. The tour has been reorganized for a smoother experience, guiding admins step by step through adding automation and choosing an automation type.
- UI Improvements, minor UI glitches have been resolved.

## [Version 3.10.3](/docs/mdmft/release-notes/changelog#version-3103)

**Highlights**

- Interactive Onboarding for Visual Orchestration, a guided Wizard Tour now introduces the Automation page, helping users explore key features step by step for a smoother, more intuitive onboarding experience.
- SSO Automation Coordinator Role Assignment, administrators can now assign Automation Coordinator roles directly during SSO setup, ensuring seamless role configuration.
- New Dashboard Widgets, the Dashboard now includes widgets for total users and license status, providing quick insights at a glance.
- Notification Emails for SSO Users, admins can now edit notification emails for SSO users, providing greater flexibility in managing user communication.
- Support for GCC-High SharePoint Integration, MFT now supports connections to Microsoft's GCC-High SharePoint environment, ensuring secure data transfer and authentication compatibility across both Commercial and Government cloud tenants
- End-User Scan Result Visibility, admins can now control whether end users see file security and scan result details through new visibility toggles, helping simplify the interface and prevent exposure of internal scanning information.
- Global BCC Configuration for Email Notifications, admins can now define a global BCC address applied to all email notifications, enabling centralized auditing and monitoring of outgoing communication.
- Verdict Supervisor Role, a new *Verdict Supervisor* role allows to review processing history, override Core verdicts, and manage supervisor approvals—offering focused control without full administrative permissions.
- Drag-and-Drop Upload for Shared Folders, users with editor access can now upload files or folders to shared locations using drag and drop, streamlining file management across shared workspaces.
- Bulk Email Update via CSV Upload, admins can now upload a CSV file to update user notification emails in bulk, simplifying large-scale email management.
- Upcoming End of Support for Legacy Windows Versions, support for Windows 10, Windows Server 2012 R2, and Windows Server 2016 will be discontinued in a future release to align with MetaDefender Core's platform strategy and ensure focus on modern, supported environments.
- Option to Make Sanitized Files Downloadable as New Clean Versions, a new option allows sanitized files to be treated and downloaded as new clean versions, offering greater flexibility in sanitized file handling.
- Automatic Redirect for Authenticated Users, users with an active session are now automatically redirected from the login page to *My Files*, streamlining navigation and improving overall user experience.

**Fixed**

- Consistent “Back” Button Placement, back buttons are now consistently placed on the left across all wizard-style pages for a uniform navigation experience.
- Clearer Group Sharing Roles, shared groups now display their assigned roles in the dropdown, preventing duplicate sharing and improving clarity.
- Consistent Network Rule Error Display, files and folders blocked by network rules now show a unified error message for a clearer download experience.
- Improved Automation Page UX, the Visual Orchestration now features an instructional empty state and enhanced running job animations for better visual clarity.
- UI Improvements, minor UI glitches have been resolved.

## [Version 3.10.2](/docs/mdmft/release-notes/changelog#version-3102)

**Highlights**

- MFA Support for MFT Pull, MFT Pull now supports MFA for secure environments. Manual Pull operations require users to complete MFA challenges, while automated jobs can authenticate using administrator-generated API keys. This ensures secure access for both interactive and automated workflows, maintaining compliance and uninterrupted file transfers.
- HA Active-Passive for MFT, MFT now supports active-passive high availability, with a Controller Service automatically promoting the passive instance if the active one fails. Manual reactivation of the original instance ensures continuous and reliable operation.
- Configurable Guest ID Length, admin UI now allows administrators to configure the length of guest IDs between 12 and 255 characters, with a default of 12. This enhancement provides flexibility for integrations and improves control over guest account identifiers.
- Set Radius as Default Login Screen, MFT now allows administrators to set Radius as the default login screen, ensuring it appears as the first and selected tab for users in trusted network environments. This improvement streamlines the login experience, supports Radius-only setups, and maintains flexibility for other authentication methods.
- MFT-to-MD Core Load Balancing, MFT now lets administrators distribute tasks to MetaDefender Cores using Basic Round-Robin or Smart CPU-based routing, automatically skipping unhealthy cores and logging routing decisions for efficient, reliable processing.
- Admin Override for Core-Blocked Files, administrators can now manually unblock files previously blocked by MetaDefender Core. Overrides are logged, and reversible, giving admins full control over file availability without altering the original Core verdict.
- Reset All Email Templates, administrators can reset all email templates to their default state in one action, creating a new active version and removing customizations, simplifying template management.
- Show Temp File Name in Processing History, processing History now includes a “Physical File Name” column, allowing administrators to trace files by their temp filenames and quickly identify files in storage, improving auditability and troubleshooting.
- Pull MFT Access for Non-Admin Users, the Pull MFT feature can now be enabled for all users, allowing non-admin roles to retrieve files from connected MFTs. This improvement streamlines file access across remote locations
- MFT Pull: Copy Files Without Folder Structure, MFT-to-MFT jobs now support an option to copy only files from the source, without preserving the original folder structure. This allows administrators to consolidate files from multiple subdirectories into a single destination folder, simplifying processing and management.
- Visual Orchestration: Job Executions & Node Filtering, automation page now shows the latest 10 job executions and allows filtering of nodes by type, integration, direction, or state. These updates improve visibility, focus, and workflow management for automated jobs.
- Windows Integrated Authentication Support, UI now supports Windows Integrated Authentication with Kerberos for SSO, allowing automatic or manual login for users in AD domains. This provides seamless authentication while maintaining fallback for non-domain PCs.
- Login UI Refactor, the login screen have been updated to a unified design across all OPSWAT products, ensuring a consistent and modern user experience for sign-in, MFA, guest, and Radius.
- Operational Dashboard Widgets, new widgets have been added to the Operational Dashboard, featuring line charts for file uploads and downloads by both volume (GB) and count. This enhancement provides real-time trend insights and improves monitoring of MFT activity.
- MFT Enrollment with CM10, MFT can now securely register with Central Management v10, enabling trusted connections for centralized management and monitoring. This improvement enhances operational control and visibility across MFT instances.
- Control Manual Synchronization, administrators can now enable or disable the manual file re-send option system-wide. When disabled, the Manual Resync option is hidden from users, giving admins greater control over file operations.
- Move Files Between Storages, admins can now move files from inactive or local storage to active or network storage. The process handles large files in batches, supports encryption, and provides tracking of progress, simplifying storage management and ensuring safe file transfers.
- Bulk File Approval with Comments, supervisors can now approve multiple files at once while adding a single comment that applies to all. This streamlines workflows, reduces repetitive tasks, and saves time for teams handling bulk file approvals.

**Fixed**

- Optimized MFT-to-MFT File Status Queries, MFT-to-MFT file status queries are now optimized with batch processing, roughly doubling retrieval speed. This improvement ensures accurate file status results while enhancing performance and reducing load during cross-MFT lookups.
- Improved Large File Push to SMB, automation Jobs now support reliable transfer of large files to SMB servers, improving stability and performance for high-volume uploads.
- Improved Installer CLI Argument Handling, the installer now parses and handles all CLI arguments, ensuring consistency with documented usage. Invalid or missing arguments produce clear error messages, improving usability and reliability of the installer
- Installer Improvements, The installer has been optimized for faster and smoother execution, with enhanced stability and additional error codes and messages to better cover edge cases, improving the overall installation experience.
- UI Improvements, minor UI glitches have been resolved.

## [Version 3.10.1](/docs/mdmft/release-notes/changelog#version-3101)

**Highlights**

- Audit Trail for MFT-to-MFT Transfers, MFT now includes an audit trail for MFT-to-MFT file transfers, allowing users to track successful sends and identify transfer errors. This improves operational visibility and supports easier troubleshooting.
- Improved Orchestration Editor, visual Orchestration now includes grouping of automated jobs by their source integrations, such as SFTP or MFT servers. This improvement reduces visual clutter, makes it easier to manage multiple jobs, and keeps connections to integrations clear and accessible.
- Pull & Push Sync Mode, automated jobs now include a Sync Mode for both Pull and Push operations, keeping local and remote folders identical. The system automatically adds, updates, or deletes files as needed, ensuring data consistency for backup, processing, and distribution workflows.
- Automated Job Alerting, automated jobs now include built-in alerting, sending configurable email notifications on job success or failure. This helps operations teams proactively monitor job status, quickly address issues, and maintain system health.
- Enhanced Transparency, users can now see file statuses on destination MFTs, including reasons for blocked files, improving visibility and simplifying transfer monitoring.
- Smarter Automation, automated jobs now support advanced routing with AND/OR logic, RegEx matching, and additional file properties, enabling precise automatic file handling and actions.
- Forward File Tags and Classification, files forwarded to other MFTs now include their tags and classification, ensuring metadata travels with the file and maintaining context across systems.
- Autosave Column Views, a new autosave feature for datatable column views preserves user layouts across sessions. This eliminates the need for manual saving and ensures a consistent experience on pages.
- Syslog Hostname Support, syslog integration now supports hostnames as well as IPs, making server configuration more flexible and ensuring reliable audit logging.

**Fixed**

- UI Update: Edit File Password Modal, the Edit File Password modal has been refactored to follow the latest design guidelines, improving consistency, usability, and alignment with the overall UI system.
- Improved User Password Security, user passwords are now secured with a stronger hashing method, enhancing account protection and reducing the risk of unauthorized access.
- Unified Page Layout, pages now use unified layout components, improving structure, simplifying development, and ensuring consistent display across file, user, and audit views.
- AD Removal Warning Modal, the AD removal warning now clearly alerts admins that deleting a sync will remove all users and their data, preventing accidental loss.
- UI Improvements, minor UI glitches have been resolved.

## [Version 3.10.0](/docs/mdmft/release-notes/changelog#version-3100)

**Highlights**

- Visual Orchestration Tool for Automated Jobs, MFT offers a unified automation view that displays MFT-to-MFT and automated job configurations in a single flow diagram. This simplifies the integration management and improves operational visibility.
- Group-Based File Size Limits, MFT lets you set file size and total storage limits for each user group. If a user belongs to multiple groups, the most permissive limit applies. This approach allows flexible and scalable storage control.
- Active Share Cleanup, MFT allows admins and folder owners to instantly remove all sharing—both explicit and inherited—from a folder and its contents with a single click. This enhances security and simplifies permission management.
- Support OAuth Email Authentication for Microsoft 365, MFT supports Microsoft 365 email sending via OAuth using Exchange Online, improving email security and ensuring compatibility with modern Microsoft authentication standards.
- Breadcrumb UI Enhancements and Notification Subpage Navigation, the breadcrumb navigation has been updated to better utilize space by fully displaying long items and limiting visible items to four, with any overflow accessible via a “more” menu. Notification subpages, such as Email Templates and SMTP, now also use breadcrumbs to follow the updated design guidelines, improving clarity and consistency across MFT.

**Fixed**

- Improved Polling Behavior in File Views, automatic polling in My Files and Shared With Me is now smarter, preventing duplicate data requests by waiting for ongoing fetches to complete. This improves performance and reduces server load.
- SMB Push and Pull Job Optimization, push and pull jobs using the SMB protocol have been optimized for high-throughput environments, resulting in significant improvements in transfer speed and efficiency compared to previous versions.
- UX Improvements: Progress Modals Face Lift, several progress modals, including the archive download and MFT pull processes, have been updated with a fresh layout to enhance user experience and align with the latest design standards.
- Stronger Controls for Restricted Administrators, restricted administrators now operate under tighter limits with enhanced permission controls to enforce security and prevent unintended access to sensitive settings and user roles.
- UI Improvements, minor UI glitches have been resolved.

## [Version 3.9.4](/docs/mdmft/release-notes/changelog#version-394)

**Highlights**

- Add Support for message *authenticator in RADIUS Authentication, MFT has stricter authentication requirements where the message* authenticator attribute can now be sent during RADIUS login. This ensures compatibility with updated FreeRADIUS servers and prevents login failures.
- UX Improvements: Sidebar Menu and Processing History Table

  - Processing History: Added horizontal scrolling, column resizing with saved settings, and pinned key columns for easier navigation.
  - Sidebar: Reorganized menu structure with clearer labels and improved responsiveness across devices and languages.
- New Folder Upload Button, users can now upload entire folders using a dedicated button, making folder uploads quicker and more accessible.
- Flexible Step-Based Approval with AD Group Support, step-based approval now supports different approval levels across teams and allows administrators to assign AD groups as supervisors at each level. Each team its own set of approval steps, and any member of the assigned group can approve at their respective level. This offers great flexibility for complex workflows.
- MFT Supports Supervisors as AD Groups, MFT now supports assigning an AD group as a supervisor, allowing any group member to approve file transfers. This feature is compatible with group-mode and multi-stage approvals, with group visibility managed through supervision settings.
- Suppress UI Warnings for Standard Users, licensing warnings are now hidden from non-admin users, keeping the interface clean while ensuring important alerts remain visible to administrators.
- Include/Exclude Users in Active Directory Sync, administrators can now preview and manually select which users and groups to include or exclude during Active Directory sync. This offers greater control and visibility over user synchronization.
- SSO Support for Citrix ADC Netscaler, MFT now supports integration with Citrix ADC Netscaler for Single Sign-On, ensuring compatibility with enterprise environments that use this IdP.
- Drag-and-Drop Upload into Folders, files and folders can now be uploaded directly into the folder structure within "My Files" using drag-and-drop. Uploads start instantly or display a modal if needed, making the process faster and more intuitive.
- Drag-and-Drop File and Folder Reorganization, users can now move files and folders within "My Files" using drag-and-drop, with support for multi-level navigation and large selections. This enhances file management and improves usability.
- Custom Message in Sharing Email Notifications, users can now add a custom message when sharing files, which is included in the email notification. This enables more personalized communication while maintaining data privacy.
- Manual Active Directory Synchronization, administrators can now manually trigger AD sync and disable automatic sync using a toggle, providing greater control over synchronization during setup and ongoing use.
- Extended Duplicate Handling for Move, Restore, and Rename, MFT now detects name conflicts during move, restore, and rename operations, providing users with clear options and feedback to maintain control and prevent accidental overwrites.

**Fixed**

- Shared with Me page refreshes automatically, files uploaded to shared folders now automatically appear in the "Shared with Me" view, just like in "My Files." This improves the user experience by maintaining pagination and making new content instantly visible without requiring a manual refresh.
- [User Mapping] Support Usernames Shorter Than 5 Characters, user mapping now supports linking accounts with usernames shorter than 5 characters, enabling smoother integration for AD, Radius, and external users, particularly in environments with automatic account creation.
- Audit Logs Include Share Role Details, audit logs now record the specific role (e.g., Downloader, Editor) assigned when files or folders are shared with users or groups, improving visibility and traceability for compliance and auditing purposes.
- UI Improvements, minor UI glitches have been resolved.

## [Version 3.9.3](/docs/mdmft/release-notes/changelog#version-393)

**Highlights**

- New "Editor" Role for File and Folder SharingNew "Editor" Role for File and Folder Sharing, an "Editor" role has been added to file and folder sharing. It grants users near-full editing capabilities - similar to the owner - including the ability to rename and delete items and upload files to shared folders while respecting access controls.
- "On-the-Fly" Guest User Creation, users can now share files with email addresses not yet registered in MFT, triggering automatic guest account creation. This streamlines external collaboration while managing validation and access flow effectively.
- Restricted Administrator Role, a new "Restricted Administrator" role has been introduced. It allows administrators to view processing history and perform rescans without being able to preview or download files. This supports secure file handling in sensitive environments.
- Enhanced Duplicate File Handling for Uploads, file uploads now feature improved duplicate handling, with options to overwrite, rename, skip, or cancel when conflicts are detected. This provides greater control and consistency across both single- and multi-file uploads.
- Visual MFT-to-MFT Configuration Overview, administrators can now view MFT-to-MFT configurations in an interactive, read-only diagram. This visual displays connection statuses and transfer policies, offering clearer insight into cross-MFT setups without allowing direct edits.
- Improved File View and Upload Experience, key file views such as My Files, Shared With Me, Archived Files, and Trash now display clearer empty states and more intuitive feedback. The interface has been refreshed with updated buttons, form elements, and a modernized header to improve usability.
- Separated Supervisor Approval Status, the Supervisor Approval status is now shown in a dedicated column across relevant views. This makes it easier to distinguish from general file statuses, improving clarity for managing user approvals.
- Adaptive Upload Button, the Upload Files button remains in the header but is now enabled or disabled based on user permissions and the current location. This improves usability and helps prevent errors.

**Fixed**

- File Upload Stability Enhancements, enhancements have been made to memory management and system handling to address causes of upload interruptions, improving overall file upload stability and reliability.
- Improved Consistency of Core Scan Results Page, scan Result and Display have been enhanced to ensure consistency between MetaDefender Core™ and MetaDefender Managed File Transfer™.
- Improvements to "Shared With Me" Page, the structure of the Shared With Me page has been optimized to improve performance, stability, and clarity.
- SQL Server 2014 Support Discontinuation, support for SQL Server 2014 has been discontinued. New installations on this version will be blocked to maintain compliance and security.
- UI Improvements, minor UI glitches have been resolved.

## [Version 3.9.2](/docs/mdmft/release-notes/changelog#version-392)

**Highlights**

- MFT-to-MFT Expiration Override, the default file expiration date can now be overwritten on the destination MFT in the API key settings. This option enables users to keep files on the destination MFT for longer periods of time.
- Duplicate Audit Log Cleanup, MFT now detects excessive audit logs and offers admins the option to clean them up before the next product upgrade. The process runs in batches with progress tracking and can be cancelled at any time. After the upgrade, MFT will run this job automatically to ensure system stability.
- LocalDB Option Removed from Installer, MFT no longer offers LocalDB as an installation option. For new installations, administrators must set up and connect to a compatible external database before proceeding.Existing installations using LocalDB can still be upgraded without interruption.
- Context-Aware Upload Button, the Upload Files button now remains in the application header at all times but adapts its functionality based on the current page in order to improve usability and prevent upload errors.
- Log Classification Changes, the enhanced logging functionality tracks file classification changes made by the file owners. When enabled, MFT generates a log report of such changes and stores it on a syslog server. This function ensures complete tracking of security classification events.
- Editable Settings for Existing API Keys, admins can now enable or disable the Skip Core Scan and Skip Supervision options for existing API keys without having to regenerate the keys. This improves flexibility and control over the integration process.
- MFT-to-MFT Status Polling, MFT now automatically polls the connection status of MFT-to-MFT links every 30 seconds, ensuring real-time status visibility.
- Email Notification for Blocked Files, in MFT-to-MFT transfers, users on the destination MFT are now notified by email if incoming files from the source MFT are blocked. This ensures that users stay informed about blocked transfers across the chain.
- Database Storage Warnings, MFT now alerts administrators when database storage usage exceeds the threshold limit. Admins can also view the detailed status of the storage or they can dismiss the warning until their next login.
- Configurable SMTP Timeout, SMTP connection timeout can now be configured manually. This improves flexibility for deployments with slower or cloud-hosted mail relays to ensure reliable email notifications in diverse environments.
- Modernized Data Table Design, a visual update across all data tables that enhances user experience through cleaner layouts, better usability, and consistent styling, without affecting underlying logic.
- Configurable SSO Claims, MFT's SSO settings now include an advanced configuration section where administrators can map user properties (e.g., username, email) to specific claim values, ensuring seamless user authentication.

**Fixed**

- Performance Enhancements for File Upload and Processing, a series of optimizations have been implemented to improve file upload, processing efficiency, and overall system performance.
- UI Terminology Updates for Improved Clarity, to enhance usability and align with common terminology, several interface elements have been renamed:

  - "Recycle Bin" is now "Trash"
  - **"Overview"** in top-level navigation is now **"Files"**
  - “Sharing” column has been renamed to “Sharing Status” under My Files
- Trusted Network Import, the Importing Trusted Network settings now works correctly, with accurate error messages and proper user context handling.
- New Destination Link in Email Notifications, the product link in the email notifications for shared files and folders now points to the "Shared with Me" page instead of the "My Files" page.
- Guest Limitation Default, enabling guest creation limits by default helps maintain system stability and manage user growth efficiently.
- Simple Recovery Mode, when newly created databases use the "Simple" recovery model, storage usage is reduced and maintenance is simplified by minimizing log file growth.
- UI improvements, UI glitches have been fixed.

## [Version 3.9.1](/docs/mdmft/release-notes/changelog#version-391)

**Highlights**

- LocalDB Warning, MFT now displays a warning banner when using LocalDB, alerting administrators that it is not recommended for production use.
- Enhanced File Sharing Experience, MFT now offers an enhanced file-sharing experience with a redesigned sharing window, providing additional information and new features for improved usability.
- Manage Engine ADSelfService SSO Integration, MFT now supports SSO integration with Manage Engine's ADSelfService, enabling seamless single sign-on functionality.
- New MFT Setup Wizard, after installation, MFT now features a brand-new setup wizard that guides users through configuring common settings before using the system. This simplifies the initial setup process, ensuring a quicker, more user-friendly configuration and reducing the chances of errors.
- File Classification, users can now apply classifications to their files from a list of predefined options set by administrators, ensuring standardized categorization and enabling more efficient file tracking and reporting.
- Automatic Guest User Creation for MFT-to-MFT Transfers, MFT-to-MFT transfers now support a conditional setting to automatically create a guest user if the uploader does not already exist. Enhancing workflow automation and reducing manual user management.
- Skip Supervision for MFT-to-MFT Transfers, similar to the Skip Core Scan option for MFT-to-MFT setups, MFT now supports skipping file supervision in MFT-to-MFT transfers, improving efficiency and reducing processing overhead.

**Fixed**

- Trusted Networks Page Pagination, the Trusted Networks page has been further improved with pagination, allowing for easier navigation and more efficient management of networks.
- Optimized Buffer Size for Faster Large File Processing, buffer size has been optimized to improve checksum generation and processing time for larger files, enhancing overall performance.
- Enhanced Automated Jobs Experience and Integration, automated jobs have received several enhancements to improve the user experience, strengthen integrations, and increase the robustness of the automation process, leading to more reliable performance and greater efficiency in handling tasks.
- UI improvements, UI glitches have been fixed.

## [Version 3.9.0](/docs/mdmft/release-notes/changelog#version-390)

**Highlights**

- New Operations and Properties for Transfer Policies, new filter operations and properties have been added to transfer policies in MFT-to-MFT integration, offering enhanced flexibility and control over data transfers for improved security and efficiency.
- Restrict Supervisor Original File Downloads, administrators can now revoke supervisors' permission to download the original version of files, enhancing control and data security.
- Workflow Support for MFT to MFTIn MFT-to-MFT scenarios, transferred files can now carry MetaDefender Core™ workflow information, allowing seamless scanning with the same MetaDefender Core™ workflow on the destination MFT. This enhances consistency, simplifies processing and ensures smooth integration.
- User-Triggered Push/Pull Jobs, a new scheduling option is now available for push/pull type automated jobs, allowing them to be triggered exclusively by the user without running on a predefined schedule.
- Manual Execution of Automated Jobs on Selected Files/Folders, administrators and Automation Coordinators can now select files and folders on the My Files page to run existing automated jobs individually or in bulk, providing greater flexibility and control.
- User Mapping Option Indicator, user info-related tables now include a new field to indicate if user mapping is enabled, providing easier tracking and management of user mapping settings.
- Single Email Notification for Multiple Shares when multiple files or folders are shared with a user, a single email notification is sent, providing a summary of the shared items for easier tracking.
- Persistent User Settings, the MFT GUI now supports persistent user settings, retaining customizations like column reordering and visibility for a consistent and time-saving user experience.
- Core connection monitoring, the MFT GUI now supports Core connection status monitoring, similar to the MFT-to-MFT page, enhancing control and visibility.

**Fixed**

- Improved Transfer Policies and Settings, improvements have been made to transfer conditions:

  - "Transfer conditions" have been renamed to "transfer policies" for better clarity.
  - The file size property now includes a selectable measurement unit, offering greater flexibility and accuracy in defining transfer limits.

These changes enhance usability and ensure more precise configuration of transfer conditions.

- Enhanced Installer Messages, improvements have been made to the dialogs and error messages in the installer, providing clearer guidance and enhancing the user experience during installation.
- Trusted Networks Page Enhancements, the Trusted Networks page now features filtering capabilities, making it easier to manage and find specific networks for improved efficiency and user experience.
- UI improvements, UI glitches have been fixed.
