<!-- source: https://www.opswat.com/docs/filescan/3.1.1/configuration/healthcheck -->

# Healthcheck

At the **Admin Panel > Setting > Configurations > Healthcheck** settings, various settings related to monitoring can be configured.

Configuration options

| Field | Description |
| --- | --- |
| `HCS_PERIOD_MIN` | The minimum time interval, in **minutes**, between health check operations. |
| `HCS_RETENTION_DAYS` | The number of **days** for which health check records are retained in the system. |
| `HCS_PROXY_HOST` | The hostname or IP address of the proxy server used for health checks. |
| `HCS_FSIO_URI` | The Sandbox URI specifying the endpoint for health check operations. |
| `SCAN_QUEUE_LONG_CHECK_TIME_INTERVAL` ¹ | Seconds between pings of long running check. Max of it or `KEEP_JOB_RESULT_SECONDS` is used |
| `SCAN_QUEUE_QUICK_CHECK_STEPS_INTERVAL`¹ | Scan iterations between quick checks. Result time is calculated to be bigger then `KEEP_JOB_RESULT_SECONDS` |
| `SCAN_QUEUE_ALLOWED_CHECKS_MISSED` ¹ | Allowed checks amount missed to still consider queue healthy |

¹Healthcheck of scan queues. Final values are calculated to be bigger then `KEEP_JOB_RESULT_SECONDS` = 10

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
