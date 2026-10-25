<!-- source: https://www.opswat.com/docs/mdemail/6.4.2/release-notes/version-5-7-6 -->

# Version 5.7.6

View as Markdown Ask ChatGPT about this page Ask Claude about this page

| Release date | Scope |
| --- | --- |
| February 19th, 2025 | MetaDefender Email Gateway Security 5.7.6 is a feature-rich maintenance release focusing on minor improvements and bug fixes. |

## [New & improved](/docs/mdemail/6.4.2/release-notes/version-5-7-6#new--improved)

### [On-arrival URL reputation check](/docs/mdemail/6.4.2/release-notes/version-5-7-6#on-arrival-url-reputation-check)

Email Gateway Security can now be integrated to MetaDefender Cloud to check the reputation of the URLs in the email body at the time of receiving the email. When a URL is detected with malicious intent, the email is classified and handled as phishing.

For details see [On-arrival URL analysis](/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works-#on-arrival-url-analysis) and [Anti-phishing and anti-spam](/docs/mdemail/6.4.2/configuration/policy#anti-phishing-and-anti-spam).

### [Add scan results as attachments](/docs/mdemail/6.4.2/release-notes/version-5-7-6#add-scan-results-as-attachments)

MetaDefender Core scan results are now supported to be attached to an email.

For details see [Policy](/docs/mdemail/6.4.2/configuration/policy).

### [Notification about delivery failures](/docs/mdemail/6.4.2/release-notes/version-5-7-6#notification-about-delivery-failures)

The [Notify the end user when email failed](https://www.opswat.com/docs/mdemail/5.7.4/release-notes#notify-the-end-user-when-email-failed) function has been modified to send the notification to the *original recipient(s)* in case of emails processed by *inbound rules*, and to the *original sender* in case of emails processed by *outbound rules*.

For details see [Alert, notification and quarantine report emails](/docs/mdemail/6.4.2/configuration/alert--notification-and-quarantine-report-emails). For security rule direction see [Direction](/docs/mdemail/6.4.2/configuration/policy#direction).

### [Skip MFT supervisor approval](/docs/mdemail/6.4.2/release-notes/version-5-7-6#skip-mft-supervisor-approval)

It is now possible to configure attachment uploads to skip supervisor approval on the MetaDefender Managed File Transfer (MFT) side (for MFT versions that support this).

For details see [Upload attachments](/docs/mdemail/6.4.2/configuration/policy#upload-attachments).

### [HTTP Strict Transport Security](/docs/mdemail/6.4.2/release-notes/version-5-7-6#http-strict-transport-security)

Email Gateway Security's REST server now sends HTTP Strict Transport Security (HSTS) headers by default.

### [Process plain text URLs](/docs/mdemail/6.4.2/release-notes/version-5-7-6#process-plain-text-urls)

With Deep CDR 7.2.3 it is supported to rewrite, redirect and time-of-click check plain text URLs (e.g. in plain text emails) for their reputation.

### [Add to allowlist by the From header](/docs/mdemail/6.4.2/release-notes/version-5-7-6#add-to-allowlist-by-the-from-header)

Trusted senders now support entries not only from the SMTP *MAIL FROM* but also from the email's *From* header. For details see [Trusted senders](/docs/mdemail/6.4.2/configuration/trustedsenders).

### [Logging improvements](/docs/mdemail/6.4.2/release-notes/version-5-7-6#logging-improvements)

Email rescans and their details are now logged on the *SOC* log level.

*CEF* syslog output has been documented. For details see [CEF log message format](/docs/mdemail/6.4.2/operating/cef-syslog-message-format).

## [Bug fixes](/docs/mdemail/6.4.2/release-notes/version-5-7-6#bug-fixes)

### [Valid port number problems](/docs/mdemail/6.4.2/release-notes/version-5-7-6#valid-port-number-problems)

While creating *Server profiles,* Email Gateway Security displayed the error message This field must contain a valid port number even when there was a valid port number specified for a server definition.

### [Winmail.dat (TNEF) problems](/docs/mdemail/6.4.2/release-notes/version-5-7-6#winmaildat-tnef-problems)

In certain edge cases when replacing an attachment in a Transport Neutral Encapsulation Format (TNEF, winmail.dat) encoded email, the attachment did not display in the email client.

### [SMTP server empty certificate list](/docs/mdemail/6.4.2/release-notes/version-5-7-6#smtp-server-empty-certificate-list)

The certificate drop down list of the inbound SMTP server configuration showed no certificates after a browser restart even when there were certificates defined with the appropriate use case (TLS).

### [Crashes after upgrade to new version](/docs/mdemail/6.4.2/release-notes/version-5-7-6#crashes-after-upgrade-to-new-version)

A *use after free* error leading to potential memory corruption has been fixed that caused the product's Windows service crashing after upgrading from version 5.6.x to 5.7.x.

### [Culture insensitive case conversation](/docs/mdemail/6.4.2/release-notes/version-5-7-6#culture-insensitive-case-conversation)

Culture insensitive upper / lower case conversation caused security rules to not match for certain locales. The conversation has been modified to culture sensitive.

### [Inline attachments not scanned](/docs/mdemail/6.4.2/release-notes/version-5-7-6#inline-attachments-not-scanned)

Inline attachments (non-text objects that are in-line in the HTML email body) were not correctly detected and scanned when there was no filename defined for the attachment in the MIME headers.

### [No actions for additional recipients](/docs/mdemail/6.4.2/release-notes/version-5-7-6#no-actions-for-additional-recipients)

When an email was processed and blocked by a security rule that had *Additional recipients* (for details see the *Additional recipients* subsection of the *Blocked notifications* section in [Advanced Threat Prevention](/docs/mdemail/6.4.2/configuration/policy#advanced-threat-prevention)), for the additional recipients of the notification the actions defined for the notification email (for details see the *Action permissions* subsection of the *Blocked notifications* section in [Advanced Threat Prevention](/docs/mdemail/6.4.2/configuration/policy#advanced-threat-prevention)) were not visible.

### [Rules for Full rescan not visible](/docs/mdemail/6.4.2/release-notes/version-5-7-6#rules-for-full-rescan-not-visible)

The dropdown list for the option *Process email using this rule* in the **Quarantine** function *Full rescan* was not scrollable and may not have showed all available security rules.

### [Legitimate characters replaced by ???](/docs/mdemail/6.4.2/release-notes/version-5-7-6#legitimate-characters-replaced-by-)

For certain emails Deep CDR returns the HTML body with UTF-8-BOM even when the content was submitted with no BOM. The unexpected encoding caused Email Gateway Security incorrectly interpret the returned content.

### [Workflows didn't load in Central Management](/docs/mdemail/6.4.2/release-notes/version-5-7-6#workflows-didnt-load-in-central-management)

In Central Management MetaDefender Core *Workflows* did not load for Email Gateway Security *Server profiles*.
