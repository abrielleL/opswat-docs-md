<!-- source: https://www.opswat.com/docs/macloud-sdp/developer-guide/get-logs-v2-0 -->

# Get Logs v2.0

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

| API version | 2.0 |
| --- | --- |
| Last Update | 10/25/2014 |
| Authentication | YES |
| Response Format | JSON |
| HTTP Method | GET |
| Rate limited | YES |
| Requests per rate limit | 10/min |

To retrieve event logs on your account.

## [API URL](/docs/cm/developer-guidelines/get-logs-v2-0#api-url)

https://gears.opswat.com/o/api/v2/logs
## [Request Parameters](/docs/cm/developer-guidelines/get-logs-v2-0#request-parameters)

| Key | Datatype | Parameter Type | Required | Description | Default |
| --- | --- | --- | --- | --- | --- |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step |  |
| limit | int | URL | Optional | Specific maximum number of event logs will be returned in the response. The value should be in [1,50]. If there are more event logs than what the limit asks for, error code will be 406. Event logs in response is ordered by date. | 1 |
| page | int | URL | Optional | Specific page number which event logs will be returned in. If the requested page exceeds the number of pages of event logs, error code will be 413. It means that the requested page number is too large, no devices will be returned in this case. | 1 |
| event_type | int | URL | Optional | Specific what kind of event logs you want to retrieve.  1: device events  2: administrator events | 1 |

## [Response HTTP Code](/docs/cm/developer-guidelines/get-logs-v2-0#response-http-code)

| HTTP Code | Description |
| --- | --- |
| 200 | Success |
| 401 | Unauthorized. Your access_token is invalid or expired |
| 406 | Too many records to return |
| 413 | Requested page number exceeds limit |

## [Response Parameters](/docs/cm/developer-guidelines/get-logs-v2-0#response-parameters)

| Key | DataType | Description |
| --- | --- | --- |
| logs | array<object> | Lists of event logs |
| eventlog | array<string> | Array of events of the event log. The information will be formated as "<hh:mm> | [AM/PM] | <event category> | <device's hostname> | <event description>" |
| date | string | timestamp when the event log occurs |

## [Example](/docs/cm/developer-guidelines/get-logs-v2-0#example)

**Example Request**

https://gears.opswat.com/o/api/v2/logs?limit=10&event_type=1&access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234

**Example Response**

{
"logs": [
{
"date": "Dec 6, 2013 ",
"eventlog": [
"05:28|PM|MetaAccess (Version 1.1.1.1)|TEST-R1W3Y|Installed",
"05:28|PM|MetaAccess (Version 1.1.1.1)|TEST-B3WMO|Installed",
"05:28|PM|MetaAccess (Version 1.1.1.1)|TEST-S0TYY|Installed",
"05:28|PM|MetaAccess (Version 1.1.1.1)|TEST-5MJG5|Installed",
"05:28|PM|MetaAccess (Version 1.1.1.1)|TEST-XYOSG|Installed",
"05:28|PM|MetaAccess (Version 1.1.1.1)|TEST-IQAJQ|Installed",
"05:28|PM|MetaAccess (Version 1.1.1.1)|TEST-H934C|Installed",
"05:28|PM|MetaAccess (Version 1.1.1.1)|TEST-EQUJC|Installed",
"05:28|PM|MetaAccess (Version 1.1.1.1)|TEST-D7D4N|Installed",
"05:28|PM|MetaAccess (Version 1.1.1.1)|TEST-2EPQL|Installed"
]
}
]}
