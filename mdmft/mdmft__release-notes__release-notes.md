<!-- source: https://www.opswat.com/docs/mdmft/release-notes/release-notes -->

# Release Notes

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
# [MetaDefender Managed File Transfer 3.12.0](/docs/mdmft/release-notes/release-notes#metadefender-managed-file-transfer-3120)

**Release Date:** 19 November 2026

MFT 3.12.0 delivers an inbound SFTP server, a .NET 10 and Entity Framework platform, local administrator MFA bypass controls, and over 90 bug fixes and reliability improvements.

# [New Features & Enhancements](/docs/mdmft/release-notes/release-notes#new-features--enhancements)

---

### [Security](/docs/mdmft/release-notes/release-notes#security)

#### [Local Administrator MFA Bypass](/docs/mdmft/release-notes/release-notes#local-administrator-mfa-bypass)

Enable local administrators to skip MFA when signing in from the MFT server, giving a recovery path when the authenticator fails.

- Sign in from localhost without an MFA challenge when MFA is required system-wide; other users and remote connections are still challenged
- Turn the localhost bypass on or off next to the MFA settings, with changes recorded in the General Audit

#### [Skip Scan Option Visibility Control](/docs/mdmft/release-notes/release-notes#skip-scan-option-visibility-control)

Restrict the Skip Scan on Upload option for external users so non-administrators cannot disable malware scanning.

#### [Authenticated Access to Public Download Links](/docs/mdmft/release-notes/release-notes#authenticated-access-to-public-download-links)

Download files uploaded from MOP as an authorized customer without disabling Download Authentication Required, so the link alone grants no access.

#### [Auto-Approval of Unsanitizable Allowed Files](/docs/mdmft/release-notes/release-notes#auto-approval-of-unsanitizable-allowed-files)

Approve files that cannot be sanitized but are marked Allowed by multiscanning without manual review, with each approval recorded in the audit log.

#### [Group-Level Email OTP Policy](/docs/mdmft/release-notes/release-notes#group-level-email-otp-policy)

Configure Email OTP or another MFA authenticator per user group instead of only at the organization level.

---

### [User Management](/docs/mdmft/release-notes/release-notes#user-management)

#### [Invitation-Based External User Registration](/docs/mdmft/release-notes/release-notes#invitation-based-external-user-registration)

Invite external users by email address and expiry date so recipients create their own accounts through an onboarding page.

#### [Shared External User Visibility](/docs/mdmft/release-notes/release-notes#shared-external-user-visibility)

Configure a global setting that lets regular users view and share with all external users, not only the ones they created.

---

### [Automation](/docs/mdmft/release-notes/release-notes#automation)

#### [MFT-to-MFT Bandwidth Limit](/docs/mdmft/release-notes/release-notes#mft-to-mft-bandwidth-limit)

Set a maximum outbound bandwidth shared by all MFT-to-MFT transfers so synchronization cannot saturate the network.

---

### [Integrations](/docs/mdmft/release-notes/release-notes#integrations)

#### [Inbound SFTP Server](/docs/mdmft/release-notes/release-notes#inbound-sftp-server)

Enable MFT to receive files over SFTP so external users and systems upload directly into the standard scan, storage, and policy pipeline.

- Authenticate with MFT credentials or registered SSH public keys, honoring locked, disabled, and expired account status
- Configure the service state, listen address, port, and host keys from Settings > Security
- Register SSH user keys with a Key only, Both required, or Inherit authentication policy
- Track SFTP sessions, uploads, and failed sign-ins in the audit log

---

### [Platform](/docs/mdmft/release-notes/release-notes#platform)

#### [Nginx and OpenSSL Upgrade](/docs/mdmft/release-notes/release-notes#nginx-and-openssl-upgrade)

Upgrade the bundled web server to Nginx 1.31.6 with OpenSSL 3.5.9, replacing an end-of-life version with known vulnerabilities.

#### [.NET 10 Platform Modernization](/docs/mdmft/release-notes/release-notes#net-10-platform-modernization)

Move MFT to .NET 10, an ASP.NET Core REST host, and Entity Framework Core data access, improving throughput and concurrency.

- Run MFT services on .NET 10 instead of the .NET Framework runtime
- Serve REST requests from an ASP.NET Core host that replaces the WCF-based host
- Access the database through Entity Framework Core instead of stored procedures

