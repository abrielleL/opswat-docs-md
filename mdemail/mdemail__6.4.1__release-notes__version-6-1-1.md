<!-- source: https://www.opswat.com/docs/mdemail/6.4.1/release-notes/version-6-1-1 -->

# Version 6.1.1

| Release date | Scope |
| --- | --- |
| 16th July, 2025 | Enhanced customization, more flexible email delivery, and fixes. |

## [New & improved](/docs/mdemail/6.4.1/release-notes/version-6-1-1#new--improved)

### [Enhanced Quarantine rescan page rebranding](/docs/mdemail/6.4.1/release-notes/version-6-1-1#enhanced-quarantine-rescan-page-rebranding)

As the first step of GUI based UI customization and rebranding support, Email Gateway Security now releases a GUI based tool to customize and rebrand the Quarantine rescan page.

For details see [User interface customization](/docs/mdemail/6.4.1/configuration/user-interface-customization).

### [Core workflows for each email component](/docs/mdemail/6.4.1/release-notes/version-6-1-1#core-workflows-for-each-email-component)

Email Gateway Security now supports separate MetaDefender Core workflows for each of email headers, email bodies and attachments. This way it is possible to use different Core workflow for email bodies and attachments.

MetaDefender Core

This capability requires [MetaDefender Core 5.12.0](https://www.opswat.com/docs/mdcore/v5.12.0/release-notes) or newer.

This is especially useful for example when different processing is needed for HTML email bodies and HTML email attachments.

For details see *Scan* section in [Security policy](/docs/mdemail/6.4.1/configuration/policy#security-policy).

### [Mirrored SMTP relay server delivery](/docs/mdemail/6.4.1/release-notes/version-6-1-1#mirrored-smtp-relay-server-delivery)

A new *Server profile type* has been introduced: `SMTP multi-delivery`. With this new profile it is possible to deliver an email to multiple SMTP servers (SMTP multi-delivery).

For details see [SMTP multi-delivery server profiles](/docs/mdemail/6.4.1/configuration/server-profiles#smtp-multi-delivery-server-profiles) and [SMTP relay](/docs/mdemail/6.4.1/configuration/policy#smtp-relay).

### [Rewrite email addresses in email headers](/docs/mdemail/6.4.1/release-notes/version-6-1-1#rewrite-email-addresses-in-email-headers)

As an enhancement to the [SMTP rewrite](https://www.opswat.com/docs/mdemail/release-notes/version-5-7-7#smtp-rewrite) feature introduced in Email Gateway Security release 5.7.7, it is now supported to rewrite the relevant email addresses in the email headers, too.

For details see the *SMTP sender or recipient rewriting* subsection in the *Advanced* section of the [Security policy](/docs/mdemail/6.4.1/configuration/policy#security-policy) settings.

### [Compact view in Email History and Quarantine](/docs/mdemail/6.4.1/release-notes/version-6-1-1#compact-view-in-email-history-and-quarantine)

Email Gateway Security now support a *Compact view* for **Audit > Email History**, **Quarantine** and **Audit > Refused Emails** lists.

The compact view shows less details of each email but can display more entries on the screen.

### [Authenticated Received Chain verification](/docs/mdemail/6.4.1/release-notes/version-6-1-1#authenticated-received-chain-verification)

Email Gateway Security now verifies ARC seals of emails and combines the result into the DKIM result.

## [Changed](/docs/mdemail/6.4.1/release-notes/version-6-1-1#changed)

To have a smooth user experience with the *Core workflows for each email component* feature, MetaDefender Core side *Workflow* selection was moved from *Server Profiles* to *Security Rules*.

Workflow per Security Rule

With this change each Security Rule can have a different Core side Workflow.

For details see the *Scan* section in [Security policy](/docs/mdemail/6.4.1/configuration/policy#security-policy).

## [Fixed](/docs/mdemail/6.4.1/release-notes/version-6-1-1#fixed)

### [SMTP server unavailable with #PKCS1 key](/docs/mdemail/6.4.1/release-notes/version-6-1-1#smtp-server-unavailable-with-pkcs1-key)

The SMTP server kept restarting when it was configured to *SMTP over TLS* with a [PKCS#1](https://datatracker.ietf.org/doc/html/rfc8017) private key. Now both PKCS#1 and [PKCS#8](https://datatracker.ietf.org/doc/html/rfc5208) private keys are supported.

### [Emails accepted when client disconnected](/docs/mdemail/6.4.1/release-notes/version-6-1-1#emails-accepted-when-client-disconnected)

Emails were accepted even before receiving the terminating `<CR><LF>.<CR><LF>` character sequence of the SMTP `DATA` command when the SMTP client disconnected.

## [Updated](/docs/mdemail/6.4.1/release-notes/version-6-1-1#updated)

### [Qt framework](/docs/mdemail/6.4.1/release-notes/version-6-1-1#qt-framework)

Qt application development framework is updated to 6.8.3.
