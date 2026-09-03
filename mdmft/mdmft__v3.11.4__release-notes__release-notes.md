<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/release-notes/release-notes -->

# Release Notes

Summarize Page    Connect to Cursor Connect to VS Code
## [MetaDefender Managed File Transfer 3.11.4](/docs/mdmft/v3.11.4/release-notes/release-notes#metadefender-managed-file-transfer-3114)

**Release Date:** 06, July 2026

MFT 3.11.4 delivers user group access controls for folder and sharing management, configurable Login Page Announcements, an expanded SFT Database Configuration Tool, and over 55 bug fixes and reliability improvements.

## [New Features & Enhancements](/docs/mdmft/v3.11.4/release-notes/release-notes#new-features--enhancements)

---

### [Security](/docs/mdmft/v3.11.4/release-notes/release-notes#security)

#### [One-Time Upload Token](/docs/mdmft/v3.11.4/release-notes/release-notes#one-time-upload-token)

Generate a single-use token for file upload authorization, enabling controlled external upload access without exposing user credentials or persistent sharing links.

#### [SSO Admin Role Assignment](/docs/mdmft/v3.11.4/release-notes/release-notes#sso-admin-role-assignment)

Assign Readonly Administrator and Helpdesk Administrator roles to users via SSO group claims, extending automatic role provisioning to administrative role types.

#### [SSO Group as Supervisor Approver](/docs/mdmft/v3.11.4/release-notes/release-notes#sso-group-as-supervisor-approver)

Assign an SSO group as the supervisor for approval workflows, enabling approval responsibility to follow group membership without per-user manual configuration.

---

### [User Management](/docs/mdmft/v3.11.4/release-notes/release-notes#user-management)

#### [User Group Access Controls](/docs/mdmft/v3.11.4/release-notes/release-notes#user-group-access-controls)

Configure folder, sharing, and Trash permissions at the group level, restricting actions for specific user groups without per-user configuration.

- **Folder creation** — prevent group members from adding folders in shared spaces where only file uploads are permitted
- **Folder renaming** — maintain consistent folder structures by disabling rename for selected groups
- **File and folder sharing** — enforce group-level data distribution policies
- **Trash access** — hide the Trash section for groups that do not require permanent deletion

#### [External User Interface Restrictions](/docs/mdmft/v3.11.4/release-notes/release-notes#external-user-interface-restrictions)

Hide the Sharing panel and My Files section for External Users, presenting a scoped interface limited to their permitted access areas.

**Minor Enhancements**

- **Ad Hoc Guest Sharing Reliability** — guest accounts created on-the-fly during file sharing are processed through a consolidated creation flow, reducing edge cases in shared space provisioning.

---

### [Automation](/docs/mdmft/v3.11.4/release-notes/release-notes#automation)

#### [Path-Based Transfer Filtering](/docs/mdmft/v3.11.4/release-notes/release-notes#path-based-transfer-filtering)

Filter file transfer operations by path patterns to restrict, allow, or redirect transfers based on source or destination path criteria.

#### [MFT-to-MFT TCP Connection Limit](/docs/mdmft/v3.11.4/release-notes/release-notes#mft-to-mft-tcp-connection-limit)

Configure the maximum number of concurrent TCP connections for MFT-to-MFT transfers over one-way network diodes, preventing connection exhaustion in high-throughput environments.

---

### [Integrations](/docs/mdmft/v3.11.4/release-notes/release-notes#integrations)

#### [Guest Sharing Email Template](/docs/mdmft/v3.11.4/release-notes/release-notes#guest-sharing-email-template)

Invitation emails sent to guest users created during file sharing use a dedicated template, providing clear first-access context separate from standard sharing notifications.

#### [File Deletion Email Notification](/docs/mdmft/v3.11.4/release-notes/release-notes#file-deletion-email-notification)

Receive an email notification when a file is moved to Trash, keeping users informed of deletions affecting shared or monitored content.

---

### [Platform](/docs/mdmft/v3.11.4/release-notes/release-notes#platform)

#### [HA Controller Live Configuration Apply](/docs/mdmft/v3.11.4/release-notes/release-notes#ha-controller-live-configuration-apply)

Configuration changes saved in the HA Controller are applied to the cluster immediately without requiring a service restart, reducing planned downtime for HA updates.

#### [SQL HA Connection String Reconfiguration](/docs/mdmft/v3.11.4/release-notes/release-notes#sql-ha-connection-string-reconfiguration)

Reconfigure the SQL connection string for MFT in an HA deployment without running the installer, reducing downtime when updating database connection settings.

**Minor Enhancements**

