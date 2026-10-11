<!-- source: https://www.opswat.com/docs/macloud-sdp/developer-guide/devices-statistics -->

# Device Statistics

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

| API version | 2.0 |
| --- | --- |
| Last Update | 09/21/2014 |
| Authentication | YES |
| Response Format | JSON |
| HTTP Method | GET |
| Rate limited | YES |
| Requests per rate limit | 10/min |

Use to statistic devices which added/not seen in past X hours.

## [API URL](/docs/cm/developer-guidelines/device-statistics#api-url)

https://gears.opswat.com/o/api/v2/devices/stats
## [Request Parameters](/docs/cm/developer-guidelines/device-statistics#request-parameters)

| Key | Datatype | Parameter Type | Required | Description | Default |
| --- | --- | --- | --- | --- | --- |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step |  |
| event |  |  | Yes | Specific what devices want to statistic  Values are supported   - added: query devices which added in the query time - not_seen: query devices which have not checked in the query time - outdated: query devices which running out-of-date agent |  |
| opt | int | URL | optional | Specify which type of the value in "devices" key will be returned in the response  Values: **0 - MAC address** or **1 - HWID** or **3 - SSID** | 0 |
| in | int | URL | optional | Query duration in second/hour/month/year which specified in "*period"* parameter. This parameter needs to go along with "*period"* parameter.  For example: query devices in the last month   - in = 1 - period = month |  |
| period | string | URL | optional | Time unit of the query duration in "*in*" parameter, which will be used for the calculation.  Values: **second**, **hour**, **month**, **ytd** |  |
| start_date | datetime | URL | optional | Starting date of the query duration. Format: **YYYYMMDD** (in UTC timezone). This parameter needs to go along with *end_date* parameter. |  |
| end_date | datetime | URL | optional | Ending date of the query duration. Format: **YYYYMMDD** (in UTC timezone)  For example: query devices from a date to a date (ex: from 10/01/2016 to 11/01/2016)   - start_date = 20161001 - end_date = 20161101 |  |
| device_type | string | URL | optional | Values: all , managed, unmanaged | all |

## [Response HTTP Code](/docs/cm/developer-guidelines/device-statistics#response-http-code)

Refer to [APIs](/docs/cm/developer-guidelines/apis) page for more details.

## [Response Parameters](/docs/cm/developer-guidelines/device-statistics#response-parameters)

| Key | Datatype | Description |
| --- | --- | --- |
| total_count | int | Number of total devices |
| devices | array<string> | Lists of devices which added/have not checked in/has out-of-date agent. Values in the array can be mac address, hardware id or SSID based on the "*opt*" parameter |

## [Example](/docs/cm/developer-guidelines/device-statistics#example)

**Example Request:**

https://gears.opswat.com/o/api/v2/devices/stats?event=not_seen&period=month&in=1&access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234

**Example Response**

{
"total_count": 3,
"devices": ["01:21:9b:06:4b:96", "02:21:9b:06:4b:96", "03:21:9b:06:4b:96"]
}
