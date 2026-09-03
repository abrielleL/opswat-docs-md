<!-- source: https://www.opswat.com/docs/mdemail/configuration/quarantine-reports -->

# Quarantine reports

## [Overview](/docs/mdemail/configuration/quarantine-reports#overview)

SMTP server profile

Quarantine reports will use the SMTP server profile configured under **Settings > Alerts & Reports / SMTP server profile** to send the report email.

Not available on secondary instances

**Settings > Quarantine reports** (and the legacy **Settings > Alerts & Reports / Quarantine Reports**) are not available on a secondary instance of a scalable deployment. The quarantine reports must be configured on the primary instance.

For details see [Scalable deployment operation](/docs/mdemail/operating/scalable-deployment-operation).

### [Reporting strategy](/docs/mdemail/configuration/quarantine-reports#reporting-strategy)

Quarantine reports follow a differential reporting strategy. It means that a quarantine report contains only the newly quarantined items since the last quarantine report.

First quarantine report

If the actual quarantine report is the first one, then it will contain all quarantined items.

As a consequence, the first quarantine report may be huge containing a huge number of quarantined items.

## [Report types](/docs/mdemail/configuration/quarantine-reports#report-types)

Setting report type

Setting the report type is only possible at the time of creating the report configuration. This field is disabled after saving the report configuration for the first time and is not allowed to be changed later on.

For details see [Operating/Quarantine reports](/docs/mdemail/operating/quarantine-reports).

### [Administrator reports](/docs/mdemail/configuration/quarantine-reports#administrator-reports)

The intended audience of administrator type quarantine reports is the administrators and operators of Email Gateway Security.

These reports include quarantined emails to any recipients within or outside the organization (to whomsoever emails there are in the quarantine).

Privacy risk

Quarantine reports may contain sensitive contents (subject, sender) from emails that can be read by others than the intended recipients of the email.

Recipients of administrator reports can perform any of the supported operations on the emails in the quarantine report.

Risks of malware outbreak

Certain actions may release potentially malicious emails from the quarantine.

### [User reports](/docs/mdemail/configuration/quarantine-reports#user-reports)

The intended audience of user type quarantine reports is the original recipients of emails quarantined by Email Gateway Security.

These reports include quarantined emails to the recipient of the quarantine report only.

### [Main configuration differences](/docs/mdemail/configuration/quarantine-reports#main-configuration-differences)

| **Property** | **Administrator report** | **User report** |
| --- | --- | --- |
| Report recipients | Can be set | Can not be set (set to the recipient of the quarantine item) |
| Report contents | All quarantined items since last report | Only quarantined items that were addressed to the recipient of the report |
| Available functions | All functions are available | Available functions can be configured |
| Affected recipients by function | All recipients | Only the recipient of the report |

### [User permissions](/docs/mdemail/configuration/quarantine-reports#user-permissions)

Under user permissions it can be set what quarantine actions for the recipient of the report will be available in the quarantine actions page.

For details see [Operating/Quarantine reports](/docs/mdemail/operating/quarantine-reports).

Risks of malware outbreak

Recipients of the quarantine report can release potentially malicious emails from the quarantine when the *Allow to deliver original email* permission is set.

Administrator report permissions

Administrator type quarantine report grants all permissions to recipients.
