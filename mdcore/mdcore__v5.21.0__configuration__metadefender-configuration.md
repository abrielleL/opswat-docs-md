<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/configuration/metadefender-configuration -->

# MetaDefender Configuration

## [Linux](/docs/mdcore/v5.21.0/configuration/metadefender-configuration#linux)

The configuration file for the server is located in `/etc/ometascan/ometascan.conf`

Notice

After modifying the server configuration file you must restart the Metadefender Core service in order for the changes to take effect. You should use the distribution-standard way to restart the service.

### [[global] section](/docs/mdcore/v5.21.0/configuration/metadefender-configuration#global-section)

| parameter | required | description |
| --- | --- | --- |
| `restaddress` | required | IP address of the computer that runs MetaDefender Core to serve REST API and web user interface (* means listening from all interfaces including IP version 4 and 6).  Just in case IP version 6 is not enabled on the system, then changing it to `0.0.0.0` to limit to IP version 4 only.  Default value: * |
| `restport` | required | Designated port number for the web management console and REST interface.  Default value: 8008 |
| `report_engine_issue` | optional | Enable reporting of engine issue count. (possible values: "true" or "false")  Default value: true |
| `dlppath` | optional | Directory for DLP-processed database and items.  Default value: [Data directory]/dlp |
| `quarantinepath` | optional | Directory for quarantine database and quarantined items.  Default value: [Data directory]/quarantine |
| `sanitizepath` | optional | Directory for sanitized database and sanitized items.  Default value: [Data directory]/sanitized |
| `archiveforensicpath` | optional | Directory for storing captured archive forensic files.  Default value: [Data directory]/archive_forensic |
| `dbmode` | optional | Support database mode, possible values:   - 0: Not used for now, reserved - 1: Standalone Core (default) - 2: Core instance in Cluster deployment - 3: Non-persistent mode (Core will not write any scan result into database, client must use webhook scanning fashion to retrieve scan result) - 4: Shared database model (all Core instances will share the same database)   After changed, a Core service restart is required to take effect. Only available starting MetaDefender Core 4.19.2 |
| `tempdirectory` | optional | Full path of a directory to use for storing temporary files rather than using their default directories: `/var/tmp/` and `/tmp`  Users need to prepare this directory in advance.  MetaDefender Core creates a subfolder called `ometascan`and `ometascan/resources` in the directory.  Default: `/var/tmp/ometascan/resources/` |
| `tempdirectory_create_timeout` | optional | Maximum time allowed for MetaDefender Core to access device and create temporary folder on it. |
| `aigcdpath` | optional | Directory for output images stored by OPSWAT AI Content Inspector engine to display file processing results.  Default value: [Data directory]/aigcd |

### [[logger] section](/docs/mdcore/v5.21.0/configuration/metadefender-configuration#logger-section)

Info

From version 5.15.1, MetaDefender Core (MD Core) allows configuring log file and syslog settings via the MD Core UI or API endpoints ([Advanced Log Configurations](/docs/mdcore/v5.21.0/configuration/advanced-log-configuration)). Therefore, the configurations here will be overridden if they conflict with the configurations for the log file or syslog set through the MD Core UI or API endpoints.

