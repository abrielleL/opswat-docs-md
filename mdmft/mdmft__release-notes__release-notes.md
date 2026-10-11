<!-- source: https://www.opswat.com/docs/mdmft/release-notes/release-notes -->

# Release Notes

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
# [MetaDefender Managed File Transfer 3.11.6](/docs/mdmft/release-notes/release-notes#metadefender-managed-file-transfer-3116)

**Release Date:** 09 October 2026

MFT 3.11.6 delivers a recipient domain allow/block list for external sharing, role-based login IP restrictions, direct line manager supervision mode, and consolidated supervisor approval notifications, and over 20 bug fixes and reliability improvements.

# [New Features & Enhancements](/docs/mdmft/release-notes/release-notes#new-features--enhancements)

---

### [Security](/docs/mdmft/release-notes/release-notes#security)

#### [Role-Based Login IP Restrictions](/docs/mdmft/release-notes/release-notes#role-based-login-ip-restrictions)

Restrict login access by IP address or range for specific roles, letting administrators require internet-facing deployments route privileged sign-ins through approved networks only.

#### [Configurable Notification Link Domains](/docs/mdmft/release-notes/release-notes#configurable-notification-link-domains)

Define up to 10 approved domains in Settings → Notifications so links in upload, share, and account emails match the address each user actually reached MFT through.

#### [Recipient Domain Allow/Block List](/docs/mdmft/release-notes/release-notes#recipient-domain-allowblock-list)

Define allowed or blocked external recipient email domains under Settings → Security so files can only be shared, invited, or downloaded by recipients on approved domains.

#### [Bulk File Status Override](/docs/mdmft/release-notes/release-notes#bulk-file-status-override)

Manage file status overrides in bulk from the File Security Report, extending single-file overrides to multiple files blocked for reasons other than multiscanning, such as missing sanitization or password protection.

#### [Direct Line Manager Supervision Mode](/docs/mdmft/release-notes/release-notes#direct-line-manager-supervision-mode)

Assign each user's Active Directory line manager as their supervisor approver, eliminating manual group management for organizations with large AD directories.

---

### [User Management](/docs/mdmft/release-notes/release-notes#user-management)

#### [External User Inactivity Auto-Disable](/docs/mdmft/release-notes/release-notes#external-user-inactivity-auto-disable)

Configure external accounts to disable after a set period without a login, with the inactivity window adjustable globally in External Users Settings.

**Minor Enhancements**

- **Last Successful Import Timestamp** — View the date and time of the last successful user mapping import on the Import/Export page, shown only after a successful import has occurred and converted to your local timezone.

---

### [Automation](/docs/mdmft/release-notes/release-notes#automation)

#### [MFT-to-MFT Storage Recovery Retry](/docs/mdmft/release-notes/release-notes#mft-to-mft-storage-recovery-retry)

Trigger MFT-to-MFT transfer retries once target storage frees up after a disk-full or transient failure, removing the need for administrators to manually resync stuck files.

#### [Per-File MFT-to-MFT Sync](/docs/mdmft/release-notes/release-notes#per-file-mft-to-mft-sync)

Manage MFT-to-MFT batch transfers so each file syncs to the destination as soon as its own scan completes, instead of holding the whole batch until every file finishes.

---

### [Integrations](/docs/mdmft/release-notes/release-notes#integrations)

#### [Consolidated Supervisor Approval Notifications](/docs/mdmft/release-notes/release-notes#consolidated-supervisor-approval-notifications)

Enable a single consolidated email notification for supervisor approval on bulk upload jobs, replacing one notification per file once scanning, validation, and approval complete for the batch.

**Minor Enhancements**

- **Blue Line Email Template Redesign** — View outbound MFT emails redesigned with OPSWAT's Blue Line visual identity across every template and locale, verified for consistent rendering across email clients.

---

### [Administration](/docs/mdmft/release-notes/release-notes#administration)

#### [Cross-Product File Journey Tracking](/docs/mdmft/release-notes/release-notes#cross-product-file-journey-tracking)

Track a file's full journey across OPSWAT products in Central Management by forwarding session and transaction identifiers through MFT, unifying scan and transfer records into a single audit trail.

**Minor Enhancements**

- **Group Core Workflow Change Alert** — View an audit trail message when a Local or AD group's Core scanning workflow changes, clarifying the change for administrators reviewing file history.
- **Group Selection Dropdown Toggle** — Enable a switch to hide the Group Selection dropdown on file uploads, applying a default group for organizations that manage users through directory sync rather than manual group assignment.
- **LDAP GUID Identifier Hint** — View a UI hint when configuring LDAP that the unique identifier field must be a GUID attribute, reducing misconfiguration during setup.

---

---

# [Bug Fixes & Improvements](/docs/mdmft/release-notes/release-notes#bug-fixes--improvements)

---

### [Security Fixes](/docs/mdmft/release-notes/release-notes#security-fixes)

#### [Readonly Administrator User Mapping Access](/docs/mdmft/release-notes/release-notes#readonly-administrator-user-mapping-access)

Readonly Administrators have consistent read access to user mapping across every user type.