- **LibreOffice Preview Engine Update** — preview Office documents using LibreOffice 26.2.1, incorporating upstream security fixes and improved compatibility with recent document formats.
- **HA Configuration Tool UI Refinements** — the HA Configuration Tool incorporates design updates for improved clarity and visual consistency with the MFT administrative interface.

---

### [Administration](/docs/mdmft/v3.11.4/release-notes/release-notes#administration)

#### [File Status on Post-Action Failure](/docs/mdmft/v3.11.4/release-notes/release-notes#file-status-on-post-action-failure)

Files processed successfully but with a failed post-action display an accurate availability status, distinguishing a completed transfer from a post-processing error.

#### [Login Page Announcement](/docs/mdmft/v3.11.4/release-notes/release-notes#login-page-announcement)

Configure a custom announcement message that displays on the MFT login page, communicating maintenance windows or access notices to all users before authentication.

- **Announcement display** — administrator-configured messages appear as banners on the login page before sign-in

#### [Column-Level Table Filtering](/docs/mdmft/v3.11.4/release-notes/release-notes#column-level-table-filtering)

Filter table data at the column level across MFT list views, enabling targeted searches by specific field values without affecting other column displays.

**Minor Enhancements**

- **SharePoint Add-in Removal** — the legacy SharePoint Add-in option is removed from the MFT interface, directing SharePoint integration to the supported SharePoint connector path.

---

### [Monitoring](/docs/mdmft/v3.11.4/release-notes/release-notes#monitoring)

#### [Usage Report](/docs/mdmft/v3.11.4/release-notes/release-notes#usage-report)

