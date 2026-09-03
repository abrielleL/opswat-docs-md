<!-- source: https://www.opswat.com/docs/cm/developer-guidelines/device-information -->

# Device Information

| API version | 3.0 |
| ---- | ---- |
| Last Update | 04/02/2019 |
| Authentication | YES |
| HTTP Method | POST |
| Content Type | application/json |
| Rate limited | YES |
| Requests per rate limit | 10/min |
| Response Format | JSON |
| Changes |  |

Use to retrieve device information.

## API URL

```plaintext
https://gears.opswat.com/o/api/v3/device_info
```

## Request Parameters

| Key | Datatype | Parameter Type | Required | Description | Default |
| ---- | ---- | ---- | ---- | ---- | ---- |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step |  |
| opt | int | Body | Optional | Specify a type of the ids parameter - 0: Device ID or Mac Address - 1: 3rd party custom ID which is linked with a device |  |
| ids | string | Body | Yes | ID of a device. It can be Device ID or Device MAC address or a custom ID - 0: Device ID or MAC Address - 1: 3rd party custom ID which is linked with a device |  |
| select | object | Body | Optional | select data to return in response data |  |
| select.categories | array<string> | Body | Optional | Specify categories which are returned in response. If this is not defined or empty, all categories applied for a device will be returned Values can be "vulnerabilities", "patch_management", "anti-malware", "encryption", "user_authentication", "anti-phishing", "backup", "firewall", "hard_drive", "operating_system", "threats", "repeated_threats", "suspicious_ips", "custom_check", "instant_messenger", "cleaner_optimizer", "developer_tool", "cloud_storage", "public_file_sharing", "remote_control", "recording_web_meeting", "uninstaller", "toolbars", "media_player", "vpn_client", "unclassified_pua", "system_security" | empty |

## Response HTTP Code

Refer to [APIs](https://www.opswat.com/docs/cm/developer-guidelines/apis) page for more details.

## Response Parameters

| Key | Datatype | Returned when | Description |
| ---- | ---- | ---- | ---- |
| device_id | string |  | Device ID which My OPSWAT Central Management generates unique for a device |
| status | string |  | status of device. Values are: - compliant: device is in compliance with a policy which the device is assigned to on your account - non-compliant: device is not in compliance with a policy which the device is assigned to on your account - exempted: device is exempted - out_of_license_usage: device is out of token usage. - unknown: device is not installed My OPSWAT Central Management agent - ignored: device is not installed My OPSWAT Central Management agent and ignored by an administrator - deleted: device is deleted - not-found: device is not found |
| severity | string |  | Severity level. Values are - critical: device has critical issues - warning: device has warning issues - no-issues: device doesn't have any issues |
| device_name | string |  | Hostname of the device. It will get "<private>" value if it's a non-collectible to each fields which related to privacy. |
| categories | array<object> |  | Details of each posture category |
| categories.id | string |  | Category ID. See available values if the description of the parameter " select.categories" in the request parameters. |
| categories.severity | int |  | Values are: - -1: this category is disabled on a policy - 0: no issues found in this category - 1: found warning issues in this category - 2: found critical issues in this category |

## Example

**Example Request**

Description: get device information and only want to get information about the "encryption" category in the response.

```plaintext
https://gears.opswat.com/o/api/v3/device_info?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
{
	"ids": ["S6YE9I3DNJ4IFMP"],
	"opt": 0,
	"select": {
		"categories": ["encryption"]
	}
}
```

## Example Response

```plaintext
[{
	"device_id": "6WXJURV8QAM0I7KC",
	"device_name": "WSEVN09",
	"severity": "critical",
	"status": "compliant",
	"categories": [{
        "id": "encryption",
        "severity": 0,
	}]
}]
```

**Example Request**

Description: get device information with device deleted and device not-found in the response.

```plaintext
https://gears.opswat.com/o/api/v3/device_info?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
{
	"opt": 0,
	"ids": ["S6YE9I3DNJ4IFMP", "TestDeleted", "TestNotFound"]
}
```

## Example Response

```plaintext
[
    {
	    "device_id": "6WXJURV8QAM0I7KC",
		"device_name": "WSEVN09",
		"severity": "critical",
		"status": "compliant",
		"categories": []
	},
	{
		"device_id": "TestDeleted",
		"status": "deleted"
	},
	{
		"device_id": "TestNotFound",
		"status": "not-found"
	}
]
```

**Example Request**

Description: get device information and include all categories information in the response.

```plaintext
https://gears.opswat.com/o/api/v3/device_info?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
{
	"ids": ["S6YE9I3DNJ4IFMP"],
	"opt": 0,
	"select": {
		"categories": []
	}
}
```

## Example Response

```plaintext
[{
	"device_id": "6WXJURV8QAM0I7KC",
	"device_name": "WSEVN09",
	"severity": "critical",
	"status": "non_compliant",
	"categories": [
		{
			"id": "anti-phishing",
			"issue": 0,
		},
		{
			"id": "anti-malware",
			"issue": 1,
		},
		{
			"id": "backup",
			"issue": 2,
		},
		{
			"id": "encryption",
			"issue": 0,
		},
		{
			"id": "firewall",
			"issue": 0,
		},
		{
			"id": "patch_management",
			"issue": -1,
		},
		{
			"id": "instant_messenger",
			"issue": -1,
		},
		{
			"id": "cleaner_optimizer",
			"issue": -1,
		},
		{
			"id": "developer_tool",
			"issue": -1,
		},
		{
			"id": "cloud_storage",
			"issue": -1,
		},
		{
			"id": "public_file_sharing",
			"issue": 0,
		},
		{
			"id": "remote_control",
			"issue": 0,
		},
		{
			"id": "recording_web_meeting",
			"issue": 0,
		},
		{
			"id": "uninstaller",
			"issue": 0,
		},
		{
			"id": "toolbars",
			"issue": 0,
		},
		{
			"id": "media_player",
			"issue": 0,
		},
		{
			"id": "vpn_client",
			"issue": 0,
		},
		{
			"id": "unclassified_pua",
			"issue": 0,
		},

		{
			"id": "hard_drive",
			"issue": 0,
		},
		{
			"id": "operating_system",
			"issue": 0,
		},
		{
			"id": "threats",
			"issue": 0,
		},
		{
			"id": "repeated_threats",
			"issue": 0,
		},
		{
			"id": "custom_check",
			"issue": -1,
		},
		{
			"id": "vulnerabilities",
			"issue": 1,
		},
		{
			"id": "user_authentication",
			"issue": 2,
		},
	]
}]
```
