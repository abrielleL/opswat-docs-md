<!-- source: https://www.opswat.com/docs/mdemail/configuration/email-tags -->

# Email tags

Email Gateway Security supports adding markers called ***tags*** to emails, to provide a user-defined notation for emails based on different processing properties of a specific email.

Per rule tags

Tags can be configured separately for each security rule.

## [Tag syntax](/docs/mdemail/configuration/email-tags#tag-syntax)

The following restriction are enforced for tag values:

1. No whitespace is allowed (space, new line, tab, etc.).
2. Colon ( : ) and/or backslash ( \ ) are not allowed.

Currently there is no restriction on the length of the tags.

## [Recommended tag values](/docs/mdemail/configuration/email-tags#recommended-tag-values)

When a tag is configured to be added to the delivered email’s subject, the following are recommended:

1. Keep the tags short (at most 10-15 characters),
2. Use US-ASCII characters only.

Restrictions for email headers

Different standards and RFCs prescribe different restrictions on the length and character sets of email headers, for example the subject.

Please keep in mind, that tags add up to the original subject of the email, and this new subject together must fulfill the requirements in the standards and RFCs.

## [Tag-able actions and statuses](/docs/mdemail/configuration/email-tags#tag-able-actions-and-statuses)

Tags can be assigned to emails in case of the following actions or statuses, for each rule:

| **Action or status** | **Location** | **Description** |
| --- | --- | --- |
| Allowed emails | SCAN / Allowed actions | These tags will be applied to emails that are allowed (i.e. have no threat detected, have no DLP violation, have no spam and phishing). |
| Blocked emails | ADVANCED THREAT PREVENTION / Blocked actions | These tags will be applied to emails that are blocked due to threat detected or DLP violation. |
| Sanitized emails | ZERO-DAY MALWARE PREVENTION | These tags will be applied to emails with disarmed and reconstructed contents (headers, body or attachments). |
| Known phishing emails | ANTI-PHISHING | These tags will be applied to emails that are known phishing (for details see [Operating/Phishing and spam](/docs/mdemail/operating/phishing-and-spam)). |
| Potential phishing emails | ANTI-PHISHING | These tags will be applied to emails that are potential phishing (for details see [Operating/Phishing and spam](/docs/mdemail/operating/phishing-and-spam)). |
| Known spam emails | ANTI-SPAM | These tags will be applied to emails that are known spam (for details see [Operating/Phishing and spam](/docs/mdemail/operating/phishing-and-spam)). |
| Potential spam emails | ANTI-SPAM | These tags will be applied to emails that are potential spam (for details see [Operating/Phishing and spam](/docs/mdemail/operating/phishing-and-spam)). |
| Bypassed emails | ADVANCED | These tags will be applied to emails that were bypassed by any reasons (for details see [Operating/Bypassing](/docs/mdemail/operating/bypassing)). |

For details see [Configuration/Policy](/docs/mdemail/configuration/policy).

## [Adding tags to the email subject](/docs/mdemail/configuration/email-tags#adding-tags-to-the-email-subject)

To add a tag to the subject of the emails processed by the rule, enable the *Add to subject* toggle switch next to the tag name.

Disabled when email is blocked

The adding tags to the subject option is disabled under *ADVANCED THREAT PREVENTION / Blocked actions* when the *Handling of the email* option is set to *Block email*.

The reason for this is that in this case no email is delivered, hence no point in adding tags to the header.
