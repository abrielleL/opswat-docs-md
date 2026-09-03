<!-- source: https://www.opswat.com/docs/mdmft/configuration/logging -->

# Logging

Summarize Page    Connect to Cursor Connect to VS Code

To change logging settings, go to "Settings" → "Logging."

Info

The default location for log files is within the Installation Directory under Services\Logs.

### [Logging Level](/docs/mdmft/configuration/logging#logging-level)

MetaDefender Managed File Transfer logs information with different levels, ranging from Debug (very detailed) to Fatal.

### [Log Rotation Options](/docs/mdmft/configuration/logging#log-rotation-options)

Log rotation settings define when a new log file should be created. You can configure the system to start a new log file when the current log file reaches a specified size, by date (creating a new log file each day) or both.

### [Log Retention Options](/docs/mdmft/configuration/logging#log-retention-options)

Log retention settings define when log files should be deleted. You can configure the system to delete previous log files by date (after a specified number of days), by size (when log size reaches a specified size), or both.

Info

When "Both" is selected for log retention options, the relation between "By size" and "By date" is an "OR," meaning whichever criteria is met first triggers the log cleanup process.

Info

The log cleanup process in MetaDefender Managed File Transfer runs every hour after the completion of the previous cleaning job and initiates after a HELPER service restart.

After configuring the desired options, click "Update."
