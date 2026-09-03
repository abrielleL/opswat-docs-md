<!-- source: https://www.opswat.com/docs/mdss/configuration/syslog-udp-external-logger7z4 -->

# Syslog TCP External Logger

Currently we support Syslog (TCP) using **only** the **RFC 5424** Output format as external logger configuration.

In order to visualize MetaDefender Storage Security audit logs in a centralized dashboard, integration with a Syslog (TCP) server is possible.

For adding a new Syslog configuration, you will need to enter the following details on the **Add External Logger window:**

- Server address - Ipv4, Ipv6 and Host Name formats are supported
- Port
- Syslog Facility
- Output format - RFC5424 format is supported

The Syslog TCP integration also supports TLS certificates. MDSS might request CA certificates for the Syslog server.

Info

Up to 5 different external loggers configurations of each type are supported.

Syslog message format

We support format **RFC5424**. You can find more details about this format [here**.**](https://datatracker.ietf.org/doc/html/rfc5424)

log format exampleCopy<PRI>VERSION TIMESTAMP HOSTNAME APP-NAME PROCID MSGID STRUCTURED-DATA MSG

| Prefix Field (click for more info) | Description |
| --- | --- |
| [PRI](https://datatracker.ietf.org/doc/html/rfc5424#section-6.2.1) | Priority value |
| [VERSION](https://datatracker.ietf.org/doc/html/rfc5424#section-6.2.2) | The version of the syslog protocol specification |
| [TIMESTAMP](https://datatracker.ietf.org/doc/html/rfc5424#section-6.2.3) | A formalized timestamp |
| [HOSTNAME](https://datatracker.ietf.org/doc/html/rfc5424#section-6.2.4) | The machine that originally sent the syslog message |
| [APP-NAME](https://datatracker.ietf.org/doc/html/rfc5424#section-6.2.5) | The device or application that originated the message |
| [PROCID](https://datatracker.ietf.org/doc/html/rfc5424#section-6.2.6) | Process name or ID associated with a syslog system |
| [MSGID](https://datatracker.ietf.org/doc/html/rfc5424#section-6.2.7) | Type of the message |
| [STRUCTURED-DATA](https://datatracker.ietf.org/doc/html/rfc5424#section-6.3) | A mechanism to express information in an easily parsable and interpretable data format |
| [MSG](https://datatracker.ietf.org/doc/html/rfc5424#section-6.4) | Free-form message that provides information about the event |

Log exampleCopy<110>1 2024-03-26T12:27:58.276724+02:00 LP10-D8569 MetaDefenderStorageSecurity 36800 - [meta UserName="jdavis" UserId="e69e8c2d-4dcc-4489-8f40-0df84199de52" EventTimestamp="03/26/2024 10:27:58" Category="3" LogType="600"] John Davis (jdavis) logged in.
