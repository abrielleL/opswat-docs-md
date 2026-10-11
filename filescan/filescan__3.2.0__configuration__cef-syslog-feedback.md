<!-- source: https://www.opswat.com/docs/filescan/3.2.0/configuration/cef-syslog-feedback -->

# CEF Syslog Feedback

View as Markdown Ask ChatGPT about this page Ask Claude about this page

The CEF syslog feature is moved from the **broker** component and now is deprecated. Please migrate the syslog settings to the **Admin Panel** as described below.

To remove the syslog feedback configuration from the broker:

**Step #1 - Open** `/home/sandbox/sandbox/broker.cfg` **in a text editor**

**Step #2 - Remove or comment out the following properties:**

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

---

## [Syslog configuration](/docs/filescan/3.2.0/configuration/cef-syslog-feedback#syslog-configuration)

The syslog can be configured by navigating to **Admin Panel -> Settings -> Configuration -> Monitoring -> Syslog**.

| Setting | Default Value | Description |
| --- | --- | --- |
| SYSLOG_ENABLED | false | Main switch to enable / disable CEF syslog feedback |
| SYSLOG_HOST |  | Host name or IP address of the syslog server |
| SYSLOG_PORT | 5514 | Port of the syslog server |
| SYSLOG_PROTOCOL | udp | Connection protocol to use: tcp or udp |
| SYSLOG_FACILITY | local0 | Facility value used in the syslog header |
| SYSLOG_TLS_ENABLED | false | Switch to enable / disable SSL/TLS verification for TCP sockets |
| SYSLOG_TLS_CA_CERT |  | The path to the certificate to use to connect to syslog server using SSL/TLS |
| SYSLOG_TLS_NOVERIFY | false | Switch to disable TLS certificate verification for syslog server, and accept self-signed certificates |
| SYSLOG_AUTH_EVENTS_LOGGING_ENABLED | false | Switch to enable / disable logging authentication events to syslog server |
| SYSLOG_ADMIN_EVENTS_LOGGING_ENABLED | false | Switch to enable / disable logging admin events to syslog server |
| SYSLOG_SCAN_RESULT_SUMMARY_LOGGING_ENABLED | false | Switch to enable / disable logging scan result summaries to syslog server |

When the **SYSLOG_AUTH_EVENTS_LOGGING_ENABLED** is enabled, the same authentication events with the same content that is in the Audit Logger Authentication is logged to the syslog server.

When the **SYSLOG_ADMIN_EVENTS_LOGGING_ENABLED** is enabled, the same admin setting change events that is in the Audit Logger Admin is logged to the syslog server. The contents of the log is reduced in some cases due to their size. The full logs can still be found under **Admin Panel -> Audit Logger -> Admin**.

## [Syslog Message Format in Sandbox](/docs/filescan/3.2.0/configuration/cef-syslog-feedback#syslog-message-format-in-sandbox)

Sandbox uses the standardized Syslog message format, following **Syslog Protocol Version 1**.

#### [**Base Format**](/docs/filescan/3.2.0/configuration/cef-syslog-feedback#base-format)

`Date Host CEF:Version|Device Vendor|Device Product|Device Version|Device Event Class ID|Name|Severity|[Extension]`

This format complies with the **Common Event Format (CEF)** standard, ensuring compatibility and reliable parsing by SIEM tools and other log management systems.

#### [**References to Syslog Standards**](/docs/filescan/3.2.0/configuration/cef-syslog-feedback#references-to-syslog-standards)

For a deeper understanding of the Syslog message format and transport methods, refer to the following RFCs:

- **Syslog Protocol (RFC 5424)** – Defines the overall message structure 📄 [RFC 5424 - Syslog Protocol](https://www.rfc-editor.org/pdfrfc/rfc5424.txt.pdf)
- **Syslog over TLS (RFC 5425)** – For secure transmission over TLS [📄](%F0%9F%93%84) [RFC 5425 - Syslog over TLS](https://www.rfc-editor.org/pdfrfc/rfc5425.txt.pdf)
- **Syslog over UDP (RFC 5426)** – For lightweight, best-effort delivery 📄 [RFC 5426 - Syslog over UDP](https://www.rfc-editor.org/pdfrfc/rfc5426.txt.pdf)

## [Example CEF syslog messages:](/docs/filescan/3.2.0/configuration/cef-syslog-feedback#example-cef-syslog-messages)

### [Authentication event](/docs/filescan/3.2.0/configuration/cef-syslog-feedback#authentication-event)

2026-07-07T12:22:44+00:00 [info] 172.22.0.4 CEF:0|OPSWAT|MetaDefender Sandbox|Filescan-Dev|Auth Event|signout|3|cs1Label=User Id cs1=698494521a5d1587c74e175a cs2Label=User Name cs2=test@opswat.com cs3Label=Route cs3=GET - /api/auth/signout cs4Label=Message cs4=Logout: test@opswat.com
2026-07-07T12:45:00+00:00 [info] 172.22.0.10 CEF:0|OPSWAT|MetaDefender Sandbox|Filescan-Dev|Auth Event|signin|7|cs2Label=User Name cs2=ip\='161.1.0.1' user_agent\='Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:152.0) Gecko/20100101 Firefox/152.0' access_token\=None cs3Label=Route cs3=POST - /api/auth/signin cs4Label=Message cs4=Login failed: test@opswat.com
2026-07-07T12:41:48+00:00 [info] 172.22.0.10 CEF:0|OPSWAT|MetaDefender Sandbox|Filescan-Dev|Auth Event|signin|3|cs1Label=User Id cs1=698494521a5d1587c74e175a cs2Label=User Name cs2=test@opswat.com cs3Label=Route cs3=POST - /api/auth/signin cs4Label=Message cs4=Login successful
### [Admin setting change event](/docs/filescan/3.2.0/configuration/cef-syslog-feedback#admin-setting-change-event)

2026-07-07T12:42:32+00:00 [info] 172.22.0.10 CEF:0|OPSWAT|MetaDefender Sandbox|Filescan-Dev|Admin Event|admin-edit-settings-group|3|cs1Label=User Id cs1=698494521a5d1587c74e175a cs2Label=User Name cs2=test@opswat.com cs3Label=Route cs3=POST - /api/admin/settings/environment cs4Label=Original cs4=name\=SYSLOG_ENABLED, id\=6a4cf438ea34385f4e3ddb08, value\=False cs5Label=New cs5=name\=SYSLOG_ENABLED, id\=6a4cf438ea34385f4e3ddb09, value\=True
### [Scan result summary](/docs/filescan/3.2.0/configuration/cef-syslog-feedback#scan-result-summary)

2026-07-07T12:44:21+00:00 [info] 172.22.0.6 CEF:0|OPSWAT|MetaDefender Sandbox|Filescan-Dev|Scan Result Summary|scan-result-summary|3|cs1Label=User ID cs1=Guest cs2Label=User Name cs2=Guest cs3Label=Scan Init ID cs3=6a4cf46bea34385f4e3ddb21 cs4Label=SHA256 cs4=02a177c43c08df4db30a8f1c2e3d71d51590403eb6ba8b8b2b7d9cf00e68e18c cs5Label=Filename cs5=qbittorrent_5.2.1_x64_setup.exe cs6Label=Media Type cs6=application/x-dosexec cs7Label=All Tags cs7=peexe,adaptive-context,anti-debug,keylogger,packed,reconnaissance,installer,expand,lolbin,crypto,fingerprint,nsis,microsoft_visual_cc cs8Label=All Signal Group IDs cs8=Y002,H020,H022,H069,H024,H027,H026,Y001,Y000,SIGG016,H011,H058,H057,H018,H083,H121,H000,H088,H007,H009,SIGG072,SIGG034,H030,H076,H031,H111,H033,H035,H115,H037,H116,H119,I001,H061,H060,H062,H064,H104,H106,H028,H105,H107,H094,BIN001,S007,H016,H122,H004,H070,H072,H071,H032,H036,H038,H117,H118 cs9Label=Verdict cs9=malicious
2026-07-07T12:45:44+00:00 [info] 172.22.0.6 CEF:0|OPSWAT|MetaDefender Sandbox|Filescan-Dev|Scan Result Summary|scan-result-summary|3|cs1Label=User ID cs1=698494521a5d1587c74e175a cs2Label=User Name cs2=test@opswat.com cs3Label=Scan Init ID cs3=6a4cf4e6ea34385f4e3ddb4b cs4Label=SHA256 cs4=507b451ab398b6daa3ae799e985244f2c66b3d1bbc4bea991f6015954ddbf0d7 cs5Label=Filename cs5=13-SANDBOX-SECURITY.pdf cs6Label=Media Type cs6=application/pdf cs7Label=All Tags cs7=pdf,html cs8Label=All Signal Group IDs cs8=I000,S060,PDF002,U014,SIGG043,U013,SIGG044,SIGG045,SIGG046,D001 cs9Label=Verdict cs9=malicious
## [Test syslog integration](/docs/filescan/3.2.0/configuration/cef-syslog-feedback#test-syslog-integration)

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
