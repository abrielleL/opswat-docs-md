<!-- source: https://www.opswat.com/docs/mdicap/configuration/configuration-file -->

[MetaDefender ICAP Server](https://www.opswat.com/docs/mdicap)Need Help?
# Configuration file

- ### [Linux](/docs/mdicap/configuration/configuration-file#linux) config file location

  - [[global] section](/docs/mdicap/configuration/configuration-file#global-section)
  - [[logger] section](/docs/mdicap/configuration/configuration-file#logger-section)
- ### [Windows](/docs/mdicap/configuration/configuration-file#windows) config file location

  - [HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\ICAP Server\global](/docs/mdicap/configuration/configuration-file#hkey_local_machinesoftwareopswaticap-serverglobal)
  - [HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\ICAP Server\logger](/docs/mdicap/configuration/configuration-file#hkey_local_machinesoftwareopswaticap-serverlogger)

## [Linux](/docs/mdicap/configuration/configuration-file#linux-config-file-location)

Note

Configuration upgrades on RHEL/CentOS

When ICAP Server is upgraded on RHEL/CentOS, the configuration file is not automatically upgraded if modifications have been made to it.

In this case the installer (RPM) creates a file called mdicapsrv.rpmnew with the upgraded configuration entries, and this file needs to be merged manually to the actual configuration file.

The configuration file for the server is located in **/etc/mdicapsrv/mdicapsrv.conf**.

After modifying the server configuration file you must restart the MetaDefender ICAP Server service for the changes to take effect. You should use the distribution-standard way to restart the mdicapsrv service.

### [[global] section](/docs/mdicap/configuration/configuration-file#logger-section)

| parameter | default value | required | description |
| --- | --- | --- | --- |
| `icapaddress` | 0.0.0.0 | required | One of the IP addresses of the computer that runs the product to serve ICAP interface Note:   - *** ->** means all interface for both IPV4 and IPv6 - **0.0.0.0** -> means all interface of IPv4 only - **127.0.0.1** -> loopback IPv4 only - **::** -> mean all interface of IPv6 - **::1** -> loopback IPv6 |
| `icapport` | 1344 | required | Designated port number for the ICAP interface. Always listening ICAP Server is always listening on this port on clear text ICAP even if TLS is enabled for the ICAP interface. |
| `icaps_port` | 11344 | optional | Designated port number for the ICAPS interface. Not always listening ICAP Server is listening on this port only if ICAPS is enabled. For details see [3.2 Configuring TLS](/docs/mdicap/configuration/configuring-tls). |
| `restaddress` | 0.0.0.0 | required | One of the IP addresses of the computer that runs the product to serve REST API and web user interface (0.0.0.0 means all interface) |
| `restport` | 8048 | required | Designated port number for the web and REST interface |
| `tempdirectory` | `/var/tmp/mdicapsrv/temp` | optional | Root directory for temporary files creation. A /temp subdirectory is automatically created within a customized directory. For example:   - If /tmp is configured as tempdirectory then - /tmp/temp will be used for creating temporary files |
| `skip_multipart_without_filename` | false | optional | Only accepting "true" / "false" value.  When enabled the ICAP server won't send files from a multipart request for scanning when the given part does not have a filename key in it's own Content-Disposition header |
| `enable_message_header_encoding` | false | optional | Only accepting "true" / "false" value.  When enabled the ICAP server will decode Base64 encoded UTF-8 filenames in HTTP Content-Disposition headers that are misused for MIME Content-Disposition (<https://tools.ietf.org/html/rfc2047>). Details Certain webmail providers misuse HTTP Content-Disposition header for MIME Content-Disposition header and put Base64 encoded strings into it. In this case -after ICAP Server side processing- the file name may be broken or even empty at the downloading side. Enabling this option can counter the situation. |
| `unique_uri_per_service` | false | optional | Only accepting "true" / "false" value.  When setting it to "true", MetaDefender ICAP server will assign unique URIs to each ICAP service (REQMOD, RESPMOD). Only available starting MetaDefender ICAP Server 4.11.0 |
| `blockedmsg_response_type` | html | optional | Only accepting "html" / "json" value.  When setting it to "json", ICAP server will forward entire scan result in JSON received from MetaDefender Core to ICAP client. Only available starting MetaDefender ICAP Server 4.11.0 |
| `max_connections` | 355 | optional | Only accepting value in range of [1, 32767]  Configure to define maximum number of connections returned to OPTIONS method request. Only available starting MetaDefender ICAP Server 4.11.0 |
| `webhook_address` | 0.0.0.0 | required with conditions | Setting IP address for MetaDefender ICAP server webhook callback URI (where MetaDefender Core sends callback response to) (Only available starting MetaDefender ICAP Server 4.11.0)  This setting is mandatory when MetaDefender ICAP server has multiple network interaces on the same machine.  **Use-case 1:** When MetaDefender Core is sitting in a different machine from MetaDefender ICAP Server, then set MetaDefender Core's IP address. For example:  *[global]*  *webhook_address=192.168.1.100*  **Use-case 2:** When MetaDefender ICAP and MetaDefender Core are installed in the same host, then set ***0.0.0.0***  *[global]*  ***webhook_address=0.0.0.0*** |
| `enable_x_client_custom_parser` | false | optional | Enable ICAP custom header, see details: [Custom ICAP Request Header](/docs/mdicap/configuration/configurate-x-client-custom--header) |
| `max_number_x_client_custom` | 16 | optional | Maximum number of custom headers is supported, see details: [Custom ICAP Request Header](/docs/mdicap/configuration/configurate-x-client-custom--header) |
| `max_header_length_x_client_custom` | 128 | optional | Maximum length (in bytes) of each custom header name (excluding `X-Client-Custom-` prefix)  Maximum length (in bytes) of each custom header value  See details: [Custom ICAP Request Header](/docs/mdicap/configuration/configurate-x-client-custom--header) |
| `notify_modified_custom_header` | false | optional | See details: [Custom ICAP Request Header](/docs/mdicap/configuration/configurate-x-client-custom--header) |
| `enable_options_ttl_header` | false | optional | true: enable options_ttl header respond for OPTIONS command false: the options_ ttl header will not return this configuration is supported to integrate with **Oracle ZFS** |
| `set_options_ttl_header_value` | 3600 | optional | [1, MAX int] (in second) |
| `system_info_logging` | false | optional | Only accepting "true" / "false" value.  When setting it to "true", MetaDefender ICAP server will collect system resource information on server where MetaDefender ICAP Server resides to log files  Only available starting MetaDefender ICAP Server 5.1.1 |
| `system_info_logging_interval` | 15 | optional | Set logging interval in second  [1, MAX int] (in second)  Only available starting MetaDefender ICAP Server 5.1.1 |
| `enable_no_content_scan_logging` | true | optional | Only accepting "true" / "false" value (default is "true")  if set to **false**, the ICAP requests with "No Content to Scan" verdict will not be logged to database  Only available from ICAP v5.6.0 |
| `enable_preview_header` | true | optional | Only accepting "true" / "false" value (default is "true")  if set to false, the header "preview" and "Transfer-Preview" will be removed out of response of OPTIONS (for Software AG integration)  Only available from ICAP v5.6.0 |
| `set_options_x_include_value` | X-Client-IP | optional | Used to override the X-include header for OPTIONS response (for GlocalScape integration) The list of below value can be used: X-Client-IP, X-Server-IP, X-Authenticated-User, X-Authenticated-Groups |
| `blockpage_allow _script_or_unsafe_html_tag` | false | optional | Set true to allow script and unsafe HTML tag in custom blockpage, otherwise set to false |
| `enable_x_result_number_header` | false |  | set true to return additional header X-Result-Number otherwise set to false |
| `curlopt_capath` | <empty> | optional | the path in Linux environment which is stored selfsign certificate for MD Core/OCM connection (Used for non-root docker image) |
| `skip_non _standard_encoding_preprocess` | <empty> | optional | List of content-encoding will be ignored decoding before send to MD Core for scanning, seperate by comma E.g: none, other_type |
| `store_first_n_characters_url` | -1 | optional |  |

### [[logger] section](/docs/mdicap/configuration/configuration-file#internal-section)

| key | default value | required | description |
| --- | --- | --- | --- |
| `logfile` | `/var/log/mdicapsrv/mdicapsrv.log` | optional | Full path of a logfile to write log messages to |
| `loglevel` | info | optional | Level of logging. Supported values are: debug, info, warning, error |
| `syslog` |  | optional | Switch on logging to a local ('local') or remote ('protocol://hostname:port') syslog server. (Multiple server can be specified separated with comma)  For **TCP** secure syslog server (support since ICAP v5.8.0) use this format: `tcps://hostname:port` |
| `syslog_level` |  | optional | Level of logging. Supported values are: debug, info, warning, error |
| `override` |  | optional | Override specific log ids to display them on another level e.g.: "1723:error,663:info". Note: when displaying these log ids their original level will remain the same. |
| `capture_traffic` |  | optional | Capture raw TCP traffic in case of bad requests. See [3.5.4 Logging traffic of bad requests](/docs/mdicap/configuration/logging-traffic-of-bad-requests). |
| `cef` | false | optional | If true, the log format is Common Event Format |
| `local_timezone` | false | optional | If true, the times sent in syslog messages will be in the server's local timezone. This does not effect entries in the log file/Windows event log. When syslog is used with cef and local_timezone enabled the timezone name can vary based on the underlying system and it's settings. Examples   - Syslog    - UTC: 2018-09-19T13:07:36Z   - Local: 2018-09-19T15:07:36+02:00 - Syslog with CEF    - UTC: Sep 19 13:12:47 UTC   - Local 1: Sep 19 15:12:47 CEST   - Local 2: Sep 19 15:12:47 Central Europe Daylight Time |
| `nginx_logfile` | `/var/log/mdicapsrv/nginx-mdicapsrv.log` | optional | File name and path to store the NGINX logs. If this value is changed, the /etc/logrotate.d/mdicapsrv should be changed accordingly. |
| `syslog_dateformat` | 1 | optional | Format the datetime of syslog  Value in list: [0, 1, 8, 9]  0: TextDate  1: ISODate  8: RFC2822Date  9: ISODateWithMs |

Note

You should set both of syslog and syslog_level or none of them and you should set both of logfile and loglevel or none of them.

### [[internal] section](/docs/mdicap/configuration/configuration-file#diagnostic-section)

| key | default value | required | description |
| --- | --- | --- | --- |
| `db_connection` | 10 | optional | Define the maximum number of concurrent connections allowed for MetaDefender ICAP to open to work with the PostgreSQL database server. Only available starting MetaDefender ICAP 5.2.0 |
| `skip_first_start_page` | false | optional | When it is set to true, the server will automatically skip the first start page on the new version |
| `sso_cross_instance_enabled` | false | optional | When it is set to true, it applies a single SSO configuration across all MD ICAP Server instances that use the same Shared Database Mode. This ensures consistency when multiple MD ICAP Server instances are deployed behind a load balancer and accessed via the same URL |

### [[diagnostic] section](/docs/mdicap/configuration/configuration-file#windows)

| key | default value | required | description |
| --- | --- | --- | --- |
| `enable_icap_test_client` | false | optional | Enables the built-in ICAP Test Client diagnostic tool, which lets administrators send a test file directly to the ICAP Server and inspect the scan result without needing an external ICAP client. When this is off (default), the Test Client API is unavailable (calls return `404`) and the Diagnostics tab is hidden from the web UI. Turn this on when you need the tool for troubleshooting or verifying server configuration. |
| `icap_test_client_allow_custom_target` | false | optional | Controls whether the Test Client can send its test scan to a remote ICAP endpoint instead of the local server. By default (off), the tool can only test the local ICAP Server; any attempt to specify a remote host is rejected with `403`. Only enable this if you need to use the tool to test connectivity to another ICAP Server on your network — since allowing remote targets carries an SSRF risk, keep it off unless you trust the network the server sits on. |
| `icap_test_client_history_retention_duration` | 300 | optional | Sets how long (in seconds) a completed test's history entry and its download token stay available after the test finishes. Once this period passes, the entry disappears from the history list and the download link stops working. The default of 300 seconds (5 minutes) is enough for a quick review; raise it (up to 86400 seconds / 24 hours) if admins need more time before revisiting results. |
| `icap_test_client_history_content_display_max_bytes` | 1024 | optional | Sets the maximum size, in bytes, of scanned content shown as an inline preview in the test history view. Content larger than this is not rendered inline — instead the UI offers it as a downloadable file. The default of 1024 bytes keeps the preview compact; increase it (up to 1 MB) if you routinely need to inspect larger raw content directly in the browser. |
| `icap_test_client_req_max_file_count` | 5 | optional | Limits how many files can be included in a single test request. Requests with more files than this are rejected before being sent to the scan engine. The default of 5 suits typical ad-hoc testing; increase it (up to 100) if you need to batch-test larger sets of files at once. |
| `icap_test_client_req_max_total_size` | 50 | optional | Limits the combined size (in MB) of all files submitted together in one test request. The UI checks this locally and blocks the upload before sending if the total is over the limit, so no time is wasted on a request that would be rejected anyway. Note the effective cap is actually the smaller of this value and the target workflow's own scan-size limit — raising this setting alone won't bypass a stricter limit set on the destination workflow. |

## [Windows](/docs/mdicap/configuration/configuration-file#windows-config-file-location)

The configuration for the server is located in **Windows Registry**.

After modifying the server configuration file you must restart the MetaDefender ICAP Server service in order for the changes to take effect.

Default logging target is Windows event log with default level of info (see below).

### [HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\ICAP Server\global](/docs/mdicap/configuration/configuration-file#hkey_local_machinesoftwareopswaticap-serverglobal)

| parameter | default value | type | required | description |
| --- | --- | --- | --- | --- |
| `icapaddress` | 0.0.0.0 | string value | required | One of the IP addresses of the computer that runs the product to serve ICAP interface (0.0.0.0 means all interface)  Note:   - *** ->** means all interface for both IPV4 and IPv6 - **0.0.0.0** -> means all interface of IPv4 only - **127.0.0.1** -> loopback IPv4 only - **::** -> mean all interface of IPv6 - **::1** -> loopback IPv6 |
| `icapport` | 1344 | string value | required | Designated port number for the ICAP interface Always listening ICAP Server is always listening on this port on clear text ICAP even if TLS is enabled for the ICAP interface. |
| `icaps_port` | 11344 | string value | optional | Designated port number for the ICAPS interface. Not always listening ICAP Server is listening on this port only if ICAPS is enabled. For details see [3.2 Configuring TLS](/docs/mdicap/configuration/configuring-tls). |
| `restaddress` | 0.0.0.0 | string value | required | One of the IP addresses of the computer that runs the product to serve REST API and web user interface (0.0.0.0 means all interface) |
| `restport` | 8048 | string value | required | Designated port number for the web and REST interface |
| `tempdirectory` | `C:\Program Files\OPSWAT\Metadefender ICAP Server\data\temp` | string value | optional | Root directory for temporary files creation. A \temp subdirectory is automatically created within a customized directory. For example:   - If C:\Temp is configured as tempdirectory then - C:\Temp\temp will be used for creating temporary files |
| `skip_multipart_without_filename` | false | string value | optional | Only accepting "true" / "false" value.  When enabled the MetaDefender ICAP server won't send files from a multipart request for scanning when the given part does not have a filename key in it's own Content-Disposition header |
| `enable_message_header_encoding` | false | string value | optional | Only accepting "true" / "false" value.  When enabled the MetaDefender ICAP server will decode Base64 encoded UTF-8 filenames in HTTP Content-Disposition headers that are misused for MIME Content-Disposition (<https://tools.ietf.org/html/rfc2047>). Details Certain webmail providers misuse HTTP Content-Disposition header for MIME Content-Disposition header and put Base64 encoded strings into it. In this case -after ICAP Server side processing- the file name may be broken or even empty at the downloading side. Enabling this option can counter the situation. |
| `unique_uri_per_service` | false | string value | optional | Only accepting "true" / "false" value.  When setting it to "true", MetaDefender ICAP server will assign unique URIs to each ICAP service (REQMOD, RESPMOD). Only available starting MetaDefender ICAP Server 4.11.0 |
| `blockedmsg_response_type` | html | string value | optional | Only accepting "html" / "json" value.  When setting it to "json", ICAP server will forward entire scan result in JSON received from MetaDefender Core to ICAP client. Only available starting MetaDefender ICAP Server 4.11.0 |
| `max_connections` | 355 | string value | optional | Only accepting value in range of [1, 32767]  Configure to define maximum number of connections returned to OPTIONS method request. Only available starting MetaDefender ICAP Server 4.11.0 |
| `webhook_address` | 0.0.0.0 | string value | required with conditions | Setting IP address for MetaDefender ICAP server webhook callback URI (where MetaDefender Core sends callback response to) (Only available starting MetaDefender ICAP Server 4.11.0)  This setting is mandatory when MetaDefender ICAP server has multiple network interaces on the same machine.  **Use-case 1:** When MetaDefender Core is sitting in a different machine from MetaDefender ICAP Server, then set MetaDefender Core's IP address. For example:  ***[global]***  ***webhook_address=192.168.1.100***  **Use-case 2:** When MetaDefender ICAP and MetaDefender Core are installed in the **same host**, then set ***127.0.0.1***  *[global]*  ***webhook_address=127.0.0.1*** |
| `enable_x_client_custom_parser` | false | string value | optional | Enable ICAP custom header, see details: [Custom ICAP Request Header](/docs/mdicap/configuration/configurate-x-client-custom--header) |
| `max_number_x_client_custom` | 16 | string value | optional | Maximum number of custom headers is supported, see details: [Custom ICAP Request Header](/docs/mdicap/configuration/configurate-x-client-custom--header) |
| `max_header_length_x_client_custom` | 128 | string value | optional | Maximum length (in bytes) of each custom header name (excluding `X-Client-Custom-` prefix)  Maximum length (in bytes) of each custom header value  See details: [Custom ICAP Request Header](/docs/mdicap/configuration/configurate-x-client-custom--header) |
| `notify_modified_custom_header` | false | string value | optional | See details: [Custom ICAP Request Header](/docs/mdicap/configuration/configurate-x-client-custom--header) |
| `maxstdio` | - 512 for MD ICAP Server 5.1.1 and older - 4096 since MD ICAP Server v5.2.0 | string value | optional | Define maximum number of files can be opened simultaneously on Windows. The acceptable range is :   - [512, 2048] for MD ICAP Server 5.1.1 and older. - [512, 8192] since MD ICAP Server 5.2.0 |
| `enable_options_ttl_header` | false | string value | optional | true: enable options_ttl header respond for OPTIONS command false: the options_ttl header will not return  this configuration is supported to integrate with **Oracle ZFS** |
| `set_options_ttl_header_value` | 3600 | string value | optional | [1, MAX int] (in second) |
| `system_info_logging` | false | string value | optional | When setting it to "true", MetaDefender ICAP server will collect system resource information on server where MetaDefender ICAP Server resides to log files  Only available starting MetaDefender ICAP Server 5.1.1 |
| `system_info_logging_interval` | 15 | string value | optional | Only available starting MetaDefender ICAP Server 5.1.1 |
| `enable_no_content_scan_logging` | true | string value | optional | Only accepting "true" / "false" value (default is "true")  if set to false, the ICAP requests with "No Content to Scan" verdict will not be logged to database  Only available from ICAP v5.6.0 |
| `enable_preview_header` | true | string value | optional | Only accepting "true" / "false" value (default is "true")  if set to false, the header "preview" and "Transfer-Preview" will be removed out of response of OPTIONS (for Software AG integration)  Only available from ICAP v5.6.0 |
| `curlsslopt_revoke_best_effort` | true | string value | optional | Support since ICAP v5.8.0 (Windows only)   - true: Ignore revocation server checking incase can not communicate to revocation server - false: return false when can not communicate to revocation server |
| `set_options_x_include_value` | X-Client-IP | String value | optional | Used to override the X-include header for OPTIONS response (for GlocalScape integration) The list of below value can be used: X-Client-IP, X-Server-IP, X-Authenticated-User, X-Authenticated-Groups |
| `blockpage_allow _script_or_unsafe_html_tag` | false | String value | optional | Set true to allow script and unsafe HTML tag in custom blockpage, otherwise set to false |
| `enable_x_result_number_header` | false | String value | optional | set true to return additional header X-Result-Number otherwise set to false |
| `skip_non_standard_encoding_preprocess` | <empty> | String value | optional | List of content-encoding will be ignored decoding before send to MD Core for scanning, seperate by comma E.g: none, other_type |
| `store_first _n_characters_url` | -1 | String value |  | Accept range [-1, 1024]   - default -1: will not trim the URL before stored - 0: the URL will be repaced by "..." - Max: 1024 |

### [HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\ICAP Server\logger](/docs/mdicap/configuration/configuration-file#hkey_local_machinesoftwareopswaticap-serverlogger)

| parameter | default value | type | required | description |
| --- | --- | --- | --- | --- |
| logfile |  | string value | optional | Location of a logfile to write log messages to |
| loglevel |  | string value | optional | Level of logging. Supported values are: debug, info, warning, error |
| log_rotation | false | string value | optional | Supported values:   - 0 or false: ICAP logs are not rotated - 1 or true:    - Rotation process will be performed every day, regardless of file size.   - Limit rotated log to be stored is 30 files, the oldest log will be deleted if file number reaches the limit.   - Rotated log name format: <logname>-<yyyyMMdd>.gz (e.g.: icap.log-20200330.gz), all saved in same location with what you set in **logfile.**   - All generated log packages included in MetaDefender ICAP Server support package. |
| wineventlog_level | info | string value | optional | Level of logging. Supported values are: debug, info, warning, error |
| syslog |  | string value | optional | Value can only by in form of 'protocol://<hostname>:<port>'. (Multiple server can be specified separated with comma)  For **TCP** secure syslog server (support since ICAP v5.8.0) use this format: `tcps://hostname:port` |
| syslog_level |  | string value | optional | Level of logging. Supported values are: debug, info, warning, error |
| override |  | string value | optional | Override specific log ids to display them on another level e.g.: "1723:error,663:info" . Note: when displaying these log ids their original level will remain the same. |
| capture_traffic |  | DWORD | optional | Capture raw TCP traffic in case of bad requests. See [3.5.4 Logging traffic of bad requests](/docs/mdicap/configuration/logging-traffic-of-bad-requests). |
| cef | false | string value | optional | If true, the log format is Common Event Format |
| local_timezone | false | string value | optional | If true, the times sent in syslog messages will be in the server's local timezone. This does not effect entries in the log file/Windows event log. When syslog is used with cef and local_timezone enabled the timezone name can vary based on the underlying system and it's settings. Examples   - Syslog    - UTC: 2018-09-19T13:07:36Z   - Local: 2018-09-19T15:07:36+02:00 - Syslog with CEF    - UTC: Sep 19 13:12:47 UTC   - Local 1: Sep 19 15:12:47 CEST   - Local 2: Sep 19 15:12:47 Central Europe Daylight Time |
| nginx_logfile | [installdir] ginx ginx.log | string value | optional | File name and path to store the NGINX logs. |
| nginx_log_rotation | false | string value | optional | If true, the log file specified by the *nginx_logfile* entry is rotated after 24 hours from creation. The last 30 log files are stored, the oldest log file will be deleted if number of files reaches the limit. Naming convention The rotated log files are named according to the following convention: <file name from nginx_logfile entry>-<yyyyMMdd>.gz. **Example** nginx-mdicapsrv-20200730-<123>.gz Support package All stored log files are included in MetaDefender ICAP's support package. |
| syslog_dateformat | 1 | string value | optional | Format the datetime of syslog  Value in list: [0, 1, 8, 9]  0: TextDate  1: ISODate  8: RFC2822Date  9: ISODateWithMs |

Note

You should set both of syslog and syslog_level or none of them and you should set both of logfile and loglevel or none of them.

### [HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\ICAP Server\internal](/docs/mdicap/configuration/configuration-file#hkey_local_machinesoftwareopswaticap-serverinternal)

| key | default value | type | required | description |
| --- | --- | --- | --- | --- |
| db_connection | 10 | string value | optional | Define maximum number of concurrent connections allows MetaDefender Core to open to work with PostgreSQL database server. Only available starting MetaDefender Core 5.2.0 |
| skip_first_start_page | false | Boolean | optional | - true: start page will be skipped - false: will keep start page |

### [HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\ICAP Server\diagnostic](/docs/mdicap/configuration/configuration-file#hkey_local_machinesoftwareopswaticap-serverdiagnostic)

| key | default value | type | required | description |
| --- | --- | --- | --- | --- |
| `enable_icap_test_client` | false | string value | optional | Enables the built-in ICAP Test Client diagnostic tool, which lets administrators send a test file directly to the ICAP Server and inspect the scan result without needing an external ICAP client. When this is off (default), the Test Client API is unavailable (calls return `404`) and the Diagnostics tab is hidden from the web UI. Turn this on when you need the tool for troubleshooting or verifying server configuration. |
| `icap_test_client_allow_custom_target` | false | string value | optional | Controls whether the Test Client can send its test scan to a remote ICAP endpoint instead of the local server. By default (off), the tool can only test the local ICAP Server; any attempt to specify a remote host is rejected with `403`. Only enable this if you need to use the tool to test connectivity to another ICAP Server on your network — since allowing remote targets carries an SSRF risk, keep it off unless you trust the network the server sits on. |
| `icap_test_client_history_retention_duration` | 300 | string value | optional | Sets how long (in seconds) a completed test's history entry and its download token stay available after the test finishes. Once this period passes, the entry disappears from the history list and the download link stops working. The default of 300 seconds (5 minutes) is enough for a quick review; raise it if admins need more time before revisiting results. |
| `icap_test_client_history_content_display_max_bytes` | 1024 | string value | optional | Sets the maximum size, in bytes, of scanned content shown as an inline preview in the test history view. Content larger than this is not rendered inline — instead the UI offers it as a downloadable file. The default of 1024 bytes keeps the preview compact; increase it if you routinely need to inspect larger raw content directly in the browser. |
| `icap_test_client_req_max_file_count` | 5 | string value | optional | Limits how many files can be included in a single test request. Requests with more files than this are rejected before being sent to the scan engine. The default of 5 suits typical ad-hoc testing; increase it if you need to batch-test larger sets of files at once. |
| `icap_test_client_req_max_total_size` | 50 | string value | optional | Limits the combined size (in MB) of all files submitted together in one test request. The UI checks this locally and blocks the upload before sending if the total is over the limit, so no time is wasted on a request that would be rejected anyway. Note the effective cap is actually the smaller of this value and the target workflow's own scan-size limit — raising this setting alone won't bypass a stricter limit set on the destination workflow. |
