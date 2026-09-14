<!-- source: https://www.opswat.com/docs/mdss/4.4.2/knowledge-base/how-to-configure-and-use-syslog-and-serilog-sinks -->

# How to Configure and Use Syslog and Serilog Sinks?

## [Syslog Configuration](/docs/mdss/4.4.2/knowledge-base/how-to-configure-and-use-syslog-and-serilog-sinks#syslog-configuration)

### [Recommended Tools:](/docs/mdss/4.4.2/knowledge-base/how-to-configure-and-use-syslog-and-serilog-sinks#recommended-tools)

- Visual Syslog Server (recommended)
- Syslog Watcher Manager (Note: Has a limit of 5000 messages/hour)

### [Configuration Steps:](/docs/mdss/4.4.2/knowledge-base/how-to-configure-and-use-syslog-and-serilog-sinks#configuration-steps)

Currently, we support Syslog (UDP) using the RFC5424 Output format for external logger configuration.

To visualize MetaDefender Storage Security audit logs centrally, integrate a Syslog (UDP) server using these details:

- Server address: IPv4, IPv6, and Host Name formats supported.
- Port: Specified Syslog server port.
- Syslog Facility: As per configuration needs.
- Output format: RFC5424.

You can add up to 5 external logger configurations of each type.

### [Syslog Message Format](/docs/mdss/4.4.2/knowledge-base/how-to-configure-and-use-syslog-and-serilog-sinks#syslog-message-format)

RFC5424 message format is supported:

<PRI>VERSION TIMESTAMP HOSTNAME APP-NAME PROCID MSGID STRUCTURED-DATA MSG

- PRI: Priority value
- VERSION: Syslog protocol specification version
- TIMESTAMP: Formalized timestamp
- HOSTNAME: Sending machine
- APP-NAME: Application or device originating message
- PROCID: Process name or ID
- MSGID: Message type
- STRUCTURED-DATA: Parsable data format
- MSG: Informative free-form message

### [Example Syslog Message](/docs/mdss/4.4.2/knowledge-base/how-to-configure-and-use-syslog-and-serilog-sinks#example-syslog-message)

ExampleCopy<110>1 2024-03-26T12:27:58.276724+02:00 LP10-D8569 MetaDefenderStorageSecurity 36800 - [meta UserName="jdavis" UserId="e69e8c2d-4dcc-4489-8f40-0df84199de52" EventTimestamp="03/26/2024 10:27:58" Category="3" LogType="600"] John Davis (jdavis) logged in.
## [Serilog Sinks](/docs/mdss/4.4.2/knowledge-base/how-to-configure-and-use-syslog-and-serilog-sinks#serilog-sinks)

### [What is Serilog?](/docs/mdss/4.4.2/knowledge-base/how-to-configure-and-use-syslog-and-serilog-sinks#what-is-serilog)

Serilog is a structured logging library for .NET applications, which allows logging to various destinations called sinks, including Syslog, files, HTTP endpoints, and console.

### [Commonly Used Serilog Sinks and Configurations:](/docs/mdss/4.4.2/knowledge-base/how-to-configure-and-use-syslog-and-serilog-sinks#commonly-used-serilog-sinks-and-configurations)

1. Serilog.Sinks.Syslog

Logs events to remote syslog servers via UDP or TCP, supporting RFC3164 and RFC5424 formats.

EventCopy"WriteTo": [
{
"Name": "TcpSyslog",
"Args": {
"host": "<ip_host>",
"port": 514,
"appName": "<your_app_name>",
"format": "RFC5424",
"facility": "<facility_name>",
"outputTemplate": "[{Timestamp:u}] [{Level}] {SourceContext}: {Message:lj}{NewLine}{Exception}"
}
}
]

2. Serilog.Sinks.Http

Sends log events via HTTP/S to remote endpoints.

EventCopy"WriteTo": [
{
"Name": "Http",
"Args": {
"requestUri": "<your_request_uri>",
"queueLimitBytes": null
}
}
]

3. Serilog.Sinks.Console

Writes log events to the console.

EventCopy"WriteTo": [
{
"Name": "Console",
"Args": {
"outputTemplate": "[{Timestamp:u}] [{Level}] {Namespace}: {Message:lj}{NewLine}{Exception}"
}
}
]

4. Serilog.Sinks.File

Writes logs to a file.

EventCopy"WriteTo": [
{
"Name": "File",
"Args": {
"buffered": false,
"fileSizeLimitBytes": 500000000,
"outputTemplate": "[{Timestamp:u}] [{Level}] {Namespace}: {Message:lj}{NewLine}{Exception}",
"path": "logs/log.txt",
"retainedFileCountLimit": "10",
"rollingInterval": "Day",
"rollOnFileSizeLimit": true
}
}
]
## [Testing & Validation:](/docs/mdss/4.4.2/knowledge-base/how-to-configure-and-use-syslog-and-serilog-sinks#testing--validation)

Use tools like Visual Syslog Server or test HTTP endpoints to validate your logging configurations and ensure logs are captured correctly.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