#### [Editor Role Folder Upload Access](/docs/mdmft/release-notes/release-notes#editor-role-folder-upload-access)

Users with Editor or Uploader access to a shared folder can upload into that folder through the API, matching the permission the API already reports for that share.

#### [MFA Enrollment Long Username Support](/docs/mdmft/release-notes/release-notes#mfa-enrollment-long-username-support)

MFA enrollment completes for users with long usernames, with the full secret key stored instead of being cut short.

---

### [Stability Fixes](/docs/mdmft/release-notes/release-notes#stability-fixes)

#### [Test Notification Modal Crash](/docs/mdmft/release-notes/release-notes#test-notification-modal-crash)

Sending a test notification from an email template opens and closes the confirmation modal cleanly.

#### [My Files Page With MFT-to-MFT Disabled](/docs/mdmft/release-notes/release-notes#my-files-page-with-mft-to-mft-disabled)

My Files and File Security Report render correctly on instances where MFT-to-MFT is disabled.

#### [Supervisor Endpoint Reliability Hardening](/docs/mdmft/release-notes/release-notes#supervisor-endpoint-reliability-hardening)

The supervisor active-configuration endpoint carries additional regression coverage after an intermittent, unreproduced service hang was reported.

---

### [Reliability Improvements](/docs/mdmft/release-notes/release-notes#reliability-improvements)

#### [Audit Log Retention Cleanup](/docs/mdmft/release-notes/release-notes#audit-log-retention-cleanup)

Audit logs are deleted according to the configured retention period even under heavy system usage and high log volume.

#### [Security Trend Widget 26-Week View](/docs/mdmft/release-notes/release-notes#security-trend-widget-26-week-view)

The Security Trend widget shows data for the Last 26 Weeks period, matching every other available date range on the dashboard.

#### [Malware Detection Engines Widget](/docs/mdmft/release-notes/release-notes#malware-detection-engines-widget)

The Top 5 Malware Detection Engines widget displays detection data whenever hits are present, matching the File Info page and other dashboard widgets.

#### [External User Welcome Email Credentials](/docs/mdmft/release-notes/release-notes#external-user-welcome-email-credentials)

External user welcome emails include the username or email address needed to sign in.

#### [Configurable Core Scan Upload Timeout](/docs/mdmft/release-notes/release-notes#configurable-core-scan-upload-timeout)

Large file uploads to MetaDefender Core apply a configurable stall timeout, with upload progress and outcome logged for failed scan submissions.

#### [Transfer Metadata Transaction ID](/docs/mdmft/release-notes/release-notes#transfer-metadata-transaction-id)

MFT transfer metadata carries a Transaction ID that links a file's journey across OPSWAT products into one audit trail record.

---

### [Behavior Corrections](/docs/mdmft/release-notes/release-notes#behavior-corrections)

#### [Group Storage Quota Indicator](/docs/mdmft/release-notes/release-notes#group-storage-quota-indicator)

The storage usage indicator in the user info panel shows remaining space when a storage quota is set at the group level, matching the display already shown for individually configured quotas.

#### [Group Upload Quota Enforcement](/docs/mdmft/release-notes/release-notes#group-upload-quota-enforcement)

Group-based file upload quotas apply consistently to third-party SSO and AD accounts, matching enforcement already applied to standard accounts.

#### [Core License Connection Status](/docs/mdmft/release-notes/release-notes#core-license-connection-status)

The Core Connection Status reflects an unlicensed MetaDefender Core instance accurately, and scan failures caused by a missing license include a clear reason.

#### [Download Page Completion State](/docs/mdmft/release-notes/release-notes#download-page-completion-state)

The shared-link download page stops polling and shows a clear confirmation once a file download succeeds.

#### [Supervisor Comment Field Validation](/docs/mdmft/release-notes/release-notes#supervisor-comment-field-validation)

The supervisor approval comment field enforces its input pattern in current Chromium-based browsers.

#### [Share Picker Refresh Pagination](/docs/mdmft/release-notes/release-notes#share-picker-refresh-pagination)

Refreshing a share or user picker replaces the visible list from the first page and continues scrolling normally afterward.

#### [Shared Folder Upload Permission Inheritance](/docs/mdmft/release-notes/release-notes#shared-folder-upload-permission-inheritance)

Files uploaded into a shared folder inherit the Editor permission assigned to that folder.

#### [Supervisor Approval Step 3 Setup](/docs/mdmft/release-notes/release-notes#supervisor-approval-step-3-setup)

Supervisor approval setup completes through every configuration step without getting stuck.

---

### [UI & Usability Fixes](/docs/mdmft/release-notes/release-notes#ui--usability-fixes)

- **Download Completion Indicator** — The download spinner stops once a file finishes downloading through an email or direct download link, matching the file-list download experience.
- **Manager-Based Supervisor Approval Wording** — Manager-based supervisor approval setup displays clearer descriptive text to guide administrators through configuration.
- **Supervisor Setup Filter Text** — Supervisor setup displays accurate guidance text for configuring the default supervisor through a filter in manager-based mode.
- **Download Page Checkmark Alignment** — The download confirmation checkmark is centered within its circular container in Firefox.

---
