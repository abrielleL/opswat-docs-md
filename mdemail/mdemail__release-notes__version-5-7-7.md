<!-- source: https://www.opswat.com/docs/mdemail/release-notes/version-5-7-7 -->

# Version 5.7.7

## [New & improved](/docs/mdemail/release-notes/version-5-7-7#new--improved)

### [Header filters](/docs/mdemail/release-notes/version-5-7-7#header-filters)

Email Gateway Security now supports email headers (like *From*, *To* or *Subject*) in filtering *Security Rules*. This way headers in emails can define how an email gets processed (e.g. emails having certain headers can be allowlisted).

For details see [Email header conditions](/docs/mdemail/configuration/policy#email-header-conditions).

### [SMTP rewrite](/docs/mdemail/release-notes/version-5-7-7#smtp-rewrite)

It is now supported to rewrite the *domain part* of SMTP sender (MAIL FROM) or SMTP recipient (RCPT TO) email addresses at the time of submitting emails to the SMTP relay. This way emails can be forwarded to alternative domains.

For details see the *SMTP sender or recipient rewriting* subsection in the [Advanced](/docs/mdemail/configuration/policy#advanced) policy settings.

### [Login banner](/docs/mdemail/release-notes/version-5-7-7#login-banner)

Email Gateway Security now supports a customizable banner in the login page.

For details see [Login banner](/docs/mdemail/configuration/settings#login-banner).

### [InSights Threat Intelligence](/docs/mdemail/release-notes/version-5-7-7#insights-threat-intelligence)

With MetaDefender Core 5.13.2 —or newer— InSights Threat Intelligence is available (when licensed). This module further improves Email Gateway Security's capabilities against malicious hyperlinks and URLs in email bodies and attachments.

For details see [InSights Threat Intelligence](https://www.opswat.com/docs/mdcore/insights-threat-intelligence).

## [Fixed](/docs/mdemail/release-notes/version-5-7-7#fixed)

### [Time-of-click prefix not applied](/docs/mdemail/release-notes/version-5-7-7#time-of-click-prefix-not-applied)

In certain corner-cases Email Gateway Security was unable to properly process email bodies. As one visible symptom, time-of-click URL reputation check redirects were not applied on these emails.

### [Quarantine reports not in config export](/docs/mdemail/release-notes/version-5-7-7#quarantine-reports-not-in-config-export)

Quarantine report configuration was missing from exported configuration.

### [SMTP profile empty after saving rule](/docs/mdemail/release-notes/version-5-7-7#smtp-profile-empty-after-saving-rule)

After a security rule was saved and the page refreshed, the SMTP profile value was not visible. It instantly became visible again when the SMTP profile dropdown was clicked.

## [Updated](/docs/mdemail/release-notes/version-5-7-7#updated)

### [OpenSSL](/docs/mdemail/release-notes/version-5-7-7#openssl)

OpenSSL was updated to 3.0.16.
