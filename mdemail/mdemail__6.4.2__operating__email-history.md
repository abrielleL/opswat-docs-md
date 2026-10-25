<!-- source: https://www.opswat.com/docs/mdemail/6.4.2/operating/email-history -->

# Email History

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Overview](/docs/mdemail/6.4.2/operating/email-history#overview)

**Audit > Email History** shows information about processing details and email related events in the system.

No auto refresh

Due to usability reasons the Email history list is not updated automatically. Click the Refresh icon to update.

N/A Scan result

The N/A *Scan result* value means that MetaDefender Core was not involved in the processing of this entry.

Such cases are:

- Notifications for blocked emails
- Released from quarantine
- Forwarded from quarantine
- Delivered for external quarantining
Empty Rule

The empty *Rule* value means that the email was not received from outside, but was generated from within Email Gateway Security.

Such cases are:

- Notifications for blocked emails
- Email alerts
- Quarantine reports
### [Search](/docs/mdemail/6.4.2/operating/email-history#search)

On the Email history list you can search for (marked red in the image below) the *Date*, Malware scan verdict, Phishing / Spam verdict, *Status*, *Sender*, *Recipient*, *Rule*, *Subject* , *Message-ID*, and *Rule direction* (for *Rule direction* see [Configuration/Policy](/docs/mdemail/6.4.2/configuration/policy)).

### [Filtering](/docs/mdemail/6.4.2/operating/email-history#filtering)

The list of emails can be filtered by the:

1. Date,
2. Security Rule (that processed the email),
3. Sender,
4. Recipient,
5. Subject,
6. Status,
7. Classifications,
8. Scan verdict,
9. Phishing/Spam verdict (see the *Phishing/Spam verdict* section below),
10. Whether the email has attachments or not,
11. Rule priority,
12. Classifications (see [Operating/Email classifications](/docs/mdemail/6.4.2/operating/email-classifications)) and
13. Tags (see [Operating/Email tags](/docs/mdemail/6.4.2/operating/email-tags)).

Multiple values

For the **status**, **classifications, phishing/spam verdict** and **tags** filters multiple values can be specified.

Time window

For the **date** filter a time window can be specified.

Visible Security Rules

The filter displays the Security Rules that are currently defined in the system and that are not disabled.

## [List verbosity](/docs/mdemail/6.4.2/operating/email-history#list-verbosity)

The Email history list supports three verbosity views:

- Compact,
- Standard and
- Detailed view.

Each level shows more details of an email but can show less entries at once.

### [Email details](/docs/mdemail/6.4.2/operating/email-history#email-details)

Clicking an Email history list entry displays public details about the processing of the specific email.

#### [Malware scan details](/docs/mdemail/6.4.2/operating/email-history#malware-scan-details)

Under the *Malware scan verdict* block links point to the scan details on the MetaDefender Core or MetaDefender Cloud instance where the actual scanning took place.

The component that caused a block on the MetaDefender Core or Cloud is marked with a `Blocked` indicator.

Each origianal, potentially malicious email component can be downloaded individually using the download button at the end of each line.

Risk

Downaloaded email components may be malicious or deceptive. Always download and handle email components with due care.

Results for files that had a hash lookup match and were taken from the cache are marked with a  (hash) symbol, while results for files that were actually scanned are marked with a  (chain) symbol.

In case of scan results the *Show results* link points to the result of the scan batch (the aggregated result of all the scanned files).

For both the hash lookup and the scan results, clicking the  (dropdown) symbol next to the *Show results* link each file has a individual link to its specific results.

File name mismatch

File names may differ even if file contents –and as so file hashes– are the same.

This may cause file names not matching (in the examples below: *cyberscape/CYBERscape.pdf* in Email Gateway Security but *meeting minutes/CYBERscape.pdf* in Core) in the email and in the scan details on MetaDefender Core / Cloud.

This can be addressed using the *Force scan on mismatch* option in the hash lookup configuration. For further details see the *Hash lookup* subsection in [Configuration/Policy/Scan](/docs/mdemail/6.4.2/configuration/policy#scan).

Broken scan details links

The scan details links utilize the Core address as specified under **Settings > Server profiles**. If Core is specified with an address that is not reachable on the machine where the actual browsing of the web management console happens, then the browser will report error.

**Example**

Core and Email Gateway Security are installed on the same machine and Core is referenced with the URI <http://127.0.0.1:8008> on Email Gateway Security. If Email Gateway Security's web management console is browsed from any other machine, then (most probably) the scan details links will be broken.

For details see [Configuration/Server profiles](/docs/mdemail/6.4.2/configuration/server-profiles).

#### [Classifications](/docs/mdemail/6.4.2/operating/email-history#classifications)

To reflect the risk level of a certain email, Email Gateway Security applies classifications. For details see [Operating/Email classifications](/docs/mdemail/6.4.2/operating/email-classifications).

#### [Phishing/Spam verdict](/docs/mdemail/6.4.2/operating/email-history#phishingspam-verdict)

Email Gateway Security's anti-spam and anti-phishing filters can categorize phishing and spam emails based on the content of the email.

For the list of supported categories (verdicts) see [Phishing and spam](/docs/mdemail/6.4.2/operating/phishing-and-spam).

#### [Priority](/docs/mdemail/6.4.2/operating/email-history#priority)

The priority of the email is displayed in the list and in the *Email details* view. The following icons represent each priority:

1. High: **↑**
2. Low: **↓**

For details see [Configuration/Policy](/docs/mdemail/6.4.2/configuration/policy).

#### [Processing history](/docs/mdemail/6.4.2/operating/email-history#processing-history)

The processing history section of the email details contains information about the processing of the email.

### [Cleanup](/docs/mdemail/6.4.2/operating/email-history#cleanup)

#### [Scheduled](/docs/mdemail/6.4.2/operating/email-history#scheduled)

Configure scheduled Email History cleanup under **Settings > Data Retention / Email history cleanup schedule**.

#### [On-demand](/docs/mdemail/6.4.2/operating/email-history#on-demand)

To clean-up Email History on demand click the icon and select the time window of the cleanup.

## [Operations](/docs/mdemail/6.4.2/operating/email-history#operations)

### [Bulk email operations](/docs/mdemail/6.4.2/operating/email-history#bulk-email-operations)

Use the checkbox in front of each row to select entries (or use the checkbox in the header row to select all visible items).

Only visible selected

Only visible elements are selected. Elements that are not visible (due to pagination, search or filtering) are not selected even by the select all checkbox.

Only Failed Pending or Reprocessing can be selected

Only emails that are in the *Failed*, *Pending* or *Reprocessing* status can be selected cause these are the only emails where Email Gateway Security still has the email content to commit the operation (e.g. *Retry email*, *Delete email*, *Download email*) or the email is in a status when the operation is applicable (*Bypass email*).

For other entries the original email is not kept, hence the operations would not work.

To understand what can make an email to be *Failed* see the section *Processing status values*.

Operations that applicable to all selected

Only those operations are available that are applicable to all emails that are selected.

For example if both *Failed* and *Reprocessing* mails are in the selection, then the *Retry email* function will be available.

#### [Bypass processing emails](/docs/mdemail/6.4.2/operating/email-history#bypass-processing-emails)

Emails can be bypassed using the *Bypass email processing* button or action in Email history. Bypassed emails are pushed immediately to the SMTP delivery queue, skipping scanning.

Only for emails Pending or Reprocessing

Bypassing is supported only for emails that are in the *Pending* or *Reprocessing* status. These are the emails where the processing has not been started yet.

Intended for emergency situations

Bypassing is intended for emergency situations only and differs from license-based bypass.

Bypassed emails have the dedicated classification: *Ignored* (see [Email classifications](/docs/mdemail/6.4.2/operating/email-classifications)). Bypassing is marked in the processing history.

Bypasses also create entries in **Audit > Audit Log**. The values in `requested_email_ids` can help to navigate to the emails that were bypassed during the request.

### [Failed and Forbidden emails](/docs/mdemail/6.4.2/operating/email-history#failed-and-forbidden-emails)

For emails with status Failed or Forbidden, the following operations are supported:

- Retry email: retry processing the email,
- Delete email: delete the email from Email History,
- Download email: download for further investigation or persistence.

Delete with due care

Emails in Failed and Forbidden statuses are stuck in Email Gateway Security as it could not complete processing them.

Deleting such emails from the Email History will cause those emails to not exist without the possibility to deliver them later.

### [Add to Trusted senders](/docs/mdemail/6.4.2/operating/email-history#add-to-trusted-senders)

Entries to the *Trusted senders* list can be created directly from the properties of a certain email.

For details see [Trusted senders](/docs/mdemail/6.4.2/configuration/trustedsenders).

### [Export to CSV](/docs/mdemail/6.4.2/operating/email-history#export-to-csv)

Clicking the **Export to CSV** button will export the history list (according to the actual filter conditions) to a CSV file.

Data range

The currently active filter conditions apply to the exported list.

All filtered data gets exported, even if the list expands to multiple pages.

## [Differentiating forked emails](/docs/mdemail/6.4.2/operating/email-history#differentiating-forked-emails)

In some cases there are seemingly duplicate entries in Email history. Such cases are when an email is:

- Released from quarantine,
- Forwarded from quarantine,
- Delivered for external quarantining.

These cases are marked in Email history with the following icons in the history list:

| **Icon** | **Fork case** |
| --- | --- |
|  | Released from quarantine |
|  | Forwarded from quarantine |
|  | Delivered for external quarantining |

## [Processing status values](/docs/mdemail/6.4.2/operating/email-history#processing-status-values)

### [Workflow statuses](/docs/mdemail/6.4.2/operating/email-history#workflow-statuses)

Emails with statuses listed below are progressing through the MetaDefender Email Gateway Security workflow.

#### [Pending](/docs/mdemail/6.4.2/operating/email-history#pending)

Email is queued waiting to be processed.

#### [Processing](/docs/mdemail/6.4.2/operating/email-history#processing)

Email is currently being processed.

#### [Sending](/docs/mdemail/6.4.2/operating/email-history#sending)

Email has been processed and is being delivered to the SMTP relay server.

#### [Completed](/docs/mdemail/6.4.2/operating/email-history#completed)

This status is deprecated since 4.4.0. It was replaced by Sent and Blocked

Email has been successfully processed and sent forward or blocked.

#### [Sent](/docs/mdemail/6.4.2/operating/email-history#sent)

Email has been successfully processed and forwarded.

#### [Blocked](/docs/mdemail/6.4.2/operating/email-history#blocked)

Email has been blocked.

### [Temporary failure statuses](/docs/mdemail/6.4.2/operating/email-history#temporary-failure-statuses)

Emails with statuses listed below are in automatic retry sequence.

#### [Reprocessing](/docs/mdemail/6.4.2/operating/email-history#reprocessing)

MetaDefender Email Gateway Security has failed to process the email and it is currently pending a retry.

**Possible causes**

- MetaDefender Core server down/not responding
- Archive engine is not active on MetaDefender Core

- Enable archive handling is not enabled for the rules on MetaDefender Core (that are defined in the Core server policies that are in use by the rules on MetaDefender Email Gateway Security)

#### [Resending](/docs/mdemail/6.4.2/operating/email-history#resending)

MetaDefender Email Gateway Security has failed to forward the email to the SMTP relay server and is currently pending retry.

#### [**Possible causes**](/docs/mdemail/6.4.2/operating/email-history#possible-causes)

- SMTP relay server down/not responding
- SMTP relay server rejects the email

### [Permanent failure statuses](/docs/mdemail/6.4.2/operating/email-history#permanent-failure-statuses)

Emails with statuses listed below require user interaction, since retry sequence is exhausted.

#### [Failed](/docs/mdemail/6.4.2/operating/email-history#failed)

Email has exceeded the retry count and cannot be processed/delivered.

**Possible causes**

- Exhausted temporary processing failures (see [Configuration/Settings](/docs/mdemail/6.4.2/configuration/settings)) lead to this permanent failure status.

#### [**Possible actions**](/docs/mdemail/6.4.2/operating/email-history#possible-actions)

- Manually retry/delete email from the MetaDefender Email Gateway Security web interface.

#### [Forbidden](/docs/mdemail/6.4.2/operating/email-history#forbidden)

No policy rule is found matching the email and requires manual delivery

#### [**Possible actions**](/docs/mdemail/6.4.2/operating/email-history#possible-actions)

- Manually retry/delete email from the MetaDefender Email Gateway Security web interface.

### [Other statuses](/docs/mdemail/6.4.2/operating/email-history#other-statuses)

#### [Quarantined](/docs/mdemail/6.4.2/operating/email-history#quarantined)

Email is located in quarantine.

#### [**Possible actions**](/docs/mdemail/6.4.2/operating/email-history#possible-actions)

- Manually deliver/delete/forward email from the MetaDefender Email Gateway Security web interface.

#### [Deleted](/docs/mdemail/6.4.2/operating/email-history#deleted)

Emails with this status has been manually deleted by a user.
