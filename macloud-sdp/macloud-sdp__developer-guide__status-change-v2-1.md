<!-- source: https://www.opswat.com/docs/macloud-sdp/developer-guide/status-change-v2-1 -->

# Status Change v2.1

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

| API version | 2.1 |
| --- | --- |
| Last Update | 01/30/2018 |
| Authentication | YES |
| Response Format | JSON |
| HTTP Method | GET |
| Rate limited | YES |
| Requests per rate limit | 10/min |

Use to obtain status change (delta) of all devices in an account in a particular time frame.

## [API URL](/docs/cm/developer-guidelines/status-change-v2-1#api-url)

https://gears.opswat.com/o/api/v2.1/devices/status_changed
## [Request Parameters](/docs/cm/developer-guidelines/status-change-v2-1#request-parameters)

| Key | Datatype | Parameter Type | Required | Description | Default |
| --- | --- | --- | --- | --- | --- |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step |  |
| verbose | int | URL | Optional | 1 - extra detailed information will return in response 0 - response does not include detailed information | 0 |
| age | long | URL | Optional | Specify age of the information in seconds. Value is from 0 to 86400  For example if you want delta of information for last 5 minutes you need to set age as 300; | 86400 |
| os_type | string | URL | Optional | Specify operating system of devices you want to fetch data   - If os_type is "win_or_mac", return only Windows/Mac devices - If os_type is "linux_or_mobile", return status for linux or mobile devices | win_or_mac |

## [Response HTTP Code](/docs/cm/developer-guidelines/status-change-v2-1#response-http-code)

| HTTP Code | Description |
| --- | --- |
| 200 | Success |
| 401 | Unauthorized. Your access_token is invalid or expired |

## [Response Parameters](/docs/cm/developer-guidelines/status-change-v2-1#response-parameters)

