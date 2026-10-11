<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/configuration/audit-settings -->

# Audit Settings

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

### Retention Settings

The "Audit history retention" field allows you to configure a retention period for general audit and file audit events, ranging from 10 to 1100 days. Any event older than the specified period will be automatically removed.

### Extended File Audit

After enabling this feature the file related audit logs will contain additional details, like file tags, file path, city, country (in MetaDefender Managed File Transfer™).

### Syslog Integration Settings

Enabling Syslog integration will instruct Managed File Transfer to transmit any audit event to the configured Syslog server.

Info

Managed File Transfer supports the UDP, TCP, and TCPS (TCP over TLS) protocols. When using UDP, Managed File Transfer cannot validate the connection to the Syslog server; however, a test message will be sent upon successful configuration.

Syslog integration supports establishing multiple Syslog servers, ensuring audit logs are replicated and transmitted to each designated server. Each server's port or address must be unique.

When a server uses the TCPS protocol, enable **Allow self-signed certificate** to accept self-signed certificates from Syslog servers that rely on TLS connections.

The following settings are available for configuration:

| Setting | Description | Default value |
| --- | --- | --- |
| Allow self-signed certificate | Confirm whether self-signed certificates are accepted for Syslog servers using TLS connections | Disabled |
| Facility | The type associated with Managed File Transfer events | User Level Messages |
| Log level | Determines which messages sent to the Syslog server, filtering out any messages less important than the one selected | Information |
| Server address | The address of the server where the Syslog is located | 0.0.0.0 |
| Server port | The open port on the Syslog server for accepting messages | 514 |
| Protocol | The network protocol used to transmit audit events to the Syslog server. Available options are UDP, TCP, and TCPS (TCP over TLS) | UDP |
| Language | The language to use for logging messages | English |
| Timezone | The time zone recorded at the time the log is sent | (UTC) Coordinated Universal Time |
| Output format | Supported message formats, including: Standard and Common Event Format (CEF) | Standard |

## CEF Message Format

**Base Format:** Date Host CEF:Version|Device Vendor|Device Product|Device Version|Device Event Class ID|Name|Severity|[Extension]

**Example**: 2020-01-16T08:45:47Z LE10-L3174 CEF:0|OPSWAT|MetaDefender MFT|1.0.0.0|1|Logon|6|requestClientApplication=127.0.0.1 deviceAction=Logon outcome=Success msg=Username logged on.
