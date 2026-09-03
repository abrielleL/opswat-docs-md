<!-- source: https://www.opswat.com/docs/mdemail/6.4.1/operating/recipient-guide -->

# Email recipient guide

This guide is to provide information about MetaDefender Email Gateway Security specific features of the emails delivered to recipients.

## [Disclaimers](/docs/mdemail/6.4.1/operating/recipient-guide#disclaimers)

What is a disclaimer?

A disclaimer is a text addendum in an email that informs the recipient about certain circumstances about the processing of the email.

Read carefully!

Always read the disclaimers carefully cause they contain relevant information about your email and call your attention to risks that may be in your email.

### Disclaimer p[ositions](https://docs.opswat.com/mdemail/configuration/disclaimers#positions)

Disclaimers may be added either

1. Before the contents of the original email body (head of the email body) or
2. After the contents of the original email body (end of the email body).

### [Disclaimer styles](/docs/mdemail/6.4.1/operating/recipient-guide#disclaimer-styles)

Disclaimers may come in the following styles with the following meaning:

1. *Information*: the disclaimer displayed with a blue marker calls your attention to informational details about your email; example:
2. *Warning*: the disclaimer displayed with a yellow marker warns you about problems regarding your email; example:
3. *Critical*: the disclaimer displayed with a red marker indicates serious risks with the email that require attention; example:

Text-only emails

Text-only emails (emails that are viewed in a text-only email client or emails with no HTML body) can show no colors and text formatting.

For these emails Email Gateway Security will add plain text disclaimers with no formatting.

For further details about disclaimers see [Disclaimers](/docs/mdemail/6.4.1/configuration/disclaimers).

## [Redirected hyperlinks](/docs/mdemail/6.4.1/operating/recipient-guide#redirected-hyperlinks)

Why need hyperlinks to be redirected?

Attackers often send emails with hyperlinks directing to phishing sites. To be able to check the phishing nature of hyperlinks inside emails at the time of clicking, Email Gateway Security redirect links through OPSWAT's Safe URL Redirect service.

MetaDefender Email Gateway Security checks the reputation of each link at the time of clicking by adding `https://metadefender.opswat.com/safe-redirect/` as a prefix to the hyperlink's URL. This way the original URL gets redirected through OPSWAT's Safe URL Redirect service.

If the URL is detected by the reputation sources, then a block page is displayed to warn the user about the potential risks:

For details see [Safe URL Redirect](https://docs.opswat.com/mdcloud/operation/safe-url-redirect) and [How anti-spam and anti-phishing works?](/docs/mdemail/6.4.1/operating/how-anti-spam-and-anti-phishing-works-).

## [Sanitized hyperlinks](/docs/mdemail/6.4.1/operating/recipient-guide#sanitized-hyperlinks)

Why need hyperlinks to be sanitized?

Attackers often send emails with hyperlinks directing to phishing sites. Sanitization helps you to be prone to these attacks by 1. not letting you to click on the link, 2. giving you insight into where the hyperlink really directs.

MetaDefender Email Gateway Security defuses potentially malicious hyperlinks by removing the hyperlink reference (`href`) from the HTML anchor (`<a>`) object.

This way recipients are unable to (accidentally) click on malicious hyperlinks.

Sanitized hyperlinks are always in the format of

`<original anchor label> (<hyperlink reference>)`, for example

`google.com (https://metadefender.opswat.com/safe-redirect/www.opsvvat.com)`

`<original anchor label>` is the text the hyperlink originally displayed (that may be completely different than the underlying URL).

`<hyperlink reference>` is the underlying URL).

For example, when sending this as the original email:

After sanitizing hyperlink the recipient will receive the following (note that the hyperlink labels are completely different from the actual URL):

## [Redacted data](/docs/mdemail/6.4.1/operating/recipient-guide#redacted-data)

Why sensitive data needs to be redacted?

Email bodies and attachments often contain sensitive data (IP addresses, identification numbers, etc.) that leak out of the organization unnoticed. To avoid this accidental data leak, Email Gateway Security can hide (redact) these pieces of information and deliver the rest of the email maintaining a continuous email flow.

When sensitive data gets detected, Email Gateway Security replaces the sensitive data by black boxes. In the example below, the sensitive data both in the Subject and in the email body was redacted:

Email Gateway Security can redact sensitive data in:

1. The From, To, CC, Bcc and Subject headers,
2. Both he text and HTML email bodies,
3. In supported attachment file types.