---

### [Administration](/docs/mdmft/release-notes/release-notes#administration)

#### [German Language Support](/docs/mdmft/release-notes/release-notes#german-language-support)

Select German as a built-in language in user settings, global language settings, and the setup wizard, including audit log and email text.

#### [Share Dialog Email Visibility](/docs/mdmft/release-notes/release-notes#share-dialog-email-visibility)

Configure whether recipients' email addresses appear next to their names in the share dialog.

---

# [Bug Fixes & Improvements](/docs/mdmft/release-notes/release-notes#bug-fixes--improvements)

---

### [Security Fixes](/docs/mdmft/release-notes/release-notes#security-fixes)

#### [Penetration Test Findings](/docs/mdmft/release-notes/release-notes#penetration-test-findings)

Penetration test findings across input validation, license enforcement, and role-based access are closed.

- **HTML injection in name fields** — Group, credential, and MFT profile names reject HTML and special characters on the server, matching the limits the web UI already enforces.
- **License user limit bypass** — The license user limit holds against attempts to add users directly through SQL Server, closing a bypass of the web management check.
- **Credential exposure to low-privileged roles** — Read-only and Helpdesk administrators cannot retrieve Active Directory credentials or the internal MetaDefender Core API key through the vpack configuration API.
- **Privilege escalation by Helpdesk administrators** — Helpdesk administrators cannot promote accounts to the Administrator role or set a new password during the role change.

#### [Guest ID Exposure](/docs/mdmft/release-notes/release-notes#guest-id-exposure)

Read-only and restricted administrators cannot see, search for, or copy guest IDs that give access to guest files.

- **Guest list** — Read-only and restricted administrators cannot copy a guest ID from the web UI to reach the guest's files.
- **Share picker** — The share dialog recipient picker hides guest IDs from read-only and restricted administrators.
- **Guest search** — The Guest Users search does not match hidden guest IDs for read-only and restricted administrators.

#### [Authentication Enforcement](/docs/mdmft/release-notes/release-notes#authentication-enforcement)

Sign-in paths enforce MFA, one-time SAML responses, account expiry, and directory password handling.

- **Guest invitation links** — Guests opening an invitation link are prompted for MFA when email OTP is enabled.
- **Directory password storage** — MFT does not store a hash of an Active Directory user's password after sign-in.
- **SAML response replay** — A SAML response that has already been used is refused when posted again to the sign-in endpoint.
- **Expired accounts** — Accounts past their expiry date are refused at sign-in without waiting for the expiry job.

#### [API Authorization Gaps](/docs/mdmft/release-notes/release-notes#api-authorization-gaps)

API calls verify that the caller owns or may manage the resource before acting on it.

- **File classification and tags** — Read-only Administrators and Auditors cannot change the classification or tags of another user's unshared file.
- **One-time token deletion** — A one-time token generated by one user cannot delete another user's group transfer.
- **API key extension** — A user cannot extend another user's API key or change its skip scan and skip supervision flags.
- **Core workflow assignment** — Only roles with account management rights over the target can set the MetaDefender Core workflow of an account.
- **Archive downloads** — Only the creator of an archive can download it, so other users cannot reach files never shared with them.
- **Archive cancellation** — Cancelling an archive download requires authentication and ownership of the archive.
- **Original file access through archives** — Archive downloads return only the sanitized copy to users who may not receive the original of a Core-converted file.

#### [Policy Enforcement Through the API](/docs/mdmft/release-notes/release-notes#policy-enforcement-through-the-api)

Settings enforced in the web UI are enforced for API requests as well.

- **Guest creation** — The Disable Guest Creation by Users setting is enforced when a guest is created on the fly through the share API.
- **Public archive passwords** — Public archive downloads follow the mandatory password protection and system password policy settings.
- **Group membership on upload** — Uploads must name one of the user's own groups when stating group membership is required.
- **Local accounts** — Local accounts created through the API follow the Force password reset on user creation setting.
- **File expiry** — Users without permission to edit file expiration receive the default expiry on upload.
- **Trusted Network downloads** — Download permissions are enforced for connections from Trusted Networks.
- **External users** — External users created through the API follow the Force password reset on user creation setting.

#### [Log Redaction Failure Handling](/docs/mdmft/release-notes/release-notes#log-redaction-failure-handling)

