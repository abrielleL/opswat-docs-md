<!-- source: https://www.opswat.com/docs/mdemail/configuration/disclaimers -->

# Disclaimers

A disclaimer is a text addendum in an email that informs the recipient about certain circumstances about the processing of the email.

## [Disclaimer use cases](/docs/mdemail/configuration/disclaimers#disclaimer-use-cases)

Disclaimers may be set for the following cases in Email Gateway Security:

- For email email that was *processed* by a specific security rule. Configure under **Security Rules /*rule*/ General / Rule disclaimer**.
- For an email that was *allowed* (e.g. no infection or sensitive data was found) under **Security Rules /*rule*/ Scan / Allowed actions**.

- For an email that was *blocked* (e.g. infected or sensitive data found) but delivered cause **Security Rules /*rule*/ Advanced Threat Prevention / Handling of the email** is set either to *Delete blocked content* or *Deliver blocked contents*. Set the disclaimer for these cases under **Security Rules /*rule*/ Advanced Threat Prevention / Blocked actions**.

- For an email that was *blocked due to password protected attachments* but was delivered cause **Security Rules /*rule*/ Advanced Threat Prevention / Handling of the email** is set either to *Delete blocked content* or *Deliver blocked contents*. Set the disclaimer for this case under **Security Rules /*rule*/ Advanced Threat Prevention / Encrypted attachments**.

- For an email that was *disarmed and reconstructed* under **Security Rules /*rule*/ Zero-Day Malware Prevention / Zero-Day Malware Prevention**.

- For an email thats *disarm and reconstruction failed* under **Security Rules /*rule*/ **Zero-Day Malware Prevention** / Zero-Day Malware Prevention / Override sanitization behavior**.

- For an email that has *attachments uploaded* under **Security Rules /*rule*/ **Upload attachments** / Upload attachments / Upload attachments to MetaDefender Managed File Transfer / Attachment notice**.

- For an email that was *bypassed* under **Security rules /*rule*/ Advanced / Override error handling behavior**.

For details see [Configuration/Policy](/docs/mdemail/configuration/policy).

## [Grouping](/docs/mdemail/configuration/disclaimers#grouping)

### [Overview](/docs/mdemail/configuration/disclaimers#overview)

To have a more compact disclaimer experience, disclaimers can be grouped together so that all disclaimers can be in a single block inside the email.

Disclaimers when not grouped:

Disclaimers when grouped:

Grouped by default

For new installations, disclaimers are grouped by default. This is a change compared to legacy systems (before Email Gateway Security 5.6.0) where disclaimer grouping was not available.

### [Configuration](/docs/mdemail/configuration/disclaimers#configuration)

Grouping the disclaimers can be enabled for each security rule among the *Advanced* settings.

The disclaimer block can be configured to be either in the head or in the tail of the email body. When disclaimers are grouped, a footer disclaimer can also be configured to provide details or additional information to the recipient.

The disclaimer block has a banner. The banner is blue when there are no *critical* style disclaimers in the group, and red, when there are *critical* style disclaimers.

## [Disclaimer editor](/docs/mdemail/configuration/disclaimers#disclaimer-editor)

For each disclaimer Email Gateway Security has a what-you-see-is-what-you-get disclaimer with all needed functionality built-in. For example, it has support for text styles, links and lists.

The position of the disclaimer can be set to before or after the contents of the email.

A disclaimer style can be applied to emphasize content to the user (HTML only).

The alignment of the disclaimer can be changed to left or right aligned clicking the  and  buttons.

## [Positions](/docs/mdemail/configuration/disclaimers#positions)

A disclaimer may be added either

1. Before the contents of the original email body (head of the email body) or
2. After the contents of the original email body (end of the email body).

## [Styles](/docs/mdemail/configuration/disclaimers#styles)

The following built-in styles are supported for disclaimers:

1. *None*: no further formatting of the disclaimer
2. *Information*: the disclaimer is displayed as a blue box (or with a blue bar on the left when grouped)
3. *Warning*: the disclaimer is displayed as a yellow box (or with a yellow bar on the left when grouped)
4. *Critical*: the disclaimer is displayed as a red box (or with a red bar on the left when grouped)

## [Views](/docs/mdemail/configuration/disclaimers#views)

Each disclaimer editor has the following two views:

1. HTML: to edit the disclaimer for **HTML formatted emails** in a what-you-see-is-what-you-get editor,
2. PLAIN TEXT: to edit the disclaimer for **plain text formatted emails** in a text editor.

## [Disclaimer variables](/docs/mdemail/configuration/disclaimers#disclaimer-variables)

### [Variable syntax](/docs/mdemail/configuration/disclaimers#variable-syntax)

The common format of a variable looks like this: %[<prefix>|{s=<suffix>}]<variable_name>[<placeholder>]%

A variable contains three parts:

- *prefix*: this text will be displayed before the value of the variable if the value is not empty or there is a placeholder defined
- *suffix*: this text will be displayed following the value of the variable if the value is not empty
- *variable_name*: the name of the variable
- *placeholder*: this text will be displayed if the vale of the variable is empty

Examples:

| **Variable token** | **Variable value** | **Output in disclaimer** |
| --- | --- | --- |
| %[]email_subject[]% | Test subject | Test subject |
| %[]email_subject[]% | "" | "" |
| %[Subject: ]email_subject[]% | Test subject | Subject: Test subject |
| %[Subject: ]email_subject[]% | "" | "" |
| %[Subject: ]email_subject[No subject]% | "" | Subject: No subject |
| %[]email_subject[No subject]% | "" | No subject |
| %[]email_subject[No subject]% | Test subject | Test subject |
| %[Subject: {s= (this is the subject)}]email_subject[]% | Test subject | Subject: Test subject (this is the subject) |

