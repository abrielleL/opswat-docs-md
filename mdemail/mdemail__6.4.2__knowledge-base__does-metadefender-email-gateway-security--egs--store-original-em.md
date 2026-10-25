<!-- source: https://www.opswat.com/docs/mdemail/6.4.2/knowledge-base/does-metadefender-email-gateway-security--egs--store-original-em -->

# Does MetaDefender Email Gateway Security (EGS) Store Original Email?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Email Gateway Security releases deployed on Windows systems.

**MetaDefender Email Gateway Security (EGS) stores the original email in the following cases only:**

- **The email fails to process or deliver; or**
- **Is blocked or sanitized, and quarantined.**

Note:

EGS quarantines original emails **only if** quarantining is enabled in the Security Rule for blocked or sanitized emails.

Quarantining of blocked or sanitized emails is enabled by default.

For configuration details, see [Quarantine Configuration](https://www.opswat.com/docs/mdemail/configuration/quarantine-configuration#internal-quarantine-configuration).

If an email is allowed and successfully forwarded to the SMTP server, it **may not be stored** in EGS and therefore it may not be possible to be downloaded. For more information on how EGS handles failed and forbidden emails, see the documentation [here](https://www.opswat.com/docs/mdemail/operating/email-history#failed-and-forbidden-emails).

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
