<!-- source: https://www.opswat.com/docs/macloud-sdp/developer-guide/device-action-v2-0 -->

# Device Action v2.0

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

| API version | 2.0 |
| --- | --- |
| Last Update | 03/24/2015 |
| Authentication | YES |
| Response Format | JSON |
| HTTP Method | POST |
| Rate limited | YES |
| Requests per rate limit | 10/min |

Use to send a command to a given device

## [API URL](/docs/cm/developer-guidelines/device-action-v2-0#api-url)

https://gears.opswat.com/o/api/v2/devices/:id/action
## [Request Parameters](/docs/cm/developer-guidelines/device-action-v2-0#request-parameters)

| Key | Datatype | Parameter Type | Required | Description | Default |
| --- | --- | --- | --- | --- | --- |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step |  |
| types | string | URL | Yes | The action type.  dhcprenew - renew ip address for interfaces. exempt_critical - enable exempt critical mode for device. exempt_all - enable exempt all mode for device. unexempt - disable exempt mode for device. |  |
| id | string | URL | Yes | HWID or MAC Address of a device to be applied the action. |  |
| opt | int | URL | Optional | 0 - MAC Address 1 - HWID | 0 |

## [Response HTTP Code](/docs/cm/developer-guidelines/device-action-v2-0#response-http-code)

| HTTP Code | Description |
| --- | --- |
| 200 | Success |
| 400 | Bad Request |
| 401 | Unauthorized. Your access_token is invalid or expired |
| 404 | Not found |

## [Response Parameters](/docs/cm/developer-guidelines/device-action-v2-0#response-parameters)

| Key | Datatype | Description |
| --- | --- | --- |
| result | int | 0 - failure 1- success |
| msg | string | Result details |

## [Example](/docs/cm/developer-guidelines/device-action-v2-0#example)

**Request** **Example**

https://gears.opswat.com/o/api/v2/devices/HWID123/action?types=dhcprenew&opt=1&access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234

**Response** **Example**

{
"result": 1,
"msg": "OK"
}
