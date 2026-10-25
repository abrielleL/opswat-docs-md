<!-- source: https://www.opswat.com/docs/mdemail/6.4.2/release-notes/version-6-2-0 -->

# Version 6.2.0

View as Markdown Ask ChatGPT about this page Ask Claude about this page

| Release date | Scope |
| --- | --- |
| 17th November, 2025 | This release provisions enforceable **quarantine areas**: separated parts of the *Quarantine* that administrators can permit less privileged users to supervise.  Support has been added for **SMTP oAuth** to deal with Microsoft's [retirement of SMTP AUTH in Exchange Online](https://techcommunity.microsoft.com/blog/exchange/exchange-online-to-retire-basic-auth-for-client-submission-smtp-auth/4114750). The current cutover date is April 30th 2026. |

## [New & improved](/docs/mdemail/6.4.2/release-notes/version-6-2-0#new--improved)

### [Quarantine areas](/docs/mdemail/6.4.2/release-notes/version-6-2-0#quarantine-areas)

Quarantine areas are separated parts of the *Quarantine* that administrators can permit less privileged users to supervise. Quarantine areas are built on top of the long existing concept of [saving filters](https://www.opswat.com/docs/mdemail/operating/quarantine#saving-filters).

For details see [Quarantine areas](/docs/mdemail/6.4.2/operating/quarantine#quarantine-areas).

### [Forward blocked emails](/docs/mdemail/6.4.2/release-notes/version-6-2-0#forward-blocked-emails)

As a new action, it is now supported to forward emails (e.g. to SoC for further analysis) that were blocked by MetaDefender Core.

For details see the *Scan* subsection under [Security policy](/docs/mdemail/6.4.2/configuration/policy#security-policy).

### [SMTP oAuth support](/docs/mdemail/6.4.2/release-notes/version-6-2-0#smtp-oauth-support)

With this release, Email Gateway Security supports SMTP OAuth to deal with Microsoft's [retirement of SMTP AUTH in Exchange Online](https://techcommunity.microsoft.com/blog/exchange/exchange-online-to-retire-basic-auth-for-client-submission-smtp-auth/4114750).

For details see [SMTP oAuth authentication](/docs/mdemail/6.4.2/configuration/server-profiles#smtp-oauth-authentication).

### [Optional SPF on From](/docs/mdemail/6.4.2/release-notes/version-6-2-0#optional-spf-on-from)

Email Gateway Security extends SPF checking SPF records not only by the `MAIL FROM` domain, but by the email's `From` header domain, too. This strict check can cause problems, so checking `From` domain for SPF has been made optional.

For details see the *SPF lookup* subsection in the *Anti-phishing specific settings* section in [Security policy](/docs/mdemail/6.4.2/configuration/policy#security-policy).

### [DKIM with sender domain](/docs/mdemail/6.4.2/release-notes/version-6-2-0#dkim-with-sender-domain)

It is supported to automatically take the domain part from the SMTP sender email address (`MAIL FROM`) and use it as the *signer domain* in DKIM or ARC signatures.

This feature may be useful for organizations with multiple sender domains.

For details see the *DKIM signing* subsection in [Direction](/docs/mdemail/6.4.2/configuration/policy#direction).

### [CEF in milliseconds](/docs/mdemail/6.4.2/release-notes/version-6-2-0#cef-in-milliseconds)

When CEF logging is enabled, it is now supported to have the log timestamps in milliseconds.

For details see the `cef_ms_ts` entry under [HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metadefender Email Security\logger](/docs/mdemail/6.4.2/configuration/registry-configuration#hkey_local_machinesoftwareopswatmetadefender-email-securitylogger).

### [SOC log improvements](/docs/mdemail/6.4.2/release-notes/version-6-2-0#soc-log-improvements)

The `soc` level has been modified to contain the MetaDefender Core side `data_id` and `scan_result` for each component.

### [Syslog over TLS](/docs/mdemail/6.4.2/release-notes/version-6-2-0#syslog-over-tls)

This release implements syslog over TLS.

For details see [HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metadefender Email Security\logger](/docs/mdemail/6.4.2/configuration/registry-configuration#hkey_local_machinesoftwareopswatmetadefender-email-securitylogger).

## [Changed](/docs/mdemail/6.4.2/release-notes/version-6-2-0#changed)

### [SOC log changes](/docs/mdemail/6.4.2/release-notes/version-6-2-0#soc-log-changes)

For password protected email rescans the `email.scan` log entry identifier was changed to `email.rescan`.

In the `email.scan` log entry the `scan_result_urls` field (that contained `display_name`*,* `is_hash_result` and `url`) was renamed to `scan_result_details`. This new entry contains the `data_id` and `scan_result`.

In the `email.scan` log entry the `batch_id` property was added that contains the MetaDefender Core side scan batch ID.

For details see [SOC log level](/docs/mdemail/6.4.2/operating/soc-log-level).

### [Single quote escaping](/docs/mdemail/6.4.2/release-notes/version-6-2-0#single-quote-escaping)

In SOC level logs, single quote `'` characters are escaped by doubling each single qoute character (e.g. `'` `''` , `''`  `''''` , etc.).

For details see [SOC log level](/docs/mdemail/6.4.2/operating/soc-log-level).

## [Fixed](/docs/mdemail/6.4.2/release-notes/version-6-2-0#fixed)

### [Database port over 32767](/docs/mdemail/6.4.2/release-notes/version-6-2-0#database-port-over-32767)

The previous releases of EGS version 6 did not accept port numbers higher than 32767 as a database port.

### [Mishandling of code pages](/docs/mdemail/6.4.2/release-notes/version-6-2-0#mishandling-of-code-pages)

Emails encoded with certain code pages (e.g. Windos-1250) were not correctly handled in certain cases (e.g. Eastern-European languages).
