<!-- source: https://www.opswat.com/docs/cm/developer-guidelines/status-change -->

# Status Change

| API version | 3.0 |
| ---- | ---- |
| Last Update | 01/30/2018 |
| Authentication | YES |
| Response Format | JSON |
| HTTP Method | POST |
| Content Type | application/json |
| Rate limited | YES |
| Requests per rate limit | 10/min |
| History | 04/10/2018: fixed a bug that the API returns HTTP 400 instead of 406 if the limit parameter is greater than 50 |

Use the above to obtain status change (delta) of all devices in an account in a particular time frame.

## API URL

```plaintext
https://gears.opswat.com/o/api/v3/devices/status_changed
```

## Request Parameters

| Key | Datatype | Parameter Type | Required | Description | Default |
| ---- | ---- | ---- | ---- | ---- | ---- |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step [here](https://docs.opswat.com/macloud-sdp/3.14.0/developer-guide/how-to-work-with-metaaccess-apis). |  |
| age | int | Body | Optional | Specify age of the information in seconds. Value is from 0 to 86400. For example, if you want delta of information for last 5 minutes you need to set age as 300. | 86400 |
| verbose | int | Body | Optional | Specify what information you want to see in response - **0**: no issue details in the response - **1**: device issue details are returned in the response | 0 |
| page | int | Body | Optional | Specify page number which devices will be returned in. If the requested page exceeds the number of pages of devices, error code will be 413. It means that the requested page number is too large, no devices will be returned in this case. | 1 |
| limit | int | Body | Optional | Specify maximum number of devices will be returned in the response. The value should be in [1,50]. If there are more devices than what the limit asks for, error code will be 406. | 20 |

## Response HTTP Code

See details in the Response HTTP Code section in [this page](https://www.opswat.com/docs/cm/developer-guidelines/apis)

## Response Parameters

| Key | Datatype | Description |
| ---- | ---- | ---- |
| device_id | string | Hardware ID of the device |
| status | string | status of device. Values are: - **compliant**: device is in compliance with a policy which the device is assigned to on your account - **non-compliant**: device is **not** in compliance with a policy which the device is assigned to on your account - **exempted**: device is exempted |
| status_detail | object | status detail of device. Values are: - exempted:   - **0**: device is not exempted   - **1**: device is exempted - pending:   - **0**: device reported to My OPSWAT Central Management cloud   - **1**: device has not been reported to My OPSWAT Central Management yet - compliant :   - **0**: device is non-compliant with policy   - **1**: device is in compliance with policy |
| severity | string | Severity level. Values are - **critical**: device has critical issues - **warning**: device has warnings - **no-issues**: device doesn't have any issues |
| issue | object | Issue details on the device |
| issue.total_issues | int | Total issues on the device |
| issue.total_critical_issues | int | Total critical issues on that device |
| issue.total_warning_issues | int | Total warnings on the device |
| group_name | string | group name which a device is assigned to |
| device_name | string | Hostname of the device. It will get "<private>" value if it's a non-collectible to each fields which related to privacy. |
| nick_name | string | a nickname for the device which an administrator can update on the My OPSWAT Central Management console |
| device_type | string | The type of the device |
| agent_version | string | Local resident My OPSWAT Central Management agent version |
| oesis_version | string | SDK version which the agent is running |
| last_seen | string | The last timestamp in GMT format when the agent reports data to the Cloud |
| public_ip | string | public IP of the device in the last report |
| country | string | Region where the device IP geographically represents |
| user_identity | string | Custom user identity information. This is only available if the account enables "Enforce users enter custom information" on **Advanced Settings** tab in **Settings > Global**. |
| user_info | object | User information block |
| user_info.username | string | username of who currently logs in. This field will be remove if it's set as privacy |
| user_info.domain | string | Currently logged in user domain |
| remediation_link | string | remediation page URL of the given device |
| os_info.family | string | OS family |
| os_info.name | string | OS name |
| os_info.vendor | string | OS vendor |
| os_info.version | string | OS version |
| os_info.service_pack_version | string | OS Service Pack Version |
| os_info.architecture | string | OS architecture |
| os_info.os_language | string | OS language |
| os_info.user_password_set | int | Values are 0: password is not set 1: password is set |
| network_info | array<object> | Network adapter information block |
| network_info.description | string | network card description |
| network_info.mac | string | Media Access Control (MAC) address of the network adapter. This field will be remove if it's a disabled field in relation to privacy settings. |
| network_info.ipv4 | string | IPv4 addresses associated with the network adapter. This field will be remove if it's a disabled field in relation to privacy settings. |
| network_info.ipv6 | string | IPv6 addresses associated with the network adapter. This field will be remove if it's a disabled field in relation to privacy settings. |
| network_info.subnet_mask | string | the subnet mask associated with the current network adapter. |
| network_info.media_state | string | network card state |
| network_info.dhcp_enabled | string | DHCP enabled state of installed network adapter. |
| network_info.dhcp_obtained | string | (Optional)The timestamp in GMT format when the lease was obtained for the IP address assigned to the computer by the DHCP server. |
| network_info.dhcp_expires | string | (Optional)The expiration timestamp in GMT format for a leased IP address that was assigned to the computer by the DHCP server. |
| network_info.dhcp_server | string | (Optional)IP address of the dynamic host configuration protocol (DHCP) server. |
| network_info.adapter_enabled | string | Indicates whether the adapter is enabled or not. |
| network_info.default_gateway | string | (Optional)Array of IP addresses of default gateways that the computer system uses. |
| network_info.dns_addresses | array<string> | (Optional)Array of server IP addresses to be used in querying for DNS servers. |
| link_user | object | User is linked by admin (editable) |
| link_user.username | string | Username is linked to device by admin |
| link_user.group | string | Group is linked to device by admin |

## Example 1: verbose as OFF

**Request:**

```plaintext
POST https://gears.opswat.com/o/api/v3/devices/status_changed?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
BODY
{
	"age": 3600,
	"page": 1,
	"limit": 20
}
```

**Response**

```plaintext
{
	"monitored_devices": [{
		"device_id": "SGN56789",
		"severity": "critical",
		"status": "compliant",
		"issue": {
			"total_issue": 10,
			"total_critical_issue": 3,
			"total_warning_issue": 7
		},
		"network_info": [{
			"ipv4": "109.184.237.115",
			"mac": "02:21:9b:06:4b:96",
		}],
	}],
	"deleted_devices":[{
		"device_id": "SGN012345",
		"network_info": [{
			"ipv4": "109.184.237.115",
			"mac": "02:21:9b:06:4b:96",
		}]
	}]
}
```

## Example 2: verbose as ON for device detail

**Request:**

```plaintext
POST https://gears.opswat.com/o/api/v3/devices/status_changed?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
BODY
{
	"age": 3600,
	"page": 1,
	"limit": 20,
	"verbose": 1
}
```

**Response**

```plaintext
{
	"monitored_devices": [{
		"device_id": "S6YE9I3DNJ4IFMP84LIGG8S8207R4E04",
		"device_type": "desktop",
		"device_name": "tle",
		"nick_name": "tle-accounting",
		"group_name": "default",
		"agent_version": "7.6.51.0",
		"oesis_version": "4.2.1041.0",
		"country": "US",
		"last_seen": "2017-10-16T03:11:09Z",
		"public_ip": "54.78.191.2",
		"remediation_link": ".../remediation.html",
		"user_identity": "accounting",
		"link_user": {
			"username": "testinguser",
			"group": "testinggroup"
		},
		"user_info": {
			"username": "tle",
			"domain": "INTL"
		},
		"network_info": [{
			"description": "Intel(R) Ethernet Connection I217-LM",
			"ipv4": "109.184.237.115",
			"ipv6": "fe80::2d88:eab7:6001:6ec7",
			"mac": "02:21:9b:06:4b:96",
			"subnet_mask": "255.255.254.0",
			"media_state": "connected",
			"dhcp_enabled": "true",
			"dhcp_obtained": "2015-10-16T03:11:09Z",
			"dhcp_expires": "2015-10-16T03:11:09Z",
			"dhcp_server": "171.64.7.111",
			"adapter_enabled": "true",
			"default_gateway": "171.65.76.1",
			"dns_addresses": ["171.67.1.234","171.64.1.234"]
		}],
		"os_info": {
			"service_pack_version": "1.0",
			"vendor": "Microsoft Corp.",
			"family": "Windows",
			"os_language": "English",
			"name": "Microsoft Windows 7 Professional ",
			"architecture": "64-bit",
			"version": "6.1.7601",
			"type": "windows"
		},
		"severity": "critical",
		"status": "compliant",
		"status_detail": {
			"exempted": 0,
			"pending": 0,
			"compliant": 0
		},
		"issue": {
			"total_issue": 10,
			"total_critical_issue": 3,
			"total_warning_issue": 7
		}
	}],
	"deleted_devices":[{
		"device_id": "SGN012345",
		"network_info": [{
			"ipv4": "109.184.237.115",
			"mac": "02:21:9b:06:4b:96",
		}]
	}]
}
```

**Example 3: when there is no devices changes status**

**Request:**

```plaintext
POST https://gears.opswat.com/o/api/v3/devices/status_changed?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
BODY
{
	"age": 3600,
	"page": 1,
	"limit": 20
}
```

**Response**

```plaintext
{ "monitored_devices": [], "deleted_devices": [] }
```

## History

| Version | URL |
| ---- | ---- |
| v2.1 | [Status Change v2.1](https://www.opswat.com/docs/macloud-sdp/developer-guide/status-change-v2-1) |
