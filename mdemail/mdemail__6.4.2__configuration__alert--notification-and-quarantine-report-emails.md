<!-- source: https://www.opswat.com/docs/mdemail/6.4.2/configuration/alert--notification-and-quarantine-report-emails -->

# Alert, notification and quarantine report emails

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Alert and report emails, and certain settings of notification emails can be configured under **Settings > Alerts & Reports**.

## [Trust](/docs/mdemail/6.4.2/configuration/alert--notification-and-quarantine-report-emails#trust)

Risk of social engineering

Notification, alert and report messages sent by the product often resemble to phishing emails.

It is a common phishing technique to trick users into clicking on links or to provide their credentials on phishing webpages. As Email Gateway Security’s own messages also ask users to click on links and provide passwords, users with due care may get confused whether they are targets of a phishing attack in case of an Email Gateway Security notification, alert or report email.

To build trust, Email Gateway Security provides the option to digitally sign notification, alert and report messages sent by the product. This way recipients can ensure whether they are facing a real Email Gateway Security notification, or a fake one.

To configure digitally signing alert, notification and report messages, perform the following steps:

1. Define a certificate and private key pair under **Settings > Certificates** for digitally singing emails.

2. Enable **Settings >Alerts & Reports / Digitally sign alerts & reports**.

3. Select the certificate created in step 1 as the **S/MIME certificate**

4. Recipients can verify the digital signature.

Sender must match certificate

The sender email address set under the **Sender email address** and the subject of the certificate set for **S/MIME certificate** must match, otherwise the digital signature on the email won’t validate.

The product verifies if the sender and the certificate subject match and displays a warning if not.

Certificate must support S/MIME

The certificate set for **S/MIME certificate** must support digitally signing emails.

The product verifies if the certificate is appropriate and displays a warning if not.

## [Common properties](/docs/mdemail/6.4.2/configuration/alert--notification-and-quarantine-report-emails#common-properties)

Some properties are common among alerts, notifications and quarantine reports.

| **SMTP server profile** | Email Gateway Security will use a specific SMTP relay to deliver all alerts, notifications and reports. This SMTP server can be defined under **Settings > Alerts & Reports** / SMTP server profile. For further details see Server. |
| --- | --- |
| **Sender email address** | Email address from which the alert, notification or quarantine report emails are sent. This is used in the SMTP *MAIL FROM* command and the email *From* header. |
| **Digitally sign alerts & reports** | Whether or not to digitally sign report, notification and alert emails sent by the product. When enabled, an S/MIME digital signature is applied to the message using the certificate configured in the *S/MIME certificate* field. |
| **S/MIME certificate** | The certificate that is used to generate the digital signature. |

## [Alerts](/docs/mdemail/6.4.2/configuration/alert--notification-and-quarantine-report-emails#alerts)

Email alerts can be configured so that certain users can instantly be notified about the occurrence of certain system events.