Log and trace redaction drops a record when scrubbing fails instead of exporting it unredacted, and its patterns run with a match timeout.

#### [Supervision Configuration Gaps](/docs/mdmft/release-notes/release-notes#supervision-configuration-gaps)

Group supervision applies to the designated group and cannot be configured into an unsupervised state.

- **Files of other groups** — Group supervisors can read and comment only on files designated to their own group container.
- **Default container** — Posting supervisor groups to the default supervision container is rejected instead of removing all default supervisors.
- **Approval count of 0** — A group supervision container saved with an approval count of 0 uses the global count or is rejected instead of leaving the group unsupervised.

---

### [Stability Fixes](/docs/mdmft/release-notes/release-notes#stability-fixes)

#### [Upgrade Completion](/docs/mdmft/release-notes/release-notes#upgrade-completion)

Upgrades from earlier versions finish with all services installed and running.

- **Services fail to start** — MFT services start after upgrading a SQL authentication installation from 3.11.4.
- **Missing Node Manager service** — Upgrades from older versions install the Node Manager service on standalone MFT.
- **Untrusted SQL Server certificate** — Upgrades complete without error 1603 when the SQL Server certificate is not trusted.

#### [UpdateCredentials and ChangeProtocol Tools](/docs/mdmft/release-notes/release-notes#updatecredentials-and-changeprotocol-tools)

The UpdateCredentials and ChangeProtocol tools start and run to completion.

#### [MFT-to-MFT Error Handling](/docs/mdmft/release-notes/release-notes#mft-to-mft-error-handling)

MFT-to-MFT sync keeps running when the source and destination differ or the destination returns an error.

- **Version mismatch between source and target** — The Next service keeps running when a source MFT is upgraded before its target MFT with Enforce Synchronization enabled.
- **Destination error responses** — The source MFT reads HTTP error responses from the destination and records the actual error in the audit log.

#### [Overlapping Outbreak Statistics Jobs](/docs/mdmft/release-notes/release-notes#overlapping-outbreak-statistics-jobs)

A scheduled statistics job that exceeds its time limit is cancelled so overlapping runs do not stack up.

#### [HA Failover Settling](/docs/mdmft/release-notes/release-notes#ha-failover-settling)

HA failover settles on the new node instead of switching back and forth between instances.

---

### [Reliability Improvements](/docs/mdmft/release-notes/release-notes#reliability-improvements)

#### [Stranded Empty File Transfers](/docs/mdmft/release-notes/release-notes#stranded-empty-file-transfers)

Empty file transfers left in the processing state are cleaned up by a background job instead of remaining indefinitely.

#### [File Security Report Accuracy](/docs/mdmft/release-notes/release-notes#file-security-report-accuracy)

File Security Report and Processing History data matches what the files actually show.

- **Locked file time** — The File Security Report shows the unlock time next to the Locked status while Outbreak Prevention holds a file.
- **Processing History** — Processing History lists each file once regardless of how many tags it has.
- **CSV export file names** — The filtered CSV export lists the same physical file names as the File Security Report grid.
- **Column sorting** — Sorting by Scan Result, Malware, Data Loss, or Vulnerabilities returns the correct order and matches the exported CSV.

#### [RADIUS Failed Sign-In Auditing](/docs/mdmft/release-notes/release-notes#radius-failed-sign-in-auditing)

Failed RADIUS sign-ins write General Audit entries for wrong passwords, unknown users, server and secret errors, and blocked login types.

#### [MFT-to-MFT Synchronization](/docs/mdmft/release-notes/release-notes#mft-to-mft-synchronization)

MFT-to-MFT sync completes for guests, existing folders, and discovered destinations.

- **Bi-directional guest items** — Guest items transfer to the destination MFT in bi-directional setups when the guest's creator exists only on the destination.
- **Duplicate guest accounts** — Concurrent group transfers from the same source user create one guest account on the destination MFT instead of duplicates that each use a license seat.
- **Folders that already exist** — Files uploaded into a folder that already exists on the destination MFT transfer without a conflict error aborting the sync.
- **Missing impersonated user** — The destination MFT creates an auto guest or falls back to the API key owner when the impersonated user does not exist, instead of returning a server error.
- **Discovered destination MFT** — A discovered network MFT can be added as a destination MFT.

