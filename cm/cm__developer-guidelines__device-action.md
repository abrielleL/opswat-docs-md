<!-- source: https://www.opswat.com/docs/cm/developer-guidelines/device-action -->

# Device Action

| API version | 3.3 |
| ---- | ---- |
| Last Update | 05/22/2024 |
| Authentication | YES |
| HTTP Method | POST |
| Content Type | application/json |
| Rate limited | YES |
| Requests per rate limit | 10/min |
| Response Format | JSON |
| Change History | 05/22/2024: Update the log records so that the admin can distinguish whether an action was performed from the admin console or through the OAuth API |

Use to do an action on multiple devices on your account

## API URL

```plaintext
https://gears.opswat.com/o/api/v3.3/devices/action
```

## Request Parameters

| Key | Datatype | Parameter Type | Required | Description | Default |
| ---- | ---- | ---- | ---- | ---- | ---- |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step |  |
| types | string | Body | Yes | Action Type: - exempt: exempt a device completely.   - Apply: all devices exclude Unknown, Ignored, Out-of-license-usage devices, Domain controller - unexempt: unexempt device   - Apply: all devices exclude Unknown, Ignored, Out-of-license-usage devices, Domain controller - ignore: ignore an unknown device   - Apply: unknown devices only - unignore: undo ignore action.   - Apply: ignored devices only - delete: delete devices   - Apply: all devices - dhcprenew: force ME call a DHCP request   - Apply: devices which installed a persistent agent only - re-identify: force ME re-identify the device   - Apply: This action is only applicable for Windows persistent agent version 7.6.71.0+ and macOS persistent agent 10.4.123.0+ and Mobile agent - assign_to_group: assign devices to a group   - Apply: all devices exclude devices with domain controller agent installed - fetch_agent_log: request to retrieve My OPSWAT Central Management agent log on devices - scan_threats: perform an on-demand threats scan on devices. This action is only applicable for Windows persistent agent version 7.6.206.0+ and macOS persistent agent 10.4.205.0+ |  |
| ids | array<string> | Body | Optional | Device IDs of devices to be applied the action. *The request body must have ids parameter or macs parameter, but not both.* |  |
| macs | array<string> | Body | Optional | MAC addresses of devices to be applied the action *The request body must have ids parameter or macs parameter, but not both.* |  |
| params | object | Body | Optional | Required parameters for a specific action. |  |
| params.exempt_time | int | Body | Optional | Specify how long you want to exempt devices in hour. Value should be less than 65000 **if this parameter equals 0,** My OPSWAT Central Management **will exempt devices forever** | 0 |
| params.group_id | string | Body | Optional | Specify which group (group id) you want to assign devices to This parameter should be specified when action type is assign_to_group | default |
| params.full_scan | int | Body | Optional | **Only apply for scan_threats action** 0: custom scan, 1: full scan |  |
| params.scan_types | array<int> | Body | Optional | **Only apply for scan_threats action** Specify which types of custom scan agent will perform the scanning. Types are defined as below 0: Memory 1: System Volume 2: Portable Volumes 3: Additional Volumes 4: Specific Path 5: Boot Records |  |
| params.path | string | Body | Optional | **Only apply for scan_threats action** Specify a location where agent will perform the scanning |  |

## Response HTTP Code

See details in the Response HTTP Code section in [this page](https://www.opswat.com/docs/cm/developer-guidelines/apis)

## Response Parameters

| Key | DataType | Description |
| ---- | ---- | ---- |
| id | string | Device ID or MAC address of a device |
| status | integer | action status. Value can be - -1: the action is not supported for a specified device - 0: failed to apply the action - 1: apply action successfully |
| command_id | string | **Apply for fetch_agent_log action and scan_threats action** Command ID of the action. This will be used in Get Report v3.0+. This parameter will be empty if the action is failed/not supported (status is -1/0) or the action type is not fetch_agent_log, scan_threats |

## Example

**Example Request: using Device ID**

```plaintext
https://gears.opswat.com/o/api/v3.3/devices/action?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
{
    "types" : "exempt",
    "ids" : ["device123","device456", "device789"],
    "params" : {
        "exempt_time": 60
    }
}
```

**Example Response**

```plaintext
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
```

**Example Request: using Device MAC address**

```plaintext
https://gears.opswat.com/o/api/v3.3/devices/action?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
{
    "types" : "fetch_agent_log",
    "ids" : ["1A:2A:3A:4A:5A:6A","1B:2B:3B:4B:5B:6B", "1C:2C:3C:4C:5C:6C"]
}
```

**Example Response**

```plaintext
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
```

**Example Request: scan_threats action**

```plaintext
https://gears.opswat.com/o/api/v3.3/devices/action?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
{
    "types" : "scan_threats",
    "ids" : ["device123","device456", "device789"],
    "params" : {
        "full_scan": 0,
		"scan_types": [1, 2, 3, 4],
		"path": "C:\\Windows"
    }
}
```

**Example Response**

```plaintext
[
	{
		"id": "device123",
		"status": 1,
		"command_id": "cdhk12j279h35k214"
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
```

## History

| Action | Version | URL |
| ---- | ---- | ---- |
| Device Action | 3.2 | [Device Action v3.2](https://www.opswat.com/docs/macloud-sdp/developer-guide/device-actionmzs) |
| Device Action | 3.1 | [Device Action v3.1](https://www.opswat.com/docs/macloud-sdp/developer-guide/device-action-v3-1) |
| Device Action | 3.0 | [Device Action v3.0](https://www.opswat.com/docs/macloud-sdp/developer-guide/device-action-v3-0) |
| Delete | 2.0 | [Delete Device v2.0](https://www.opswat.com/docs/macloud-sdp/developer-guide/delete-device-v2-0) |
| Renew IP Exempt Unexempt | 2.0 | [Device Action v2.0](https://www.opswat.com/docs/macloud-sdp/developer-guide/device-action-v2-0) |