| **SMTP server not responding** | An alert is sent if the inbound SMTP server is not responding as expected |
| --- | --- |
| **SMTP relay not responding** | An alert is sent if an SMTP relay configured in a server profile is not responding as expected |
| **MetaDefender Core not responding** | An alert is sent if a MetaDefender Core server configured in a server profile is not responding as expected |
| **MetaDefender MFT not responding** | A notification will be sent if a MetaDefender Managed File Transfer server configured in a server profile is not responding |
| **MetaDefender** **MFT** **upload failure** | An alert is sent if one or more attachments failed to upload to MetaDefender Managed File Transfer |
| **Scan failure** | An alert is sent if a scan failure occurs during the processing of an email |
| **Sanitization failure** | An alert is sent if a sanitization failure occurs during the processing of an email |
| **Delivery of sanitized blocked email content** | An alert is sent if a blocked sanitized email is delivered to recipient(s). *MetaDefender Email Gateway Security will only deliver blocked sanitized content to recipient(s) when the option* ***Security Rules > rule / ZERO-DAY MALWARE PREVENTION / Override sanitization behavior / Send sanitized version of blocked files*** *is enabled. For further details see the Zero-Day Malware Prevention section in* [*Configuration/Policy*](/docs/mdemail/6.4.2/configuration/policy)*__.* |
| **Email refused** | An alert is sent when an email is refused by MetaDefender Email Gateway Security. |
| **Email failed** | An alert is sent when an email fails processing and is moved to Failed.  There is an option to notify the **original recipient or sender** of the email, too.    The idea behind this option is that this way the original recipients or sender can be aware that they have an email withheld by Email Gateway Security and they may need to take actions to get the email from the server. The content and layout of the recipient alert email can be configured in the `<installation directory>\mailagenthost\xslt\alert_email_failed_original_recipients.xsl` template (default: "C:\Program Files\OPSWAT\MetaDefender Email Security\mailagenthost\xslt\alert_email_failed_original_recipients.xsl"). For customization details see [Notification, alert and report emails](/docs/mdemail/6.4.2/configuration/translation-support#notification-alert-and-report-emails).    For emails processed by an *Inbound* rule it is the original recipients that get the notification, for emails processed by an *Outbound* rule it is the original sender. For details on rule direction see [Policy](/docs/mdemail/6.4.2/configuration/policy). |
| **Email bypassed** | A notification will be sent if Email Gateway Security bypassed scanning an email. |
| **Email refused by SMTP relay** | A notification will be sent if an email is refused by a configured SMTP relay server.  **Example**  Deep CDR processing may significantly increase the email size. As a consequence the SMTP relay might refuse the email due to email size limitations (even if the recipient is valid).  This notification can call the administrators' attention to cases like that. |
| **Anti-Spam scan failure** | An alert is sent when there is an error scanning an email with the anti-spam module |
| **Anti-Spam engine not responding** | An alert is sent when anti-spam engine is not responding |
| **Queue size** | A notification will be sent if the MetaDefender Email Gateway Security queue size exceeds the threshold configured for the QUEUE SIZE THRESHOLD value.  **Note**  A large queue does not necessarily indicate a failure, but can be due to a large influx of emails and processing of them is queued up to ensure optimal performance of MetaDefender Email Gateway Security. |
| **No valid license** | The product is not licensed (has never been, or the license expired). |
| **License expiry alert** | Email Gateway Security can send email alerts in advance—with the configured lead time—of license expiration, and at the day of expiration.  This alert is only sent once a day—each day until expiration—at midday (server local time). |

Persistent conditions

 For persistent failures or conditions a notification email will be sent once an hour.

**Example**

If the queue size keeps exceeding the threshold for hours, then the alert is sent once every hour. But if the queue size is fluctuating around the threshold (sometimes exceeds, sometimes drops below) then the alert is sent every time the threshold is exceeded.

Alert for each occurrence

 These alerts are sent every time the condition evaluates to true.

**Example**

If EMAIL BYPASSED option is set, then an alert is sent every time an email is bypassed by Email Gateway Security.

Priority

Alert emails are handled with priority. When the processing queue is long, alerts won't suffer a delay as alert emails are put to the head of the queue.

## [Notifications](/docs/mdemail/6.4.2/configuration/alert--notification-and-quarantine-report-emails#notifications)

### [Emails blocked due to malware or sensitive data](/docs/mdemail/6.4.2/configuration/alert--notification-and-quarantine-report-emails#emails-blocked-due-to-malware-or-sensitive-data)

Notifications for emails that were blocked due to malware or sensitive are sent when emails are blocked by Advanced Threat Prevention (Multiscanning, OPSWAT Sandbox and Proactive DLP) and **Security Rules >*rule*/ ADVANCED THREAT PREVENTION / Handling of the email** is set to *Block email*.

Notifying recipients about the blocked email can be enabled by **Security Rules >*rule*/ ADVANCED THREAT PREVENTION / Notify recipients if email is blocked**.

For further details see the *Advanced Threat Prevention* section in [Configuration/Policy](/docs/mdemail/6.4.2/configuration/policy).

A notification email informs the recipient about the fact that the email was blocked, the blocking reason and the potential next steps.

### [Quarantined spam and phishing emails](/docs/mdemail/6.4.2/configuration/alert--notification-and-quarantine-report-emails#quarantined-spam-and-phishing-emails)

When the action on Known Spam, Potential Spam, Known Phishing or Potential Phishing emails is set to Quarantine, Email Gateway Security can be configured to send a notification about the quarantined email.

The notification settings for spam and phishing are the same as for notifications for emails blocked due to malware or sensitive data. The notification can be configured for each (Potential) Spam and (Potential) Phishing emails on the appropriate configuration tab in the security rule.

A notification email for a quarantined spam looks like the following:

### [Actions](/docs/mdemail/6.4.2/configuration/alert--notification-and-quarantine-report-emails#actions)

Similarly to Quarantine reports, Email Gateway Security supports actions for the quarantined email from the notification email.

For the supported actions see [Supported functions](/docs/mdemail/6.4.2/operating/quarantine-reports#supported-functions).

#### [Notifications after a rescan](/docs/mdemail/6.4.2/configuration/alert--notification-and-quarantine-report-emails#notifications-after-a-rescan)

When *Advanced / Rescan notifications / Send rescan notification again if email keeps being blocked and quarantined* is enabled for the security rule processing the email, the configured notifications are sent again if the email is kept quarantined after a __[*full rescan*](https://www.opswat.com/docs/mdemail/operating/quarantine-reports#full-rescan-email) or [*anti-malware rescan*](https://www.opswat.com/docs/mdemail/operating/quarantine-reports#anti-malware-rescan-email).

Email template

Notifications are rendered from the single `notification_blocked` template. The post-rescan header is selected automatically via the `is_rescanned` flag. This means any customization of the blocked-notification body applies to both first-block and post-rescan cases.

For details see [Security policy](/docs/mdemail/6.4.2/configuration/policy#security-policy) and [Supported functions](/docs/mdemail/6.4.2/operating/quarantine-reports#supported-functions).

## [Legacy quarantine reports](/docs/mdemail/6.4.2/configuration/alert--notification-and-quarantine-report-emails#legacy-quarantine-reports)

Obsolete function

This function is obsolete and will be removed in a future version of Email Gateway Security.

Use the new quarantine report functionality configured under **Settings > Quarantine reports** instead.

For details see [Configuration/Quarantine reports](/docs/mdemail/6.4.2/configuration/quarantine-reports).

Not available on secondary instances

**Settings > Alerts & Reports / Quarantine Reports** are not available on a secondary instance of a scalable deployment. The quarantine reports must be configured on the primary instance.

For details see [Scalable deployment operation](/docs/mdemail/6.4.2/operating/scalable-deployment-operation).

MetaDefender Email Gateway Security can be configured to periodically send reports about the quarantine status.

Quarantine reports can be configured under **Settings > Alerts & Reports / Quarantine Report**.

The *Quarantine report schedule* can be the following in the MetaDefender Email Gateway Security server's time:

1. Off: no reports are sent
2. Hourly: a report is sent at every o'clock
3. Daily a report is sent every day, at midday
4. Weekly: a report is sent every Monday, at midday
5. Monthly: a report is sent on the first day of every month, at midday

With *Quarantine report rule* the digest email may be restricted to inbound or outbound quarantined items only.

Both the *Advanced Threat Prevention* and the *Zero-Day Malware Prevention* (see [Configuration/Policy](/docs/mdemail/6.4.2/configuration/policy)) features can quarantine emails. With *Only include quarantined emails that were blocked* the quarantine report can be restricted to items quarantined by *Advanced Threat Prevention* only.

Quarantine report limitation

Quarantine report will not contain more than 1000 entries. If there were more than 1000 new quarantined entries since the last quarantine report you will have to check the actual quarantine for more information. If you set a restriction for reporting only blocked emails and/or reporting only inbound/outbound emails the numbers and entries in the quarantine report will reflect those options.
