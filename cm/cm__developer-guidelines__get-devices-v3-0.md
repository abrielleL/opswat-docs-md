<!-- source: https://www.opswat.com/docs/cm/developer-guidelines/get-devices-v3-0 -->

# Get Devices v3.0

| API version | 3.0 |
| ---- | ---- |
| Last Update | 05/08/2018 |
| Authentication | YES |
| HTTP Method | POST |
| Content Type | application/json |
| Rate limited | YES |
| Requests per rate limit | 10/min |
| Response Format | JSON |
| Changes | 05/08/2018: Fixed a bug that the API returns all devices with any group_id 04/10/2018: fixed a bug that the API returns HTTP 200 in response instead of 413 when the page parameter exceeds a page limit 03/12/2018: fixed a bug when "limit" parameter is missed in the API input. It now returns 1 device per request instead of all devices 01/30/2018: removed "guest" value in the "agent_type" input parameter. API will return all monitored devices if agent_type is set to "guest" |

Use to retrieve devices with certain criteria.

## API URL

```plaintext
https://gears.opswat.com/o/api/v3/devices
```

## Request Parameters

| Key | Datatype | Parameter Type | Required | Description | Default |
| ---- | ---- | ---- | ---- | ---- | ---- |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step |  |
| filter | object | Body | Optional | Specify filter criteria |  |
| filter.device_type | array<string> | Body | Optional | Specify type of device. Values can be "desktop","laptop","phone","tablet","server","vm" |  |
| filter.category | array<string> | Body | Optional | Specify category which device has issues. Values can be "antiphishing", "antivirus", "backupclient", "hard_disk_encryption", "firewall", "patch_mangement_agent", "instant_messegener", "cleaner_optimizer", "developer_tool", "cloud_storage", "publicfilesharing", "remote_control", "recording_web_meeting", "uninstaller", "toolbars", "media_player", "vpn_client", "unclassified_pua", "system", "hard_drive", "osupdate", "systemsecurity", "threat_antivirus", "threat_metascan", "threat_ip" |  |
| filter.severity | array<string> | Body | Optional | Specific issue severity which device has Values can be: "critical", "warning", "no_issues" |  |
| filter.os | array<string> | Body | Optional | Specify OS type. Values can be: "windows","mac", "linux", "ios", "android" |  |
| filter.device_status | array<string> | Body | Optional | Specify device status Values can be: "compliant", "non_compliant", "exempted", "out_of_license_usage", "unknown", "ignored", "installed", "pending", "quarantined" |  |
| filter.agent_status | array<string> | Body | Optional | Specify agent status Values can be: "connected", "disconnected", "unseen", "out_of_date" |  |
| filter.agent_type | array<string> | Body | Optional | Specify agent type Values can be: "managed", "dc" |  |
| filter.group_id | array<string> | Body | Optional | Specify group id which a device is assigned to Values can be: |  |
| sort | object | Body | Optional | Specify how to sort devices in result-set By default: sort devices by status in DESC order: quarantined, non-compliant, exempted, compliant, pending, out_of_license_usage, unknown, ignored |  |
| sort.order | string | Body | Optional | Specify sort order. Values can be: - asc: sort devices in ascending order. - desc: sort devices in descending order. | DESC |
| sort.field | string | Body | Optional | Specify which field will be sorted by Values can be: status, ip, nickname, user_name, os, last_seen, issues, group_policy | status |
| search | string | Body | Optional | keyword to search devices. |  |
| limit | int | Body | Optional | Specify maximum number of devices will be returned in the response. The value should be in [1,50]. If there are more devices than what the limit asks for, error code will be 406. | 1 |
| page | int | Body | Optional | Specify page number which devices will be returned in. If the requested page exceeds the number of pages of devices, error code will be 413. It means that the requested page number is too large, no devices will be returned in this case. | 1 |
| verbose | int | Body | Optional | Specify what information you want to see in response - 0: no issue details in the response - 1: device issue details are returned in the response ***(has not supported yet)*** | 0 |

Notes:

- criteria in a same parameter will be combined with OR operator
- criteria in different parameter will be combined with AND operator

## Response HTTP Code

| HTTP Code | Description |
| ---- | ---- |
| 200 | Success |
| 400 | Bad request |
| 401 | Unauthorized. Your access_token is invalid or expired |
| 404 | Not found |
| 406 | Too many devices to return |
| 413 | Requested page number exceeds limit |
| 415 | Unsupported Media Type |

