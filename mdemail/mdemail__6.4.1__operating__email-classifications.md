<!-- source: https://www.opswat.com/docs/mdemail/6.4.1/operating/email-classifications -->

# Email classifications

To better reflect the risk level associated to a certain email and for easier understanding what potential risks an email carries, Email Gateway Security introduced classifications of emails.

One-to-many

A certain email may have multiple classifications.

Classifications assigned to a certain email can be reviewed in the *Email details* view under **Audit > Email history** or **Quarantine**. For further details see [Operating/Email History](/docs/mdemail/6.4.1/operating/email-history) and [Operating/Quarantine](/docs/mdemail/6.4.1/operating/quarantine).

## [Negative classifications](/docs/mdemail/6.4.1/operating/email-classifications#negative-classifications)

Classifications in this group are negative in terms of that they indicate high risk or failure. They are marked with red color in the GUI.

### [Emails with problems](/docs/mdemail/6.4.1/operating/email-classifications#emails-with-problems)

Most of he emails classified according to the classes below are blocked by default as they expose the organization to significant risk (the exceptions are marked below).

| **Classification** | **Description** |
| --- | --- |
| Scan failure | Anti-malware scan of the *Advanced Threat Detection* capability failed. |
| Malware detected | Malware threat was detected in the email by the *Advanced Threat Detection* capability. |
| Phishing | The email was detected as known phishing (probability level 9) by the *Anti-phishing* capability. For details see the *Anti-phishing and anti-spam* section under [Configuration/Policy](/docs/mdemail/6.4.1/configuration/policy). |
| Encrypted | The email contains one or more encrypted and/or password protected attachments. For details see [Operating/Password protected attachments](/docs/mdemail/6.4.1/operating/password-protected-attachments). |
| DLP violation | The email contents violate the Data Loss Prevention policy defined by the *Sensitive Data Loss Prevention* capability. For details see <https://www.opswat.com/docs/mdcore/proactive-dlp>. |
| Blocked | Blocked for any other reason not mentioned above. |
| Not scanned | The *Advanced Threat Detection* capability was configured to not scan this email. |
| Bypassed | The email bypassed one or more processing steps according to the bypassing settings in [Policy](/docs/mdemail/6.4.1/configuration/policy). Bypassed emails are not blocked. |
| No license | The email was not processed as the product is not licensed or the number of recipients served exceeded the number of licensed recipients. Email of no license cases are not blocked. |
| SPF Fail | The SPF verification failed. This email will also automatically be assigned the classification *Phishing*. |
| SPF Soft fail | The SPF verification failed with a *Soft Fail* result. This email will also be assigned the classification *Potential phishing*. |
| DKIM Invalid | The DKIM signature for the email is invalid. This email will also automatically be assigned the classification *Phishing*. |
| DMARC Fail | The DMARC verfication failed. |
| YARA match | Content in this email has triggered a YARA rule in MetaDefender Core. |
| Suspicious behavior | The content of this email displays *Suspicious behavior* patterns, identified by OPSWAT Filescan. |
| Malicious behavior | The content of this email displays *Malicious behavior* patterns, identified by OPSWAT Filescan. |

### [Unsolicited emails](/docs/mdemail/6.4.1/operating/email-classifications#unsolicited-emails)

The emails classified according to the classes below are blocked by default as they most probably are unsolicited emails.

| **Classification** | **Description** |
| --- | --- |
| Spam | The email was detected as known spam (probability level 9) by the *Anti-spam* capability. For details see the *Anti-phishing and anti-spam* section under [Configuration/Policy](/docs/mdemail/6.4.1/configuration/policy). |
| Marketing | The email was detected as marketing by the *Anti-spam* capability. For details see the *Anti-phishing and anti-spam* section under [Configuration/Policy](/docs/mdemail/6.4.1/configuration/policy). |

### [Processing failures](/docs/mdemail/6.4.1/operating/email-classifications#processing-failures)

Classifications in this group indicate problems in the email processing pipeline making the email undeliverable. The problems listed below do not, however, expose the system to risk.

| **Classification** | **Description** |
| --- | --- |
| Send failure | The email was failed to be sent due to outage of the next hop in the email relay chain. |
| Anti-spam engine failure | Anti-spam scan of the *Anti-spam* capability failed. |
| Sanitization failure | Processing of the *Zero-Day Malware Prevention* capability failed. For details see <https://www.opswat.com/docs/mdcore/deep-cdr>. |
| SPF Error | There was an error attempting to validate the sender's SPF record. |
| DKIM Error | There was an error verifying the emails DKIM signature. |
| DMARC Error | There was an error during the DMARC verification. |

## [Classifications indicating risk](/docs/mdemail/6.4.1/operating/email-classifications#classifications-indicating-risk)

Classifications in this group indicate moderate risk. They are marked with orange color in the GUI.

Classifications in this group indicate risk due to the

1. potentially harmful contents of the email or
2. action that was performed on the email.

Classifications of this group are marked with green color in the GUI.

### [Email content risks](/docs/mdemail/6.4.1/operating/email-classifications#email-content-risks)

