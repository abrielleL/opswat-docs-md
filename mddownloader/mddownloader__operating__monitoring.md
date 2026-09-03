<!-- source: https://www.opswat.com/docs/mddownloader/operating/monitoring -->

# Monitoring

## [Overview](/docs/mddownloader/operating/monitoring#overview)

The `/readyz` API provides a simple way to monitor the health and status of your MetaDefender Downloader instance. This endpoint is particularly valuable for air-gapped environments where active monitoring of engine updates and system health is required.

## [API Endpoint](/docs/mddownloader/operating/monitoring#api-endpoint)

GET /readyz

## [Query Parameters](/docs/mddownloader/operating/monitoring#query-parameters)

The API accepts an optional `info` query parameter with the following possible values:

| Parameter Value | Description |
| --- | --- |
| version | Returns the MetaDefender Downloader version |
| *updater_server_connection* | Checks connectivity to the updater server |
| diskspace | Reports free and total disk space for the data directory (in bytes) |
| engine | Returns status of all engine and database packages |
| update | Provides update-related information including timestamps and status |
| all | Returns all information listed above. Note: when using `all` , if other options also included -> it will be considered as invalid option |

Multiple values can be requested by separating them with commas (e.g., info=diskspace,version).

## [Default Response](/docs/mddownloader/operating/monitoring#default-response)

When called without the `info` parameter, the API returns:

- Downloader version
- Connection status to updater server

## [Example Requests](/docs/mddownloader/operating/monitoring#example-requests)

### [Basic Health Check](/docs/mddownloader/operating/monitoring#basic-health-check)

GET /readyz

**Response:**

JavascriptCopy{
"updater_server": "connected",
"version": "3.2.3"
}
### [Request Specific Information](/docs/mddownloader/operating/monitoring#request-specific-information)

GET /readyz?info=diskspace,updater_server_connection

**Response:**

JavascriptCopy{
"free_disk_space": 22213443584,
"total_disk_space": 247882248192,
"updater_server": "connected"
}
### [Request All Available Information](/docs/mddownloader/operating/monitoring#request-all-available-information)

GET /readyz?info=all

**Response:**

JavascriptCopy{
"updater_server": "connected",
"version": "3.2.3",
"free_disk_space": 37685030912,
"total_disk_space": 247882248192,
"update_info": {
"export_running": true,
"last_update": 1746761060690,
"last_update_was_successful": true,
"next_update": 1746772282162,
"update_running": true
},
"engines": [
{
"abandoned": false,
"download_progress": 100,
"download_time": "2025-05-09T03:24:20.750Z",
"eng_id": "7z_17_windows",
"eng_name": "Archive Extraction",
"eng_type": "Bundled engine",
"eng_ver": "6.4.0-3939",
"engine_type": "archive",
"pinned": false,
"state": "validating",
"type": "engine"
},
{
"abandoned": false,
"download_progress": 100,
"download_time": "2025-05-09T03:24:20.762Z",
"eng_id": "ahnlab_1_windows",
"eng_name": "AhnLab",
"eng_type": "Bundled engine",
"eng_ver": "3.23.3.2-1947",
"engine_type": "av",
"pinned": false,
"state": "ready",
"type": "engine"
},
{
"abandoned": false,
"download_progress": 42,
"download_time": "2025-05-09T03:24:20.805Z",
"eng_id": "dlp_13_windows",
"eng_name": "Proactive DLP",
"eng_type": "Bundled engine",
"eng_ver": "2.10.0-1639650749",
"engine_type": "dlp",
"pinned": false,
"state": "downloading",
"type": "engine"
}
]
}
## [Response Codes](/docs/mddownloader/operating/monitoring#response-codes)

| Status Code | Description |
| --- | --- |
| 200 | Request successful |
| 400 | Invalid parameter(s) provided |

## [Error Handling](/docs/mddownloader/operating/monitoring#error-handling)

If an invalid `info` parameter is supplied, the API returns:

GET /readyz?info=invalid

**Response:**

JavascriptCopy{
"err": "Invalid param info"
}
## [Monitoring Best Practices](/docs/mddownloader/operating/monitoring#monitoring-best-practices)

1. **Regular Polling**: Set up automated checks every 5-15 minutes
2. **Alert on Failures**: Configure alerts for:

   - Disconnected updater server
   - Low disk space (below 10% free)
   - Failed update status

## [Implementation Notes](/docs/mddownloader/operating/monitoring#implementation-notes)

- Disk space is reported in bytes
- If engines are actively downloading, the updater server connection is automatically considered "connected"