## Response Parameters

| Key | DataType | Description |
| ---- | ---- | ---- |
| device_id | string | HWID of a device |
| severity | string | Issue severity of the device Values can be: "critical", "warning", "no_issues" |
| status | string | device status Values can be: "compliant", "non_compliant", "exempted", "out_of_license_usage", "unknown", "ignored", "installed", "pending", "quarantined" |
| device_name | string | device name |
| nickname | string | device nickname (editable on the cloud console) |
| device_type | string | device type Values can be "desktop","laptop","phone","tablet","server","vm" |
| last_seen | string | The last timestamp in GMT format when MetaAccess reports its data to Cloud |
| agent_version | string | agent version |
| remediation_link | string | URL of remediation page for the given device |
| group_name | string | Group name which a device is assigned to |
| issue | object | Summary of issues a device has |
| issue.total_issues | int | number of issues a device has |
| issue.total_critical_issue | int | number of critical issues a device has |
| issue.total_warning_issue | int | number of warning issues a device has |
| geo_info | object | Location details of the device where the device was in the last report |
| geo_info.country | string | country of the device where the device was in the last report |
| network_info | array<object> | Network adapter information block |
| network_info.mac | string | MAC address of a network adapter |
| network_info.ipv4 | string | IPV4 address of a network adapter |
| os_info | array<object> | Operation system block |
| os_info.family | string | OS family |
| os_info.name | string | OS name |
| os_info.vendor | string | OS vendor |
| os_info.version | string | OS version |
| os_info.type | string | OS type. Values can be: "windows","mac", "linux", "ios", "android" |
| link_user | object | Linked user details |
| link_user.username | string | Username |
| link_user.group | string | group which the user is associated to |
| user_info | object | User information block |
| user_info.username | string | Currently logged in username |
| user_info.domain | string | Currently logged in user domain |

## Example

**Example Request**

Description: retrieve 20 first Windows devices which has antivirus issues or encryption issues and sort devices in ASC order by number of issues

```plaintext
https://gears.opswat.com/o/api/v3/devices?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
{
	"filter": {
		"category": ["antivirus", "hard_disk_encryption"],
		"os": ["windows"]
	},
	"sort": {
		order: "asc",
		field: "issues"
	},
	"limit": 20,
	"page": 1
}
```

## Example Response

```plaintext
[{
	"device_id": "6WXJURV8QAM0I7KC",
	"severity": "critical",
	"status": "compliant",
	"device_name": "WSEVN09",
	"nickname": "WSEVN09",
	"device_type": "laptop",
	"last_seen": "2013-12-04T08:00:00Z",
 
	"agent_version": "6.1.51.0",
	"remediation_link": "https://gears.opswat.com/gears/remediation/2dac92f8fa8dfe02414835d792fb412f/6WXJURV8QAM0I7KC/009nOa7nMaInXaDnMaZ1J/remediation.html",
	"group_name": "default",
	"issue": {
		"total_issues": 10,
		"total_critical_isues": 3,
		"total_warning_issues": 7
	},
	"geo_info": {
		"country": "VN"
	},
	"network_info": [{
		"mac": "00:aa:cc:Dd:ee:ff",
		"ipv4": "10.0.50.106"
	}],
	"os_info": {
		"family": "Windows",
		"name": "Windows 7 Enterprise",
		"vendor": "Microsoft Corp.",
		"version": "6.1.7600",
		"type": "mac"
	},
	"link_user": {
		"username": "Thang",
		"group": "MEM"
	},
	"user_info": {
		"username": "tle",
		"domain": "intl.opswat.com"
	}
}]
```

## History

| Version | URL |
| ---- | ---- |
| v2.3 | [Get Devices v2.3](https://www.opswat.com/docs/cm/developer-guidelines/get-devices-v2-3) |
| v2.2 | [Get Devices v2.2](https://www.opswat.com/docs/cm/developer-guidelines/get-devices-v2-2) |
| v2.1 | [Get Devices v2.1](https://www.opswat.com/docs/cm/developer-guidelines/get-devices-v2-1) |
| v2.1 | [Search Devices v2.1](https://www.opswat.com/docs/cm/developer-guidelines/search-devices-v2-1).1 |