For details see [Redact sensitive information](https://docs.opswat.com/mdcore/proactive-dlp/redact-sensitive-information).

## [Notification emails](/docs/mdemail/6.4.1/operating/recipient-guide#notification-emails)

What is a notification email?

MetaDefender Email Gateway Security sends a notification email when it blocks the original email due to malware infection, encrypted attachments, or any other violation of the organizational policy.

Notification emails contain all relevant metadata (sender, recipient(s), subject, etc.) about the original email for easier identification.

Notification emails also contain a link to the processing results of the particular email.

Clicking this link the recipient can have further details why the email was blocked (in the example below the blocking was caused by a matching YARA rule).

Each box in the processing result page represents a MetaDefender Email Gateway Security technology that processed the email in question.

The color codes of the boxes are the following:

- Red: the technology detected an unresolvable policy violation and caused the email to block (example the *YARA* block below)
- Yellow: non-blocking problem occurred during processing (example the *Proactive DLP* block below)
- Green: no problem found, or resolvable violations found during processing (example the *Metascan* block below)

## [Rescan emails with encrypted attachments](/docs/mdemail/6.4.1/operating/recipient-guide#rescan-emails-with-encrypted-attachments)

What are encrypted attachments?

Certain file types support being encrypted using passwords. An encrypted attachment is a password encrypted file sent as an email attachment.

For example in Microsoft Word the following function can encrypt the file with a password:

### [Supported file types](https://docs.opswat.com/mdemail/operating/password-protected-attachments#supported-file-types)

The following file types are supported as encrypted attachments:

| **Category** | **File types (extension)** |
| --- | --- |
| Archive files | .zip, .7z |
| Portable Document Format files | .pdf |
| Microsoft Office files | .doc, .docx, .xls, .xlsx, .ppt, .pptx |
| GnuPG *symmetric encryption* | .gpg |

Unsupported file types

Encrypted attachments of unsupported file types can not be processed and will remain blocked by Email Gateway Security.

### [Rescan process](/docs/mdemail/6.4.1/operating/recipient-guide#rescan-process)

Who knows the password?

Email Gateway Security's assumption is that the recipient of the email knows the passwords of the encrypted attachments.

If the recipient does not know the password then there is no point in delivering the encrypted attachments as the recipient won't be able to open it.

1. Given by the nature of encryption, real —potentially malicious— contents of encrypted attachments are hidden from MetaDefender Email Gateway Security, thus emails with encrypted attachments are blocked by default.
2. MetaDefender Email Gateway Security sends a notification about the blocked email to the recipient(s) containing a link to the Quarantine actions.

4. MetaDefender Email Gateway Security displays a password box for each encrypted attachments. Also, the email body is displayed in the rescan page for cases when password formulation instructions are in the email body.

5. For attachments requiring multiple passwords (e.g. encrypted zip archives containing encrypted doc files) multiple passwords can be entered in the password box. After each password, hit the Enter key on the keyboard so that you can start writing the next password.

6. When the rescan fails (wrong password for example) the user is notified by a message in a red box.
7. When the rescan succeeds the user is informed by a message in a green box.

For further details about password protected attachments and rescanning them see [Password protected attachments](/docs/mdemail/6.4.1/operating/password-protected-attachments).

## [Quarantine reports](/docs/mdemail/6.4.1/operating/recipient-guide#quarantine-reports)

What are quarantine reports?

Quarantine reports are digest emails about the emails that got quarantined by Email Gateway Security since the last quarantine report.

### [Quarantined emails](/docs/mdemail/6.4.1/operating/recipient-guide#quarantined-emails)

Email Gateway Security quarantines:

1. Emails that get blocked:

   1. Due to malware infection (anti-malware scan),
   2. Due to malicious behaviour (sandbox),
   3. Were blocklisted by administrators,
   4. Due to sensitive data,
   5. Spam or phishing emails,
   6. Emails with encrypted attachments.
2. Emails with disarmed and reconstructed contents.

### [Quarantine report emails](/docs/mdemail/6.4.1/operating/recipient-guide#quarantine-report-emails)

Email Gateway Security sends a list of emails of the recipient, that have been quarantined since the last report (if this is the first quarantine report, then the list contains all quarantined emails of the recipient) in a quarantine report email.

For each entry in the quarantine report email there is an *Actions* link that directs the recipient to Email Gateway Security's Quarantine page for actions on the quarantined email.

Depending on the configuration at the organization, the quarantine actions page currently supports the following actions on quarantined emails:

- Rescan quarantined email: scan the email again as with updated engines the outcome may be different.
- Delete quarantined email: permanently delete the email from the quarantine.
- Deliver quarantined email: release the potentially malicious email from the quarantine.

Risk of malware outbreak

Users can release potentially malicious emails from the quarantine using *Deliver quarantined email* action. For this reason this action is usually not enabled for recipients.

For further details about quarantine reports see [Quarantine reports](/docs/mdemail/6.4.1/operating/quarantine-reports).
