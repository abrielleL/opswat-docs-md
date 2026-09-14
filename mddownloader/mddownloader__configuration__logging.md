<!-- source: https://www.opswat.com/docs/mddownloader/configuration/logging -->

# Logging

MetaDefender Update Downloader has wide variety of options to configure logging. Log settings are in the configuration files or web console

## [Configure via web console](/docs/mddownloader/configuration/logging#configure-via-web-console)

Web console support:

- Log file path
- Log file path level
- Syslog connection
- Syslog level

For more configuration, please use the configuration file.

Warning

Please note that when changing logging configuration, Update Downloader will automatically reload it service, during this time, the service is unavailable

**Limitation:** On Rocky/RHEL 9, in certain situations, the service may not automatically reload as expected. In such cases, users are required to manually reload the service.

## [Configure via the configuration file](/docs/mddownloader/configuration/logging#configure-via-the-configuration-file)

To configure the log outputs and levels, consult the following paragraphs:

- [Update Downloader server configuration file](/docs/mddownloader/configuration/update-downloader-server-configuration-file)

In case of using linux operating system the installer configures the **logrotate** service to handle the Metascan log files.

Configuration file is located:

- `/etc/logrotate.d/ometadownloader`

The default configuration will rotate daily and store the last 30 days.

If the log file path is modified, the logrotate config file should be updated as well.

The new log settings will be used after a service restart or a HUP signal.

## [Debug logging](/docs/mddownloader/configuration/logging#debug-logging)

To provide debug logs for the OPSWAT support team, the level of the logfile for the given service (ometadownloader) must be set to 'debug'.

Next, execute the scenarios requested by the support team, and collect the generated log files from the configured location.

After that the log level should be set back to 'info'. In debug level the size of the logfile size will increase significantly.

For information on how to modify the logging settings of the product consult the paragraph: [Configuration](/docs/mddownloader/configuration/logging)

For information on other data that OPSWAT support might require go to [How to create support package?](/docs/mddownloader/troubleshooting/how-to-create-support-package)

For information on how to interpret the log files consult: [How to read the Update Downloader log?](/docs/mddownloader/troubleshooting/how-to-read-the-update-downloader-log)
