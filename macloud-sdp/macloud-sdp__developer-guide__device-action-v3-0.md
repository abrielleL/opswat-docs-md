<!-- source: https://www.opswat.com/docs/macloud-sdp/developer-guide/device-action-v3-0 -->

# Device Action v3.0

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

| API version | 3.0 |
| --- | --- |
| Last Update | 06/28/2017 |
| Authentication | YES |
| HTTP Method | POST |
| Content Type | application/json |
| Rate limited | YES |
| Requests per rate limit | 10/min |
| Response Format | JSON |
| Change History | 04/10/2018: fixed a bug that the API returns HTTP 400 when group id doesn't exist on an account with assign to group action  05/23/2017: added one more action type (types parameter in request), re-identify 06/28/2017: added one more action type (types parameter in request), assign_to_group |

Use to do an action on multiple devices on your account

## [API URL](/docs/cm/developer-guidelines/device-action-v3-0#api-url)

https://gears.opswat.com/o/api/v3/devices/action
## [Request Parameters](/docs/cm/developer-guidelines/device-action-v3-0#request-parameters)

| Key | Datatype | Parameter Type | Required | Description | Default |
| --- | --- | --- | --- | --- | --- |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step |  |
| types | string | Body | Yes | Action Type:   - exempt: exempt a device completely.    - Apply: all devices exclude Unknown, Ignored, Out-of-license-usage devices - unexempt: unexempt device    - Apply: all devices exclude Unknown, Ignored, Out-of-license-usage devices - ignore: ignore an unknown device    - Apply: unknown devices only - unignore: undo ignore action.    - Apply: ignored devices only - delete: delete devices    - Apply: all devices - dhcprenew: force ME call a DHCP request    - Apply: devices which installed a persistent agent only - re-identify: force ME re-identify the device    - Apply: all devices exclude Unknown, Ignored, Out-of-license-usage devices - assign_to_group: assign devices to a group    - Apply: all devices exclude devices with domain controller agent installed |  |
| ids | array<string> | Body | Optional | HWIDs of devices to be applied the action.  *The request body must have ids parameter or macs parameter, but not both.* |  |
| macs | array<string> | Body | Optional | MAC addresses of devices to be applied the action  *The request body must have ids parameter or macs parameter, but not both.* |  |
| params | object | Body | Optional | Required parameters for a specific action. |  |
| params.exempt_time | int | Body | Optional | Specify how long you want to exempt devices in hour. Value should be less than 65000  **if this parameter equals 0, we will do exempt devices forever** | 0 |
| params.group_id | string | Body | Optional | Specify which group (group id) you want to assign devices to  This parameter should be specified when action type is assign_to_group | default |

## [Response HTTP Code](/docs/cm/developer-guidelines/device-action-v3-0#response-http-code)

See [APIs](https://www.opswat.com/docs/macloud-sdp/3.54.0/developer-guide/apis)

## [Response Parameters](/docs/cm/developer-guidelines/device-action-v3-0#response-parameters)

| Key | DataType | Description |
| --- | --- | --- |
| <hwid> or <mac address> | int | Result for a device which has the given HWID/MAC address  -1: not support 0: apply action failed  1: apply action successfully |

## [Example](/docs/cm/developer-guidelines/device-action-v3-0#example)

**Example Request: using Device ID**

https://gears.opswat.com/o/api/v3/devices/action?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
{
"types" : "exempt",
"ids" : ["device123","device456", "device789"],
"params" : {
"exempt_time": 60
}
}

**Example Response**

{
"device123": -1,
"device456": 0,
"device789": 1
}
## [History](/docs/cm/developer-guidelines/device-action-v3-0#history)

| Action | Version | URL |
| --- | --- | --- |
| Delete | 2.0 | [Delete Devices v2.0](/docs/cm/developer-guidelines/delete-devices-v2-0) |
| Renew IP  Exempt  Unexempt | 2.0 | [Delete Devices v2.0](/docs/cm/developer-guidelines/delete-devices-v2-0) |
