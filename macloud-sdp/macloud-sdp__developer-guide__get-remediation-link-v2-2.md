<!-- source: https://www.opswat.com/docs/macloud-sdp/developer-guide/get-remediation-link-v2-2 -->

# Get Remediation Link v2.2

Summarize Page    Connect to Cursor Connect to VS Code

| API version | 2.2 |
| --- | --- |
| Last Update | 05/28/2015 |
| Authentication | YES |
| Response Format | JSON |
| HTTP Method | GET |
| Rate limited | YES |
| Requests per rate limit | 10/min |

Use to fetch a remediation link for a given device

## [API URL](/docs/cm/developer-guidelines/get-remediation-link-v2-2#api-url)

https://gears.opswat.com/o/api/v2.2/devices/:value/remediation
## [Request Parameters](/docs/cm/developer-guidelines/get-remediation-link-v2-2#request-parameters)

| Key | Datatype | Parameter Type | Required | Description | Default |
| --- | --- | --- | --- | --- | --- |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step |  |
| value | string | URL | Yes | HWID or MAC address of the device |  |
| opt | sint | URL | Optional | Type of the given value in the URL.  1 - the given value is HWID. 0 - the given value is MAC Address | 0 |

## [Response HTTP Code](/docs/cm/developer-guidelines/get-remediation-link-v2-2#response-http-code)

See [APIs](https://www.opswat.com/docs/macloud-sdp/3.54.0/developer-guide/apis)

## [Response Parameters](/docs/cm/developer-guidelines/get-remediation-link-v2-2#response-parameters)

| Key | DataType | Description |
| --- | --- | --- |
| remediation_link | string | (optional) remediation page URL for the given device. |
| result | int | (optional) indicate if the request is processed successfully.   - 0: failure |
| msg | string | (optional) error details |

## [Example](/docs/cm/developer-guidelines/get-remediation-link-v2-2#example)

**Example Request**

https://gears.opswat.com/o/api/v2.2/devices/00:0c:29:f2:7a:29/remediation?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234

**Example Response**

//if the given device has issues
{
"remediation_link" : "https://gears.opswat.com/gears/remediation/AKLOMFNH123518/00:0c:29:f2:7a:29/123AG138545132156/remediation.html"
}
 
 
//if the given device has no issues
{
"result": 0,
"msg": "Device has no issues"
}
 
 
//if the given device is not found in the associated account
{
"result": 0,
"msg": "Device not found"
}
## [History](/docs/cm/developer-guidelines/get-remediation-link-v2-2#history)

| Version | URL |
| --- | --- |
| v2.0 | [Get Remediation Link 2.0](/docs/cm/developer-guidelines/get-remediation-link-2-0) |
