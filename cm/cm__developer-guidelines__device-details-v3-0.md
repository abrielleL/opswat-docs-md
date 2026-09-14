<!-- source: https://www.opswat.com/docs/cm/developer-guidelines/device-details-v3-0 -->

# Device Details v3.0

| API version | 3.0 |
| ---- | ---- |
| Last Update | 12/12/2017 |
| Authentication | YES |
| HTTP Method | POST |
| Content Type | application/json |
| Rate limited | YES |
| Requests per rate limit | 10/min |
| Response Format | JSON |
| Changes | 05/23/2017: add one more parameter to response json, user_identity. 07/18/2017: add support verbose parameter in the json input 12/12/2017: add release_date parameter to each missing patch |

Use to fetch device details by ID or MAC address.

## API URL

```plaintext
https://gears.opswat.com/o/api/v3/devices/:value
```

## Request Parameters

| Key | Datatype | Parameter Type | Required | Description | Default |
| ---- | ---- | ---- | ---- | ---- | ---- |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step |  |
| value | string | URL | Yes | The Device ID or MAC Address of a device you want to fetch information. |  |
| verbose | object | Body | Optional | Specify what information you are look for |  |
| verbose.categories | int | Body | Optional | Specify if categories issues the device has are included on the response Values can be: - 0: not include - 1: include | 1 |
| verbose.unclassified | int | Body | Optional | Only applicable for Wins/macOS devices Specify if unclassified applications are included on the response Values can be: - 0: not include - 1: include | 0 |
| verbose.mobile_apps | int | Body | Optional | Only applicable for iOS/Android devices Specify if installed applications are included on the response Values can be: - 0: not include - 1: include | 0 |
| verbose.detected_processes | int | Body | Optional | Only applicable for Linux devices Specify if running processes are included on the response Values can be: - 0: not include - 1: include | 0 |
| verbose.detected_packages | int | Body | Optional | Only applicable for Linux devices Specify if installed packages are included on the response Values can be: - 0: not include - 1: include | 0 |
| verbose.detected_patches | int | Body | Optional | Only applicable for wins/macOS devices Specify if missing OS patches are included on the response Values can be: - 0: not include - 1: include | 0 |

## Response HTTP Code

| HTTP Code | Description |
| ---- | ---- |
| 200 | Success |
| 401 | Unauthorized. Your access_token is invalid or expired |
| 404 | Not found |

## Response Parameters

