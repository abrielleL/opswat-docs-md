<!-- source: https://www.opswat.com/docs/macloud-sdp/developer-guide/devices-action-v2-0 -->

# Devices Action v2.0

| API version | 2.0 |
| --- | --- |
| Last Update | 01/12/2015 |
| Authentication | YES |
| Response Format | JSON |
| HTTP Method | POST |
| Rate limited | YES |
| Requests per rate limit | 10/min |

Use to send a remote command to given devices

## [API URL](/docs/macloud-sdp/developer-guide/devices-action-v2-0#api-url)

https://gears.opswat.com/o/api/v2/devices/action
## [Request Parameters](/docs/macloud-sdp/developer-guide/devices-action-v2-0#request-parameters)

| Key | Datatype | Parameter Type | Required | Description | Default |
| --- | --- | --- | --- | --- | --- |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step |  |
| opt | int | Body | Optional | **0 -** MAC address**1** - HWID | 0 |
| types | string | Body | Yes | The action type: dhcprenew - renew ip address for network interfaces on devices. exempt_all - exempt devices. unexempt - unexempt devices. |  |
| MAC_list | array<string> | Body | Optional | MAC addresses of devices you want to send remote command. \ *The request body must have MAC_list parameter or HWID_list parameter, but not both.* |  |
| HWID_list | array<string> | Body | Optional | HWIDs of devices you want to send remote command. **The request body must have MAC_list parameter or HWID_list parameter, but not both*.* |  |

## [Response HTTP Code](/docs/macloud-sdp/developer-guide/devices-action-v2-0#response-http-code)

| HTTP Code | Description |
| --- | --- |
| 200 | Success |
| 400 | Bad request |
| 401 | Unauthorized. Your access_token is invalid or expired |
| 404 | Not found |

## [Response Parameters](/docs/macloud-sdp/developer-guide/devices-action-v2-0#response-parameters)

| Key | DataType | Description |
| --- | --- | --- |
| result | array<int> | The result of batch action. Result[i] value means that the action on device[i] is   - 0: failure - 1: success |

Note: reasons can cause failure

- the cloud couldn't find any devices which reports the given MAC address or HWID
- the given MAC address is invalid

## [Example](/docs/macloud-sdp/developer-guide/devices-action-v2-0#example)

**Example Request**

https://gears.opswat.com/o/api/v2/devices/action?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
{
"types" : "dhcprenew",
"MAC_list" : ["00:0c:29:cd:c7:b2", "00:0c:30:cd:ff:b2"],
"opt" : 0
}

**Example Response**

{
"result": [0, 1]
}