| key | required | description |
| --- | --- | --- |
| `logfile` | optional | Full path of a logfile to write log messages to.  Default value: /var/log/ometascan/ometascan.log |
| `loglevel` | optional | Level of logging. Supported values are: debug, info, warning, error.  Default value: info |
| `log_rotation` | optional | Should only set this key when **logfile** key is also set accordingly. Supported values:   - 0: All logs are not rotated, except for NGINX log. - 1 (default mode), enable to rotate log:    - Rotation process will be performed every day or when file size reaches 1GB.   - Limit rotated log to be stored is 30 files, the oldest log will be deleted if file number reaches the limit.   - Rotated log name format: <logname>-<yyyyMMdd>.gz (e.g.: core.log-20200330.gz), all saved in same location with what you set in **logfile.**   - All generated log packages included in MetaDefender Core support package. |
| `syslog` | optional | Switch on logging to a local ('local') or remote ('protocol://<hostname>:<port>') syslog server (Multiple server can be specified separated with comma). More details: [HERE](https://www.opswat.com/docs/mdcore/configuration/logging) |
| `syslog_level` | optional | Level of logging. Supported values are: debug, info, warning, error |
| `local_timezone` | optional | Set local timezone for events sending to local syslog server.  Default value: false |
| `override` | optional | Override specific log ids to display them on another level e.g.: "1723:error,663:info"  If there is no level set for an id, it will be displayed on every occasion. e.g.: "1723,663:info" means id 1723 dump message will be displayed every time and id 663 warning message is reduced to info level. |
| `cef` | optional | If true, the log format is Common Event Format.  Default value: false |
| `nginx_logfile` | optional | File name and path to store the NGINX logs. If this value is changed, the /etc/logrotate.d/ometascan should be changed accordingly.  Default value: /var/log/ometascan/nginx-ometascan.log |

Notice

Setting both `syslog` and `syslog_level`, or none of them.

Notice

Setting both `logfile` and `loglevel`, or none of them.

### [[internal] section](/docs/mdcore/v5.21.0/configuration/metadefender-configuration#internal-section)

| key | required | description |
| --- | --- | --- |
| `db_connection` | optional | Define maximum number of concurrent connections allows MetaDefender Core to open to work with PostgreSQL database server. Only available starting MetaDefender Core 4.19.1.  Default value: 10 |
| `data_directory` | optional | Full path for MD Core’s data (database, updates etc.) E.g. /var/lib/ometascan/test  Default value: /var/lib/ometascan |
| `skip_upgrade_scan_data` | optional | When enabled (set to 1), upgrading MetaDefender Core will auto skip migrating history processing data which is usually big in size (only migrate configurations and audit history).  This setting is to save upgrade time when users do not need to migrate entire scan data.  Default value: 0 |
| `parallelcount` | optional | Set maximum number of threads (files) sending to engine at the same time, applicable to all engines.  Default value: 20  Exception:   - Archive engine (extraction): default = -1 (unlimited) - Archive engine (compression): default = 20 - Proactive DLP engine: default = 5 - Sandbox engine: default = 5 - SBOM engine: default = 5 - Threat Intelligence engine: default = 5 - OPSWAT AI Content Inspector engine: default =5 |
| `parallelcount_<enginename>` | optional | `<enginename>` is the first part of engine id which all can be found in <MD Core folder>\data\updates\metadescriptor  For example:  engine id: `symantec_1_windows` → `<enginename>` = `symantec`  Some common use-cases:   - **ds (parallelcount_ds)**: Deep CDR engine. By default, `parallelcount_ds` = 20 - **7z (parallelcount_7z)**: Archive engine, applicable to archive extraction only. By default, `parallelcount_7z` = -1 (unlimited threads)    - **7z_extract (parallelcount_7z_extract)**: Archive engine, extraction only. By default, `parallelcount_7z_extract` = -1 (unlimited threads)   - **7z_compress (parallelcount_7z_compress)** : Archive engine, compression only for archive sanitization. By default, `parallelcount_7z_compress` = 20 |
| `next_extraction_polling_interval` | optional | Fine-tuning this interval between the range of 100-200ms may help stabilize the performance and processing time when dealing with small archive files or office document files under high load.  In case this polling interval is set to out of range (invalid number, < 100, or > 1000), the application cannot start, and an exception will log to system event log.  Default value: 1000 |

### [[ocm] section](/docs/mdcore/v5.21.0/configuration/metadefender-configuration#ocm-section)

| key | required | description |
| --- | --- | --- |
| `allow_ocm_urls` | optional | The allowlist of enrollment URLs permitted for enrollment in My OPSWAT Central Management |

## [Windows](/docs/mdcore/v5.21.0/configuration/metadefender-configuration#windows)

The configuration for the server is located in **Windows Registry:** `HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metascan\`

Notice

After modifying the server configuration file you must restart the MetaDefender Core service in order for the changes to take effect.

### [Global](/docs/mdcore/v5.21.0/configuration/metadefender-configuration#global)

`HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metascan\global`

| parameter | type | required | description |
| --- | --- | --- | --- |
| `restaddress` | string value | required | IP address of the computer that runs MetaDefender Core to serve REST API and web user interface (* means listening from all interfaces including IP version 4 and 6).  Just in case IP version 6 is not enabled on the system, then changing it to `0.0.0.0` to limit to IP version 4 only.  Default value: * |
| `restport` | string value | required | Designated port number for the web and REST interface.  Default value: 8008 |
| `report_engine_issue` | string value | optional | Enable reporting of engine issue count. (possible values: "true" or "false").  Default value: true |
| `dlppath` | string value | optional | Directory for DLP-processed database and items.  Default value: [installdir]\data\dlp |
| `quarantinepath` | string value | optional | Directory for quarantine database and quarantined items.  Default value: [installdir]\data\quarantine |
| `sanitizepath` | string value | optional | Directory for sanitized database and sanitized items.  Default value: [installdir]\data\sanitized |
| `archiveforensicpath` | string value | optional | Directory for storing captured archive forensic files.  Default value: [installdir]\archive_forensic |
| `dbmode` | string value | optional | Support database mode, possible values:   - 0: Not used for now, reserved - 1: Standalone Core (default) - 2: Core instance in Cluster deployment - 3: Non-persistent mode (Core will not write any scan result into database, client must use webhook scanning fashion to retrieve scan result) - 4: Shared database model (all Core instances will share the same database)   After changed, a Core service restart is required to take effect. Only available starting MetaDefender Core 4.19.2 |
| `tempdirectory` | string value | optional | Full path of a directory to use for storing temporary files.  Users need to prepare this directory in advance.  MetaDefender Core creates a subfolder called `resources` in this folder.  Default: `<installation directory>\data\resources` |
| `tempdirectory_create_timeout` | string value | optional | Maximum time allowed for MetaDefender Core to access device and create temporary folder on it. |
| `aigcdpath` | string value | optional | Directory for output images stored by OPSWAT AI Content Inspector engine to display file processing results.  Default value: [Data directory]/aigcd |

### [Logger](/docs/mdcore/v5.21.0/configuration/metadefender-configuration#logger)

`HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metascan\logger`

Info

From version 5.15.1, MetaDefender Core (MD Core) allows configuring log file and syslog settings via the MD Core UI or API endpoints ([Advanced Log Configurations](/docs/mdcore/v5.21.0/configuration/advanced-log-configuration)). Therefore, the configurations here will be overridden if they conflict with the configurations for the log file or syslog set through the MD Core UI or API endpoints.

Event Viewer logging can only be configured in the registry.

| key | type | required | description |
| --- | --- | --- | --- |
| `logfile` | string value | optional | Full path of a logfile to write log messages to.  Default value: C:\Program Files\OPSWAT\MetaDefender Core\data\logs\core.log |
| `loglevel` | string value | optional | Level of logging. Supported values are: debug, info, warning, error.  Must set value on this key when **logfile** key is also set accordingly.  Default value: info |
| `log_rotation` | string value | optional | This setting is only applicable on Windows only (on Linux, we use built-in OS log rotation). Should only set this key when **logfile** key is also set accordingly. Supported values:   - 0: Core logs are not rotated. - 1 (default mode), enable to rotate log:    - Rotation process will be performed every day or when file size reaches 1GB.   - Limit rotated log to be stored is 30 files, the oldest log will be deleted if file number reaches the limit.   - Rotated log name format: <logname>-<yyyyMMdd>.gz (e.g.: core.log-20200330.gz), all saved in same location with what you set in **logfile.**   - All generated log packages included in MetaDefender Core support package. |
| `wineventlog_level` | string value | optional | Level of event viewer logging. Supported values are: debug, info, warning, error.  Default value: info |
| `syslog` | string value | optional | Value can only by in form of 'protocol://<hostname>:<port>' (Multiple server can be specified separated with comma). More details: [HERE](https://www.opswat.com/docs/mdcore/configuration/logging) |
| `syslog_level` | string value | optional | Level of logging. Supported values are: debug, info, warning, error. Must set value on this key when **syslog** key is also set accordingly. |
| `local_timezone` | string value | optional | Set local timezone for events sending to local syslog server.  Default value: false |
| `override` | string value | optional | Override specific log ids to display them on another level e.g.: "1723:error,663:info".  If there is no level set for an id, it will be displayed on every occasion. e.g.: "1723,663:info" means id 1723 dump message will be displayed every time and id 663 warning message is reduced to info level. |
| `cef` | string value | optional | If true, the log format is Common Event Format.  Default value: false |
| `nginx_logfile` | string value | optional | File name and path to store the NGINX logs.  Default value: [installdir]\nginx\nginx.log |
| `nginx_log_rotation` | string value | optional | This setting is only applicable on Windows only (on Linux, we use built-in OS log rotation). Should only set this key when **nginx_logfile** key is also set accordingly. Supported values:   - 0: Nginx logs are not rotated. - 1 (default), enable to rotate log:    - Rotation process will be performed every day, regardless of file size.   - Limit rotated log to be stored is 30 files, the oldest log will be deleted if file number reaches the limit.   - Rotated log name format: <logname>-<yyyyMMdd>.gz (e.g.: nginxlog.log-20200330.gz), all saved in same location with what you set in **nginx_logfile.**   - All generated log packages included in MetaDefender Core support package |

Notice

Setting both `syslog`and `syslog_level`, or none of them.

Notice

Setting both `logfile` and `loglevel`, or none of them.

### [Internal](/docs/mdcore/v5.21.0/configuration/metadefender-configuration#internal)

`HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metascan\internal`

| key | type | required | description |
| --- | --- | --- | --- |
| `db_connection` | string value | optional | Define maximum number of concurrent connections allows MetaDefender Core to open to work with PostgreSQL database server. Only available since MetaDefender Core 4.19.1.  Default value: 10 |
| `data_directory` | string value | optional | Full path for MD Core’s data (database, updates etc.) E.g. D:\custom_path  Default value: <MD Core installation folder>\data |
| `skip_upgrade_scan_data` | string value | optional | When enabled (set to 1), upgrading MetaDefender Core will auto skip migrating history processing data which is usually big in size (only migrate configurations and audit history).  This setting is to save upgrade time when users do not need to migrate entire scan data.  Default value: 0 |
| `parallelcount` | string value | optional | Set maximum number of threads (files) sending to engine at the same time, applicable to all engines  Default value: 20  **Exception:**   - Archive engine (extraction): default = -1 (unlimited) - Archive engine (compression): default = 20 - Proactive DLP engine: default = 5 - Sandbox engine: default=5 |
| `parallelcount_<enginename>` | string value | optional | `<enginename>` is the first part of engine id which all can be found in <MD Core folder>\data\updates\metadescriptor  For example:  engine id: `symantec_1_windows` → `<enginename>` = `symantec`  Some common use-cases:   - **ds (parallelcount_ds)**: Deep CDR engine. By default, `parallelcount_ds` = 20 - **7z (parallelcount_7z)**: Archive engine, applicable to archive extraction only. By default, `parallelcount_7z` = -1 (unlimited threads)    - **7z_extract (parallelcount_7z_extract)**: Archive engine, extraction only. By default, `parallelcount_7z_extract` = -1 (unlimited threads)   - **7z_compress (parallelcount_7z_compress)** : Archive engine, compression only for archive sanitization. By default, `parallelcount_7z_compress` = 20 |
| `next_extraction_polling_interval` | string value | optional | Fine-tuning this interval between the range of 100-200ms may help stabilize the performance and processing time when dealing with small archive files or office document files under high load.  In case this polling interval is set to out of range (invalid number, < 100, or > 1000), the application cannot start, and an exception will log to system event log.  Default value: 1000 |

### [OCM](/docs/mdcore/v5.21.0/configuration/metadefender-configuration#ocm)

| key | required | description |
| --- | --- | --- |
| `allow_ocm_urls` | optional | The allowlist of enrollment URLs permitted for enrollment in My OPSWAT Central Management |
