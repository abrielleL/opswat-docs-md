<!-- source: https://www.opswat.com/docs/mdemail/configuration/registry-configuration -->

# Registry configuration

Some configuration options of the server are available in Windows Registry.

Note

After modifying the server configuration entries in the Windows Registry, you must restart the Metadefender Email Gateway Security service in order for the changes to take effect.

Default logging target is Windows Event Log with default level of info (see below).

Ambiguous path values

Nginx may interpret certain Windows path elements in an unexpected way.

For example the '\n' substring in a path value is interpreted as a new line character, '\t' substring in a path value is interpreted as a tab character (e.g. *C:\Windows\temp* is interpreted as *C:\Windows emp*).

To address this, in path values forward slash '/' may be used instead of backslash ''.

## [HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metadefender Email Security](/docs/mdemail/configuration/registry-configuration#hkey_local_machinesoftwareopswatmetadefender-email-security)

| Parameter | Default value | Type | Required | Description |
| --- | --- | --- | --- | --- |
| ExchangeMode | N/A | N/A | N/A | This value is set when Email Gateway Security is installed in Exchange plugin mode. For details see [Integrations/Onsite Microsoft Exchange deployment](/docs/mdemail/integrations/onsite-microsoft-exchange-deployment).  *Do not change this value manually!* |
| InstallationFolder | C:\Program Files\OPSWAT\MetaDefender Email Security\ | string | N/A | This value is by the Email Gateway Security installation.  *Do not change this value manually!* |
| external_quarantine_block |  | dword | optional | Enable quarantining the original copy of blocked emails on an other mail server. For details see [Configuration/Quarantine configuration](/docs/mdemail/configuration/quarantine-configuration).  *If the parameter does not exist or if it is 0, then the internal quarantine will be used in case of blocked emails.* |
| external_quarantine_sanitize |  | dword | optional | Enable quarantining the original copy of sanitized emails on an other mail server. For details see [Configuration/Quarantine configuration](/docs/mdemail/configuration/quarantine-configuration).  *If the parameter does not exist or if it is 0, then the internal quarantine will be used in case of sanitized emails.* |
| sender_helo_domain | *computer name* | string | optional | The fully qualified domain name (FQDN) that Email Gateway Security will send in HELO/EHLO commands to relay SMTP servers to customize SMTP greetings. Besides this FQDN the external IP address of Email Security will also be sent. For details see section *Opening and closing* in [RFC 821](https://tools.ietf.org/html/rfc821).  *If the parameter does not exist or if it is empty then the computer name of Email Gateway Security is sent in HELO/EHLO.* |
| receiver_helo_domain | *computer name* | string | optional | The fully qualified domain name (FQDN) that Email Gateway Security will send in HELO/EHLO commands to SMTP clients to customize SMTP greetings. For details see section *Opening and closing* in [RFC 821](https://tools.ietf.org/html/rfc821).  *If the parameter does not exist or if it is empty then the computer name of Email Gateway Security is sent in the response to a HELO/EHLO.* |
| exchange_exclude_probe_emails |  | dword | optional | Microsoft Exchange Server sends probe email messages to monitor the health status of the email processing components. This probe messages can, however, fill [Operating/Email History](/docs/mdemail/operating/email-history). Setting this parameter to 0 will enable listing Exchange probe messages in **Audit > Email History**.  *If the parameter does not exist or if it is 1, then Exchange probe messages are not listed in* ***Audit > Email History***____ ***__*** _**** __ _**** _**** __ _**** _**** __ ***** ***** *** _ __ . No service restart is needed There is no need to restart any services for this setting to take effect, because the transport agent reads and applies this registry setting for each email.* |
| processing_threshold | 75 | dword | optional | This parameter limits the number of emails with "Processing" status at the same time. If this parameter is not present then this number is 75 by default. Setting this value lower can reduce the processing load on both Email Gateway Security and Core.  *If the parameter is 0 then the throttling is disabled.* |
| concurrency_threshold | N/A | dword | optional | This parameter limits the number of concurrent threads submitting emails to MetaDefender Core for scanning. Example By default Email Gateway Security submits emails to Core on several threads. This causes the components of different emails to mix in the Core queue.  *If this parameter is set to 1, then contents are sent to Core email by email with no overlapping, whereas If the parameter is 0 then no direct limitation is applied.* |
| in_folder_timer_interval | 1000 | dword | optional | Interval –in milliseconds– between polling of new emails. |
| max_email_insert_count | 100 | dword | optional | Maximum number of emails to insert into the database in a single batch. |
| processing_task_timeout | 10 | string | optional | The email processing task timeout (in minutes). If this timer elapses, Email Gateway Security will give up trying to process the email. |

## [HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metadefender Email Security\global](/docs/mdemail/configuration/registry-configuration#hkey_local_machinesoftwareopswatmetadefender-email-securityglobal)

| Parameter | Default value | Type | Required | Description |
| --- | --- | --- | --- | --- |
| restaddress |  | string | required | One or all of the IP addresses of the computer that runs the product to serve the web user interface.  *Supported value: * : all IPv4 and IPv6 interfaces One specific IPv4 or IPv6 address : the specific IPv4 or IPv6 address*  *(* = all interfaces)* |
| restport | 8058 | string | required | Designated port number for the web management console (REST) interface |
| public_rescan_port | N/A | string | optional | Designated port number for the rescan functionality web and REST interface.  *Rescan functionality is always -even if this value is defined- available on the restport. For details about rescan__see* [*Operating/Password protected attachments*](/docs/mdemail/operating/password-protected-attachments)*.* |
| recipient_quarantine_port | N/A | string | optional | Designated port number for the Recipient Quarantine functionality web and REST interface. The Recipient Quarantine feature is not available unless this port is configured. For details see [Recipient Quarantine configuration](/docs/mdemail/configuration/recipient-quarantine) and the Recipient Quarantine subpage under [Email recipient guide](/docs/mdemail/operating/recipient-guide). |
| smtpaddress |  | string | optional | One or all of the IP addresses of the computer that runs the product to serve the SMTP interface (* means all interfaces)  *Supported values Missing or * : all IPv4 and IPv6 interfaces One specific IPv4 or IPv6 address : the specific IPv4 or IPv6 address* |
| public_id_length | 32 | string | optional | Length of id generated for public rescan links. Allowed values are 32-64. |

## [HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metadefender Email Security\logger](/docs/mdemail/configuration/registry-configuration#hkey_local_machinesoftwareopswatmetadefender-email-securitylogger)

| Parameter | Default value | Type | Required | Description |
| --- | --- | --- | --- | --- |
| logfile | <InstallationFolder>\data\logs\mdemailsecurity.log | string | optional | Location of a log file to write log messages to. If the parameter does not exist, then no logs are written to any logfile.  *Empty string is not allowed as a value.* |
| loglevel | info | string | optional | Level of logging. Supported values are: `debug, info, warning, error, soc`. |
| wineventlog_level | info | string | optional | Level of logging. Supported values are: `debug, info, warning, error, soc`. If the parameter does not exist, then no logs are written to the Windows Logs. |
| syslog |  | string | optional | Value can only be in form of `:<protocol>://<hostname>:<port>`. If the parameter does not exist, then no logs are written to syslog. (Multiple server can be specified separated with comma).  The `protocol` may be:   - `udp` , - `tcp` , - `ssl` .   For the `ssl` option the `syslog_nosslverify`, the `syslog_clientcert`and the `syslog_clientkey`options are supported, too. For details see below. |
| syslog_level |  | string | optional | Level of logging. Supported values are: `debug, info, warning, error, soc`. |
| syslog_nosslverify |  | string | optional | Supported values: `true` or `false` . If `true` and syslog is enabled and the syslog `protocol` is `ssl` , Email Gateway Security won’t verify the syslog server's certificate. |
| syslog_clientcert |  | string | optional | Path to the client side certificate in PEM format.  If syslog is enabled and the syslog `protocol` is `ssl` and certificate based client authentication is needed, Email Gateway Security will send the file with the configured path as the client certificate. |
| syslog_clientkey |  | string | optional | Path to the client side private key pair of `syslog_clientcert` in PEM format.  If syslog is enabled and the syslog `protocol` is `ssl` and certificate based client authentication is needed, Email Gateway Security will use the file with the configured path as private key during the client authentication. |
| override |  | string | optional | Override specific log ids to display them on another level e.g.: "1723:error,663:info". Note: when displaying these log ids their original level will remain the same.  *Empty string is allowed as a value.* |
| cef | false | string | optional | If true, the log format is Common Event Format. |
| cef_ms_ts | false | string | optional | If true (and `cef` is enabled, too), CEF logs will have timestamps in milliseconds. By default, CEF logs have timestamps in seconds. |
| local_timezone | false | string | optional | If true, the times sent in syslog messages will be in the server's local time zone. This does not effect entries in the log file/Windows event log. When syslog is used with cef and local_timezone enabled the time zone name can vary based on the underlying system and it's settings. Examples   - Syslog    - UTC: 2018-09-19T13:07:36Z   - Local: 2018-09-19T15:07:36+02:00 - Syslog with CEF    - UTC: Sep 19 13:12:47 UTC   - Local 1: Sep 19 15:12:47 CEST   - Local 2: Sep 19 15:12:47 Central Europe Daylight Time |
| nginx_logfile | <InstallationFolder>\nginx \nginx.log | string | optional | File name and path to store the Nginx logs. |
| log_rotation | true | string | optional | If true, the log file specified by the *logfile* entry is rotated after 24 hours from creation.  The last 30 log files are stored, the oldest log file will be deleted if number of files reaches the limit. The *logfile* entry must be set for this option to work.  *The rotated log files are named according to the following convention: <file name from logfile entry>-<yyyyMMdd>-<nnn>.gz The trailing three digits (<nnn>) ensure that the file name is unique.*  *Example: mdemailsecurity-20200525.gz*  *All stored log files are included in MetaDefender Email Gateway Security's support package.* |
| nginx_log_rotation | false | string | optional | If true, the log file specified by the *nginx_logfile* entry is rotated after 24 hours from creation.  The last 30 log files are stored, the oldest log file will be deleted if number of files reaches the limit.  *The rotated log files are named according to the following convention: <file name from nginx_logfile entry>-<yyyyMMdd>-<nnn>.gz The trailing three digits (<nnn>) ensure that the file name is unique.*  *Example nginx-20200730.gz*  *All stored Nginx log files are included in MetaDefender Email Gateway Security's support package.* |

Related values

You must set both of *syslog* and *syslog_level* or none of them, and you must set both of *logfile* and *loglevel* or none of them.

## [HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metadefender Email Security\database](/docs/mdemail/configuration/registry-configuration#hkey_local_machinesoftwareopswatmetadefender-email-securitydatabase)

| Parameter | Default value | Type | Required | Description |
| --- | --- | --- | --- | --- |
| instance | *computer name* | string | required | This parameter is the name of the Email Gateway Security instance in scalable mode. This parameter is relevant when upgrading a standalone instance to scalable.  For details see [Scalable deployment operation](/docs/mdemail/operating/scalable-deployment-operation)*.* |
| max_connections | 30 | dword | required | Controls the connection pool size against the Postgres database. This value should correlate with the settings on the database side. Configuring out-of-bounds values will be clamped to the respective minimum or maximum value. Valid range is between 20 - 100 (inclusive). |
| db_mode | N/A | dword | required | Specifies if the application should run with its own hosted Postgres database, or connect to a customer-managed one. 0 means self-hosted, 1 means external. Valid range is 0 or 1. |
| db_port | N/A | dword | required | Specifies on which port the Postgres database is accessible. Valid range is 1024 - 65535 (inclusive). |
| db_host | N/A | string | required | Specifies where (on which host) the PostgreSQL database is accessible. Valid values are IP addresses or FQDNs. |
| db_user_name | N/A | string | required | The user that will be used to connect to the PostgreSQL database. Valid values are single word usernames. |

## [HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metadefender Email Security\s](https://docs.opswat.com/mdemail/configuration#hkey_local_machinesoftwareopswatmetadefender-email-securityinternal)mtp_config

| Parameter | Default value | Type | Required | Description |
| --- | --- | --- | --- | --- |
| enable_chunking_support | 0 | string | optional | Set to 1 to enable SMTP server BDAT verb. For details, see [RFC 3030](https://datatracker.ietf.org/doc/html/rfc3030) |
| monitor_server_name | localhost | string | optional | Override the server name used when monitoring the MetaDefender Email Gateway Security's inbound SMTP server. This might be required when TLS is used and the certificate subject lacks *localhost* entry. |
| timeout_seconds | 120 | dword | optional | When `smtp_config/timeout_seconds` is set to a positive integer in the Registry, the service applies that value as the SMTP network operation timeout for all outgoing SMTP connections. |

## [HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metadefender Email Security\internal](https://docs.opswat.com/mdemail/configuration#hkey_local_machinesoftwareopswatmetadefender-email-securityinternal)

| Parameter | Default value | Type | Required | Description |
| --- | --- | --- | --- | --- |
| antispam_proxy_ip | N/A | string | optional | IP address of the HTTP proxy to reach the anti-spam service. For details about the location of the anti-spam service see [Prerequisites/External services](/docs/mdemail/installation/prerequisites#external-services). |
| antispam_proxy_port | N/A | string | optional | TCP port of the HTTP proxy to reach the anti-spam service. For details about the location of the anti-spam service see [Prerequisites/External services](/docs/mdemail/installation/prerequisites#external-services). |
| quarantine_report_hourly_minute | 00 | string | optional | The minute in each hour when hourly quarantine reports are to be assembled and sent. The valid range is 00-59. For details about quarantine reports see [Quarantine reports](/docs/mdemail/operating/quarantine-reports). |
| quarantine_report_daily_time | 12:00 (midday) | string | optional | The time on each day when daily quarantine reports are to be assembled and sent. The valid range is 00:00-23:59. For details about quarantine reports see [Quarantine reports](/docs/mdemail/operating/quarantine-reports). |
| hsts_max_age | 31536000 (1 year) | string | optional | HTTP Strict-Transport-Security response header (HSTS) max age value in seconds. |
| html_prioritize_header_charset | 0 | dword | optional | Set to 1 to prioritize header charset for HTML body content (instead of `<meta>` charset tag). |
| scan_tnef | 1 | dword | optional | Set to 0 to prevent sending unparsed TNEF (winmail.dat) for scanning |
| add_scan_headers | 0 | dword | optional | Set to 1 to prevent Email Gateway Security adding any diagnostics headers to inbound emails. |
| ignore_certificate_revocation_list | 0 | dword | optional | Set to 1 to skip certificate revocation lists when validating certificates |
| spf_dns_servers | N/A | multi-string | optional | List of DNS servers to be used by Sender Policy Framework (SPF) component |
| domain_lookup_level | N/A | string | optional | This option controls whether Email Gateway Security should perform a reverse DNS lookup on the sending IP address as an anti-phishing measure.  When enabled, in case the sending IP address does not belong to a domain (any domain), the email can be classified as *Possible phishing* or *Phishing* based on the value of this option. Supported values:   - `disabled`: reverse DNS lookup not performed - `possible phishing`: reverse DNS lookup performed, and if no domain is returned then the email is classified as *Possible phishing* and handled according to the *Potential Phishing* settings - `phishing`: reverse DNS lookup performed, and if no domain is returned then the email is classified as *Phishing* and handled according to the *Known Phishing* settings   The reverse DNS lookup uses the DNS server that is set in the `spf_dns_servers`option abpve.  For details about classifications see [Email classifications](/docs/mdemail/operating/email-classifications).  For details about handling Potential Phishing and Known Phishing see [Anti-phishing and anti-spam](/docs/mdemail/configuration/policy#anti-phishing-and-anti-spam). |
| dkim_phishing_verdicts | - Invalid | multi-string | optional | This option configures what DKIM verification results will result in the email being classified as *Phishing* and handled according to the *Known Phishing* settings. The available results are:   - No signature - Invalid - Error   For details about classifications see [Email classifications](/docs/mdemail/operating/email-classifications).  For details about handling Potential Phishing and Known Phishing see [Anti-phishing and anti-spam](/docs/mdemail/configuration/policy#anti-phishing-and-anti-spam). |
| dkim_possible_phishing_verdicts | N/A | multi-string | optional | This option configures what DKIM verification results will result in the email being classified as *Possible phishing* and handled according to the *Potential Phishing* settings.  The available results are:   - No signature - Invalid - Error   For details about classifications see [Email classifications](/docs/mdemail/operating/email-classifications).  For details about handling Potential Phishing and Known Phishing see [Anti-phishing and anti-spam](/docs/mdemail/configuration/policy#anti-phishing-and-anti-spam). |
| spf_phishing_verdicts | - Fail - Soft fail | multi-string | optional | This option configures what SPF check results will result in the email being classified as *Phishing* and handled according to the *Known Phishing* settings. The available results are:   - No record - Neutral - Soft fail - Fail - Error   For details about classifications see [Email classifications](/docs/mdemail/operating/email-classifications).  For details about handling Potential Phishing and Known Phishing see [Anti-phishing and anti-spam](/docs/mdemail/configuration/policy#anti-phishing-and-anti-spam). |
| spf_possible_phishing_verdicts | N/A | multi-string | optional | This option configures what SPF check results will result in the email being classified as *Possible phishing* and handled according to the *Potential Phishing* settings.  The available results are:   - No record - Neutral - Soft fail - Fail - Error   For details about classifications see [Email classifications](/docs/mdemail/operating/email-classifications).  For details about handling Potential Phishing and Known Phishing see [Anti-phishing and anti-spam](/docs/mdemail/configuration/policy#anti-phishing-and-anti-spam). |
| dmarc_enforcement_phishing_verdicts | Reject Quarantine | multistring | optional | This option configures what DMARC policies will result in the email being classified as *Phishing* and handled according to the *Known Phishing* settings. The available policies are:   - None - Reject - Quarantine   For details about classifications see [Email classifications](/docs/mdemail/operating/email-classifications).  For details about handling Potential Phishing and Known Phishing see [Anti-phishing and anti-spam](/docs/mdemail/configuration/policy#anti-phishing-and-anti-spam). |
| dmarc_enforcement_possible_phishing_verdicts | N/A | multistring | optional | This option configures what DMARC policies will result in the email being classified as *Possible phishing* and handled according to the *Potential Phishing* settings.  The available policies are:   - None - Reject - Quarantine   For details about classifications see [Email classifications](/docs/mdemail/operating/email-classifications).  For details about handling Potential Phishing and Known Phishing see [Anti-phishing and anti-spam](/docs/mdemail/configuration/policy#anti-phishing-and-anti-spam). |
| preserve_eml_content_type | false | string | optional | When this option is *true*, Email Gateway Security will preserve the `Content-type` in the MIME section of attached `.eml` files. This is a workaround that can prevent Microsoft Exchange rejecting large `.eml` attachments after being processed by MetaDefender Core's Archive Compression and Extraction utility modules. |
| telemetry_export_interval_ms | 60000 | dword | optional | Interval of metric exports towards the configured collectors, in milliseconds. Valid range is between 1000 - 3600000 (inclusive, i.e. one second to one hour). Must be greater than `telemetry_export_timeout_ms` |
| `telemetry_export_timeout_ms` | 10000 | dword | optional | Timeout of a metric export attempt, in milliseconds. Valid range is between 0 - 60000 (inclusive). Values of 0 or less fall back to the default. Must be less than `telemetry_export_interval_ms` |

## [HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metadefender Email Database\logger](/docs/mdemail/configuration/registry-configuration#hkey_local_machinesoftwareopswatmetadefender-email-databaselogger)

This key is to configure the logging options of the `OPSWAT MetaDefender Email Gateway Security Database Server` service. The same options are available as in the *HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metadefender Email Security\logger* section above.

OPSWAT MetaDefender Email Gateway Security Database Server service

This service operates the embedded PostgreSQL database in case of a standalone database deployment. For details see [Standalone deployment](/docs/mdemail/installation/standalone-deployment).

## [HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metadefender Email Database\database](/docs/mdemail/configuration/registry-configuration#hkey_local_machinesoftwareopswatmetadefender-email-databasedatabase)

This key is to configure the database settings of the `OPSWAT MetaDefender Email Gateway Security Database Server` service. The same options are available as in the *HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metadefender Email Security\database* section above.

OPSWAT MetaDefender Email Gateway Security Database Server service

This service operates the embedded PostgreSQL database in case of a standalone database deployment. For details see [Standalone deployment](/docs/mdemail/installation/standalone-deployment).

Configuration settings

This key must mirror the settings in *HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Metadefender Email Security\database* so that the database can operate correctly.

Modify settings under this key with care!