Report Aggregated Data — anonymized statistics, measures, and usage information as defined in the [OPSWAT Terms of Service](https://www.opswat.com/legal/terms-of-service) — to help OPSWAT improve its products.

---

### [File Storage](/docs/mdmft/v3.11.4/release-notes/release-notes#file-storage)

#### [Flexible File Download Format](/docs/mdmft/v3.11.4/release-notes/release-notes#flexible-file-download-format)

Download multiple files as a single ZIP archive or as individual files, choosing the format best suited to the recipient's workflow at the time of download.

---

## [Bug Fixes & Improvements](/docs/mdmft/v3.11.4/release-notes/release-notes#bug-fixes--improvements)

---

### [Security Fixes](/docs/mdmft/v3.11.4/release-notes/release-notes#security-fixes)

#### [SSO Update Button Permission](/docs/mdmft/v3.11.4/release-notes/release-notes#sso-update-button-permission)

The SSO configuration Update button is disabled for Readonly Administrators, consistent with their non-write access to authentication settings.

#### [REST API Denial of Service Vulnerability](/docs/mdmft/v3.11.4/release-notes/release-notes#rest-api-denial-of-service-vulnerability)

The MFT REST API applies request rate limiting and input validation controls to close a Denial of Service exposure path in the REST layer.

#### [Database Tool SQL Auth Certificate Trust](/docs/mdmft/v3.11.4/release-notes/release-notes#database-tool-sql-auth-certificate-trust)

The SFT Database Configuration Tool enforces SQL Server certificate validation in SQL authentication mode rather than unconditionally trusting self-signed certificates.

---

### [Stability Fixes](/docs/mdmft/v3.11.4/release-notes/release-notes#stability-fixes)

#### [Automation Job Memory Growth](/docs/mdmft/v3.11.4/release-notes/release-notes#automation-job-memory-growth)

The Next service memory usage returns to baseline after prolonged automation job execution, without requiring a service restart to recover.

#### [HA HTTPS Login Page Loading](/docs/mdmft/v3.11.4/release-notes/release-notes#ha-https-login-page-loading)

The MFT login page loads correctly when both the HA Controller and MFT nodes are configured to run in HTTPS mode.

#### [Archive Download Job Creation](/docs/mdmft/v3.11.4/release-notes/release-notes#archive-download-job-creation)

Creating archive download jobs completes successfully without encountering configuration or initialization errors.

#### [Upload Request Stream Disposal](/docs/mdmft/v3.11.4/release-notes/release-notes#upload-request-stream-disposal)

File upload request streams are disposed correctly after transfer completion, preventing resource accumulation during high-volume upload operations.

#### [Job Recovery After SQL Connectivity Loss](/docs/mdmft/v3.11.4/release-notes/release-notes#job-recovery-after-sql-connectivity-loss)

Automation jobs interrupted by a transient SQL connectivity loss release their in-memory lock and resume processing rather than remaining permanently stuck.

#### [SFT Database Configuration Tool Installation](/docs/mdmft/v3.11.4/release-notes/release-notes#sft-database-configuration-tool-installation)

Installation, upgrade, and rollback operations complete without unexpected failures across Windows Authentication and SQL authentication modes.

- **Windows Authentication** — the tool completes Windows Auth configuration without a DLL not found error
- **Upgrade database connection** — installer upgrades complete the database connection step without failing in environments with custom SQL parameters
- **Rollback state restoration** — rolling back a configuration change restores the original state, leaving MFT fully operational

---

### [Reliability Improvements](/docs/mdmft/v3.11.4/release-notes/release-notes#reliability-improvements)

#### [File Classification Pull Job Status](/docs/mdmft/v3.11.4/release-notes/release-notes#file-classification-pull-job-status)

MFT pull jobs with file classification report an accurate completion status reflecting whether a file was transferred, rather than showing success when no transfer occurred.

#### [Permanent File Deletion Audit Log](/docs/mdmft/v3.11.4/release-notes/release-notes#permanent-file-deletion-audit-log)

Permanent file deletions complete without generating repeated error log entries about missing metadata, and audit records for deleted files are removed from the file audit correctly.

#### [MFT-to-MFT Transfer Logging](/docs/mdmft/v3.11.4/release-notes/release-notes#mft-to-mft-transfer-logging)

MFT-to-MFT file transfers emit detailed log entries for each transfer step, improving diagnostic visibility for transfer failures and latency issues.

#### [SMB Pull Connection Loss Handling](/docs/mdmft/v3.11.4/release-notes/release-notes#smb-pull-connection-loss-handling)

SMB Pull jobs complete successfully without reporting a false client disconnection failure when the SMB connection remains active throughout the transfer.

#### [SQL Query Performance](/docs/mdmft/v3.11.4/release-notes/release-notes#sql-query-performance)

Database query execution for common MFT operations is optimized, reducing latency for high-frequency administrative and transfer workflows.

#### [Expired OTP Audit Logging](/docs/mdmft/v3.11.4/release-notes/release-notes#expired-otp-audit-logging)

Attempts to authenticate with an expired OTP code are recorded in the audit log, providing a complete record of failed authentication events.

#### [Shared Space Reliability](/docs/mdmft/v3.11.4/release-notes/release-notes#shared-space-reliability)

Shared content is accessible and deliverable across all sharing configurations and user types.

- **Shared With Me downloads** — files listed in the Shared With Me view download successfully across all permission levels
- **Ad hoc guest access** — guest users created on-the-fly during file sharing access the shared space without encountering a user collection validation error

---

### [Behavior Corrections](/docs/mdmft/v3.11.4/release-notes/release-notes#behavior-corrections)

#### [Sharing Disabled State Response](/docs/mdmft/v3.11.4/release-notes/release-notes#sharing-disabled-state-response)

Accessing sharing endpoints when sharing is globally disabled returns a handled response rather than a 500 server error.

#### [Setup Wizard Rate Limit Configuration](/docs/mdmft/v3.11.4/release-notes/release-notes#setup-wizard-rate-limit-configuration)

Rate limit values configured during the Setup Wizard via the spark ignition file are applied to the running MFT instance.

#### [SFTP SSH Key Passphrase Error Message](/docs/mdmft/v3.11.4/release-notes/release-notes#sftp-ssh-key-passphrase-error-message)

SFTP connections configured for SSH key-only authentication reject passphrase-protected keys with a password required message rather than an incorrect key error.

#### [HA Controller Upgrade Directory Enforcement](/docs/mdmft/v3.11.4/release-notes/release-notes#ha-controller-upgrade-directory-enforcement)

Upgrading the HA Controller retains the original installation directory and does not present an option to select a different path during the upgrade process.

#### [External User File Sharing Permission](/docs/mdmft/v3.11.4/release-notes/release-notes#external-user-file-sharing-permission)

External users with the Allow External Users to Share Files setting enabled can share files as expected, consistent with the configured policy.

#### [Pull to User CSV Special Character Support](/docs/mdmft/v3.11.4/release-notes/release-notes#pull-to-user-csv-special-character-support)

CSV recipient files for SFTP Pull to User jobs process entries containing non-alphabetic and special characters without parsing errors.

#### [Email Template User Name Display](/docs/mdmft/v3.11.4/release-notes/release-notes#email-template-user-name-display)

Notification emails display the recipient's username or display name as defined in the email template, rather than falling back to a system-generated default.

#### [Orphaned Required Question Upload Block](/docs/mdmft/v3.11.4/release-notes/release-notes#orphaned-required-question-upload-block)

Required questions in secure web form sections with no parent section no longer block file uploads for non-administrator users.

#### [Duplicate Section Name Handling](/docs/mdmft/v3.11.4/release-notes/release-notes#duplicate-section-name-handling)

Secure web form sections with identical names are displayed as distinct sections rather than merged into a single combined view.

#### [File Scan State on Core Unavailability](/docs/mdmft/v3.11.4/release-notes/release-notes#file-scan-state-on-core-unavailability)

Files enter a correct error state when the scanning service returns a 503 response, rather than remaining indefinitely in the Processing - Scanning state.

#### [File Deletion With Trash Disabled](/docs/mdmft/v3.11.4/release-notes/release-notes#file-deletion-with-trash-disabled)

Users in groups with Trash disabled can delete files directly, rather than encountering a deletion error caused by the absence of the Trash destination.

#### [No-Email User Warning List Scope](/docs/mdmft/v3.11.4/release-notes/release-notes#no-email-user-warning-list-scope)

The warning list for users without configured email addresses excludes Central Management-managed accounts and third-party user accounts, which do not require local email configuration.

#### [SFT Database Configuration Tool Behavior](/docs/mdmft/v3.11.4/release-notes/release-notes#sft-database-configuration-tool-behavior)

Configuration and rollback operations in the SFT Database Configuration Tool produce accurate results across all scenarios.

- **Password special characters** — accepts passwords containing special characters, supporting the full range permitted by SQL Server
- **Log on as account rollback** — restores the original Windows account for MFT services to its pre-change state after rollback
- **Rollback service notification** — completes rollback without reporting a false mftHelper service failure when the service restarts successfully

#### [File Security Report Filters](/docs/mdmft/v3.11.4/release-notes/release-notes#file-security-report-filters)

File Security Report filters behave correctly across all filter types, value combinations, and character sets.

- **Filter persistence** — active filters are preserved when navigating away and returning to the page
- **OR logic** — combining values in the Origin column returns files matching any of the selected values
- **Non-Latin characters** — file classification filter values with accented or non-Latin characters are processed correctly
- **Date range boundary** — the to date includes records on the specified date, using inclusive boundary behavior

---

### [UI & Usability Fixes](/docs/mdmft/v3.11.4/release-notes/release-notes#ui--usability-fixes)

- **Supervisor Level 2 Dropdown** — the supervisor approval dropdown for level 2 in mixed step-based approval workflows opens and responds to selection correctly.
- **Automation Job Target MFT Field State** — input fields for MFT-specific job configuration are disabled when no target MFT is selected.
- **Upload Questionnaire Navigation Button** — multi-step upload questionnaires display the Next button at intermediate steps and the Complete Upload button only at the final step.
- **Upload Question Column Header Display** — pending approval views show the correct column header rather than the question text in the column label position.
- **Automation Job Group User View** — automation jobs display a consistent configuration view for users who are members of a group.
- **Blank Username Validation** — automation job usernames containing only whitespace characters fail validation with a clear error message.
- **HA Configuration Tool Error Styling** — error messages in the HA Configuration Tool are displayed in red, providing the expected visual feedback for validation and runtime failures.
- **Audit Filter Dropdown Behavior** — filter dropdowns on the Audit page open and display available options correctly across all filtering categories.
- **Email OTP Authentication UI** — the email OTP authentication flow includes updated interface elements for improved clarity and consistency.
- **Automation Job Period Input Validation** — the Set Period field rejects negative and decimal number inputs, accepting only positive integer values.
- **AD User Notification Email GUI Update** — adding a notification email address for Active Directory users reflects the update in the interface immediately without a page reload.
- **Automation Job UI Rendering** — automation job configuration pages render correctly across all job types, displaying complete form fields and controls.
- **Database Tool --trust-server-certificate Help** — the SFT Database Configuration Tool command-line help displays valid argument descriptions for the --trust-server-certificate flag.
- **Database Tool --encrypt Help** — the SFT Database Configuration Tool command-line help displays valid argument descriptions for the --encrypt flag.
- **Database Tool Service Account Validation** — the tool reports a clear error when the selected Windows account is not a member of the Log on as a service security group.
- **Pull to User Path Configuration Visibility** — the path configuration field is hidden when Enable sync all users is active, displaying only settings relevant to the selected mode.
- **MFT Pull Toggle Label Clarity** — the MFT Pull to User toggle displays a label that accurately reflects the current operational mode.
- **SFTP Push Option Label Clarity** — SFTP Push job configuration labels are updated to accurately describe each option's behavior.
- **Malware Detection Count Filter Display** — the Malware detection count filter on the File Security Report does not present -1 as a selectable filter value.
- **Secure Web Forms General Availability** — Secure Web Forms is available as a generally available feature, with the BETA designation removed from all UI surfaces.
