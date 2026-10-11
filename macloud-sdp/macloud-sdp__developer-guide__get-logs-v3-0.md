<!-- source: https://www.opswat.com/docs/macloud-sdp/developer-guide/get-logs-v3-0 -->

# Get Logs v3.0

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

| API version | 3.0 |
| --- | --- |
| Last Update | 04/25/2017 |
| Authentication | YES |
| HTTP Method | POST |
| Content Type | application/json |
| Rate limited | YES |
| Requests per rate limit | 10/min |
| Response Format | JSON |

My OPSWAT Central Management records events on your accounts. There are 2 types of event logs: admin event logs and device event logs. To retrieve event logs on your account, you can use this API. You can set filters in parameters to filter event logs you concern.

## [API URL](/docs/cm/developer-guidelines/get-logs-v3-0#api-url)

https://gears.opswat.com/o/api/v3/logs
## [Request Parameters](/docs/cm/developer-guidelines/get-logs-v3-0#request-parameters)

| Key | Datatype | Parameter Type | Required | Description | Default |
| --- | --- | --- | --- | --- | --- |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step |  |
| limit | int | Body | Optional | Specific maximum number of event logs will be returned in the response. The value should be in [1,50]. If there are more event logs than what the limit asks for, error code will be 406. Event logs in response is ordered by date. | 20 |
| page | int | Body | Optional | Specific page number which event logs will be returned in. If the requested page exceeds the number of pages of event logs, error code will be 413. It means that the requested page number is too large, no devices will be returned in this case. | 1 |
| start_date | string | Body | Optional | Specific the start date for the query duration. Starting date of the query. Format: YYYY/MM/DD |  |
| end_date | string | Body | Optional | Specific the end date for the query duration. Format: YYYY/MM/DD |  |
| age | int | Body | Optional | Specify age of the information in seconds. Maximum value is 86400 (1 day)  For example: if you want to query event logs in last 5 minutes, you need to pass age as 300. |  |
| filter | array<string> | Body | Optional | Specify which events you want to retrieve.  Options can be:   - *added*: events when a device is added - *deleted*: events when a device is deleted by Admin - *deleted_user*: events when a device is uninstalled by remote users on endpoints - *unseen*: events when a device is deleted by Lost Devices feature (a device is unseen for a long time) - *compliant*: events when a device becomes/changes status to COMPLIANT - *noncompliant*: events when a device becomes/changes status to NON-COMPLIANT |  |

## [Response HTTP Code](/docs/cm/developer-guidelines/get-logs-v3-0#response-http-code)

See [APIs](https://www.opswat.com/docs/macloud-sdp/3.54.0/developer-guide/apis)

## [Response Parameters](/docs/cm/developer-guidelines/get-logs-v3-0#response-parameters)

| Key | DataType | Description |
| --- | --- | --- |
| logs | array<object> | Lists of event logs |
| logs.timestamp | string | timestamp when the event log occurs |
| logs.event | string | Event text |
| logs.device_id | string | HWID of the device which the event occurred on |
| logs.device_name | string | Device name which the event occurred on |
| logs.mac_addresses | string | MAC address of the device which the event occurred on |
| logs.details | array<string> | Event details. The format is: ["category", "application", "version", "status"] |

## [Example](/docs/cm/developer-guidelines/get-logs-v3-0#example)

**Example Request**

https://gears.opswat.com/o/api/v3/logs?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
{
"filter": ["added", "deleted", "deleted_user", "unseen", "compliant", "noncompliant" ],
"start_date": "2016/05/30",
"end_date": "2016/05/15",
"page": 1,
"limit" : 20
}

**Example Response**

{
logs: [
{
timestamp: "2016-05-25T21:00:19Z",
event: "deleted by Admin",
device_id :"HWID129",
mac_addresses: ["11:11:11:11:11:11"],
device_name: "WSEVN15"
},
{
timestamp: "2016-05-24T21:00:19Z",
event: "deleted by Users",
device_id :"HWID128",
mac_addresses: ["22:22:22:22:22:22"],
device_name: "WSEVN14"
},
{
timestamp: "2016-05-23T21:00:19Z",
event: "unseen in 14 days",
device_id :"HWID127",
mac_addresses: ["33:33:33:33:33:33"],
device_name: "WSEVN13"
},
{
timestamp: "2016-05-22T21:00:19Z",
event: "deleted by MEM",
device_id :"HWID126",
mac_addresses: ["44:44:44:44:44:44"],
device_name: "WSEVN12"
},
{
timestamp: "2016-05-21T21:00:19Z",
event: "installed",
device_id :"HWID125",
mac_addresses: ["55:55:55:55:55:55"],
device_name: "WSEVN11"
},
{
timestamp: "2016-05-20T21:00:19Z",
event: "changes status to COMPLIANT",
device_id :"HWID124",
mac_addresses: ["66:66:66:66:66:66"],
device_name: "WSEVN10",
},
{
timestamp: "2016-05-19T21:00:19Z",
event: "reported as being NONCOMPLIANT",
device_id :"HWID123",
mac_addresses: ["77:77:77:77:77:77"],
device_name: "WSEVN09",
details: [
["OS Update and Patches", "Windows Update Agent", "7.9.9600.18235", "OS IS MISSING PATCHES"]
]
}
]
}
## [History](/docs/cm/developer-guidelines/get-logs-v3-0#history)

| Version | URL |
| --- | --- |
| v2.0 | [Get Logs v2.0](/docs/cm/developer-guidelines/get-logs-v2-0) |
