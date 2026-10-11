<!-- source: https://www.opswat.com/docs/mdss/where-to-get-help/how-to-read-the-logs- -->

# How to read the logs

The log files are plain text files that can be opened with any text editor.

For MetaDefender Storage Security, the default logging level is set to **Information**. To access additional log levels, you need to enable Extra Logging in the Configuration. Extra logging is recommended only for troubleshooting purposes and should be enabled only when necessary.

For more details, refer to this article: [How to Enable Extra Logging in the Configuration?](https://www.opswat.com/docs/mdss/where-to-get-help/how-to-enable-extra-logging-in-the-configuration)

## File Locations

- **Linux**: Log files are located at `/etc/mdss/services_logs`
- **Windows**: The default path is `C:\Program Files\OPSWAT\MetaDefender Storage Security\services\`

## Log Format

The messages stored in the service logs follow this format:

```powershell
[TIMESTAMP] [LEVEL] service.name: Message
```

**Example:**

```powershell
[2024-06-12 10:17:55Z] [Information] nfs.service: HTTP POST /ObjectOperations/Download responded 200 in 37.0824 ms
```

## Log Levels

- **Debug : Provides detailed information useful for troubleshooting.**
- **Information**: The default logging level, capturing general operational messages.
- **Warning**: Highlights potentially harmful situations.
- **Error**: Logs issues that affect functionality or cause interruptions.
- **Fatal**: Reserved for very critical issues that require immediate attention.

> **Support:**
>
> If you have any difficulty reading MetaDefender Storage Security logs, please create[ a support case or chat with our support engineer](https://my.opswat.com/support).

## Analysis Guide

This guide helps customer support representatives efficiently locate error messages in product logs when troubleshooting customer issues.

Storage-type specific code (Amazon S3, Azure, Google Cloud, Box, SharePoint, SFTP, FTP, and so on) runs inside the central Storages, Discovery and Remediations services, and inside the Scanning service when it downloads files, so their errors appear in those services' logs. Only NFS and SMB have a separate sidecar service with its own log folder.

| Behavior | Log folder under `services_logs` |
| ---- | ---- |
| Failed to add a storage unit | `mdss_storagesservice` `mdintegrations_nfsservice` / `mdintegrations_smbservice` (NFS and SMB storages only) |
| Failed to add MD Core or Cloud instance | `mdcs_scanningservice` (connection, API key and saving the instance) `mdss_workflowmanager` (workflow rule checks) |
| Failed to start a scan No files are discovered | `mdss_workflowmanager` (scan start) `mdss_discoveryservice` `mdcs_jobdispatcher` (scan scheduling and job state) `mdintegrations_nfsservice` / `mdintegrations_smbservice` (NFS and SMB storages only) |
| Failed to scan a file No files are scanned | `mdcs_scanningservice` |
| Failed to remediate a file Remediations not applied Sanitization failed Sanitization not applied | `mdss_remediationsservice` `mdintegrations_nfsservice` / `mdintegrations_smbservice` (NFS and SMB storages only) |
| Login or API key problems | `mdss_identityservice` `mdcs_apigateway` |
| License not applied or expired | `mdcs_licensingservice` |
| Notifications (email, webhook) not sent | `mdcs_notificationservice` |
| Syslog or other external log output not received | `mdcs_loggingservice` |

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
