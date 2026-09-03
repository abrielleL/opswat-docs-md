<!-- source: https://www.opswat.com/docs/mdicap/configuration/configuration -->

# Configuration

## [Logging configuration](/docs/mdicap/configuration/configuration#logging-configuration)

To configure the log outputs and levels, consult the [3.1.2 MetaDefender ICAP Server configuration file](/docs/mdicap/configuration/configuration-file) section.

## [Linux log rotation](/docs/mdicap/configuration/configuration#linux-log-rotation)

The installer configures the logrotate service to rotate MetaDefender ICAP server log files.

Configuration file is located in:

/etc/logrotate.d/mdicapsrvInfo

The default configuration will rotate daily and store the last 30 days.

Note

If the log file path is modified, the logrotate config file should be updated as well.

Note

The new log settings will be used after a service restart or a HUP signal.