| Key | Datatype | Verbose | Description |
| --- | --- | --- | --- |
| devices | array<object> |  | Lists of devices which changed status in the particular time frame |
| devices.hwid |  |  | Hardware ID of a device. |
| devices.mac_address | array<string> | OFF | ***Only available when device status as 2 or Verbose set as OFF***  Lists of MAC addresses of network inferfaces of a device |
| devices.status | int |  | Reports the health status of the endpoint device as identified by the Mac Address. This status is based on the defined policy within My OPSWAT Central Management.  Status values are:   - **0** – the endpoint is in compliance with My OPSWAT Central Management account’s policies - **1** – the endpoint is **not** in compliance with My OPSWAT Central Management account’s policies - **2** – MAC address is not found, it means that the agent was uninstalled on the endpoint or deleted on My OPSWAT Central Management console. - **3** – the endpoint is still sending information to My OPSWAT Central Management and not yet completed   ***Note: if a device doesn't exist on the cloud any more (status as 2), very minimum information will be returned: hwid, and mac_addresses*** |
| devices.critical_status | int |  | This critical status is based on the defined policy within My OPSWAT Central Management. This status apply for the whole device.  Critical status values are:   - **0** – the endpoint doesn't have critical issues - **1** – the endpoint has critical issues - **2** – the endpoint is not found |
| devices.total_issue | int |  | Number of issues were seen on the device. |
| devices.total_critical_issue | int |  | Number of critical issues were seen on the device |
| devices.policy_name | string | ON | Reversed for future  Policy name which the device is assigned to |
| devices.user | string | ON | Username of a group. |
| devices.user_info | object | ON | Details of a user who logging on the device |
| devices.user_info.username | string | ON | username who currently logs in. This field will be removed if it's set as privacy |
| devices.user_info.domain | string | ON | domain which the current user logged in |
| devices.location | string | ON | Reserved for future |
| devices.device_type | string | ON | Specific device type (laptop, desktop, vm, server) |
| devices.os_info | object | ON | Detailed Operating System information |
| devices.os_info.family | string | ON | OS family |
| devices. [os_info.name](http://os_info.name/) | string | ON | OS name |
| devices.os_info.vendor | string | ON | OS vendor |
| devices.os_info.version | string | ON | OS version |
| devices.os_info.service_pack_version | string | ON | OS Service Pack Version |
| devices.os_info.architecture | string | ON | OS architecture |
| devices.os_info.os_language | string | ON | OS language |
| devices.os_info.user_password_set | int | ON | If user password is set on OS, 1 is set, 0 is not set |
| devices.agent_type | int | ON | Agent type that runs on the device. (optional)  agent_type values are:   - **0** – Persistent |
| devices.network_info | array<object> | ON | Network adapter information block |
| devices.network_info.mac_addr | string | ON | MAC address for adapter. This field will be removed if it's a non-collectible to each fields which related to privacy. |
| devices.network_info.ipv4_addr | string | ON | IPV4 address. This field will be removed if it's a non-collectible to each fields which related to privacy. |
| devices.network_info.ip6_addr | string | ON | IPV6 address. This field will be removed if it's a non-collectible to each fields which related to privacy |
| devices.last_seen | string | ON | timestamp when the endpoint device sent the last health report to the server. |
| devices.issues | array<object> | ON | Lists of issues of the given device. If a device is without issue, the issues array will appear blank (as shown in the example below) |
| devices.issues.<category_group> | array<object> | ON | Details of issues on a specific category group |
| devices.issues.<category_group>.category | string | ON | Category name which has issues |
| devices.issues.<category_group>.issues | array<string> | ON | Lists of issues a device has in a specific category |
| devices.infections | array<object> | ON | That includes scanning for malware on active programs as well as automatically uploading files to Metascan Online for additional scanning when not recognized. Additionally, we report on any repeated threats detected by your installed antivirus. |
| devices.infections.category | string | ON | Type of infection scan.   - malware_scan: Daily Anti-malware Infection scan - repeated_threats: repeated threats detected by local anti-malware products. - ip_scan: IP Connections scan |
| devices.infections.critical_issue | int | ON | 0 - no critical issue, 1 - has critical issue |
| devices.infections.has_issue | int | ON | 0 - no issue, 1 - out of compliance |
| devices.infections.has_critical_issue | int | ON | 0 - no critical issue, 1 - has critical issue |
| devices.infections.total_threats | int | ON | Total of found threats. |
| devices.infections.total_engines | int | ON | Total of engines which used to scan. |
| devices.infections.total_source | int | ON | number of sources of the feed |
| devices.infections.last_scan_time | string | ON | Timestamp of the last scan. |
| devices.infections.last_report | string | ON | Time stamp of the last report. |
| devices.infections.threats | array<object> | ON | Lists of found threats. |
| devices.infections.threats.FoundTime | string | ON | Timestamp when the threat was found. |
| devices.infections.threats.ThreatName | string | ON | Threat name |
| devices.infections.threats.File | string | ON | File which found a threat |
| devices.infections.threats.link | string | ON | URL on Metadefender Cloud to check scan details |
| devices.infections.threats.hash | string | ON | Unique hash (fingerprint) of the threat. |
| devices.infections.threats.action | string | ON | Last action taken by the local anti-malware product. |
| devices.infections.threats.found_time | string | ON | Timestamp when the repeated threat was last seen. |
| devices.infections.threats.times_detected | string | ON | Number of times the threat was seen by the local anti-malware product |
| devices.infections.threats.engine_name | string | ON | local anti-malware product which detected the threat |
| devices.infections.threats.ip_address | string | ON | suspicious IP address which a device connecting to |
| devices.infections.threats.details | object | ON | Details of the suspicious IP address |
| devices.infections.threats.details.confident | int | ON | Represents the reliability of the detection based on several factors. The higher the score, the more reliable the result. |
| devices.infections.threats.details.source_name | string | ON | Source of the feed, usually the domain where the feed is from (e.g., [example.com](http://example.com/) ) |
| devices.infections.threats.details.assessment | string | ON | Type of threat detected |
| devices.infections.threats.status | string | ON | indicates the scanning object is clear, dirty or in-progress |
| devices.infections.threats.geo_info | object | ON | An object represents the geolocation of address |
| devices.infections.threats.geo_info.city | string | ON | Country name of the network address (e.g., Brazil) |
| devices.infections.threats.geo_info.country_name | string | ON | Country name of the network address (e.g., BR) |
| devices.infections.threats.geo_info.country_code | string | ON | Region name of the network address (e.g., San Paulo) |
| devices.infections.threats.geo_info.region_name | string | ON | Region code of the network address (e.g., 27) |
| infections.threats.geo_info.region_code | string | ON | City name of the network address (e.g., San Paulo) |
| devices.remediation | string | ON | Reversed for future |
| devices.remediation_link | string | ON | Remediation page URL of the device. |
| devices.notification | string | ON | Reversed for future |

## [Example](/docs/cm/developer-guidelines/status-change-v2-1#example)

**Example Request:**

https://gears.opswat.com/o/api/v2.1/devices/status_changed?age=300&access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234

**Example Response with verbose as OFF for Windows and macOS devices **

{
"devices": [{
"mac_addresses": ["11:11:11:11:11:11"],
"status": 1,
"total_issue": 3,
"critical_status": 1,
"total_critical_issue": 1,
"hwid": "XZI1PJCDE8WU3K0P"
}]
}

**Example Response:** **with verbose as ON for Windows and macOS devices**

{
"devices": [{
"hwid": "YxLfE8Wkn5p5VOBhcEiGDid5MtqQA4is",
"network_info": [{
"mac_addr": "00:50:56:c0:00:08",
"ipv4_addr": "192.168.222.1",
"ipv6_addr": "fe80::192a:8bfb:cfef:d089"
}],
"status": 1,
"total_issue": 3,
"critical_status": 1,
"total_critical_issue": 1,
"policy_name": "",
"user_info": {
"username": "mpham",
"domain": "INTL"
},
"user": "",
"location": "US",
"device_type": "laptop",
"os_info": {
"user_password_set": "1",
"service_pack_version": "1.7601",
"vendor": "Microsoft Corp.",
"family": "Windows",
"os_language": "",
"name": "Windows 7 Enterprise",
"architecture": "64-Bit",
"version": "6.1.7601"
},
"agent_type": 0,
"last_seen ": "2013-12-04T08:00:00Z",
"issues": [{
"protection": [{
"category": "antiphishing",
"issues": ["Antiphishing protection is disabled"]
}, {
"category": "antivirus",
"issues": ["No Antivirus application is installed", "Real time protection is off"]
}]
}, {
"system": [{
"category": "user_authentication",
"issues": ["Password protection is off"]
}]
}],
"infections": [{
"category": "malware_scan",
"critical_issue": 0,
"total_threats": 1,
"has_issue": 1,
"threats": [{
"FoundTime": "5/06/2015 02:22:37",
"ThreatName": "RiskWare[WebToolbar:not-a-virus]/Win32.CrossRider",
"File": "C:\\Program Files (x86)\\24Seven savings\\24seven_savings_notification_service.exe",
"link": "https://www.metascan-online.com/en/scanresult/hash/9d9b2707dba677ee55cbb7fb7be9e7cd",
"hash": "9d9b2707dba677ee55cbb7fb7be9e7cd",
"action": "cleaned"
}],
"last_scan_time": "2015-05-06T02:22:37Z",
"has_critical_issue": 0,
"total_engines": 41
}, {
"category": "repeated_threats",
"critical_issue": 1,
"last_report": "2015-05-05T09:48:38Z",
"total_threats": 1,
"has_issue": 1,
"has_critical_issue": 1,
"threats": [{
"found_time": "2015-05-05T06:45:28Z",
"file": "C:\\Users\\yiyi\\Desktop\\b o\\WHY-WIN.EXE|:.RTP",
"threat_name": "Test/Conduit.Virus.B",
"times_detected": 2,
"engine_name": "Emsisoft Anti-Malware"
}]
}],
"remediation": "",
"remediation_link": "https://gears.opswat.com/gears/remediation/2dac92f8fa8dfe02414835d792fb412f/6WXJURV8QAM0I7KC/009nOa7nMaInXaDnMaZ1J/remediation.html",
"notification": ""
}]
}

**Example response: with verbose as ON for Linux, iOS, and Android devices **

{
"devices": [{
"hwid": "YxLfE8Wkn5p5VOBhcEiGDid5MtqQA4is",
"total_issue": 2,
"remediation": "",
"critical_status": 0,
"status": 0,
"device_type": "phone",
"notification": "",
"policy_name": "",
"total_critical_issue": 0,
"last_seen": "2016-05-11T10:38:26Z",
"remediation_link": "https://gears.opswat.com/gears/remediation/2dac92f8fa8dfe02414835d792fb412f/6WXJURV8QAM0I7KC/009nOa7nMaInXaDnMaZ1J/remediation.html?od=2",
"user": "Thang",
"network_info": [{
"mac_addr": "0C:48:85:CE:65:F3",
"ipv4_addr": "10.0.61.114",
"ipv6_addr": "FE80::E48:85FF:FECE:65F3"
}],
"os_info": {
"user_password_set": "-1",
"service_pack_version": null,
"vendor": "Apple Inc.",
"family": "ios",
"os_language": "",
"name": "iOS",
"architecture": null,
"languageName": "Unknown",
"version": "9.1"
},
"issues": [{
"system": [{
"category": "Security & Health",
"issues": ["Device's operating system does not meet minimum version", "Screen lock and passcode are disabled"]
}]
}],
"infections": [{
"category": "malware_scan",
"critical_issue": 0,
"total_threats": 0,
"has_issue": 0,
"threats": [],
"last_scan_time": "",
"has_critical_issue": 0,
"total_engines": 43
}, {
"category": "ip_scan",
"critical_issue": 0,
"total_threats": 1,
"last_scan_time": "",
"threats": [{
"ip_address": "104.238.102.226",
"details": [{
"confident": 40,
"source_name": "MalwareDomainList",
"assessment": "malware"
}],
"status": "dirty",
"geo_info": {
"region_name": "",
"region_code": "",
"country_code": "CA",
"country_name": "Canada",
"city": ""
}
}],
"has_issue": 1,
"total_sources": 12,
"has_critical_issue": 0
}]
}]
}

**Example response: when there is no devices changes status**

{ "devices": [] }
