<!-- source: https://www.opswat.com/docs/mdss/4.4.2/where-to-get-help/how-to-read-the-logs- -->

# How to read the logs

The log files are plain text files that can be opened with any text editor.

For MetaDefender Storage Security, the default logging level is set to **Information**. To access additional log levels, you need to enable Extra Logging in the Configuration. Extra logging is recommended only for troubleshooting purposes and should be enabled only when necessary.

For more details, refer to this article: [How to Enable Extra Logging in the Configuration?](/docs/mdss/4.4.2/where-to-get-help/how-to-enable-extra-logging-in-the-configuration)

## [File Locations](/docs/mdss/4.4.2/where-to-get-help/how-to-read-the-logs-#file-locations)

- **Linux**: Log files are located at `/etc/mdss/services_logs`
- **Windows**: The default path is `C:\Program Files\OPSWAT\MetaDefender Storage Security\services\`

## [Log Format](/docs/mdss/4.4.2/where-to-get-help/how-to-read-the-logs-#log-format)

The messages stored in the service logs follow this format:

LogCopy[TIMESTAMP] [LEVEL] service.name: Message

**Example:**

LogCopy[2024-06-12 10:17:55Z] [Information] nfs.service: HTTP POST /ObjectOperations/Download responded 200 in 37.0824 ms
## [Log Levels](/docs/mdss/4.4.2/where-to-get-help/how-to-read-the-logs-#log-levels)

- **Debug : Provides detailed information useful for troubleshooting.**
- **Information**: The default logging level, capturing general operational messages.
- **Warning**: Highlights potentially harmful situations.
- **Error**: Logs issues that affect functionality or cause interruptions.
- **Fatal**: Reserved for very critical issues that require immediate attention.

Support:

If you have any difficulty reading MetaDefender Storage Security logs, please create [a support case or chat with our support engineer](https://my.opswat.com/support).

## [Analysis Guide](/docs/mdss/4.4.2/where-to-get-help/how-to-read-the-logs-#analysis-guide)

This guide helps customer support representatives efficiently locate error messages in product logs when troubleshooting customer issues.

| Behavior | Container |
| --- | --- |
| Failed to add a storage unit | mdss_nfsservice / mdss_smbservice / mdss_sftpservice (if applicable)  *mdss*_{storageType}_*storagesservice*  *mdss_storagesservice* |
| Failed to add MD Core or Cloud instance | mdss_workflowmanagerservice |
| Failed to start a scan  No files are discovered | mdss_nfsservice / mdss_smbservice / mdss_sftpservice (if applicable)  *mdss*_{storageType}_*discoveryservice*  *mdss_discoveryservice* |
| Failed to scan a file  No files are scanned | mdcs_scanningservice |
| Failed to remediate a file  Remediations not applied  Sanitization failed  Sanitization not applied | mdss_remediationsservice  mdss__{storageType}_*remediationsservice* |
