<!-- source: https://www.opswat.com/docs/mdemail/6.4.1/configuration/quarantine-configuration -->

# Quarantine configuration

## [Quarantine modes](/docs/mdemail/6.4.1/configuration/quarantine-configuration#quarantine-modes)

MetaDefender Email Gateway Security supports two quarantine modes for each of blocked, and allowed-and-sanitized emails independently, in an exclusive fashion (there is an exclusive or relation between the two: either this, or that):

1. Internal
2. External

By default MetaDefender Email Gateway Security uses the internal quarantine mode for both blocked and allowed-and-sanitized emails.

## [Internal quarantine configuration](/docs/mdemail/6.4.1/configuration/quarantine-configuration#internal-quarantine-configuration)

## [Blocked emails](/docs/mdemail/6.4.1/configuration/quarantine-configuration#blocked-emails)

Enable **Security Rules >*rule*/ ADVANCED THREAT PREVENTION / Quarantine original email** to send the original copy of blocked emails to the quarantine.

For details see [Configuration/Policy](/docs/mdemail/6.4.1/configuration/policy).

## [Disarmed and reconstructed emails](/docs/mdemail/6.4.1/configuration/quarantine-configuration#disarmed-and-reconstructed-emails)

Enable **Security Rules >*rule*/ ZERO-DAY MALWARE PREVENTION / Quarantine original email** to send the original copy of disarmed and reconstructed emails to the quarantine.

For details see [Configuration/Policy](/docs/mdemail/6.4.1/configuration/policy).

## [Quarantine reports](/docs/mdemail/6.4.1/configuration/quarantine-configuration#quarantine-reports)

Quarantine reports configuration can be done under **Settings > Alerts & Reports / Quarantine Reports**.

For details see [Configuration/Alert, notification and quarantine report emails](/docs/mdemail/6.4.1/configuration/alert--notification-and-quarantine-report-emails).

## [Cleanup](/docs/mdemail/6.4.1/configuration/quarantine-configuration#cleanup)

Automated quarantine cleanup can be configured under **Settings > Data Retention / Quarantine cleanup schedule**.

Pinned items

Entries pinned in the quarantine won’t be removed by cleanup. For details see [Operating/Quarantine](/docs/mdemail/6.4.1/operating/quarantine).

## [External quarantine](/docs/mdemail/6.4.1/configuration/quarantine-configuration#external-quarantine)

MetaDefender Email Gateway Security does not provide access to quarantined files for each email users other than access to administrator for all the quarantined emails. If your email server (either hosted or on-site mail server) has quarantine management capability for each user, it is recommended to quarantine email on your email server. By default, MetaDefender Email Gateway Security will quarantine emails in its own quarantine but you can change this behavior.

Changing quarantine mode will allow you to quarantine emails –that are detected as blocked or allowed-and-sanitized by MetaDefender Email Gateway Security– on a different email server.

Details

When external_quarantine_block is set to 1 the original copy of any blocked emails will be delivered with the X-Metadefender-To-Quarantine header added. When external_quarantine_sanitize is set to 1 the original copy of any allowed-and-sanitized emails will be delivered with the X-Metadefender-To-Quarantine header added.

By default MetaDefender Email Gateway Security uses the internal quarantine mode for both blocked and allowed-and-sanitized emails (neither the value external_quarantine_block nor the external_quarantine_sanitize exist under the registry key HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metadefender Email Security; see the *Setup* section).

### [External quarantine summary](/docs/mdemail/6.4.1/configuration/quarantine-configuration#external-quarantine-summary)

|  | Key | Value |
| --- | --- | --- |
| **Registry key name** | HKEY_LOCAL___MACHINE\SOFTWARE\OPSWAT\Metadefender Email Security | N/A |
| **Registry value name (blocked emails)** | external_quarantine_block | 1 |
| **Registry value name (allowed-and-sanitized emails)** | external_quarantine_sanitize | 1 |
| **Email header** | X-Metadefender-To-Quarantine | True |

### [External quarantining design](/docs/mdemail/6.4.1/configuration/quarantine-configuration#external-quarantining-design)

The external quarantine support is designed in the following way:

1. A header is appended to the original (potentially harmful) email,
2. The (potentially harmful) email gets delivered to the original recipient,
3. The receiving email server is configured to quarantine emails that contain this header.

| **Header key** | **Header value** |
| --- | --- |
| X-Metadefender-To-Quarantine | True |

### [Configuration](/docs/mdemail/6.4.1/configuration/quarantine-configuration#configuration)

#### [Prerequisites](/docs/mdemail/6.4.1/configuration/quarantine-configuration#prerequisites)

1. Quarantine must be enabled for blocked and/or allowed-and-sanitized emails (see the section *Internal quarantine configuration*) for emails to be quarantined at all

#### [Setup](/docs/mdemail/6.4.1/configuration/quarantine-configuration#setup)

1. Stop MetaDefender Email Gateway Security service

> net stop mdemailsecurity

2. Enable or disable external quarantine support for blocked emails:

   1. Enable external quarantine (and disable internal quarantine) support for blocked emails by setting the value external_quarantine_block under the registry key HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metadefender Email Security (DWORD) to 1

> reg add "HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metadefender Email Security" /v external_quarantine_block /t REG_DWORD /d 1

2. Disable external quarantine (and enable internal quarantine) support for blocked emails by deleting the value external_quarantine_block under the registry key HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metadefender Email Security

> reg delete "HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metadefender Email Security" /v external_quarantine_block

3. Enable or disable external quarantine support for allowed-and-sanitized emails:

   1. Enable external quarantine (and disable internal quarantine) support for allowed-and-sanitized emails by setting the value external_quarantine_sanitized under the registry key HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metadefender Email Security (DWORD) to 1

> reg add "HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metadefender Email Security" /v external_quarantine_sanitize /t REG_DWORD /d 1

2. Disable external quarantine (and enable internal quarantine) support for allowed-and-sanitized emails by deleting the value external_quarantine_sanitize under the registry key HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metadefender Email Security

> reg delete "HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metadefender Email Security" /v external_quarantine_sanitize

4. Start MetaDefender Email Gateway Security service

> net start mdemailsecurity
### [Example](/docs/mdemail/6.4.1/configuration/quarantine-configuration#example)

The following screenshot shows the source of an email delivered for external quarantining. Please note the position of the X-Metadefender-To-Quarantine header added to the email.
