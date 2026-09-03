<!-- source: https://www.opswat.com/docs/mdemail/6.4.1/release-notes/version-6-4-0 -->

# Version 6.4.0

| Version | 6.4.0 |
| --- | --- |
| Release date | 1st June, 2026 |
| Scope | Email recipients of the organization can now be authorized to manage their own quarantined emails through Email Gateway Security's new dedicated *Recipient Quarantine* portal. This way the quarantine related load can be lowered on administrators. |

## [New & improved](/docs/mdemail/6.4.1/release-notes/version-6-4-0#new--improved)

### [Recipient quarantine](/docs/mdemail/6.4.1/release-notes/version-6-4-0#recipient-quarantine)

Email recipients of the organization can now be authorized to manage their own quarantined emails through Email Gateway Security's new Recipient Quarantine functionality. This way the quarantine related tasks can cause less load to administrators.

Potential information disclosure

The following potentially sensitive information is disclosed to email recipients in the recipient quarantine that may reveal information about how and with what technologies emails are processed:

- Classifications: (for details see [Email classifications](/docs/mdemail/6.4.1/operating/email-classifications))
- Malware scan verdict (if there is malware in the email or not)

For details see [Registry configuration](/docs/mdemail/6.4.1/configuration/registry-configuration), [Recipient Quarantine configuration](/docs/mdemail/6.4.1/configuration/recipient-quarantine) and the Recipient Quarantine subpage of the [Email recipient guide](/docs/mdemail/6.4.1/operating/recipient-guide).

### [DLP hits in email preview](/docs/mdemail/6.4.1/release-notes/version-6-4-0#dlp-hits-in-email-preview)

The [Preview HTML & plain text body](https://www.opswat.com/docs/mdemail/release-notes/version-6-3-2#preview-html--plain-text-body) feature has been improved to highlight Proactive DLP hits in the text of the HTML or plain text email body.

This feature was also extended with a new view that can show the raw markup code of the HTML body so that hidden sensitive data in the HTML code can also be revealed.

For details see [Preview email body](/docs/mdemail/6.4.1/operating/quarantine#preview-email-body).

Sensitive data disclosure

This function obviously makes sensitive data visible to administrators. Act with due care when granting access to the Quarantine.

### [Scan email as a whole](/docs/mdemail/6.4.1/release-notes/version-6-4-0#scan-email-as-a-whole)

A new option in Email Gateway Security is available now for each Security Rule to send the email as a whole as an `.eml` file in raw MIME format to MetaDefender Core or MetaDefender Cloud for scanning.

The reason why this new option was introduced is that [MetaDefender Aether](https://www.opswat.com/products/metadefender/aether) can provide better scan accuracy when the email is sent to it as a whole.

For details see [Security policy](/docs/mdemail/6.4.1/configuration/policy#security-policy).

### [Block when unlicensed](/docs/mdemail/6.4.1/release-notes/version-6-4-0#block-when-unlicensed)

Email Gateway Security can now be configured to block and quarantine emails when recipients or the whole product is not licensed.

For details see [Licensing](/docs/mdemail/6.4.1/configuration/settings#licensing).

## [Fixed](/docs/mdemail/6.4.1/release-notes/version-6-4-0#fixed)

### [Startup failure after upgrade](/docs/mdemail/6.4.1/release-notes/version-6-4-0#startup-failure-after-upgrade)

When Email Gateway Security had certain types of [Server profiles](/docs/mdemail/6.4.1/configuration/server-profiles) with certain encrypted credentials, upgrade to release 6.2.0 or later ended up with the service fail to start.

### [Search by Message-ID fails](/docs/mdemail/6.4.1/release-notes/version-6-4-0#search-by-message-id-fails)

Email Gateway Security's [Search](/docs/mdemail/6.4.1/operating/email-history#search) function in the [Email History](/docs/mdemail/6.4.1/operating/email-history) and [Quarantine](/docs/mdemail/6.4.1/operating/quarantine) gave unexpected results when the search term contained certain special characters.

### [SAML integration to CyberArk](/docs/mdemail/6.4.1/release-notes/version-6-4-0#saml-integration-to-cyberark)

Previous releases of Email Gateway Security did supports array values ([SAML 2.0 - Section 2.7.3.1](https://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf)) for the `Groups` attribute, so the role mapping did not work for users belonging to multiple groups.

### [Emails rejected by Exchange](/docs/mdemail/6.4.1/release-notes/version-6-4-0#emails-rejected-by-exchange)

When EML was enabled in the MetaDefender Core workflow Compression section, emails with large `.eml` attachments got rejected by Exchange Server.

This release provides a workaround for this problem. For details see the `preserve_eml_content_type` option in [Registry configuration](/docs/mdemail/6.4.1/configuration/registry-configuration).
