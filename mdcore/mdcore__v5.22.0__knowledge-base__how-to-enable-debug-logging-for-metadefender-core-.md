<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/how-to-enable-debug-logging-for-metadefender-core- -->

# How to enable debug logging for MetaDefender Core?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows and Linux systems.

Note:

To assist the OPSWAT Support team in diagnosing issues more effectively, we may require debug logs from your MetaDefender Core for a detailed analysis.

Enabling debug logging level on MetaDefender Core should only be used when necessary and advised by the OPSWAT team.

To enable debug logging for MetaDefender Core, please follow the appropriate guide based on your operating system:

## [Windows](https://www.opswat.com/docs/mdcore/knowledge-base/how-to-enable-debug-logging-for-metadefender-core-#windows)

The log level can be updated through the Web UI (available starting with MD Core v5.15.1) or via the Windows Registry.

1. Web Console:

   - Navigate to ***Settings*** > ***Logs*** > ***Log File*** section
   - Click on the ***Edit*** button and update the ***Log level*** to ***debug***
   - Save the changes (service restart is **NOT** required)

2. Windows Registry:

   - Open the Registry Editor
   - Navigate to `HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metascan\logger`
   - Change the value of `loglevel`to `debug`
   - Restart the MetaDefender Core service

## [Linux](https://www.opswat.com/docs/mdcore/knowledge-base/how-to-enable-debug-logging-for-metadefender-core-#linux)

The log level can be updated through the Web UI (available starting with MD Core v5.15.1) or via the ***ometascan.conf*** configuration file.

1. Web Console:

   - Navigate to ***Settings*** > ***Logs*** > ***Log File*** section
   - Click on the ***Edit*** button and update the ***Log level*** to ***debug***
   - Save the changes (service restart is **NOT** required)
2. Configuration file:

   - Open the file at `/etc/ometascan/ometascan.conf` with your preferred text editor.
   - In the **[logger]** section, change the value of `loglevel` to `debug`.
   - Restart the MetaDefender Core service.

Attention:

After finishing with debug logging mode, the **loglevel** should be set back to **info**. Failed to do so, the size of your log files could increase significantly.

## [Generating a Support Package](https://www.opswat.com/docs/mdcore/knowledge-base/how-to-enable-debug-logging-for-metadefender-core-#generating-a-support-package)

Once debug logging is enabled, please attempt to reproduce the issue you are experiencing. Afterward, generate a Support Package and send it to the Support team so we can properly investigate the issue.

For a detailed guide on generating a Support Package, please refer to the following URLs:

- [How to Create Support Package With Web Console](https://www.opswat.com/docs/mdcore/troubleshooting/how-to-create-support-package-with-web-console)
- [How to Create Support Package With Bundle Tools](https://www.opswat.com/docs/mdcore/troubleshooting/how-to-create-support-package-)

Support:

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/portal/support).
