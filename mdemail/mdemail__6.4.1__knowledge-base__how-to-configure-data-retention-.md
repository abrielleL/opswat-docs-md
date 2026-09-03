<!-- source: https://www.opswat.com/docs/mdemail/6.4.1/knowledge-base/how-to-configure-data-retention- -->

# How to configure Data Retention?

MetaDefender Email Security allows you to set retention cleanup schedules for the following options:

Please monitor your disk space over time and set accordingly, to prevent disk space from filling up.

The default install directory for MetaDefender Email Security is listed below, please check the properties and folders within to view their size over time

C:\Program Files\OPSWAT\Metadefender Email Security

---

MetaDefender Email Security also stores logs within the Event Viewer, default path is listed below:

C:\Windows\System32\WinEvt\Logs

Options for retention:

1. Please communicate with your Administrator to set effective retention settings within Windows Event Viewer, outside of the MetaDefender Email Security UI.
2. Within the registry editor, set values for `logfile`, `loglevel`, `log_rotation` to automatically store the logs inside a desired location.

Location: Computer\HKEY_LOCAL___MACHINE\SOFTWARE\OPSWAT\MetaDefender Email Security\logger

Warning

You must set logfile with loglevel, setting one without the other will result in a failure to start the “OPSWAT MetaDefender Email Security” service.

The following are strings, please reference our documentation: <https://www.opswat.com/docs/mdemail/configuration#hkey_local_machinesoftwareopswatmetadefender-email-securitylogger>

- `logfile` - create an empty .log file and store it in a desired location. The example below displays the egs.log stored in documents.

Info

.log files can be created using Notepad++ or other desired methods. By saving file as .log under “All file Types”

- `loglevel`- set value to “info”
- `log_rotation` - set value to “true”, this will create a new log file every 24 hours, and delete files older than 30 days.

Support

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
