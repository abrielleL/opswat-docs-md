<!-- source: https://www.opswat.com/docs/mdemail/6.4.1/configuration/additional-email-headers -->

# Additional email headers

Email Gateway Security supports adding extra headers to emails, to provide a user-defined notation for emails based on different processing properties of a specific email.

Per rule additional headers

Additional headers can be configured separately for each security rule.

## [Actions and statuses with additional headers](/docs/mdemail/6.4.1/configuration/additional-email-headers#actions-and-statuses-with-additional-headers)

Additional headers can be assigned to emails in case of the following actions or statuses, for each rule:

| **Action or status** | **Location** | **Description** |
| --- | --- | --- |
| Allowed emails | SCAN / Allowed actions | These headers will be applied to emails that are allowed (i.e. have no threat detected, have no DLP violation, have no spam and phishing). |
| Blocked emails | ADVANCED THREAT PREVENTION / Blocked actions | These headers will be applied to emails that are blocked due to threat detected or DLP violation. |
| Blocked email notification | ADVANCED THREAT PREVENTION / Notify recipients if email is blocked | These headers will be applied to notification emails that notify about the original email being blocked due to threat detected or DLP violation. |
| Sanitized emails | ZERO-DAY MALWARE PREVENTION | These headers will be applied to emails with disarmed and reconstructed contents (headers, body or attachments). |
| Known phishing emails | ANTI-PHISHING / Known Phishing | These headers will be applied to emails that are known phishing (for details see [Operating/Phishing and spam](/docs/mdemail/6.4.1/operating/phishing-and-spam)). |
| Potential phishing emails | ANTI-PHISHING / Potential Phishing | These headers will be applied to emails that are potential phishing (for details see [Operating/Phishing and spam](/docs/mdemail/6.4.1/operating/phishing-and-spam)). |
| Phishing notification | ANTI-PHISHING / Notifications | These headers will be applied to notification emails that notify about the original email being *quarantined* as known or potential phishing. |
| Known spam emails | ANTI-SPAM / Known Spam | These headers will be applied to emails that are known spam (for details see [Operating/Phishing and spam](/docs/mdemail/6.4.1/operating/phishing-and-spam)). |
| Potential spam emails | ANTI-SPAM / Potential Spam | These headers will be applied to emails that are potential spam (for details see [Operating/Phishing and spam](/docs/mdemail/6.4.1/operating/phishing-and-spam)). |
| Spam notification | ANTI-SPAM/ Notifications | These headers will be applied to notification emails that notify about the original email being *quarantined* as known or potential spam. |
| Bypassed emails | ADVANCED | These headers will be applied to emails that were bypassed by any reasons (for details see [Operating/Bypassing](/docs/mdemail/6.4.1/operating/bypassing)). |

For details see [Configuration/Policy](/docs/mdemail/6.4.1/configuration/policy).

## [Field variable support in header values](https://www.opswat.com/docs/mdemail/release-notes/version-5-7-1#field-variable-support-in-header-values)

Field variables can now also be used in header values. This allows inserting of dynamic data, such as sender, recipient, email classifications etc. into custom X-headers. For a list of available field variables, see [Available variables](/docs/mdemail/6.4.1/configuration/disclaimers#available-variables).
