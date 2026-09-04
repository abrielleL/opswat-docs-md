<!-- source: https://www.opswat.com/docs/macloud-sdp/developer-guide/delete-devices-v2-0 -->

# Delete Devices v2.0

| API version | 2.0 |
| --- | --- |
| Last Update | 08/19/2014 |
| Authentication | YES |
| Response Format | JSON |
| HTTP Method | POST |
| Rate limited | YES |
| Requests per rate limit | 10/min |

Use to delete devices on an account

## [API URL](/docs/macloud-sdp/developer-guide/delete-devices-v2-0#api-url)

https://gears.opswat.com/o/api/v2/devices/delete
## [Request Parameters](/docs/macloud-sdp/developer-guide/delete-devices-v2-0#request-parameters)

| Key | Datatype | Parameter Type | Required | Description | Default |
| --- | --- | --- | --- | --- | --- |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step |  |
| opt | int | Body | Optional | 0 – Only uninstall client agent from device but keep the data in Cloud database1 – Remove Cloud database entry for the device as well as uninstall the client agent from device2 – Archive Cloud database entry for the device as well as uninstall the client agent from device | 1 |
| MAC_list | array<string> | Body | Optional | MAC addresses of devices you want to delete. Don't use this parameter if you already use HWID_list in the body |  |
| HWID_list | array<string> | Body | Optional | HWIDs of devices you want to delete. Don't use this parameter if you already use MAC_list in the body |  |

## [Response HTTP Code](/docs/macloud-sdp/developer-guide/delete-devices-v2-0#response-http-code)

| HTTP Code | Description |
| --- | --- |
| 200 | Success |
| 400 | Bad request |
| 401 | Unauthorized. Your access_token is invalid or expired |

## [Response Parameters](/docs/macloud-sdp/developer-guide/delete-devices-v2-0#response-parameters)

| Key | DataType | Description |
| --- | --- | --- |
| result | array<int> | The result of batch delete operation. Result[i] value means that   - 0: couldn't delete devices[i] in the list - 1: delete devices[i] in the list successfully |

Note: reasons cause failure in deleting a device

- the cloud couldn't find any devices which reports the given MAC address or HWID
- the given MAC address is invalid

## [Example](/docs/macloud-sdp/developer-guide/delete-devices-v2-0#example)

**Example Request**

https://gears.opswat.com/o/api/v2/devices/delete?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
 
Posting data (by MAC address):
{
"MAC_list" : ["00:0c:29:cd:c7:b2", "00:0c:30:cd:ff:b2"],
"opt": 0
}
 
Posting data (by HWID):
{
"HWID_list" : ["12ds44f5gacd52234", "cd7323a67effe2ab53"],
"opt": 0
}

**Example Response**

{
"result": [0,1]
}
