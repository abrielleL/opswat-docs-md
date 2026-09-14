<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/how-do-i-configure-v4debug-dat-for-enhanced-logging -->

# How do I configure v4Debug.dat for enhanced logging?

This article is applied to MetaDefender Endpoint Security SDK (OESIS) releases deployed on Windows, MacOS and Linux systems.

## [Overview](/docs/mdsdk/knowledge-base/how-do-i-configure-v4debug-dat-for-enhanced-logging#overview)

The `v4Debug.dat` file enables a logging mechanism that can be used to extract necessary logs. Creating an empty `v4Debug.dat` file in the deployment folder (Working Directory) of the binaries is usually sufficient to initiate logging. For more specific logging configurations, you can add parameters to the `v4Debug.dat` file.

## [Arguments Description](/docs/mdsdk/knowledge-base/how-do-i-configure-v4debug-dat-for-enhanced-logging#arguments-description)

| Argument | Description |
| --- | --- |
| `debug_log_output_path` | - The path you want the logs exported to. - **Default value is the deployment path**. - Will create the destination folder if it doesn't exist. |
| `debug_log_level` | - The logging level. - highest priority of log filtering. - **Default value is** `ALL`**.** - Available Options:    - `OFF, INFO, WARN, ERR, FATAL, WADEBUG, TRACE, ALL` |
| `debug_log_components` | - The logging components - Second priority of log filtering - **Default value is** `ALL`. - Available Options:    - `CORE, SETUP, TEARDOWN, INVOKE, ALL` |
| `debug_log_file_size` | - The max size of **one log file** (in MB) - When this threshold is reached, a new log file will be generated. - **Default and minimum value is** `5` **(MB).** |
| `debug_log_folder_size` | - The max size of the **log folder** (in MB) - When this threshold is reached the oldest log file is deleted. - **Default and minimum value is** `100` **(MB).** |
| `debug_log_time` | - The max amount of time for log retention (in hours) - All files which pass the specified threshold are deleted. - **Default and minimum is** `48` **(hours)** |
| `debug_log_count` | - The max number of files to store - All files which pass the specified threshold are deleted. - **Default and minimum is** `20` **(log files)** |

## [Logging output](/docs/mdsdk/knowledge-base/how-do-i-configure-v4debug-dat-for-enhanced-logging#logging-output)

Resulting log files will follow this format:

`v4DebugInfo_[EPOCH_TIME_SECONDS]_[EPOCH_TIME_MILLISECONDS]_P[PROCESS_ID].log`

**Example:** `v4DebugInfo_1646211492_1791146406_P6624.log`

## [Sample Configuration](/docs/mdsdk/knowledge-base/how-do-i-configure-v4debug-dat-for-enhanced-logging#sample-configuration)

A full sample config is available for reference:

JsonCopy{
"debug_log_output_path": "%userprofile%\\Desktop\\OPSWAT\\",
"debug_log_level": "ALL",
"debug_log_components": ["ALL"],
"debug_log_file_size": 5,
"debug_log_folder_size": 100,
"debug_log_time": 72,
"debug_log_count": 30
}Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
