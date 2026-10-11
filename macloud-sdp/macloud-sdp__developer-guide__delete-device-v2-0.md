<!-- source: https://www.opswat.com/docs/macloud-sdp/developer-guide/delete-device-v2-0 -->

# Delete Device v2.0

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

| API version | 2.0 |
| --- | --- |
| Last Update | 7/17/2014 |
| Authentication | YES |
| Response Format | JSON |
| HTTP Method | POST |
| Rate limited | YES |
| Requests per rate limit | 10/min |

Use to delete a device on a given account

## [API URL](/docs/cm/developer-guidelines/delete-device-v2-0#api-url)

https://gears.opswat.com/o/api/v2/devices/:value/delete
## [Request Parameters](/docs/cm/developer-guidelines/delete-device-v2-0#request-parameters)

| Key | Datatype | Parameter Type | Required | Description | Default |
| --- | --- | --- | --- | --- | --- |
| value | string | URL | Yes | MAC Address or HWID of a device to be deleted |  |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step |  |
| opt | int | URL | Optional | 0 – Only uninstall an agent on the device but keep the device data on Cloud  1 – Remove device data on Cloud as well as uninstall an agent on the device  2 - Archive Cloud database entry for the device and uninstall an agent on the device | 1 |

## [Response HTTP Code](/docs/cm/developer-guidelines/delete-device-v2-0#response-http-code)

| HTTP Code | Description |
| --- | --- |
| 200 | Success |
| 401 | Unauthorized. Your access_token is invalid or expired |
| 404 | Not found |

## [Response Parameters](/docs/cm/developer-guidelines/delete-device-v2-0#response-parameters)

| Key | Datatype | Description |
| --- | --- | --- |
| result | int | 0 - failure 1 - success |
| msg | string | Result details |

## [Example](/docs/cm/developer-guidelines/delete-device-v2-0#example)

**Request** **Example**

https://gears.opswat.com/o/api/v2.2/devices/0CQN6GRVGU2F1/delete?opt=0&access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234

Response Example** **

{
"result": 1,
"msg": "Device has been deleted"
}