#### [Share Notification Emails](/docs/mdmft/release-notes/release-notes#share-notification-emails)

Share-related notification emails are sent with the correct content.

- **Upload notifications** — Upload notification emails name the shared folder correctly and link to its contents for both owner and uploader.
- **Unshare notifications** — The removed-access notification email is sent when a file or folder share is removed.

#### [Pull Job Duplicate File Handling](/docs/mdmft/release-notes/release-notes#pull-job-duplicate-file-handling)

Skip duplicates and Overwrite existing files detect existing destination files for FTPS and SharePoint Online pull jobs.

#### [Upload Commits](/docs/mdmft/release-notes/release-notes#upload-commits)

Uploads complete or are discarded cleanly for users in groups that disable sharing.

- **Groups with sharing disabled** — Uploads succeed for users whose group disables sharing, and per-file commits respect the selected recipients.
- **Refused commits** — A refused upload commit discards the file instead of leaving it stuck in Processing in My Files.

---

### [Behavior Corrections](/docs/mdmft/release-notes/release-notes#behavior-corrections)

### [Settings and Configuration](/docs/mdmft/release-notes/release-notes#settings-and-configuration)

#### [Skip Scanning of Trashed Files](/docs/mdmft/release-notes/release-notes#skip-scanning-of-trashed-files)

An option excludes files in the trash from scanning so retained files are not rescanned.

#### [Single-Label Recipient Domain Exceptions](/docs/mdmft/release-notes/release-notes#single-label-recipient-domain-exceptions)

Recipient domain exceptions accept single-label domains such as name@corp while unlisted domains are blocked.

#### [API Key Display](/docs/mdmft/release-notes/release-notes#api-key-display)

API keys show their value and dates in the management console.

- **Key value after creation** — A newly generated API key is displayed after creation in Security and My Credentials.
- **Creation and expiry dates** — Existing and new API keys show their creation and expiry dates in the management console after an upgrade.

#### [DSA SSH Key Support Notice](/docs/mdmft/release-notes/release-notes#dsa-ssh-key-support-notice)

The Add SSH key dialog lists only supported key formats after DSA was removed with the SSH library upgrade.

#### [Customization Settings Save](/docs/mdmft/release-notes/release-notes#customization-settings-save)

Changes to the logo, login background, favicon, and loading animation are saved.

### [Integrations](/docs/mdmft/release-notes/release-notes#integrations)

#### [Core Workflow Missing Notifications](/docs/mdmft/release-notes/release-notes#core-workflow-missing-notifications)

Core workflow warnings and file statuses reflect the actual workflow configuration.

- **Multiple Cores** — The MetaDefender Core workflow missing banner stays hidden when integrated Cores name their workflows differently.
- **Banner text** — The workflow missing banner names the renamed default Core workflow behind the warning.
- **File processing status** — Files show MetaDefender Core Workflow Not Found instead of Scan Failed when the fallback default workflow was renamed in Core.

#### [RADIUS Sign-In Errors](/docs/mdmft/release-notes/release-notes#radius-sign-in-errors)

RADIUS sign-in shows an accurate error for each failure.

- **Wrong password** — A wrong RADIUS password returns an invalid-credentials error instead of the disabled login type message.
- **Configuration errors** — RADIUS sign-in separates an unreachable server, a wrong shared secret, and disabled RADIUS from invalid credentials.

#### [Password Reset Emails for AD Users](/docs/mdmft/release-notes/release-notes#password-reset-emails-for-ad-users)

Password reset emails are sent only to local accounts, not to Active Directory users.

#### [CM10 Inactive External Users Setting](/docs/mdmft/release-notes/release-notes#cm10-inactive-external-users-setting)

The Disable Inactive External Users setting is included in the CM10 vpack.

#### [MFT Pull Requests](/docs/mdmft/release-notes/release-notes#mft-pull-requests)

Pulling files from another MFT instance completes and reports progress.

- **Pull request errors** — Pulling files from another MFT instance with local user credentials completes without the generic Pull MFT request error.
- **Progress dialog** — The progress dialog completes when a file is pulled from another MFT instance.

#### [AD and Local Email Sign-In Fallback](/docs/mdmft/release-notes/release-notes#ad-and-local-email-sign-in-fallback)

A local user signs in by email with a local password when an Active Directory user shares the email, as the documentation describes.

