<!-- source: https://www.opswat.com/docs/filescan/3.1.1/configuration/jobs -->

# Jobs

In the **Admin Panel > Setting > Configurations > Jobs** settings, jobs can be parameterized, such as the number and timing of retries, or the maximum number of database queries running in parallel.

Configuration options

| Field | Description | Value |
| --- | --- | --- |
| `JOBS_PARALLEL_DB_QUERIES_LIMIT` | The maximum number of database queries that can occur concurrently. |  |
| `JOB_MEMORY_LIMIT` | Stop the job if it exceeds this memory limit. | MB |
| `JOBS_QUERIES_INTERVAL` | Defines the interval, in seconds, at which the system queries the jobs. | sec (float) |
| `MIN_SYSTEM_AVAILABLE_MEMORY_THRESHOLD` | If system has less available memory left than this value, app will start stopping all jobs. | MB |
| `SCAN_BROKER_STUCK_RETRY_MAX_UPLOAD_SIZE` | If the upload size exceeds this value, retries are not performed if the broker is stuck. | MB |
| `QUEUED_SCAN_CHANGE_PRIORITY_TIMEOUT` | The time before the priority of scans waiting in the queue is increased. | sec |
| `QUEUED_SCAN_CANCEL_TIMEOUT` | The time before a scan waiting in the queue is canceled. | sec |
| `CREATE_SCANS_ABOVE_LIMIT_FACTOR` | How many scans users are allowed to add above the queue limit, relative to this limit. (value is in %) | from 0 to 1 |
| `MOVE_SCAN_KEEP_FREE_RATIO` | Determines the amount of free space that remains in the target queue when moving items between queues. Set to 1 to disable changing scans priority. | from 0 to 1 |
| `QUICK_RETRY_MAX_COUNT` | Max amount of quick retries due to failed report. Min of it or `TASKS_QUEUE_JOB_RETRY_LIMIT` (broker rescans) is used. |  |
| `RESCAN_MAX_COUNT` | Amount of delayed rescan attempts to make for failed reports. Set to 0 to disable rescans. |  |
| `RESCAN_MIN_AGE_HOURS` | The minimum age, in hours, before a rescan can be initiated for a report. |  |
| `REPORT_INTERRUPT_TIMEOUT` | Defines the timeout period, in seconds, after which a report generation process will be interrupted if it takes too long to complete. | sec |
| `SCAN_REQUEST_FAILED_RETRY_WAIT` | Specifies the time, in seconds, to wait before retrying a failed scan request. | sec |
| `SCAN_BROKER_STUCK_RETRY_WAIT_1` | Defines the initial time, in seconds, to wait before retrying a scan request if the broker is stuck | sec |
| `SCAN_BROKER_STUCK_RETRY_WAIT_2` | Defines the time, in seconds, to wait before retrying a scan request if the broker is stuck after the second tries is failed. | sec |
| `SCAN_BROKER_STUCK_RETRY_WAIT_3` | Defines the time, in seconds, to wait before retrying a scan request if the broker is stuck after the third tries is failed. | sec |
| `RESCAN_QUOTA_FACTOR` | Allow only certain part of queue to be occupied by rescans. | from 0 to 1 |
| `SCAN_MAX_PRIORITY_JOBS_LIMIT` | Specifies the maximum number of jobs allowed with the highest priority in the scan queue. |  |
| `SCAN_MEDIUM_PRIORITY_JOBS_LIMIT` | Specifies the maximum number of jobs allowed with medium priority in the scan queue. |  |
| `SCAN_LOW_PRIORITY_JOBS_LIMIT` | Specifies the maximum number of jobs allowed with low priority in the scan queue. |  |
| `SCAN_LEAST_PRIORITY_JOBS_LIMIT` | Specifies the minimum number of jobs allowed with the lowest priority in the scan queue. |  |
| `TASKS_QUEUE_JOB_TIMEOUT` | Time limit for arq jobs from start till job is cancelled. | sec |
| REPORT_FORMAT_STRINGS_LIMIT | Only include this amount of extracted strings into HTML/PDF report |  |
| REPORT_FORMAT_STRINGS_MODE | What strings to include into HTML/PDF report. `Prefer interesting` means - include interesting strings first, and than other strings till limit is reached |  |
| REPORT_FORMAT_HISTORY_CLEANUP_TIMEOUT | Interval to cleanup exporting reports history. Also affected by interval of launching cleanup job | min |

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
