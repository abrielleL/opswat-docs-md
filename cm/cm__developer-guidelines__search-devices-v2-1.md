<!-- source: https://www.opswat.com/docs/cm/developer-guidelines/search-devices-v2-1 -->

# Search Devices v2.1

| API version | 2.1 |
| ---- | ---- |
| Last Update | 01/30/2018 |
| Authentication | YES |
| Response Format | JSON |
| HTTP Method | GET |
| Rate limited | YES |
| Requests per rate limit | 10/min |
| Changes | 01/30/2018: removed agent_type in input parameters. API will ignore agent_type parameter in the input |

Use to query devices on a given account

## API URL

```plaintext
https://gears.opswat.com/o/api/v2.1/devices/search
```

## Request Parameters

| Key | Datatype | Parameter Type | Required | Description | Default |
| ---- | ---- | ---- | ---- | ---- | ---- |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step |  |
| q | string | URL | Yes | Specific search keywords, as well as any qualifiers. Multi-words are separated by **+**, for example Tomas Hertus is searched as tomas+hertus. Minimum of characters is **3**. Maximum of characters is **100** |  |
| in | string | URL | Yes | Qualifies which fields are used for search. The caller of the API is responsible for providing this information. |  |
| limit | int | URL | Optional | Specific maximum number of devices will be returned in the response. The value should be in [1,50]. If there are more devices than what the limit asks for, error code will be 406. **Maximum value is 50** | 10 |
| page | int | URL | Optional | Specific page number which devices will be returned in. If the requested page exceeds the number of pages of devices, error code will be 413. It means that the requested page number is too large, no devices will be returned in this case. | 1 |

## Response HTTP Code

| HTTP Code | Description |
| ---- | ---- |
| 200 | Success |
| 400 | Bad request |
| 401 | Unauthorized. Your access_token is invalid or expired |
| 404 | Not found |
| 406 | Too many devices to return |
| 413 | Requested page number exceeds limit |

## Response Parameters

| Key | DataType | Description |
| ---- | ---- | ---- |
| total_count | int | Number of devices which match to search criteria |
| results | array<object> | Lists of devices which match to search criteria |
| results.hwid | string | Hardware ID of the device |
| results.remediation_link | string | URL on remediation page for given device |
| results.status | int | Reports the health status of the endpoint device. This status is based on the defined policy within . Status values are: - **0** – the endpoint is in compliance with MetaAccess account’s policies - **1** – the endpoint is **not** in compliance with MetaAccess account’s policies - **3** – the endpoint is still sending information to and not yet completed |
| results.hostname | string | Hostname of the device |
| results.nickname | string | nickname for the device (admin editable) |
| results.agent_version | string | Local resident MetaAccess agent version |
| results.last_seen | string | The last timestamp in GMT format when MetaAccess agent reports its data to Cloud |
| results.machine_type | string | The type of devices |
| results.country | string | Region where the device IP geographically represents |
| results.active | int | 1 - device is active, 0 - deactive |
| results.total_issue | int | Number of issues were seen on the device |
| results.user | string | Username of a group |
| results.user_info | object | User information block |
| results.user_info.username | string | Currently logged in username |
| results.user_info.domain | string | Currently logged in user domain |
| results.os_info | object | Operation system block |
| results.os_info.family | string | OS family |
| [results.os_info.name](http://os_info.name) | string | OS name |
| results.os_info.vendor | string | OS vendor |
| results.os_info.version | string | OS version |
| results.os_info.service_pack_version | string | OS Service Pack Version |
| results.os_info.architecture | string | OS architecture |
| results.os_info.os_language | string | OS language |
| results.os_info.user_password_set | int | If user password is set on OS, 1 is set, 0 is not set |
| results.network_info | array<object> | Network adapter information block |
| results.network_info.mac_addr | string | MAC address for adapter |
| results.network_info.ipv4_addr | string | IPV4 address |
| results.network_info.ipv6_addr | string | IPV6 address |

## Example

**Example Request**

```plaintext
//Search by Device Name and Nick Name:
https://gears.opswat.com/o/api/v2.1/devices/search?q=test&in=name&access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
 
//Search by Device ID:
https://gears.opswat.com/o/api/v2.1/devices/search?q=234fs23&in=id&access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
 
//Search by MAC Address:
https://gears.opswat.com/o/api/v2.1/devices/search?q=00:1d:09:2d:c7:95&in=mac_address&access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
 
//Search by IP Address:
https://gears.opswat.com/o/api/v2.1/devices/search?q=192.168.1.1&in=ip_address&access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
 
Search by Username:
https://gears.opswat.com/o/api/v2.1/devices/search?q=tomas+hertus&in=username&access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
```

**Advanced Example Request**

```plaintext
Search by IP and MAC Address:
https://gears.opswat.com/o/api/v2.1/devices/search?q=00:1d&in=ip_address,mac_address&access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
 
Search by Name and ID:
https://gears.opswat.com/o/api/v2.1/devices/search?q=asd&in=name,id&access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
```

**Example Response**

```plaintext
{
	"total_count": 40,
	"results": [{
		"hwid": "6WXJURV8QAM0I7KC",
		"hostname": "Win_7ENTx64_English",
		"nickname": "Win_7ENTx64_English",
		"agent_version": "6.1.51.0",
		"last_seen": "2013-12-04T08:00:00Z",
		"machine_type": "laptop",
		"country": "Unknown",
		"active": 1,
		"total_issue": 10,
		"user_info": {
			"username": "test",
			"domain": "WIN_7ENTX64_ENG"
		},
		"user": "",
		"os_info": {
			"family": "Windows",
			"name": "Windows 7 Enterprise",
			"vendor": "Microsoft Corp.",
			"version": "6.1.7600",
			"service_pack_version": "0.0",
			"architecture": "64-Bit",
			"os_language": "",
			"user_password_set": "1"
		},
		"network_info": [{
			"mac_addr": "00:0c:29:f2:7a:29",
			"ipv4_addr": "10.0.50.106",
			"ipv6_addr": "fe80::3c64:7e44:4e78:677"
		}],
		"status": 1,
		"remediation_link": "https://gears.opswat.com/gears/remediation/2dac92f8fa8dfe02414835d792fb412f/6WXJURV8QAM0I7KC/009nOa7nMaInXaDnMaZ1J/remediation.html"
	}]
}
```
