<!-- source: https://www.opswat.com/docs/mdemail/6.4.2/operating/soc-log-level -->

# SOC log level

View as Markdown Ask ChatGPT about this page Ask Claude about this page

---

The `SOC` log level has been introduced to support easier parsing or exporting data to 3rd party aggregators, such as `Syslog`. The `SOC` log level has the following entries:

| Event | Log identifier | Fields |
| --- | --- | --- |
| Email received | email.receive | `email_id`, `ip_address`, `sender`, `recipients`, `subject`, `processing_id`, `message_id` |
| Email refused | email.refuse | `ip_address`, `sender`, `recipient`, `response` |
| Email scanned Email rescanned | email.scan email.rescan | `email_id`, `sender`, `recipients`, `subject`, `processing_id`, `message_id`, `classifications`, `scan_result`, `anti_spam_result`, `rule_name`, `scan_result_details` , `batch_id` |
| Email completed | email.complete | `email_id`, `sender`, `recipients`, `subject`, `processing_id`, `message_id`, `classifications`, `status` |
| Email quarantined | email.quarantine | `email_id`, `sender`, `recipients`, `subject`, `processing_id`, `message_id`, `classifications` |
| Email retrying | email.retry | `email_id` , `sender`, `recipients`, `subject`, `processing_id`, `message_id`, `classifications`, `retry_count`, `next_retry` |
| Email failed | email.failure | `email_id`, `sender`, `recipients`, `subject`, `processing_id`, `message_id`, `classifications` |

Fields

`processing_id`: Unique message identifier on the Email Gateway Security REST API (internal; for support).

`message_id`: The `Message-ID` field according to [RFC 5322](https://datatracker.ietf.org/doc/html/rfc5322) that contains a single unique message identifier.

`email_id`: Unique message identifier inside Email Gateway Security (internal; for support).

`classifications`: Classifications according to [Email classifications](https://www.opswat.com/docs/mdemail/6.1.2/operating/email-classifications).

`scan_result`: Overall scan result by MetaDefender Core. The value may be `Allowed` or `Blocked` based on the setting in the *Allowed processing results on MetaDefender Core* image below.

`antispam_result`: Anti-spam and Anti-phishing classifications according to [Spam classifications](https://www.opswat.com/docs/mdemail/6.1.2/operating/phishing-and-spam#classifications) and [Phishing classifications](https://www.opswat.com/docs/mdemail/6.1.2/operating/phishing-and-spam#classifications) respectively.

`scan_result_details`: scan details (URLs, data IDs, verdicts, etc.) on MetaDefender Core for each email component (headers, bodies, each attachments).

`status`: Status of the email according to [Processing status values](https://www.opswat.com/docs/mdemail/6.1.2/operating/email-history#processing-status-values).

`retry_count`: Number of retry attempts have done in case of a processing or delivery failure.

`next_retry`: The time of the next retry attempt in case of a processing or delivery failure.

`batch_id`: The identifier of the MetaDefender Core side batch that combines the components of the email.

Allowed processing results on MetaDefender Core

Quote escaping in log entry parameters

Certain SOC level logs contain parameters of that entry. For example the `ip_address` parameter below:

`Sep 23 10:32:06 UTC LE11-D8766 CEF:0|OPSWAT|MDEMAIL|6.1.2RC1|email.receive|Email receive, email_id='804cc4c0-226f-45bc-800f-29a88ee94caf', ip_address='127.0.0.1', message_id='e842c3d7-0694-4ba5-97f1-03eed504f62a@remo.te', processing_id='a9b68d415e754798b63ab274f47177f4', recipients='joe@loc.al', sender='dan@remo.te', subject='bec'|5|OMStid=6976 OMSmsgid=0`

The values of these parameters might contain the delimiter single qoute `'` character. In these cases the single quote `'` characters are escaped by doubling each single qoute character (e.g. `'``''` , `''` `''''` , etc.).