### [Files, Sharing, and Users](/docs/mdmft/release-notes/release-notes#files-sharing-and-users)

#### [Restricted Administrator File Actions](/docs/mdmft/release-notes/release-notes#restricted-administrator-file-actions)

Restricted administrators can perform the file actions their role permits.

- **Original file download** — Restricted administrators can download the original version of files shared with them in Shared With Me.
- **Pending files in shared folders** — Restricted administrators can download both versions of a pending file inside a shared folder.
- **Rescan** — Restricted administrators can rescan other users' files from the File Security Report.
- **Override blocked status** — Restricted administrators and verdict supervisors can override a blocked file status from the File Security Report.
- **Override scan result** — Restricted administrators can override the scan result for files whose processing failed.
- **Scan result page** — Restricted administrators can open the scan result page of other users' files.

#### [Folder Navigation from Paginated Lists](/docs/mdmft/release-notes/release-notes#folder-navigation-from-paginated-lists)

Opening a folder from a later page of a long list shows that folder.

- **Opening from page 2** — Opening a folder from the second page of a long folder list shows that folder's contents instead of returning to the first page of the parent.
- **List auto-refresh** — Opening a folder from page 2 holds when the 20-second list refresh fires while the folder loads.

#### [Shared With Me Search Scope](/docs/mdmft/release-notes/release-notes#shared-with-me-search-scope)

Search under Shared With Me covers all shared folders, matching the behavior of My Files.

#### [Blocked Files in Folder Downloads](/docs/mdmft/release-notes/release-notes#blocked-files-in-folder-downloads)

Folder downloads through a download link show a warning when some files were blocked by MetaDefender Core.

#### [Sharing Rules and API](/docs/mdmft/release-notes/release-notes#sharing-rules-and-api)

Sharing requests report errors and apply ownership consistently.

- **Unknown username** — Sharing with a username that does not exist returns a validation error instead of reporting success.
- **Groups with sharing disabled** — Sharing a folder with a group that has sharing disabled returns a validation error instead of an HTTP 500.
- **Existing shares** — Owners can update items already shared with a group whose Allow Sharing With This Group option was switched off later.
- **Recipient uploads through the API** — Files that recipients upload into a shared folder through the REST API belong to the folder owner, who receives a notification.
- **Upload response link** — The upload response links a recipient to the shared folder instead of the owner's personal folder.

#### [File Action Availability](/docs/mdmft/release-notes/release-notes#file-action-availability)

The File Security Report offers only the actions that apply to a file's supervision state.

- **Revoked guest files** — Revoke and Archive are hidden in the File Security Report for guest files the supervisor has revoked.
- **Rejected files** — Rejected files cannot be archived from the File Security Report.

#### [External and Guest Users](/docs/mdmft/release-notes/release-notes#external-and-guest-users)

External and guest accounts are created, enabled, and restricted as configured.

- **Guests without email** — Guests without an email address can be created after an SSO user's email was stored as an empty value.
- **Blocked email domains** — The creator of an external user cannot re-enable the account while its email domain is blocked.
- **Re-enabling external users** — Turning off Disable External User Creation restores only the external users that were enabled before it was turned on.

---

### [UI & Usability Fixes](/docs/mdmft/release-notes/release-notes#ui--usability-fixes)

- **SMB Pull Wildcard Legend Layout** — The wildcard path legend on the SMB Pull job form is concise and keeps the form in a single balanced block.
- **MFT-to-MFT Settings Toggle Alignment** — The left and right toggles stay aligned when the Transfer all files warning banner appears.
- **Blocked Domain Share Warning** — The share dialog warning for a new guest on a blocked domain tells the user to ask an administrator to allow the domain.
- **Localized Placeholder Names** — French and Japanese language files keep the original placeholder names so values display instead of raw {{...}} text.
- **S3 Storage Error Messages** — The S3 storage region and service URL error messages show the correct text.
- **HA Node Activation Timeout Display** — The HA Configurator settings page shows the HA controller's Node Activation Timeout.
- **Share Picker Long Email Tooltip** — The share picker shows a tooltip with the full email address when a long address is truncated.
- **Notification Email in Share Picker** — The share picker shows the user's notification email as well as the account email.
- **Upload Reason Refusal Message** — The refusal message for updating an upload reason shows the user and file names instead of empty placeholders.
