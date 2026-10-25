<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/knowledge-base/why-do-metadefender-core-webhook-callbacks-fail-with-http-413-re -->

# Why Do MetaDefender Core Webhook Callbacks Fail with HTTP 413 Request Entity Too Large?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to MetaDefender ICAP Server version 5.x onwards, deployed on Windows and Linux servers.

1. Description of the Issue

When MetaDefender Core processes large files — particularly PDF documents with Content Disarm & Reconstruction (CDR) running in analysis mode — the resulting scan-result JSON payload can grow very large. This occurs because CDR enumerates every embedded link, URL, and object found within the file; a single large PDF may yield thousands of entries, producing a JSON response exceeding 1 MB.

MetaDefender Core delivers scan results by sending an HTTP POST request to the webhook endpoint configured on the ICAP Server. The ICAP Server's embedded NGINX instance enforces a maximum request-body size controlled by the ICAP configuration key internal/max_size_upload, which defaults to 1,024 KB. When the JSON payload from Core exceeds this threshold, NGINX rejects the inbound POST with an HTTP 413 Request Entity Too Large response.

As a result, MetaDefender Core never receives a 200 OK acknowledgement and repeatedly retries the webhook delivery, generating a cascade of 413 errors visible in both the NGINX log and the MetaDefender Core application log.

Note:

Starting from MetaDefender ICAP Server 5.14.0, the default value of internal/max_size_ upload will be increased to 2 MB. For earlier versions, or if your environment generates payloads larger than 2 MB, the manual configuration steps in Section 3 are required.

2. Steps to Identify

Follow the steps below to confirm that HTTP 413 errors are the root cause of missing webhook callbacks.

2.1 Check the NGINX Log on the ICAP Server

Log file locations:

- Windows: C:\Program Files\OPSWAT\Metadefender ICAP Server\nginx\nginx.log
- Linux: /var/log/mdicapsrv/nginx-mdicapsrv.log

Open the log file and search for lines referencing client intended to send too large body combined with a /webhook/ URI path. This confirms NGINX rejected the request from MetaDefender Core:

NGINX nginx.log — 413 body-size rejection (client = MetaDefender Core)

# ── NGINX nginx.log ─────────────────────────────────────────────────────────
2026/05/20 11:55:52 [error] 11156#21392: *76 client intended to send too large body:
1330126 bytes, client: 192.168.0.100, server: ,
request: "POST /webhook/6b012e5b821347188369a699aa07a4be HTTP/1.1",
host: "192.168.0.101:8048"
192.168.0.100 - - [20/May/2026:11:55:52 -0700]
"POST /webhook/6b012e5b821347188369a699aa07a4be HTTP/1.1" 413 176 "-" "OPSWAT MetaDefender Core" 0.012

The HTTP 413 status code alongside the OPSWAT MetaDefender Core user-agent confirms that Core's webhook POST is being rejected by NGINX due to payload size.

2.2 Check the MetaDefender Core Application Log

Log file locations:

- Windows: C:\Program Files\OPSWAT\MetaDefender Core\data\logs\Core.log
- Linux: /var/log/ometascan/ometascan.log

Search for Webhook response failed with status='413'. You will typically see multiple repeated entries for the same data_id as Core retries delivery:

MetaDefender Core application log — repeated 413 webhook retries

# ── MetaDefender Core application log ───────────────────────────────────────
[WARNING] 2026.05.20 20:25:43.203: (core.webhook) Webhook response failed,
data_id='b2c7ee7cd035424e91860fc769a77c81', type='Callback webhook',
Responser Id='0', status='413', error_code='299',
description='an unknown error related to the remote content was detected',
thread_id='lms::core::WebhookResponser(0x25f2de00)' [msgid: 3926]
[ ... repeated with exponential back-off ... ]

The same data_id appearing across multiple consecutive WARNING lines confirms that Core is retrying the same webhook POST and every attempt is rejected by NGINX.

3. Steps to Resolve

The correct and persistent fix is to increase the internal/max_size_upload configuration key on the ICAP Server. This key controls the client_max_body_size directive that ICAP writes into the generated nginx.conf at every start-up and configuration reload.

IMPORTANT:

Do NOT manually edit nginx.conf directly. The ICAP Server regenerates that file from an internal template on every restart and configuration change. Any manual edit will be silently overwritten, reverting the limit back to 1 MB.

