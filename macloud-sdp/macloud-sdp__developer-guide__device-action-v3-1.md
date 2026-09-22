<!-- source: https://www.opswat.com/docs/macloud-sdp/developer-guide/device-action-v3-1 -->

# Device Action v3.1

Summarize Page    Connect to Cursor Connect to VS Code

| API version | 3.1 |
| --- | --- |
| Last Update | 07/16/2019 |
| Authentication | YES |
| HTTP Method | POST |
| Content Type | application/json |
| Rate limited | YES |
| Requests per rate limit | 10/min |
| Response Format | JSON |
| Change History | 07/16/2019: updated agent version which supports fetch_log command  01/22/2019: add one more action type, fetch_agent_log, to support retrieve OPSWAT Client log |

Use to do an action on multiple devices on your account

## [API URL](/docs/cm/developer-guidelines/device-action-v3-1#api-url)

https://gears.opswat.com/o/api/v3.1/devices/action
## [Request Parameters](/docs/cm/developer-guidelines/device-action-v3-1#request-parameters)

| Key | Datatype | Parameter Type | Required | Description | Default |
| --- | --- | --- | --- | --- | --- |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step |  |
| types | string | Body | Yes | Action Type:   - exempt: exempt devices.    - Apply: all devices exclude Unknown, Ignored, Out-of-license-usage devices - unexempt: unexempt devices    - Apply: all devices exclude Unknown, Ignored, Out-of-license-usage devices - ignore: ignore unknown devices    - Apply: unknown devices - unignore: undo ignore action.    - Apply: ignored devices - delete: delete devices    - Apply: all devices - dhcprenew: force agents call a DHCP request    - Apply: devices which installed a persistent agent - re-identify: force agents to request end-users re-enter their custom information    - Apply: all devices exclude Unknown, Ignored, Out-of-license-usage devices - assign_to_group: assign devices to a group    - Apply: all devices exclude devices with domain controller agent installed - fetch_agent_log : retrieve OPSWAT Client log on devices    - Apply: devices which installed a persistent agent version 7.6.231.0+/ 10.4.225.0+ |  |
| ids | array<string> | Body | Optional | Device IDs of devices to be applied the action.  *The request body must have ids parameter or macs parameter, but not both.* |  |
| macs | array<string> | Body | Optional | MAC addresses of devices to be applied the action  *The request body must have ids parameter or macs parameter, but not both.* |  |
| params | object | Body | Optional | Required parameters for a specific action. |  |
| params.exempt_time | int | Body | Optional | Specify how long you want to exempt devices in hour. Value should be less than 65000  **if this parameter equals 0, My OPSWAT Central Management will exempt devices forever** | 0 |
| params.group_id | string | Body | Optional | Specify which group (group id) you want to assign devices to  This parameter should be specified when action type is assign_to_group | default |

## [Response HTTP Code](/docs/cm/developer-guidelines/device-action-v3-1#response-http-code)

See [APIs](https://www.opswat.com/docs/macloud-sdp/3.54.0/developer-guide/apis)

## [Response Parameters](/docs/cm/developer-guidelines/device-action-v3-1#response-parameters)

| Key | DataType | Description |
| --- | --- | --- |
| id | string | Device ID or MAC address of a device |
| status | integer | action status. Value can be   - -1: not support - 0: apply action failed - 1: apply action successfully |
| command_id | string | **Only apply for fetch_agent_log action**  Command ID of the action. This will be used in Get Report v3.0+. This parameter will be empty if the action is failed/not supported (status is 01/0) or the action type is not fetch_agent_log |

## [Example](/docs/cm/developer-guidelines/device-action-v3-1#example)

**Example Request: using Device ID**

https://gears.opswat.com/o/api/v3.1/devices/action?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
{
"types" : "exempt",
"ids" : ["device123","device456", "device789"],
"params" : {
"exempt_time": 60
}
}

**Example Response**

[
{
"id": "device123",
"status": 1,
"command_id": ""
},
{
"id": "device456",
"status": 0,
"command_id": ""
},
{
"id": "device789",
"status": -1,
"command_id": ""
}
]

**Example Request: using Device MAC address**

https://gears.opswat.com/o/api/v3.1/devices/action?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
{
"types" : "fetch_agent_log",
"ids" : ["1A:2A:3A:4A:5A:6A","1B:2B:3B:4B:5B:6B", "1C:2C:3C:4C:5C:6C"],
"params" : {
"exempt_time": 60
}
}

**Example Response**

[
{
"id": "1A:2A:3A:4A:5A:6A",
"status": 1,
"command_id": "cdhk12j279h35k214"
},
{
"id": "1B:2B:3B:4B:5B:6B",
"status": 0,
"command_id": ""
},
{
"id": "1C:2C:3C:4C:5C:6C",
"status": -1,
"command_id": ""
}
]
## [History](/docs/cm/developer-guidelines/device-action-v3-1#history)

| Action | Version | URL |
| --- | --- | --- |
| Device Action | 3.0 | [Device Action v3.0](/docs/cm/developer-guidelines/device-action-v3-0) |
| Delete | 2.0 | [Delete Device v2.0](/docs/cm/developer-guidelines/delete-device-v2-0) |
| Renew IP  Exempt  Unexempt | 2.0 | [Devices Action v2.0](/docs/cm/developer-guidelines/devices-action-v2-0) [Device Action v2.0](/docs/cm/developer-guidelines/device-action-v2-0) |