| Key | Datatype | Description |
| ---- | ---- | ---- |
| device_id | string | Hardware ID of the device |
| status | string | status of device. Values are: - compliant: device is in compliance with a policy which the device is assigned to on your account - non-compliant: device is **not** in compliance with a policy which the device is assigned to on your account - exempted: device is exempted - out_of_license_usage: device is out of token usage. - unknown: device is not installed MetaDefender Endpoint - ignored: device is not installed MetaDefender Endpoint and ignored by an administrator |
| status_detail | object | status detail of device. Values are: - agent_installed :   - 1 : device is installed MetaDefender Endpoint   - 2 : device is not installed MetaDefender Endpoint but detected by Network Discovery or Domain Controller agent   - 3 : device is not installed MetaDefender Endpoint but detected by Network Discovery or Domain Controller agent and ignored by an administrator - out_of_token:   - 0 :device is not out of token usage   - 1 :device is out of token usage - exempted:   - 0: device is not exempted   - 1: device is exempted - pending:   - 0: device reported to My OPSWAT Central Management cloud   - 1: device has not been reported to My OPSWAT Central Management cloud yet - compliant :   - 0: device is non-compliance with policy   - 1: device is in compliance with policy - quarantined :   - 0: device is not quarantined   - 1: device is quarantined |
| severity | string | Severity level. Values are - critical: device has critical issues - warning: device has warning issues - no-issues: device doesn't have any issues |
| issue | object | Issue details on the device |
| issue.total_issues | int | Total issues of device |
| issue.total_critical_issues | int | Total critical issues of device |
| issue.total_warning_issues | int | Total warning issues of device |
| group_name | string | group name which a device is assigned to |
| agent_type | string | Type of agent Values: managed – Managed device dc - Domain controller device |
| device_name | string | Hostname of the device. It will get "<private>" value if it's a non-collectible to each fields which related to privacy. |
| nick_name | string | a nickname for the device which an administrator can update on the My OPSWAT Central Management console |
| device_type | string | The type of the device |
| agent_version | string | Local resident MetaDefender Endpoint version |
| oesis_version | string | SDK version which the agent is running |
| last_seen | string | The last timestamp in GMT format when the agent reports data to the Cloud |
| public_ip | string | public IP of the device in the last report |
| country | string | Region where the device IP geographically represents |
| user_identity | string | Custom user identity information. This is only available if the account enables "Enforce users enter custom information" on Advanced Setting tab on Global Settings |
| user_info | object | User information block |
| user_info.username | string | username who currently logs in. This field will be remove if it's set as privacy |
| user_info.domain | string | Currently logged in user domain |
| remediation_link | string | remediation page URL of the given device |
| categories | array<object> | Details of each posture category |
| categories.category_id | string | category ID which the current block stands for |
| categories.issue | int | Severity of the category based on the defined policy on your My OPSWAT Central Management account. Values are: - -1 - category is disabled - 0 – no issues - 1 – warning - 2 – critical |
| categories.apps | array<object> | detailed products in a category |
| categories.apps.id | string | Product ID |
| categories.apps.name | string | Name of the product |
| categories.apps.vendor | string | Name of the product vendor |
| categories.apps.version | string | Product version |
| categories.apps.category_id | string | category ID of the product |
| categories.apps.health_status | array<object> | health information of the product |
| categories.apps.health_status.status | string | product compliance details |
| categories.apps.health_status.issue | int | Severity of the product based on the defined policy on your My OPSWAT Central Management account Values are: - -1 - Not an approved product - 0 - no issues - 1 - warning - 2 - critical |
| unclassified | array<object> | Lists of unclassified products |
| unclassified.id | string | product ID |
| unclassified.name | string | product name |
| unclassified.vendor | string | product vendor |
| unclassified.version | string | product version |
| os_info | object | Operation system information |
| os_info.family | string | OS family |
| os_info.name | string | OS name |
| os_info.vendor | string | OS vendor |
| os_info.version | string | OS version |
| os_info.service_pack_version | string | OS Service Pack Version |
| os_info.architecture | string | OS architecture |
| os_info.os_language | string | OS language |
| os_info.user_password_set | int | If user password is set on OS, 1 is set, 0 is not set |
| network_info | array<object> | Network adapter information block |
| network_info.description | string | network card description |
| network_info.mac | string | Media Access Control (MAC) address of the network adapter.. This field will be remove if it's a non-collectible to each fields which related to privacy. |
| network_info.ipv4 | string | IPv4 addresses associated with the network adapter. This field will be remove if it's a non-collectible to each fields which related to privacy. |
| network_info.ipv6 | string | IPv6 addresses associated with the network adapter. This field will be remove if it's a non-collectible to each fields which related to privacy. |
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
| mobile_apps | array<object> | **Only applicable for iOS/Android devices** Lists of applications installed on the device |
| mobile_apps.name | string | application name |
| mobile_apps.vendor | string | application vendor |
| mobile_apps.community_rate | string | rating from community |
| mobile_apps.community_reviewer | string | number of community reviewers who reviewed the application |
| detected_processes | object | **Only applicable for Linux devices** Details about running processes on the device when the device reports data to My OPSWAT Central Management cloud |
| detected_processes.total | int | number of running processes on the device when the device reports data to My OPSWAT Central Management cloud |
| detected_processes.processes | array<object> | Lists of running processes on the device when the device reports data to My OPSWAT Central Management cloud with details |
| detected_packages | object | **Only applicable for Linux devices** Details about packages installed on the device when the device reports data to My OPSWAT Central Management cloud |
| detected_packages.total | int | number of packages installed on the device when the device reports data to My OPSWAT Central Management cloud |
| detected_packages.processes | array<object> | Lists of packages installed on the device when the device reports data to My OPSWAT Central Management cloud |
| detected_patches | object | Only applicable for Windows/macOS devices Details about missing patches on the device when the device reports data to My OPSWAT Central Management cloud |
| detected_patches.timestamp | string | timestamp in GMT format when the device reports data to My OPSWAT Central Management cloud |
| detected_patches.total | int | Total missing patches on the device when the device reports data to My OPSWAT Central Management cloud |
| detected_patches.patches | array<object> | Lists of missing patches on the device when the device reports data to My OPSWAT Central Management cloud |
| detected_patches.patches.category | string | The category of a missing patch: 'security_update', 'update_rollup', 'critical_update', 'update', 'driver', 'service_pack', 'unknown'. |
| detected_patches.patches.titles | string | The title of a missing patch. |
| detected_patches.patches.description | string | The description of a missing patch. |
| detected_patches.patches.product | string | The product missing this patch. |
| detected_patches.patches.vendor | string | (optional) The vendor of the product missing this patch |
| detected_patches.patches.severity | string | The severity of a missing patch: 'low', 'moderate', 'important', 'critical', 'unknown'. |
| detected_patches.patches.kb_name | string | (optional)The knowledge base article id of a missing patch. May duplicate security_update_id on some platforms. |
| detected_patches.patches.release_date | string | A timestamp in GMT format when a patch is released |
| infection | object | Details on threat detection |
| infection.metascan | object | Only applicable for Windows/macOS/Linux devices Infection information block which is detected by [Metadefender Cloud](https://www.metadefender.com) |
| infection.metascan.total | int | Total infections which is detected by [Metadefender Cloud](https://www.metadefender.com) |
| infection.metascan.issue | int | Status of Daily [Metadefender Cloud](https://www.metadefender.com/) anti-malware scan based on a device policy on your My OPSWAT Central Management account Values are: - -1 – category is disabled - 0 – category doesnot have issues - 1 – category has issues - 2 – category has critical issues |
| infection.metascan.threats | array<object> | Lists of found threats |
| infection.metascan.threats.critical | int | Critical status of the threat Values are: - 0 – not critical - 1 – critical |
| infection.metascan.threats.scan_time | string | timestamp when found the threat |
| infection.metascan.threats.file | string | File was found the threat |
| infection.metascan.threats.hash | string | hash of the file |
| infection.metascan.threats.threat_name | string | Threat name |
| infection.metascan.threats.details | array<object> | threat details on each engine which detected the threat |
| infection.metascan.threats.details.threat_name | string | Threat name which detected on a specific engine |
| infection.metascan.threats.details.av_name | string | engine name |
| infection.antivirus | object | Only applicable for Windows/macOS devices Repeated threat details detected by local anti-malware applications |
| infection.antivirus.total | int | Total repeated threats which are detected by local anti-malware applications |
| infection.antivirus.issue | int | Status of repeated threats based on a device policy on your My OPSWAT Central Management account Values are: - -1 – category is disabled - 0 – category doesnot have issues - 1 – category has issues - 2 – category has critical issues |
| infection.antivirus.threats | array<object> | Lists of repeated threats |
| infection.antivirus.threats.critical | int | Critical status of the threat Values are: - 0 – not critical - 1 – critical |
| infection.antivirus.threats.scan_time | string | Last timestamp when the threat was detected |
| infection.antivirus.threats.repeat | int | Number of times the threat was detected |
| infection.antivirus.threats.file | string | File was detected as a threat |
| infection.antivirus.threats.hash | string | hash of the file |
| infection.antivirus.threats.threat_name | string | threat name |
| infection.antivirus.threats.product_name | string | product name which detected the threat |
| infection.antivirus.threats.product_vendor | string | vendor name |
| infection.antivirus.threats.product_version | string | product version |
| infection.antivirus.threats.severity | string | threat severity |
| infection.antivirus.threats.action | string | The type of remediation ( unknown, cleaned, deleted, quarantined) |
| infection.ip_scanning | object | Only applicable for LINUX/MOBILE devices Details of daily scan for suspicious IP connections |
| infection.ip_scanning.total | int | Total of suspicious IPs |
| infection.ip_scanning.issue | int | Status of the suspicious IP based on a device policy on your My OPSWAT Central Management account Values are: - -1 – category is disabled - 0 – category doesnot have issues - 1 – category has issues |
| infection.ip_scanning.threats | array<object> | Lists of suspicious IPs |
| infection.ip_scanning.threats.geo_info | object | An object represents the geolocation of the suspicious IP |
| infection.ip_scanning.threats.geo_info.country_code | string | Region name of the network address (e.g., San Paulo) |
| infection.ip_scanning.threats.geo_info.city | string | Country name of the network address (e.g., Brazil) |
| infection.ip_scanning.threats.geo_info.country_name | string | Country name of the network address (e.g., BR) |
| infection.ip_scanning.threats.geo_info.region_name | string | Region code of the network address (e.g., 27) |
| infection.ip_scanning.threats.geo_info.region_code | string | City name of the network address (e.g., San Paulo) |
| infection.ip_scanning.threats.network_address | string | IP address of the suspicious IP |
| infection.ip_scanning.threats.status | string | indicates the scanning object is clear, dirty or in-progress |
| infection.ip_scanning.threats.total_source | int | number of total source |
| infection.ip_scanning.threats.threats | array<object> | details of IP connections |
| infection.ip_scanning.threats.threats.assessment | string | Type of threat detected |
| infection.ip_scanning.threats.threats.confident | string | Represents the reliability of the detection based on several factors. The higher the score, the more reliable the result. |
| infection.ip_scanning.threats.threats.source_name | string | Source of the feed, usually the domain where the feed is from (e.g., [example.com](http://example.com/) ) |

## Example

**Example Request**

```plaintext
https://gears.opswat.com/o/api/v3/devices/02:21:9b:06:4b:96?access_token=YOUR_ACCESS_TOKEN
{
	"verbose": {
		"categories": 1,
		"unclassified": 1,
		"mobile_apps": 1,
		"detected_processes": 1,
		"detected_packages": 1,
		"detected_patches": 1
	}
}
```

**Example Response**

```plaintext
{
	"device_id": "S6YE9I3DNJ4IFMP84LIGG8S8207R4E04",
	"device_type": "desktop",
	"device_name": "tle",
	"nick_name": "tle-accounting",
	"agent_version": "7.6.51.0",
	"oesis_version": "4.2.1041.0",
	"country": "US",
	"last_seen": "2017-10-16T03:11:09Z",
	"public_ip": "54.78.191.2",
	"agent_type": "managed",
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
		"dns_addresses": ["171.67.1.234", "171.64.1.234"]
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
		"agent_installed": 1,
		"out_of_token": 0,
		"exempted": 0,
		"pending": 0,
		"compliant": 0,
		"quarantined": 0
	},
	"group_name": "default",
	"issue": {
		"total_issue": 10,
		"total_critical_issue": 3,
		"total_warning_issue": 7
	},
	"categories": [{
		"category_id": "Firewall",
		"issue": 0,
		"apps": [{
			"id": "d609bfa8601edf0e8fcb6e919570204e",
			"name": "Microsoft Windows Firewall",
			"vendor": "Microsoft Corp.",
			"version": "7",
			"category_id": "Firewall",
			"health_status": [{
				"status": "Enabled",
				"issue": 0
			}],
			"issue": 0
		}]
	}, {
		"category_id": "Antivirus",
		"issue": 1,
		"apps": [{
			"id": "a896b7b839ef62671314990f8d1d6794",
			"name": "Microsoft Security Essentials",
			"vendor": "Microsoft Corp.",
			"version": "4.4.0304.0",
			"health_status": [{
				"status": "Real time protection is on",
				"issue": 0
			}, {
				"status": "Virus definitions were updated within the last 3 days",
				"issue": 0
			}, {
				"status": "A full system scan was run within the last week",
				"issue": 0
			}, {
				"status": "35 threats detected within the last week",
				"issue": 1
			}],
			"issue": 1
		}]
	}],
	"unclassified": [{
		"id": "d609bfa8601edf0e8fcb6e919570204e",
		"name": "OPSWAT GEARS",
		"vendor": "OPSWAT, Inc.",
		"version": "7"
	}],
	"detected_patches": {
		"timestamp": "May 25, 2016 2:04:42 AM",
		"total": 500,
		"patches": [{
			"category": "security_update",
			"title": "Cumulative Security Update for......",
			"description": "A security issue has been identified in a Microsoft ....",
			"product": "Windows 8",
			"vendor": "Microsoft Corporation",
			"severity": "critical",
			"sev_num": 1,
			"kb_name": "KB2900986",
			"release_date": "2017-10-16T03:11:09Z",
		}]
	},
	"infection": {
		"metascan": {
			"total": 100,
			"issue": 1,
			"threats": [{
				"critical": 0,
				"file": "C:\\ProgramData\\WindowsMangerProtect\\ProtectWindowsManager.exe",
				"hash": "e152e3ea7c356cfed40306ff946233d0",
				"scan_time": "2015-05-13T17:00:34Z",
				"threat_name": "Generic6.WQW",
				"details": [{
					"threat_name": "ADWARE/ELEX.Gen",
					"av_name": "ClamAV"
				}]
			}]
		},
		"antivirus": {
			"total": 100,
			"issue": 1,
			"threats": [{
				"critical": 0,
				"file": "C:\\Windows\\KMSEmulator.exe",
				"hash": "c53051184211d40f13e6d7876f5d9db1",
				"scan_time": "2015-05-12T23:32:19Z",
				"threat_name": "@ApplicUnwnt.Win32/HackKMS.A",
				"repeat": 2,
				"product_name": "ESET Endpoint Security",
				"product_vendor": "ESET",
				"product_version": "5.0.2211.0",
				"severity": "0",
				"action": "5",
				"type": "0"
			}]
		}
	}
}
```

## Example response for domain controller device

```plaintext
{
	"device_id": "DCYE9I3DNJ4IFMP84LIGG8S8207R4E04",
	"device_type": "server",
	"device_name": "tle-domain",
	"nick_name": "tle-domain",
	"agent_version": "1.1.1.1",
	"last_seen": "2015-10-16T03:11:09Z",
	"public_ip": "54.78.191.2",
	"agent_type": "dc",
	"network_info": [{
		"description": "Intel(R) Ethernet Connection I217-LM",
		"ipv4": "109.184.237.115",
		"ipv6": "fe80::2d88:eab7:6001:6ec7",
		"mac": "10:60:4B:62:01:AC",
		"subnet_mask": "255.255.254.0",
		"media_state": "connected",
		"dhcp_enabled": "true",
		"dhcp_obtained": "N/A",
		"dhcp_expires": "N/A",
		"dhcp_server": "N/A",
		"adapter_enabled": "N/A",
		"default_gateway": "N/A",
		"dns_addresses": ["N/A"]
	}],
	"os_info": {
		"service_pack_version": "1.0",
		"vendor": "Microsoft Corp.",
		"family": "Windows",
		"os_language": "English",
		"name": "Windows Server 2012",
		"architecture": "64-bit",
		"version": "6.3",
		"type": "windows"
	}
}
```

## History

| Version | URL |
| ---- | ---- |
| v2.6 | [Device Details v2.6](https://www.opswat.com/docs/cm/developer-guidelines/device-details-v2-6) |
| v2.5 | [Device Details v2.5](https://www.opswat.com/docs/cm/developer-guidelines/device-details-v2-5) |
| v2.4 | [Device Details v2.4](https://www.opswat.com/docs/cm/developer-guidelines/device-details-v2-4) |
| v2.3 | [Device Details v2.3](https://www.opswat.com/docs/cm/developer-guidelines/device-details-v2-3) |
| v2.2 | [Device Details v2.2](https://www.opswat.com/docs/cm/developer-guidelines/device-details-v2-2) |
| v2.1 | [Device Details v2.1](https://www.opswat.com/docs/cm/developer-guidelines/device-details-v2-1) |