Configuration key details:

- Key: internal/max_size_upload
- Unit: kilobytes (KB)
- Default: 1024 (1 MB)
- Valid range: 0 – 102400 (0 = unlimited; maximum 100 MB)
- Suggested value: 10240 (10 MB)

3.1 Windows

On Windows, the ICAP Server stores its configuration in the Windows Registry. Set the max_size_upload value under the internal key:

1. Open the Registry Editor (regedit.exe) as Administrator and navigate to: HKEY_LOCAL_MACHINE\Software\OPSWAT\ICAP Server\internal
2. Create a new String value named max_size_upload and set its data to 10240.

Windows Registry — max_size_upload entry

Registry path: HKLM\Software\OPSWAT\ICAP Server\internal
Name: max_size_upload
Type: String
Data: 10240

Alternatively, apply the change from an elevated PowerShell or Command Prompt:

# PowerShell — run as Administrator
Set-ItemProperty `
-Path "HKLM:\Software\OPSWAT\ICAP Server\internal" `
-Name "max_size_upload" `
-Value 10240 `
-Type String

3. Restart the OPSWAT Metadefender ICAP Server Windows service to apply the change:

# PowerShell — run as Administrator
Restart-Service -Name "mdicapsrv" -Force

After restart, ICAP will regenerate nginx.conf with client_max_body_size 10240K; in the server block. The value persists across future restarts and configuration changes.

3.2 Linux

On Linux, the ICAP Server reads its configuration from /etc/mdicapsrv/mdicapsrv.conf. Add or update the max_size_upload key under the [internal] section:

1. Open /etc/mdicapsrv/mdicapsrv.conf in a text editor with root privileges:

Linux — open ICAP configuration file

sudo nano /etc/mdicapsrv/mdicapsrv.conf
# or
sudo vi /etc/mdicapsrv/mdicapsrv.conf

2. Add or update the following lines under the [internal] section:

/etc/mdicapsrv/mdicapsrv.conf — updated entry

[internal]
max_size_upload=10240

3. Save the file and restart the mdicapsrv service to apply the change:

sudo systemctl restart mdicapsrv
# Verify the service started successfully:
sudo systemctl status mdicapsrv

After restart, ICAP will regenerate nginx.conf with client_max_body_size 10240K; in the server block.

4. Steps to Check Functionality

After applying the configuration change, verify end-to-end webhook delivery by re-scanning a large PDF file with CDR in analysis mode or your previous file that triggered the issue.

1. Submit a large PDF file (one that previously triggered the 413 error) for scanning through the ICAP Server or directly via the MetaDefender Core REST API.
2. Monitor the MetaDefender Core application log in real time and confirm that no new Webhook response failed entries appear for the test scan's data_id:

MetaDefender Core application log — real-time webhook monitoring

# Linux — follow Core log during test scan
tail -f /var/log/ometascan/ometascan.log | grep -i webhook
# Windows (PowerShell) — follow Core log during test scan
Get-Content "C:\Program Files\OPSWAT\MetaDefender Core\data\logs\core.log"
-Wait | Select-String -Pattern "webhook"

3. Check the ICAP NGINX log to confirm that webhook POSTs now return 200 instead of 413:

NGINX nginx.log — successful 200 response after fix

# Linux
grep "webhook" /var/log/mdicapsrv/nginx-mdicapsrv.log | tail -20
# Windows (PowerShell)
Get-Content " C:\Program Files\OPSWAT\Metadefender ICAP Server\nginx\nginx.log"
-Wait | Select-String -Pattern "webhook"
# Expected success entry (status 200, no [error] lines):
192.168.0.100 - - [20/May/2026:12:10:05 -0700]
"POST /webhook/6b012e5b821347188369a699aa07a4be HTTP/1.1"
200 0 "-" "OPSWAT MetaDefender Core" 0.003

4. Verify the scan result was correctly received on the ICAP side by confirming the file disposition (clean / infected / blocked) is reflected in the ICAP Server's scan history or the upstream application's response.

Note

Note that internal/max_size_ upload is a global limit that applies to all common REST endpoints on the ICAP Server, not exclusively to /webhook/ paths. Set the value appropriate to your largest expected payload. Values above 100 MB (102400) are not supported.

Support:

If Further Assistance is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).
