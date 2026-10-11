<!-- source: https://www.opswat.com/docs/mddownloader/v3.5.0/configuration/update-downloader-server-configuration-file -->

# Update Downloader server configuration file

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Linux](/docs/mddownloader/v3.5.0/configuration/update-downloader-server-configuration-file#linux)

The configuration file for the server is located in `/etc/ometadownloader/ometadownloader.conf`

After modifying the server configuration file you must restart the Metascan service in order for the changes to take effect. You should use the distribution-standard way to restart the ometadownloader service.

## [[global] section](/docs/mddownloader/v3.5.0/configuration/update-downloader-server-configuration-file#global-section)

| parameter | default value | required | description |
| --- | --- | --- | --- |
| restaddress | 0.0.0.0 | required | One of the IP addresses of the computer that runs the product to serve REST API and web user interface (0.0.0.0 means all interface) |
| restport | 8028 | required | Designated port number for the web and REST interface |

## [[logger] section](/docs/mddownloader/v3.5.0/configuration/update-downloader-server-configuration-file#logger-section)

| key | default value | required | description |
| --- | --- | --- | --- |
| logfile | /var/log/ometadownloader/ometadownloader.log | optional | Full path of a logfile to write log messages to |
| loglevel | info | optional | Level of logging. Supported values are: debug, info, warning, error |
| syslog |  | optional | Switch on logging to a local ('local') or remote ('protocol://hostname:port') syslog server |
| syslog_level |  | optional | Level of logging. Supported values are: debug, info, warning, error |
| override |  | optional | override specific log ids to display them on another level e.g.: "1723:error,663:info" |
| cef | false | optional | If true, the log format is Common Event Format. |

You should set both of syslog and syslog_level or none of them and you should set both of logfile and loglevel or none of them.

## [Windows](/docs/mddownloader/v3.5.0/configuration/update-downloader-server-configuration-file#windows)

The configuration for the server is located in **Windows Registry**

After modifying the server configuration file you must restart the OPSWAT Metadefender Update Downloader service in order for the changes to take effect.

Default logging target is Windows event log with default level of info (see below).

## [HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metadownloader\global](/docs/mddownloader/v3.5.0/configuration/update-downloader-server-configuration-file#hkey_local_machinesoftwareopswatmetadownloaderglobal)

| parameter | default value | type | required | description |
| --- | --- | --- | --- | --- |
| restaddress | 0.0.0.0 | string value | required | One of the IP addresses of the computer that runs the product to serve REST API and web user interface (0.0.0.0 means all interface) |
| restport | 8028 | string value | required | Designated port number for the web and REST interface |

## [HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metadownloader\logger](/docs/mddownloader/v3.5.0/configuration/update-downloader-server-configuration-file#hkey_local_machinesoftwareopswatmetadownloaderlogger)

| key | default value | type | required | description |
| --- | --- | --- | --- | --- |
| logfile |  | string value | optional | Location of a logfile to write log messages to |
| loglevel |  | string value | optional | Level of logging. Supported values are: debug, info, warning, error |
| wineventlog_level | info | string value | optional | Level of logging. Supported values are: debug, info, warning, error |
| syslog |  | string value | optional | Value can only by in form of `udp://<hostname>:<port>` |
| syslog_level |  | string value | optional | Level of logging. Supported values are: debug, info, warning, error |
| override |  | string value | optional | override specific log ids to display them on another level e.g.: "1723:error,663:info" |
| cef | false | string value | optional | If true, the log format is Common Event Format. |

You should set both of syslog and syslog_level or none of them and you should set both of logfile and loglevel or none of them.

For override a list of log message ids needed with optionally a level. If there is no level set for an id, it will be displayed on every occasion. e.g.: "1723,663:info" means id 1723 dump message will be displayed every time and id 663 warning message is reduced to info level.
