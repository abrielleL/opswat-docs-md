<!-- source: https://www.opswat.com/docs/filescan/3.1.1/configuration/cef-syslog-feedback -->

# CEF Syslog Feedback

The broker component can be configured to send a CEF syslog summary string to any endpoint via TCP or UDP.

The CEF syslog feedback is generated and sent to the configured endpoint when the main transform task and all its subtasks are in a final processing state.

To modify the syslog feedback configuration:

**Step #1 - Open** `/home/sandbox/sandbox/broker.cfg` **in a text editor**

**Step #2 - Add or modify the following properties (no need to overwrite default values):**

broker.cfgCopy##############################
# CEF Syslog Feedback settings
##############################
cefSyslogEnabled=false
cefSyslogHost=
cefSyslogPort=514
cefSyslogProtocol=tcp
cefSyslogTimeoutMs=10000
cefSyslogUseSSL=false
# Syslog header config
syslogHeaderPrivalFacility=16
syslogHeaderPrivalSeverity=6
syslogHeaderHost=

**Step #3 - Save the file and restart the** `sandbox` **service**

## [Property details](/docs/filescan/3.1.1/configuration/cef-syslog-feedback#property-details)

| Property Name | Default Value | Description |
| --- | --- | --- |
| cefSyslogEnabled | false | Main switch to enable / disable CEF syslog feedback |
| cefSyslogHost |  | Host name or IP address of the log server |
| cefSyslogPort | 514 | Port of the log server |
| cefSyslogProtocol | tcp | Connection protocol to use: tcp or udp |
| cefSyslogTimeoutMs | 10 seconds | Connection timeout used for TCP sockets |
| cefSyslogUseSSL | false | Switch to enable / disable SSL verification for TCP sockets |
| syslogHeaderPrivalFacility | 16 | Facility value used in the syslog header |
| syslogHeaderPrivalSeverity | 6 | Severity value used in the syslog header |
| syslogHeaderHost |  | The hostname value is used in the syslog header. If not configured, the application will try to detect and use the local hostname. |

syslogHeaderHost

Since the broker is running in a dockerized environment, the detected hostname might not be useful, therefore it is possible to set a user defined hostname which will be used in the syslog header.

## [Syslog Message Format in Sandbox](/docs/filescan/3.1.1/configuration/cef-syslog-feedback#syslog-message-format-in-sandbox)

Sandbox uses the standardized Syslog message format, following **Syslog Protocol Version 1**.

#### [**Base Format**](/docs/filescan/3.1.1/configuration/cef-syslog-feedback#base-format)

`Date Host CEF:Version|Device Vendor|Device Product|Device Version|Device Event Class ID|Name|Severity|[Extension]`

This format complies with the **Common Event Format (CEF)** standard, ensuring compatibility and reliable parsing by SIEM tools and other log management systems.

#### [**References to Syslog Standards**](/docs/filescan/3.1.1/configuration/cef-syslog-feedback#references-to-syslog-standards)

For a deeper understanding of the Syslog message format and transport methods, refer to the following RFCs:

- **Syslog Protocol (RFC 5424)** – Defines the overall message structure 📄 [RFC 5424 - Syslog Protocol](https://www.rfc-editor.org/pdfrfc/rfc5424.txt.pdf)
- **Syslog over TLS (RFC 5425)** – For secure transmission over TLS [📄](%F0%9F%93%84) [RFC 5425 - Syslog over TLS](https://www.rfc-editor.org/pdfrfc/rfc5425.txt.pdf)
- **Syslog over UDP (RFC 5426)** – For lightweight, best-effort delivery 📄 [RFC 5426 - Syslog over UDP](https://www.rfc-editor.org/pdfrfc/rfc5426.txt.pdf)

## [Example CEF syslog message:](/docs/filescan/3.1.1/configuration/cef-syslog-feedback#example-cef-syslog-message)

<134>1 2024-09-05T08:04:24.410Z hostname - - - - CEF:0|OPSWAT Inc.|broker|1.1.0-53dd79f|transform-file|OPSWAT Sandbox scan result|6|cs1Label=Task ID cs1=6c77d761-6958-4e2a-aa7c-88de393c4cf1 cs2Label=SHA256 cs2=6c297c89d32d7fb5c6d10b1da2612c9557a5126715c4a78690d5d8067488f5f2 cs3Label=Media Type cs3=application/x-ms-installer cs4Label=Date cs4=2024-09-05 10:17+0200249 cs5Label=All Tags cs5=expand,fingerprint,lolbin,msi cs6Label=All Signal Group IDs cs6=H061,S007,R007,H071,PE000,SIGG038,I001
## [Scan verdict and CEF severity mapping](/docs/filescan/3.1.1/configuration/cef-syslog-feedback#scan-verdict-and-cef-severity-mapping)

| Scan verdict | CEF severity |
| --- | --- |
| BENIGN | 0 |
| NO_THREAT | 1 |
| SUSPICIOUS | 3 |
| LIKELY_MALICIOUS | 6 |
| MALICIOUS | 9 |
| UNKNOWN | 0 |

## [Test syslog integration](/docs/filescan/3.1.1/configuration/cef-syslog-feedback#test-syslog-integration)

The syslog integration can be tested with the help of a commonly used syslog server like [syslog-ng](https://syslog-ng.github.io/). You can find an example syslog-ng configuration file below, accepting messages on tcp or udp and storing them to a local file.

Example syslog-ng test configurationCopy@version: 4.11
source s_net {
syslog(
ip("0.0.0.0") port(514) transport("udp")
);
syslog(
ip("0.0.0.0") port(514) transport("tcp")
);
};
destination d_file {
file("/var/log/syslog-ng/messages");
};
log {source(s_net); destination(d_file); };BashCopy#!/usr/bin/env bash
#
# Run syslog-ng in Docker, listening on UDP/TCP 514, writing to ./logs.
#
set -euo pipefail
CONTAINER_NAME="syslog-ng"
CONF_FILE="$PWD/syslog-ng.conf"
LOG_DIR="$PWD/logs"
IMAGE="balabit/syslog-ng:latest"
# Sanity check: config file must exist
if [[ ! -f "$CONF_FILE" ]]; then
echo "Error: $CONF_FILE not found" >&2
exit 1
fi
# Make sure the log directory exists
mkdir -p "$LOG_DIR"
# Remove any previous container with the same name
if sudo docker ps -a --format '{{.Names}}' | grep -qx "$CONTAINER_NAME"; then
echo "Removing existing container '$CONTAINER_NAME'..."
sudo docker rm -f "$CONTAINER_NAME" >/dev/null
fi
echo "Starting $CONTAINER_NAME (Ctrl-C to stop)..."
sudo docker run -it --rm \
--name "$CONTAINER_NAME" \
-p 514:514/udp \
-p 514:514/tcp \
-v "$CONF_FILE":/etc/syslog-ng/syslog-ng.conf \
-v "$LOG_DIR":/var/log/syslog-ng \
"$IMAGE" \
--no-caps

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
