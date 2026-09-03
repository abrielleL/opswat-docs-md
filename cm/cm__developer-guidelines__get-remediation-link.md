<!-- source: https://www.opswat.com/docs/cm/developer-guidelines/get-remediation-link -->

# Get Remediation Link

| API version | 3.0 |
| ---- | ---- |
| Last Update | 10/22/2019 |
| Authentication | YES |
| Response Format | JSON |
| HTTP Method | GET |
| Rate limited | YES |
| Requests per rate limit | 10/min |

Use to fetch a remediation link for a given device

## API URL

```plaintext
https://gears.opswat.com/o/api/v3/devices/:value/remediation
```

## Request Parameters

| Key | Datatype | Parameter Type | Required | Description | Default |
| ---- | ---- | ---- | ---- | ---- | ---- |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step |  |
| value | string | URL | Yes | it can be a device ID or MAC address or a custom ID of a device. It depends on value of the "opt" parameter |  |
| opt | int | URL | Optional | Type of the given value in the URL. 0: Device ID or Mac Address 1: 3rd party custom ID which is linked with a device | 0 |

## Response HTTP Code

See details in the Response HTTP Code section in [this page](https://www.opswat.com/docs/cm/developer-guidelines/apis)

## Response Parameters

| Key | DataType | Description |
| ---- | ---- | ---- |
| remediation_link | string | remediation page URL for the given device. |
| result | int | Result for get a remediation page which has the given HWID/MAC address - -1: device is found, but the device status is [Out of license usage](https://www.opswat.com/docs/cm/knowledge-base/what-are-the-different-devices-statuses-and-what-do-they-mean-) - 0: device is not found. - 1: device is found, and the device's remediation page URL is returned in the remediation_link parameter |

## Example

**Example Request**

```plaintext
https://gears.opswat.com/o/api/v3/devices/00:0c:29:f2:7a:29/remediation?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
```

**Example Request With opt=0**

```plaintext
https://gears.opswat.com/o/api/v3/devices/1dc0aaaa292ce801f5379042d68bb6cb/remediation?opt=0&access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61235
```

**Example Response**

```plaintext
//if the given device is compliant / non-compliant / exempted
{
   "result": 1,
   "remediation_link" : "https://gears.opswat.com/gears/remediation/AKLOMFNH123518/1dc0aaaa292ce801f5379042d68bb6cb/123AG138545132156/remediation.html"
}
 
//if the given device is not found in the associated account
{
   "result": 0,
   "remediation_link" : ""
}
 
//if the given device is out-of-license(not support)
{
   "result": -1,
   "remediation_link" : ""
}
```

**Example Request With Invalid opt**

```plaintext
https://gears.opswat.com/o/api/v3/devices/1dc0aaaa292ce801f5379042d68bb6cb/remediation?opt=5&access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61235
```

**Example Response With Invalid opt**

HTTP code 400 Bad Request

```plaintext
{
"error": "invalid_request",
"error_description": "Invalid option"
}
```

## History

| Version | URL |
| ---- | ---- |
| v2.2 | [Get Remediation Link v2.2](https://www.opswat.com/docs/macloud-sdp/developer-guide/get-remediation-link-v2-2) |
| v2.0 | [Get Remediation Link 2.0](https://www.opswat.com/docs/macloud-sdp/developer-guide/get-remediation-link-2-0) |