Emails in this group expose the organization to risk given by their potentially malicious contents.

| Classification | Description |
| --- | --- |
| Possible malware detected | Possible malware threat was detected in the email by the *Advanced Threat Detection* capability. |
| Possible phishing | The email was detected as possible phishing (probability level 1-8 depending on the *Probability level* set for the rule’s anti-phishing) by the *Anti-phishing* capability. For details see the *Anti-phishing and anti-spam* section under [Configuration/Policy](/docs/mdemail/6.4.1/configuration/policy). |
| Possible marketing | The email was detected as possible marketing by the *Anti-spam* capability. For details see the *Anti-phishing and anti-spam* section under [Configuration/Policy](/docs/mdemail/6.4.1/configuration/policy). |
| Possible spam | The email was detected as possible spam (probability level 1-8 depending on the *Probability level* set for the rule’s anti-spam) by the *Anti-spam* capability. For details see the *Anti-phishing and anti-spam* section under [Configuration/Policy](/docs/mdemail/6.4.1/configuration/policy). |
| Possible DLP violation | The email contains data that was detected as possibly violating the Data Loss Prevention policy defined by the *Sensitive Data Loss Prevention* capability. For details see <https://www.opswat.com/docs/mdcore/proactive-dlp>. |
| Partially sanitized | Processing of the *Zero-Day Malware Prevention* capability succeeded partially only. For details see <https://www.opswat.com/docs/mdcore/deep-cdr>. |

### [Email operation risks](/docs/mdemail/6.4.1/operating/email-classifications#email-operation-risks)

Emails in this group were let out from the quarantine.

| Classification | Description |
| --- | --- |
| Released | Potentially malicious email was released from the [Quarantine](/docs/mdemail/6.4.1/operating/quarantine). |
| Forwarded | Potentially malicious email was forwarded from the [Quarantine](/docs/mdemail/6.4.1/operating/quarantine). |

## [Positive classifications](/docs/mdemail/6.4.1/operating/email-classifications#positive-classifications)

Classifications in this group are positive in terms of that they indicate that the email

1. was clean,
2. its risk was mitigated or
3. the system was configured to bypass it.

Classifications of this group are marked with green color in the GUI.

### [Clean emails](/docs/mdemail/6.4.1/operating/email-classifications#clean-emails)

| **Classification** | **Description** |
| --- | --- |
| Spam allowlisted | The sender IP address of the email is on the allowlist. For details see [Anti-spam](/docs/mdemail/6.4.1/configuration/settings#anti-spam). |
| Sanitized | The contents of the email were successfully processed by the *Zero-Day Malware Prevention* capability: all potentially malicious components have been removed. For details see: <https://www.opswat.com/docs/mdcore/deep-cdr>. |
| No malware detected | The *Advanced Threat Detection* capability found all the contents of the email clean. |

### [Notifications, alerts and reports](/docs/mdemail/6.4.1/operating/email-classifications#notifications-alerts-and-reports)

Emails with the classifications below originate from Email Gateway Security and are clean inherently. For further details see [Configuration/Alert, notification and quarantine report emails](/docs/mdemail/6.4.1/configuration/alert--notification-and-quarantine-report-emails).

| **Classification** | **Description** |
| --- | --- |
| Notification | Notifications are sent when emails are blocked by *Advanced Threat Prevention* and Email Gateway Security is configured to *block* the *email*. |
| Alert | Email alerts can be configured so that certain users can instantly be notified about the occurrence of certain system events. |
| Report | Report emails sent by Email Gateway Security. |

### [Not blocked emails](/docs/mdemail/6.4.1/operating/email-classifications#not-blocked-emails)

| **Classification** | **Description** |
| --- | --- |
| Sanitized original | When Email Gateway Security is configured to quarantine an original copy of sanitized emails, the original copy will receive this classification. |
| DLP original | When Email Gateway Security is configured to quarantine an original copy of DLP processed emails, the original copy will receive this classification. |
| DLP redacted | The sensitive information found by the *Sensitive Data Loss Prevention* capability has been redacted. |
| Rescanned | The email is a result of a successful rescan operation. For details see [Rescan email](/docs/mdemail/6.4.1/operating/quarantine#rescan-email). |
| Removed attachments | Attachments were removed from the email according the settings in [Policy](/docs/mdemail/6.4.1/configuration/policy). |
| SPF No record | No SPF record was found for the sender. |
| SPF Neutral | Email sender SPF verification resulted in a *Neutral* result. |
| SPF Pass | Email sender SPF verification resulted in a *Pass* result. |
| DKIM No signature | No DKIM signature was detected in the email. |
| DKIM Valid | The email's DKIM signature is valid. |
| DMARC Pass | The DMARC verification resulted in a *Pass* result. |
| Release requested | One or more recipients have requested this email to be released. |

### [No classification](/docs/mdemail/6.4.1/operating/email-classifications#no-classification)

| **Classification** | **Description** |
| --- | --- |
| No classification | The email did not apply to any other classification. This very rare condition may appear when Email Gateway Security is licensed and works normally, but is configured to not process the email in any way (no malware and spam scanning, no data sanitization, DLP, etc.). |
