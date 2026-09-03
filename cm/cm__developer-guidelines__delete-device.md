<!-- source: https://www.opswat.com/docs/cm/developer-guidelines/delete-device -->

# Delete Device

| API version | 2.2 |
| ---- | ---- |
| Last Update | 05/28/2015 |
| Authentication | YES |
| Response Format | JSON |
| HTTP Method | POST |
| Rate limited | YES |
| Requests per rate limit | 10/min |

Use to delete a device on a given account

## API URL

```plaintext
https://gears.opswat.com/o/api/v2.2/devices/:value/delete
```

## Request Parameters

| Key | Datatype | Parameter Type | Required | Description | Default |
| ---- | ---- | ---- | ---- | ---- | ---- |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step |  |
| value | string | URL | Yes | MAC Address or HWID of a device to be deleted |  |
| opt | int | URL | Optional | 0 – Only uninstall an agent on the device but keep the device data on Cloud 1 – Remove device data on Cloud as well as uninstall an agent on the device 2 - Archive Cloud database entry for the device and uninstall an agent on the device | 1 |

## Response HTTP Code

See details in the Response HTTP Code section in [this page](https://www.opswat.com/docs/cm/developer-guidelines/apis)

## Response Parameters

| Key | Datatype | Description |
| ---- | ---- | ---- |
| result | int | 0 - failure 1 - success |
| msg | string | Result details |

## Example

*_Request *_Example

```plaintext
https://gears.opswat.com/o/api/v2.2/devices/0CQN6GRVGU2F1/delete?opt=0&access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
```

Response Example** **

```plaintext
{
   "result": 1,
   "msg": "Device has been deleted"
}
```

## History

| Version | Link |
| ---- | ---- |
| 2.0 | [Delete Device v2.0](https://www.opswat.com/docs/macloud-sdp/developer-guide/delete-device-v2-0) |
