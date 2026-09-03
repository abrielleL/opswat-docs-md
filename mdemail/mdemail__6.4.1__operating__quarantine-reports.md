<!-- source: https://www.opswat.com/docs/mdemail/6.4.1/operating/quarantine-reports -->

# Quarantine reports

## [Overview](/docs/mdemail/6.4.1/operating/quarantine-reports#overview)

Quarantine reports are intended to lower the load on Email Gateway Security operations by delegating certain quarantine related tasks to the recipient of the quarantined item.

Example

Based on permissions, certain groups at an organization may be authorized to release the original copy of their quarantined email.

### [Workflow](/docs/mdemail/6.4.1/operating/quarantine-reports#workflow)

Quarantine reports work the following way:

1. At the configured time Email Gateway Security sends a report email to the configured recipients (administrator reports) or the recipient of the quarantined email (user reports). For details see [Configuration/Quarantine reports](/docs/mdemail/6.4.1/configuration/quarantine-reports).

2. Clicking the actions link takes the user to Email Gateway Security’s quarantine actions page.

3. Based on the report type and the permissions set in the report, different functions may be available in the quarantine actions page.

## [Supported functions](/docs/mdemail/6.4.1/operating/quarantine-reports#supported-functions)

Quarantine reports and the quarantine actions page currently support the following functions on quarantined emails:

- Full rescan email
- Anti-malware rescan email
- Delete quarantined email
- Deliver quarantined email
- Request release of quarantined email

### [Full rescan email](/docs/mdemail/6.4.1/operating/quarantine-reports#full-rescan-email)

This action initiates a full rescan (including anti-spam checks) of the email.

If the rescan result is allowed this time, then the email is processed and delivered according to the security rules applied to the email.

Rationale

The rationale of this action is to process the email with updated scan engines that may not block the contents any more.

### [Anti-malware rescan email](/docs/mdemail/6.4.1/operating/quarantine-reports#anti-malware-rescan-email)

This action initiates an anti-malware-only rescan (excluding anti-spam checks) of the email.

If the rescan result is allowed this time, then the email is processed and delivered according to the security rules applied to the email.

Rationale

This action is intended to help handling spam false positives. Administrators can authorize recipients to rescan spam emails using the *anti-malware rescan* action.

This way -if the email turns out to be non-malicious- recipients can deliver a secure, processed (with Multiscanning, CDR, etc.) copy of the spam email (opposed to the situation when they are authorized to simply deliver the original -potentially malicious- email from the quarantine using the *Deliver quarantined email* action).

### [Delete quarantined email](/docs/mdemail/6.4.1/operating/quarantine-reports#delete-quarantined-email)

This action deletes the email from the quarantine.

Automatic quarantine cleanup

Please note that Email Gateway Security can automatically clean-up the quarantine, so there is no need for manual cleanup of quarantined emails.

Automatic clean up of the quarantine can be configured under **Settings > Data retention / Quarantine cleanup schedule**.

### [Deliver quarantined email](/docs/mdemail/6.4.1/operating/quarantine-reports#deliver-quarantined-email)

Delivers the original, potentially malicious copy of the email from quarantine.

Risk of malicious content

The original copy delivered from the quarantine may include malicious contents.

Depending on the quarantine report type all original recipients (administrator reports) or only the report recipient (user reports) will receive the original copy.

For details see [Configuration/Quarantine reports](/docs/mdemail/6.4.1/configuration/quarantine-reports).

### [Request release of quarantined email](/docs/mdemail/6.4.1/operating/quarantine-reports#request-release-of-quarantined-email)

Adds the *Release Requested* classification to the quarantined email. An Administrator can afterwards review and decide to release the email to the recipient.

Quarantine Report with release requested emails

It is possible to create a quarantine report with all emails which end users have requested to release. To do this, create an Administrator Quarantine Report and select *Release Requested* as the included email classification.

### [Add to trusted senders](/docs/mdemail/6.4.1/operating/quarantine-reports#add-to-trusted-senders)

These functions add the sender of the quarantined email to the [Trusted senders](/docs/mdemail/6.4.1/configuration/trustedsenders).

#### [Add to trusted senders (user)](/docs/mdemail/6.4.1/operating/quarantine-reports#add-to-trusted-senders-user)

This function will add the sender of the quarantined email to the trusted senders list **for the recipient of the quarantine report only**.

#### [Add to trusted senders (global)](/docs/mdemail/6.4.1/operating/quarantine-reports#add-to-trusted-senders-global)

This function will add the sender of the quarantined email to the trusted senders list **for all recipients**.

Risk of trusting malicious senders

Giving permission to *Add to trusted senders (global)* to recipients increases the risk that malicious senders or spammers get added to the trusted senders.

## [Notes](/docs/mdemail/6.4.1/operating/quarantine-reports#notes)

Actions link expiry time

Link expiry time for *Actions* links in user type reports actions can be set in **General > General / Rescan link availability**.

Administrator reports links **do not expire**.

Risks of malware outbreak

Users can release potentially malicious emails from the quarantine using *Deliver quarantined email* action.

Action availability period

If the report allows a user action when at the time of sending the report, then the user can take the action until the link expires.

There is no way to recall an action until the *Actions* link expires.
