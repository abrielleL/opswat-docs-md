<!-- source: https://www.opswat.com/docs/mdemail/6.4.2/release-notes/version-6-1-0 -->

# Version 6.1.0

View as Markdown Ask ChatGPT about this page Ask Claude about this page

| Release date | Scope |
| --- | --- |
| June 3rd, 2025 | MetaDefender Email Gateway Security is a major release merging version 5 and version 6 of Email Gateway Security into a single version. The maintenance of Email Gateway Security version 5 continues in version 6. |

Migration from version 5

Migration of Email Gateway Security from version 5 to version 6 is supported with release 6.1.0:

1. A system on version 5 must be upgraded to the last version 5 release 5.7.7 first.
2. Then the system can be migrated to version 6, to release 6.1.0.

Customers migrating from version 5 please also read the [6.0.0 release notes](https://www.opswat.com/docs/mdemail/6.0.0/release-notes) for important changes.

## [New & improved](/docs/mdemail/6.4.2/release-notes/version-6-1-0#new--improved)

### [Migration from version 5](/docs/mdemail/6.4.2/release-notes/version-6-1-0#migration-from-version-5)

Migration from version 5 release 5.7.7 is now supported. For details see [Migration From MetaDefender Email Gateway Security v5](/docs/mdemail/6.4.2/installation/migration#from-metadefender-email-gateway-security-v5).

### [SMTP connection control](/docs/mdemail/6.4.2/release-notes/version-6-1-0#smtp-connection-control)

Email Gateway Security now supports limiting connections to its SMTP server to avoid accidental overload or prevent DoS attacks.

For details see [SMTP server connection control](/docs/mdemail/6.4.2/configuration/smtp-server-connection-control).

### [Rule wide header support](/docs/mdemail/6.4.2/release-notes/version-6-1-0#rule-wide-header-support)

It is now supported to add security rule specific custom headers to the email when the email is processed by a certain rule (irrelevant of the processing outcome). This way the header is always added if the email is processed by the security rule.

For details see [Rule actions](/docs/mdemail/6.4.2/configuration/policy#rule-actions).

### [Trusted senders for end users](/docs/mdemail/6.4.2/release-notes/version-6-1-0#trusted-senders-for-end-users)

Email recipients in the organization are now supported to add entries to the trusted senders list. Emails of trusted senders skip anti-spam and anti-phishing checks. Entries added by a certain recipient apply to that recipient only.

Recipients can add sender email addresses to the trusted senders using notification or quarantine report actions. For details see [Supported functions](/docs/mdemail/6.4.2/operating/quarantine-reports#supported-functions).

For details about the trusted senders see [Trusted senders](/docs/mdemail/6.4.2/configuration/trustedsenders).

### [Possible open relay detection](/docs/mdemail/6.4.2/release-notes/version-6-1-0#possible-open-relay-detection)

Email Gateway Security displays warnings for Security Rules that expose the system to possible [open relay](https://en.wikipedia.org/wiki/Open_mail_relay).

For details see [Open relay](/docs/mdemail/6.4.2/configuration/policy#open-relay).

## [Changed](/docs/mdemail/6.4.2/release-notes/version-6-1-0#changed)

### [File logging is on by default](/docs/mdemail/6.4.2/release-notes/version-6-1-0#file-logging-is-on-by-default)

For new installations file logging is enabled now on the `info` level by default. Rotation of the logfiles is also turned on by default.

For existing installations the existing settings are kept.

For details see the `logfile`, `loglevel` and `log_rotation` entries in [Logging registry configuration](/docs/mdemail/6.4.2/configuration/registry-configuration#hkey_local_machinesoftwareopswatmetadefender-email-securitylogger).

## [Fixed](/docs/mdemail/6.4.2/release-notes/version-6-1-0#fixed)

### [Workflows in Central Management](https://www.opswat.com/docs/mdemail/5.7.6/release-notes#workflows-didnt-load-in-central-management)

In Central Management version 7, MetaDefender Core *Workflows* did not load for Email Gateway Security release 6.0.0 *Server profiles*.

## [Updated](https://www.opswat.com/docs/mdemail/release-notes/version-5-7-7#updated)

### [OpenSSL](https://www.opswat.com/docs/mdemail/release-notes/version-5-7-7#openssl)

OpenSSL was updated to 3.0.16.