### [Available variables](/docs/mdemail/configuration/disclaimers#available-variables)

#### [Generally available variables](/docs/mdemail/configuration/disclaimers#generally-available-variables)

The following variables are available for any disclaimer:

**email_date**

Email message date sent

**email_sender**

Sender email address

**email_recipients**

Recipient email address(es) (Comma separated if more than one)

**email_subject**

Email subject

**email_message_id**

Email message-id header

**email_classifications**

Classifications assigned to the email during processing (Comma separated if more than one)

**origin_ip**

Email last HOP IP address

**scan_verdicts**

Email scanning verdicts

**Attachment related variables**

**email_attachment_names**

Original file name of the email attachments.

Deep CDR or Proactive DLP processing might change the file names of attachments. This variable holds the original attachment file names as a comma separated list.

**email_attachment_count**

Total number of regular (non-inline) attachments in email

**email_attachment_password_count**

Total number of password protected attachments

**email_attachment_uploaded_count**

Total number of uploaded attachments

**email_attachment_sanitized_count**

Total number of sanitized attachments

**email_attachment_sanitization_failed_count**

Total number of attachments where sanitization failed

**email_attachment_sanitization_blocked_count**

Total number of sanitized blocked attachments

**email_attachment_blocked_count**

Total number of blocked attachments

**email_attachment_removed_count**

Total number of removed attachments

**email_blocked_attachments**

List of blocked attachment file names

#### [Context specific variables](/docs/mdemail/configuration/disclaimers#context-specific-variables)

**Emails with encrypted attachments**

The following variables are available for *disclaimers to emails with encrypted attachments* only:

**rescan_link_url**

Replaced by the **Settings > General / Configuration / Public server name** (see [Configuration/Settings](/docs/mdemail/configuration/settings)). If the *Public server name* is not set then the "*Your administrator did not set a public server address for rescan*" text will be displayed instead.

**rescan_link_expiry**

Replaced by the **Settings > General / Configuration / Rescan link availability** value.

**rescan_link_expiry_time**

Replaced by the date and time value calculated using the **Settings > General / Configuration / Rescan link availability** value. **Calculation method** The date and time value is calculated as: (Time of email arrival to Email Gateway Security) + (**Settings > General / Configuration / Rescan link availability**) **UTC or server local time** The value of **Settings > General / Configuration / Use the server's local timezone** affects the format of this value.

*Examples: Date format with* ***server local timezone*** *enabled: 2021-09-26 10:39:49 (UTC+02:00) Date format with* ***server local timezone*** *disabled: 2021-09-26 08:39:49 UTC*

**Sanitized emails**

The following variables are available for emails that have *sanitized contents*:

**hyperlinks**

This variable applies when an email got processed by Deep CDR, and disclaimers are enabled for emails with sanitized contents.

The Deep CDR engine in MetaDefender Core (under **Inventory > Modules / Deep CDR / Settings / HTML CONFIGURATION / PROCESS HYPERLINK BEHAVIOR**) can be configured to return the list of hyperlinks in the processed file.

**sanitization_details**

This variable provides details of the sanitization operations applied to the email in the following format:

*[email subject]/[filename]: object [action], object [action] etc.*

**Emails with attachments uploaded to MetaDefender** **Managed File Transfer**

The following variables are available only for *disclaimers to emails with attachments uploaded to* MetaDefender Managed File Transfer:

**mft_name**

First name and last name of the MFT account to which the attachments were uploaded to.

**mft_email**

Email address of the account on MFT to which the attachments were uploaded to.

**mft_user**

The user name of the MFT account to which the attachments were uploaded to.

**mft_list**

List of each attachments uploaded to MFT.

**mft_url**

A link to the root folder on MetaDefender Managed File Transfer to where all the attachments were uploaded to. This variable may be used as an alternative to `mft_list` to avoid a long list of files.

Not a link by default

The value of this variable won't produce a link (as `mft_list` will), so this variable may be specified as a `href` of an `<a>` (anchor) tag in the raw HTML view of the disclaimer editor.

### [Example disclaimer with variables](/docs/mdemail/configuration/disclaimers#example-disclaimer-with-variables)

Here is an example disclaimer for blocked contents:

---
MetaDefender Email Gateway Security has removed one or more attachments in this email because it contained potentially malicious embedded objects. For more information on MetaDefender Email Gateway Security, please visit https://www.opswat.com/products/metadefender/email-security.
 
%[Date: ]email_date[]%
%[Sender: ]email_sender[]%
%[Recipients: ]email_recipients[]%
%[Subject: ]email_subject[]%
%[Message ID: ]email_message_id[]%
%[Origin IP: ]origin_ip[]%
%[Scan verdicts: ]scan_verdicts[]%

And an example result after sending an infected attachment:

---
MetaDefender Email Gateway Security has removed one or more attachments in this email because it contained potentially malicious embedded objects. For more information on MetaDefender Email Gateway Security, please visit https://www.opswat.com/products/metadefender/email-security.
 
Date: 2018-08-15 13:07:51 UTC
Sender: test1@test.com
Recipients: test2@test.com
Subject: Eicar attachment
Message ID: 90b5cc66-cf5d-9ef5-9ac8-4f9dcce083aa@test.com
Origin IP: 127.0.0.1
Scan verdicts: Eicar attachment/eicar.com: Infected
