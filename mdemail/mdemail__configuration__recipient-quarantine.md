<!-- source: https://www.opswat.com/docs/mdemail/configuration/recipient-quarantine -->

# Recipient Quarantine

## [Overview](/docs/mdemail/configuration/recipient-quarantine#overview)

Email recipients at the organization can be authorized to manage their own quarantined emails. This way the quarantine operation load can be lowered on administrators.

Email Gateway Security supports multiple recipient quarantine configuration sets so that different recipients or groups can have different permissions on the quarantined emails.

When multiple configurations apply

When multiple recipient quarantine configurations apply to a certain recipient, the permissions will be the union of the permissions of the applicable configurations.

Potential information disclosure

The following potentially sensitive information is disclosed to email recipients in the recipient quarantine that may reveal information about how and with what technologies emails are processed:

- Classifications: (for details see [Email classifications](/docs/mdemail/operating/email-classifications))
- Malware scan verdict (if there is malware in the email or not)
## [Configuration](/docs/mdemail/configuration/recipient-quarantine#configuration)

The following options need to be set

- **Name**: The distinctive and descriptive name of this recipient quarantine configuration.
- **Recipient email address filter**: a plain domain name or a regular expression to match recipient email addresses to who this configuration will apply.
- **Allowed recipient actions**: actions that the recipients of this recipient quarantine configuration will be authorized to perform. Mutiple actions can be selected.

### [Available actions](/docs/mdemail/configuration/recipient-quarantine#available-actions)

Currently the following actions are supported:

- Release request: authorize the recipient to mark emails for release from the Quarantine by Email Gateway Security administrators.
- Delete emails: authorize the recipient to delete emails from the Quarantine.

### [Service availabilitly](/docs/mdemail/configuration/recipient-quarantine#service-availabilitly)

The Recipient Quarantine service can be enabled configuring the `recipient_quarantine_port` registry option. For details see [Registry configuration](/docs/mdemail/configuration/registry-configuration).

### [User access](/docs/mdemail/configuration/recipient-quarantine#user-access)

Recipients whose email address has a configuration to the Recipient Quarantine can log in to the service using One-Time Passwords (OTP) sent to their email addresses.

### [One-Time Password email layout](/docs/mdemail/configuration/recipient-quarantine#one-time-password-email-layout)

The One-Time Password email layout and language can be configured the way as described in [Translation support](/docs/mdemail/configuration/translation-support).

The email template file name is `otp.xsl` .
