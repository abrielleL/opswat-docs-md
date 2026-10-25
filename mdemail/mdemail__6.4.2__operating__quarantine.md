<!-- source: https://www.opswat.com/docs/mdemail/6.4.2/operating/quarantine -->

# Quarantine

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Overview](/docs/mdemail/6.4.2/operating/quarantine#overview)

Quarantine is the safe storage for emails which were blocked or sanitized by MetaDefender Email Gateway Security.

For details about quarantine configuration, which emails are quarantined see [Configuration/Quarantine configuration](/docs/mdemail/6.4.2/configuration/quarantine-configuration).

Infection risk level

The machine hosting the quarantine is safe from infections as long as items in the quarantine are not opened or executed.

Quarantine access risks

Care must be taken when granting access to the quarantine as releasing or forwarding the items from the quarantine might cause harm.

## [Search, Filtering, List verbosity and Email details](/docs/mdemail/6.4.2/operating/quarantine#search-filtering-list-verbosity-and-email-details)

For details see [Operating/Email History](/docs/mdemail/6.4.2/operating/email-history).

## [Quarantine areas](/docs/mdemail/6.4.2/operating/quarantine#quarantine-areas)

Under **Quarantine > Quarantine** in the filter  section it is supported to save the already created filters to make it easier to manage the quarantine. Once the filter is set according to the needs, click on the *Add filter as quarantine area* button at the bottom of the filter configuration dialog.

When an *already defined quarantine area* is selected, the filters set for that quarantine area are applied to the email list. Emails only according to the quarantine area filter settings will be displayed.

Quarantine areas can be saved for the actual user only. This case results in the same behaviour as the old [saved filters](https://www.opswat.com/docs/mdemail/operating/quarantine#saving-filters).

Personal quarantine areas

Personal quarantine areas -that are visible to the current user only- are marked with a grey background.

### [Global quarantine areas](/docs/mdemail/6.4.2/operating/quarantine#global-quarantine-areas)

Quarantine areas can be added as global ones.

Access to global quarantine areas can be controlled under **User Management > Roles**. Whenever a new global quarantine area is created, an entry is added for it among the role permissions.

No access by default

By default, no roles (except *Administrators* as this role has full access to everything) get access to a newly created quarantine area even when the role has *Full* permission to the Quarantine.

With global quarantine areas, special roles in Email Gateway Security can be created who can administer dedicated parts of the Quarantine.

For example to permit a role to handle spam emails in the quarantine:

1. Create a quarantine area filtering for spam

2. Create a role that has access to this new quarantine area (only)

3. Create users with this new role

4. Users created like this will have access to the dedicated quarantine area only

Global quarantine areas

Global quarantine areas are marked with a blue background.

#### [Functions](/docs/mdemail/6.4.2/operating/quarantine#functions)

Global quarantine areas currently support the following functions:

- Release
- Delete
- Preview email body

## [Cleanup](/docs/mdemail/6.4.2/operating/quarantine#cleanup)

### [Scheduled](/docs/mdemail/6.4.2/operating/quarantine#scheduled)

For details see [Configuration/Quarantine configuration](/docs/mdemail/6.4.2/configuration/quarantine-configuration).

### [On-demand](/docs/mdemail/6.4.2/operating/quarantine#on-demand)

To clean-up quarantine on demand click the  icon and select the time window of the cleanup.

### [Pin emails](/docs/mdemail/6.4.2/operating/quarantine#pin-emails)

Email that are pinned won’t be removed from the quarantine by the scheduled or the on-demand cleanup, or by a [Release email](/docs/mdemail/6.4.2/operating/quarantine#release-email) operation.

Clicking the  button will pin the selected email(s).

## [Operations](/docs/mdemail/6.4.2/operating/quarantine#operations)

The following operations are available as both bulk and single email operations:

| Operation | Icon | Description |
| --- | --- | --- |
| Full rescan |  | Initiate a full (including anti-spam checks) rescan of the email(s). For details see [Rescan email](/docs/mdemail/6.4.2/operating/quarantine#rescan-email). |
| Anti-Malware rescan |  | Initiate an anti-malware (not including anti-spam checks) rescan only of the email(s). For details see [Rescan email](/docs/mdemail/6.4.2/operating/quarantine#rescan-email). |
| Release |  | Release the selected email(s). The original, potentially harmful email gets delivered. For details see [Release email](/docs/mdemail/6.4.2/operating/quarantine#release-email) |
| Forward |  | Forward the selected email(s) to the specified recipient(s) for further investigation, for example. The original, potentially harmful email gets delivered. |
| Delete |  | Delete the selected email(s) from the quarantine. The operation can not be undone. |
| Download |  | Download the selected email(s) az a zip archive file. The original, potentially harmful emails are downloaded. |

Encrypt downloaded emails

Upon download it is possible to encrypt the downloaded zip archive with a password.

### [Bulk operations](/docs/mdemail/6.4.2/operating/quarantine#bulk-operations)

Use the checkbox in front of each row to select entries (or use the checkbox in the header row to select all visible items).

Only visible selected

Only visible elements are selected. Elements that are not visible (due to pagination, search or filtering) are not selected even by the select all checkbox.

## [Single email operations](/docs/mdemail/6.4.2/operating/quarantine#single-email-operations)

Click the  in *Email details* to open the single email menu.

View email functions

The *View raw email* and *Preview email body* operations are not available as bulk operations.

These functions can help investigating why the email was quarantined as they show the raw text or rendered format of an email.

### [Preview email body](/docs/mdemail/6.4.2/operating/quarantine#preview-email-body)

This function renders the email as it would be shown in an email client. It can render the

- HTML view of the body as standard email clients would show,
- Plain text body as limited, text only email clients would show,
- The raw HTML body to be able to highlight sensitive data hidden in the HTML markup.

Hyperlinks in HTML email body preview

The email body preview is running in the browser sandbox that prohibits top level navigation. As a consequence hyperlinks in the HTML preview won't work.

### [Mark DLP hits](/docs/mdemail/6.4.2/operating/quarantine#mark-dlp-hits)

The *Preview email body* function highlights DLP hits (if any) both in the plain text, in the HTML email body and in the raw HTML body to reveal sensitive data hidden in the HTML markup code.

The number of DLP hits in each body type is marked by the number in the body type tab header.

Show all DLP hits

The *Show DLP hits* function lists all—even overlapping—DLP hits in the email bodies.

Overlapping DLP hits

Overlapping DLP hits are also marked as shown in the screenshots below.

Sensitive data in images

Images are not supported by the DLP highlight function.

## [Adding to Trusted Senders](/docs/mdemail/6.4.2/operating/quarantine#adding-to-trusted-senders)

It is now possible to add sender (email or IP address) to the trusted senders list directly from the Quarantine view. Click the  in *Email information* to open the single email menu.

## [Full rescan email](/docs/mdemail/6.4.2/operating/quarantine#full-rescan-email)

MetaDefender Email Gateway Security provides the capability to rescan emails that were previously blocked and ended up in the quarantine. After a rescan the email may be allowed and delivered normally. Some of the reasons why emails may be rescanned:

- To process the email with updated scan engines that may not block the contents,
- To process the email with an alternative rule that may give different results,

  - To sanitize a blocked email before releasing (see the section *Disarm, reconstruct and release*)
- To provide password for encrypted attachments and process the decrypted contents.

### [Select alternative rule](/docs/mdemail/6.4.2/operating/quarantine#select-alternative-rule)

### [Provide password](/docs/mdemail/6.4.2/operating/quarantine#provide-password)

For details see [Operating/Password protected attachments](/docs/mdemail/6.4.2/operating/password-protected-attachments).

## [Anti-malware rescan email](/docs/mdemail/6.4.2/operating/quarantine#anti-malware-rescan-email)

It is also possible to rescan an email using only the anti-malware technologies available in MetaDefender Email Gateway Security, omitting anti-spam & anti-phishing checks. This simplifies tasks, such as releasing a spam false positive while still ensuring that the email is free from malware. For details see [Handling spam false positives](/docs/mdemail/6.4.2/operating/handling-spam-false-positives).

## [Release email](/docs/mdemail/6.4.2/operating/quarantine#release-email)

This function will release the selected original emails from the quarantine and send them to the original recipients. The original emails are removed from the quarantine except [Pinned emails](/docs/mdemail/6.4.2/operating/quarantine#pin-emails).

Risk of outbreak

The recipients will receive the (potentially) malicious contents.

SMTP server profile required

For this function to work correctly **Settings > Alerts & Reports** */ SMTP server profile* needs to be set. For details see [Configuration/Alert, notification and quarantine report emails](/docs/mdemail/6.4.2/configuration/alert--notification-and-quarantine-report-emails).

Duplicate history entries

Quarantining puts the original email into the quarantine and sends a notification or a disinfected/sanitized copy to the original recipient. As a result, releasing from the quarantine virtually duplicates the history entry for the quarantined email.

These duplicates are marked with a *paper plane* icon in **Audit > Email history**. For details see [Operating/Email History](/docs/mdemail/6.4.2/operating/email-history).

## [Disarm, reconstruct and release](/docs/mdemail/6.4.2/operating/quarantine#disarm-reconstruct-and-release)

It is a potential use case to sanitize emails before releasing them. This feature is not supported by the regular *Release email* function but can be achieved using *Rescan email*.

### [Preparations](/docs/mdemail/6.4.2/operating/quarantine#preparations)

1. On MetaDefender Core servers create a rule that does not scan, but applies the desired sanitization.

   1. It is necessary to allow the not scanned results for the Core rule (in Core under **Policy > Workflow rules** / Add/Modify Rule / ADVANCED / OVERRIDE SCAN RESULTS CLASSIFIED AS ALLOWED / NOT SCANNED). To allow password protected archives to be processed, the encrypted archive results must be disabled (in Core under **Policy > Workflow rules** / Add/Modify Rule / ADVANCED / OVERRIDE SCAN RESULTS CLASSIFIED AS ALLOWED / ENCRYPTED ARCHIVE)

2. On Email Gateway Security create a MetaDefender Core type server profile having the Core servers and rules created in the previous step. For details see [Configuration/Server profiles](/docs/mdemail/6.4.2/configuration/server-profiles).
3. On Email Gateway Security, under **Security Rules** create a rule using the server profile created in the previous step.

   1. Optionally set 0.0.0.0 as SENDER IP ADDRESS for this rule to not match any regular incoming emails or
   2. Set the priority of this rule accordingly if it is expected to process regular incoming emails.

### [Release](/docs/mdemail/6.4.2/operating/quarantine#release)

1. Instead of using the Release function use the *Rescan* function.
2. In the confirmation dialog select the rule created in the previous section:

3. The email will be re-processed using the newly selected rule.

   1. If the new rule allows the email, then it gets delivered normally.
