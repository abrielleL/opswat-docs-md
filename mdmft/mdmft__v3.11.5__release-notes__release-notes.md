<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/release-notes/release-notes -->

# Release Notes

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
# [MetaDefender Managed File Transfer 3.11.5](/docs/mdmft/v3.11.5/release-notes/release-notes#metadefender-managed-file-transfer-3115)

**Release Date:** 24 August 2026

MFT 3.11.5 delivers per-group predefined folders, full SSO role mapping across every MFT role, designated folder upload restrictions, a consolidated MFT-to-MFT transfer status column, and over 30 bug fixes and reliability improvements.

# [New Features & Enhancements](/docs/mdmft/v3.11.5/release-notes/release-notes#new-features--enhancements)

---

### [Security](/docs/mdmft/v3.11.5/release-notes/release-notes#security)

#### [User Manager Role](/docs/mdmft/v3.11.5/release-notes/release-notes#user-manager-role)

Assign a read-only User Manager role for user management and audit, grantable via an AD group.

#### [Designated Folder Upload Restrictions](/docs/mdmft/v3.11.5/release-notes/release-notes#designated-folder-upload-restrictions)

Restrict uploads and downloads to folders an administrator assigns, keeping transfers out of unauthorized locations.

#### [Full SSO Role Mapping](/docs/mdmft/v3.11.5/release-notes/release-notes#full-sso-role-mapping)

Assign any MFT role to an SSO user, extending mapping beyond Admin and Automation Coordinator.

#### [External User Password Enforcement](/docs/mdmft/v3.11.5/release-notes/release-notes#external-user-password-enforcement)

Enforce a password creation or change prompt for external users at first login, matching the existing local-user requirement.

---

### [User Management](/docs/mdmft/v3.11.5/release-notes/release-notes#user-management)

#### [Per-Group Predefined Folders](/docs/mdmft/v3.11.5/release-notes/release-notes#per-group-predefined-folders)

Define a fixed set of root-level folders per user group, replacing free-form My Files access.

- Configure the folder list per group from Group Settings
- Folder changes propagate automatically as group membership changes

#### [Per-Group Navigation Visibility](/docs/mdmft/v3.11.5/release-notes/release-notes#per-group-navigation-visibility)

Configure Shared With Me and User Management navigation visibility per user group.

---

### [Automation](/docs/mdmft/v3.11.5/release-notes/release-notes#automation)

#### [MFT-to-MFT Destination Workflow Selection](/docs/mdmft/v3.11.5/release-notes/release-notes#mft-to-mft-destination-workflow-selection)

Assign a distinct destination scan workflow for each MFT-to-MFT synchronization direction.

---

### [Integrations](/docs/mdmft/v3.11.5/release-notes/release-notes#integrations)

#### [SMTP Sender Email Override](/docs/mdmft/v3.11.5/release-notes/release-notes#smtp-sender-email-override)

Set a single override sender address for all outbound SMTP messages, replacing the default administrator sender.

**Minor Enhancements**

- **File Integrity Email Clarity** — view clearer checksum terminology and a direct link to the affected file in integrity verification failure emails.

---

### [Platform](/docs/mdmft/v3.11.5/release-notes/release-notes#platform)

#### [SQL Server LocalDB Removal](/docs/mdmft/v3.11.5/release-notes/release-notes#sql-server-localdb-removal)

Enforce migration off SQL Server LocalDB before upgrading, so unsupported database configurations no longer receive new installer updates.

#### [HA Max Request Body Size](/docs/mdmft/v3.11.5/release-notes/release-notes#ha-max-request-body-size)

Configure the maximum allowed request body size for HA deployments to match workload requirements.

**Minor Enhancements**

- **HA Controller Version Display** — view HA Controller version numbers alongside MFT version numbers on the HA Configuration Tool Overview page.
- **LibreOffice Preview Engine Update** — preview Office documents using the latest LibreOffice release, incorporating upstream security fixes.

---

### [Administration](/docs/mdmft/v3.11.5/release-notes/release-notes#administration)

#### [Filtered File Security Export](/docs/mdmft/v3.11.5/release-notes/release-notes#filtered-file-security-export)

Export the File Security Report table in its currently filtered, sorted, and configured state.

#### [TCP Syslog Forwarding](/docs/mdmft/v3.11.5/release-notes/release-notes#tcp-syslog-forwarding)

