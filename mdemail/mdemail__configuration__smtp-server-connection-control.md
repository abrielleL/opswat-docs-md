<!-- source: https://www.opswat.com/docs/mdemail/configuration/smtp-server-connection-control -->

# SMTP server connection control

## [Overview](/docs/mdemail/configuration/smtp-server-connection-control#overview)

In order to protect Email Gateway Security from accidental SMTP overload or DoS attacks, throttling and tarpitting options are supported for the following *use-cases*:

- Connecting SMTP client IP address

  - use-case: `connection`
  - evaluated at the time of SMTP `HELO` or `EHLO`
- SMTP sender address

  - use-case: `sender`
  - evaluated at the time of SMTP `MAIL FROM`
- SMTP recipient address

  - use-case: `recipient`
  - evaluated at the time of each SMTP `RCPT TO`

Connection control applied by recipients

For the SMTP recipient address throttling, the settings apply by recipient.

For example, when an email has multiple recipients and the limit within the timeframe is reached for one recipient address, but not for the others; the penalty defined by the `throttling_recipient_behaviour` applies to the address only that reached the limit.

For details see the Examples below.

- Potential directory harvest attempts (not hosted email addresses)

  - use-case: `directory`
  - evaluated at the time of each SMTP `RCPT TO`

Warning

The `recipient` use case has an impact on the `directory` use case in terms of whichever has more strict `throttling_<use-case>_limit` and `throttling_<use-case>_interval_s` will take effect on an email address that is not hosted by the system.

For details see the Examples below.

## [Configuration options](/docs/mdemail/configuration/smtp-server-connection-control#configuration-options)

For each above use-case the following parameters are supported that must be specified under `HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metadefender Email Security\smtp_config`:

| Parameter | Type | Description |
| --- | --- | --- |
| throttling_<use-case>_behaviour | string | Accepted values are:   - `tarpit` or - `refuse`.   When it is set to `tarpit`, then the SMTP response is delayed by the time set by the `throttling_<use-case>_tarpit_s` option once the limit set by `throttling_<use-case>_limit` is reached. This way the client's connection attempts can be slowed down.  When it is set to refuse, then a 451 SMTP status is sent when the limit set by `throttling_<use-case>_limit` is reached. The SMTP status and message is:  `451 4.7.0 Error: Throttling policy enforced, please try again after <throttling_<use-case>_tarpit_s>` .  The appropriate penalty (`tarpit` or `reject`) is applied at the time of the response to the appropriate SMTP command (`HELO`/`EHLO`, `MAIL FROM` or `RCPT TO`). For details see the Examples below. |
| throttling_<use-case>_limit | dword | The number of connections allowed within the timeframe defined by `throttling_<use-case>_interval_s` without applying the penalty defined by `throttling_<use-case>_behaviour` . The connections must be evenly distributed within the timeframe. This means, for example, that when `throttling_<use-case>_limit` = 10 and `throttling_<use-case>_interval_s` = 1 then a connection within the 1 second window must not come earlier than 100ms of the previous connection. |
| throttling_<use-case>_burst_limit | dword | This option is to overcome the even distribution restriction described for `throttling_<use-case>_limit`. For example, when `throttling_<use-case>_limit` = 10 and `throttling_<use-case>_interval_s` = 1 and`throttling_<use-case>_burst_limit` = 5 then 5 connections are allowed even within 100ms in the 1 second window. The other 5 connections must not come earlier than 100ms of the previous connection. |
| throttling_<use-case>_ interval_s | dword | The timeframe in which `throttling_<use-case>_limit` is applied. |
| throttling_<use-case>_tarpit_s | dword | When `throttling_<use-case>_behaviour` is set to `tarpit`, then the SMTP response is delayed by the time set by the `throttling_<use-case>_tarpit_s` option once the limit set by `throttling_<use-case>_limit` is reached. |

### [Examples](/docs/mdemail/configuration/smtp-server-connection-control#examples)

#### [Throttling by the recipient](/docs/mdemail/configuration/smtp-server-connection-control#throttling-by-the-recipient)

When the following options are set:

throttling_recipient_behaviour refuse
throttling_recipient_limit 10
throttling_recipient_burst_limit 5
throttling_recipient_interval_s 30
throttling_recipient_tarpit_s 10

and an email arrives for two recipients: `joe@loc.al` and `admin@loc.al` and `joe@loc.al` has reached the throttling limit but `admin@loc.al` has not reached the limit yet, the following pseudo SMTP conversation will happen:

S: 220 SERVER v6.5.0.0 ESMTP ready
C: EHLO CLIENT
S: 250 OK
C: MAIL FROM: sender@remo.te
S: 250 OK
C: RCPT TO: joe@loc.al
S: 451 4.7.0 Error: Throttling policy enforced, please try again after 10
C: RCPT TO: admin@loc.al
S: 250 OK
...
#### [Directory harvest protection](/docs/mdemail/configuration/smtp-server-connection-control#directory-harvest-protection)

When the following options are set:

throttling_recipient_behaviour refuse
throttling_recipient_limit 5
throttling_recipient_interval_s 30
throttling_directory_behaviour refuse
throttling_directory_limit 10
throttling_directory_interval_s 30

and an email arrives to a non hosted email address, the email address **gets refused after 5 attempts** by the `recipient` use case and **not only after 10** attempts by the `directory` use case.