Configure Syslog forwarding over TCP in addition to UDP for reliable audit event delivery.

#### [Audit Log Sanitization Hashes](/docs/mdmft/v3.11.5/release-notes/release-notes#audit-log-sanitization-hashes)

View file hashes captured before and after sanitization directly in the audit log entry.

#### [Database Health Status Banner](/docs/mdmft/v3.11.5/release-notes/release-notes#database-health-status-banner)

View a banner alerting administrators when the database connection is degraded or unreachable.

**Minor Enhancements**

- **Managed Folder Delete Confirmation** — view a confirmation dialog before a managed folder is deleted, preventing accidental removal.

---

### [Monitoring](/docs/mdmft/v3.11.5/release-notes/release-notes#monitoring)

#### [MFT-to-MFT Transfer Status Column](/docs/mdmft/v3.11.5/release-notes/release-notes#mft-to-mft-transfer-status-column)

View a single file transfer status column in My Files and File Analysis showing sync state and time.

---

# [Bug Fixes & Improvements](/docs/mdmft/v3.11.5/release-notes/release-notes#bug-fixes--improvements)

---

### [Security Fixes](/docs/mdmft/v3.11.5/release-notes/release-notes#security-fixes)

#### [SMTP Verification Response Disclosure](/docs/mdmft/v3.11.5/release-notes/release-notes#smtp-verification-response-disclosure)

SMTP server validation responses no longer reveal whether internal services on the MFT server or connected servers are reachable, closing a service enumeration path.

#### [MFT API Denial of Service](/docs/mdmft/v3.11.5/release-notes/release-notes#mft-api-denial-of-service)

The MFT API applies rate limiting and validation controls to close a Denial of Service exposure path identified during a customer security assessment.

#### [AD Credential and API Key Exposure](/docs/mdmft/v3.11.5/release-notes/release-notes#ad-credential-and-api-key-exposure)

AD credentials and the MD Core API key are no longer exposed through the access path identified during a penetration test.

#### [SSO Email Role Uniqueness](/docs/mdmft/v3.11.5/release-notes/release-notes#sso-email-role-uniqueness)

An SSO email address can be assigned to only one role at a time, preventing the same identity from being mapped to multiple conflicting roles.

---

### [Stability Fixes](/docs/mdmft/v3.11.5/release-notes/release-notes#stability-fixes)

#### [Processor Service Deadlock](/docs/mdmft/v3.11.5/release-notes/release-notes#processor-service-deadlock)

File transfer delete operations in the processor service complete without triggering a database deadlock that previously caused the operation to fail.

#### [Automation Job Log Page Rendering](/docs/mdmft/v3.11.5/release-notes/release-notes#automation-job-log-page-rendering)

The automation job execution log page renders correctly for jobs with a large number of log entries, rather than displaying a blank screen.

#### [Upload Progress Indicator Freeze](/docs/mdmft/v3.11.5/release-notes/release-notes#upload-progress-indicator-freeze)

The floating upload progress indicator updates and clears correctly during a Pull from MFT operation, rather than remaining frozen on screen.

#### [File Status After Version Upgrade](/docs/mdmft/v3.11.5/release-notes/release-notes#file-status-after-version-upgrade)

Files retain their correct processing status after upgrading from version 3.9.4 to 3.11.3, rather than becoming stuck in a Processing state.

#### [Automation Jobs Page Crash](/docs/mdmft/v3.11.5/release-notes/release-notes#automation-jobs-page-crash)

The automation jobs page loads without crashing due to a missing pipe provider.

#### [Email Template Configuration Modal](/docs/mdmft/v3.11.5/release-notes/release-notes#email-template-configuration-modal)

The General Configuration modal for email templates opens without console errors.

---

### [Reliability Improvements](/docs/mdmft/v3.11.5/release-notes/release-notes#reliability-improvements)

#### [Audit Logging Completeness](/docs/mdmft/v3.11.5/release-notes/release-notes#audit-logging-completeness)

Audit log entries are captured for actions that previously left no trail.

- **User mapping import/export** — importing or exporting the user mapping list is recorded in the audit log
- **Interrupted uploads** — interrupted file uploads are recorded in the audit trail

#### [User Creation Orphaned Record Conflicts](/docs/mdmft/v3.11.5/release-notes/release-notes#user-creation-orphaned-record-conflicts)

User creation completes without conflicting against orphaned records left behind by incomplete prior operations.

#### [Aggregated Data Reporting Toggle](/docs/mdmft/v3.11.5/release-notes/release-notes#aggregated-data-reporting-toggle)

The Aggregated Data Reporting toggle displays its true configured state, and telemetry metrics are captured accurately for every instance.

#### [Shared Folder Email Direct Link](/docs/mdmft/v3.11.5/release-notes/release-notes#shared-folder-email-direct-link)

Share invitation emails for an upload-only folder link directly to the target folder or the Shared With Me landing page.

#### [Scheduled SFTP Push Timing](/docs/mdmft/v3.11.5/release-notes/release-notes#scheduled-sftp-push-timing)

Scheduled SFTP Push jobs with no files to send complete without an unnecessary 15-second delay.

---

### [Behavior Corrections](/docs/mdmft/v3.11.5/release-notes/release-notes#behavior-corrections)

#### [File Storage Move Status Message](/docs/mdmft/v3.11.5/release-notes/release-notes#file-storage-move-status-message)

The success message shown after a storage move operation reflects whether files were actually moved to active storage, rather than reporting success when none were moved.

#### [MFT-to-MFT Manual Sync Toggle Enforcement](/docs/mdmft/v3.11.5/release-notes/release-notes#mft-to-mft-manual-sync-toggle-enforcement)

The manual sync-to-destination action is unavailable when Allow Users to Start Manual Synchronization is turned off, matching the configured setting.

#### [Imported Configuration External User Settings](/docs/mdmft/v3.11.5/release-notes/release-notes#imported-configuration-external-user-settings)

Importing a configuration file from a previous MFT version preserves the Show My Files and Allow to Share Files settings for external users.

#### [SSO Redirect URL Update](/docs/mdmft/v3.11.5/release-notes/release-notes#sso-redirect-url-update)

The SSO configuration redirect URL can be updated and saved successfully.

#### [Shared Folder Upload Actor Attribution](/docs/mdmft/v3.11.5/release-notes/release-notes#shared-folder-upload-actor-attribution)

Email notifications for an upload to a shared folder credit the user who performed the upload, rather than always crediting the folder owner.

#### [MFT-to-MFT Guest User Deletion Scope](/docs/mdmft/v3.11.5/release-notes/release-notes#mft-to-mft-guest-user-deletion-scope)

Deleting an auto-created guest user at the destination MFT no longer deletes the corresponding local user at the source MFT.

#### [File Status After Scan Completion](/docs/mdmft/v3.11.5/release-notes/release-notes#file-status-after-scan-completion)

A file's status updates correctly once its scan completes, rather than remaining in Processing indefinitely.

#### [Group File Policy Behavior](/docs/mdmft/v3.11.5/release-notes/release-notes#group-file-policy-behavior)

A group's file policy applies its managed folders correctly across membership and naming changes.

- **Folder creation after group assignment** — folders defined in a group's file policy are created for members assigned to the group after the policy was configured
- **Policy scope to like-named folders** — a group's file policy applies only to its managed folder, rather than to every folder at the My Files root sharing the same name

#### [Share Menu Group Restriction Visibility](/docs/mdmft/v3.11.5/release-notes/release-notes#share-menu-group-restriction-visibility)

Users in a group with sharing disabled are hidden from the share menu, rather than appearing as available recipients.

#### [Share Dropdown Duplicate Supervisor Entry](/docs/mdmft/v3.11.5/release-notes/release-notes#share-dropdown-duplicate-supervisor-entry)

The share-with dropdown for a shared folder lists its supervisor once instead of twice, so folder sharing notifications reach the intended recipient.

---

### [UI & Usability Fixes](/docs/mdmft/v3.11.5/release-notes/release-notes#ui--usability-fixes)

- **File Security Report Size Filter Unit** — the file size filter slider on the File Security Report displays values in a readable unit rather than raw bytes.
- **Upload Modal Share Field State** — share-related fields in the file upload modal are disabled when file or folder sharing is not allowed for the user.
- **Local Users Page Role Display** — special user roles display their actual role on the Local Users page, rather than appearing as a simple user.
- **External Password Hint Text** — the hint text for Enforce Random Password for External Users accurately describes which accounts can set a password and notes the required SMTP configuration.
