<!-- source: https://www.opswat.com/docs/macloud-sdp/developer-guide/device-details-v2-4 -->

# Device Details v2.4

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

| API version | 2.4 |
| --- | --- |
| Last Update | 08/18/2015 |
| Authentication | YES |
| Response Format | JSON |
| HTTP Method | GET |
| Rate limited | YES |
| Requests per rate limit | 10/min |
| Changes | Add agent_type to output |

Use to fetch device details by ID or MAC address.

## [API URL](/docs/cm/developer-guidelines/device-details-v2-4#api-url)

https://gears.opswat.com/o/api/v2.4/devices/:value
## [Request Parameters](/docs/cm/developer-guidelines/device-details-v2-4#request-parameters)

| Key | Datatype | Parameter Type | Required | Description | Default |
| --- | --- | --- | --- | --- | --- |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step |  |
| value | string | URL | Yes | The Device ID or MAC Address of a device you want to fetch information. |  |
| opt | int | URL | Optional | Type of the given value in the URL.  0 - the given value is HWID. 1 - the given value is MAC Address | 0 |

## [Response HTTP Code](/docs/cm/developer-guidelines/device-details-v2-4#response-http-code)

| HTTP Code | Description |
| --- | --- |
| 200 | Success |
| 401 | Unauthorized. Your access_token is invalid or expired |
| 404 | Not found |

## [Response Parameters](/docs/cm/developer-guidelines/device-details-v2-4#response-parameters)

| Key | Datatype | Description |
| --- | --- | --- |
| hwid | string | Hardware ID of the device |
| status | int | Reports the health status of the device. This status is based on the defined policy within My OPSWAT Central Management.  Value could be:   - **0** – the endpoint is in compliance with My OPSWAT Central Management account’s policies - **1** – the endpoint is **not** in compliance with My OPSWAT Central Management account’s policies - **3** – the endpoint is still sending information to My OPSWAT Central Management and not yet completed |
| critical_issue | int | This critical status is based on the defined policy within My OPSWAT Central Management. This status apply for the whole device.  Value could be:   - **0** – the endpoint doesn't have critical issues - **1** – the endpoint has critical issues |
| total_issue | int | Number of issues were seen on the device |
| total_critical_issue | int | Number of critical issues were seen on the device |
| exempt | int | Exempt status of the device.  Value could be:   - **0** – Endpoint device is not exempted - **1** – Endpoint device is exempted |
| agent_type | string | (optional) Agent type that runs on the device. Value can be **managed** or **guest** |
| hostname | string | Hostname of the device. This field will be remove if it's a non-collectible to each fields which related to privacy. |
| country | string | Region where the device IP geographically represents |
| machine_type | string | The type of devices |
| agent_version | string | Local resident MetaDefender Endpoint version |
| active | int | - 1: device is active - 0: device is deactive |
| last_seen | string | The last timestamp when MetaDefender Endpoint reports data to the Cloud, (GMT format) |
| user | string | Username of a group |
| user_info | object | User information block |
| user_info.username | string | username who currently logs in. This field will be remove if it's set as privacy |
| user_info.domain | string | Currently logged in user domain |
| remediation_link | string | remediation page URL of the given device |
| applications | array<object> | Details of each posture category |
| applications.category | string | category which the current block stands for |
| applications.critical_status | int | This critical issue status is based on the defined policy within My OPSWAT Central Management. This critical issue status apply for each category.  Value could be:   - **0** – good (blue) if this category is healthy AND the box in Configuration is checked - **1** – bad (red) if the category is healthy AND the box in Configuration is checked. - **-1** – If the box in Configuration is not checked |
| applications.has_issue | int | 0 - no issue, 1 - out of compliance |
| applications.has_critical_issue | int | 0 - no critical issue, 1 - has critical issue |
| applications.apps | array<object> | detailed products in a category |
| applications.apps.name | string | Name of the product |
| applications.apps.vendor | string | Name of the product vendor |
| applications.apps.version | string | Product version |
| applications.apps.health | object | health informationof a product |
| applications.apps.health.status | string | product compliance details |
| applications.apps.health.is_issue | int | 1 - is an issue, 0 - not an issue |
| os_info | object | Operation system information |
| os_info.family | string | OS family |
| [os_info.name](http://os_info.name/) | string | OS name |
| os_info.vendor | string | OS vendor |
| os_info.version | string | OS version |
| os_info.service_pack_version | string | OS Service Pack Version |
| os_info.architecture | string | OS architecture |
| os_info.os_language | string | OS language |
| os_info.user_password_set | int | If user password is set on OS, 1 is set, 0 is not set |
| network_info | array<object> | Network adapter information block |
| network_info.mac_addr | string | MAC address for adapter. This field will be remove if it's a non-collectible to each fields which related to privacy. |
| network_info.ipv4_addr | string | IPV4 address. This field will be remove if it's a non-collectible to each fields which related to privacy. |
| network_info.ipv6_addr | string | IPV6 address. This field will be remove if it's a non-collectible to each fields which related to privacy. |
| infections | array | Infections information |
| infections.category | string | Infections category name |
| infections.critical_status | int | 0 - no critical issue, 1 - has critical issue |
| infections.total_threats | int | number of detected threats |
| infections.has_issue | int | 0 - no issue, 1 - out of compliance |
| infections.has_critical_issue | int | 0 - no critical issue, 1 - has critical issue |
| infections.threats | array<object> | detailed threats |
| infections.threats.ThreatName | string | Name of threat found |
| infections.threats.File | string | file which the threat found |
| infections.threats.FoundTime | string | The timestamp in GMT format when the threat found. |
| infections.threats.hash | string | hash code of the scanning object if the object is a file or process |
| infections.threats.link | string | a URL to view scan details on [Metadefender Cloud](http://metadefender.com) |
| infections.last_scan_time | string | The timestamp in GMT format when the agent did a scan |
| infections.total_engines | int | number of engines scanned a file |
| infections.last_report | string | the timestamp in GMT format when agent reported threat log from local anti-malware product |

## [Example](/docs/cm/developer-guidelines/device-details-v2-4#example)

**Example Request**

https://gears.opswat.com/o/api/v2.4/devices/02:21:9b:06:4b:96?opt=1&access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234

**Example Response**

{
"user_info": {
"username": "ble",
"domain": "INTL"
},
"exempt": 0,
"agent_type": "managed",
"status": 1,
"network_info": [{
"mac_addr": "02:21:9b:06:4b:96",
"ipv4_addr": "192.168.255.1",
"ipv6_addr": "fe80::401b:f2c2:a540:f965"
}],
"hostname": "WSEVN22",
"os_info": {
"user_password_set": "1",
"service_pack_version": "1.0",
"vendor": "Microsoft Corp.",
"family": "Windows",
"os_language": "English",
"name": "Microsoft Windows 7 Professional ",
"architecture": "64-bit",
"version": "6.1.7601"
},
"hwid": "CD53F6F80B584D599E0BC978149A19AC",
"total_issue": 9,
"country": "Vietnam",
"machine_type": "desktop",
"agent_version": "7.4.65.0",
"critical_status": 1,
"active": 1,
"applications": [{
"category": "Cloud Storage",
"critical_issue": 1,
"apps": [{
"vendor": "Dropbox, Inc.",
"name": "Dropbox",
"health": [{
"status": "Cloud Storage running",
"is_issue": 1
}],
"version": "3.6.7"
}],
"has_issue": 1,
"has_critical_issue": 1
}, {
"category": "Developer Tool",
"critical_issue": 0,
"apps": [{
"vendor": "",
"name": "No product detected",
"health": [{
"status": "No developer tool detected",
"is_issue": 0
}],
"version": ""
}],
"has_issue": 0,
"has_critical_issue": 0
}, {
"category": "Encryption",
"critical_issue": 1,
"apps": [{
"vendor": "",
"name": "No product detected",
"health": [{
"status": "No product detected",
"is_issue": 1
}],
"version": ""
}],
"has_issue": 1,
"has_critical_issue": 1
}, {
"category": "Uninstaller",
"critical_issue": 0,
"apps": [{
"vendor": "",
"name": "No product detected",
"health": [{
"status": "No uninstaller detected",
"is_issue": 0
}],
"version": ""
}],
"has_issue": 0,
"has_critical_issue": 0
}, {
"category": "Antiphishing",
"critical_issue": 0,
"apps": [{
"vendor": "Microsoft Corporation",
"name": "Internet Explorer",
"health": [{
"status": "Enabled",
"is_issue": 0
}],
"version": "11.00.9600.16428"
}, {
"vendor": "Google Inc.",
"name": "Google Chrome",
"health": [{
"status": "Enabled",
"is_issue": 0
}],
"version": "43.0.2357.124"
}, {
"vendor": "Mozilla Corporation",
"name": "Mozilla Firefox",
"health": [{
"status": "Enabled",
"is_issue": 0
}],
"version": "38.0.5"
}],
"has_issue": 0,
"has_critical_issue": 0
}, {
"category": "Media Player",
"critical_issue": 0,
"apps": [{
"vendor": "",
"name": "No product detected",
"health": [{
"status": "No media player detected",
"is_issue": 0
}],
"version": ""
}],
"has_issue": 0,
"has_critical_issue": 0
}, {
"category": "3rd Party Patch Mgmt.",
"critical_issue": 0,
"apps": [{
"vendor": "Microsoft Corporation",
"name": "Windows Update Agent",
"health": [{
"status": "Enabled",
"is_issue": 0
}],
"version": "7.6.7601.18804"
}],
"has_issue": 0,
"has_critical_issue": 0
}, {
"category": "Toolbar",
"critical_issue": 0,
"apps": [{
"vendor": "",
"name": "No product detected",
"health": [{
"status": "No toolbar detected",
"is_issue": 0
}],
"version": ""
}],
"has_issue": 0,
"has_critical_issue": 0
}, {
"category": "Public File Sharing",
"critical_issue": 0,
"apps": [{
"vendor": "",
"name": "No product detected",
"health": [{
"status": "No public file sharing detected",
"is_issue": 0
}],
"version": ""
}],
"has_issue": 0,
"has_critical_issue": 0
}, {
"category": "OS Update",
"critical_issue": -1,
"apps": [{
"vendor": "Microsoft Corporation",
"name": "Windows Update Agent",
"health": [{
"status": "OS automatic updates are enabled",
"is_issue": 0
}, {
"status": "OS is not missing patches, updates or service packs",
"is_issue": 0
}],
"version": "7.6.7601.18804"
}],
"has_issue": 0,
"has_critical_issue": 0
}, {
"category": "Screen Sharing",
"critical_issue": 0,
"apps": [{
"vendor": "",
"name": "No product detected",
"health": [{
"status": "No screen sharing detected",
"is_issue": 0
}],
"version": ""
}],
"has_issue": 0,
"has_critical_issue": 0
}, {
"category": "Firewall",
"critical_issue": 1,
"apps": [{
"vendor": "Microsoft Corporation",
"name": "Windows Firewall",
"health": [{
"status": "Not enabled",
"is_issue": 1
}],
"version": "6.1.7600.16385"
}],
"has_issue": 1,
"has_critical_issue": 1
}, {
"category": "Chat / IM",
"critical_issue": 1,
"apps": [{
"vendor": "Microsoft Corporation",
"name": "Windows Live Messenger",
"health": [{
"status": "Chat / IM detected",
"is_issue": 1
}],
"version": "16.4.3528.0331"
}],
"has_issue": 1,
"has_critical_issue": 1
}, {
"category": "Antivirus",
"critical_issue": 1,
"apps": [{
"vendor": "ESET",
"name": "ESET Endpoint Security",
"health": [{
"status": "Real time protection is on",
"is_issue": 0
}, {
"status": "Virus definitions were last updated more than 3 day(s) ago",
"is_issue": 1
}, {
"status": "The last full system scan was more than 7 day(s) ago",
"is_issue": 1
}, {
"status": "0 threats detected within the last 7 day(s)",
"is_issue": 0
}],
"version": "5.0.2211.0"
}],
"has_issue": 1,
"has_critical_issue": 1
}, {
"category": "Cleaner / Optimizer",
"critical_issue": 0,
"apps": [{
"vendor": "",
"name": "No product detected",
"health": [{
"status": "No cleaner / optimizer detected",
"is_issue": 0
}],
"version": ""
}],
"has_issue": 0,
"has_critical_issue": 0
}, {
"category": "VPN Client",
"critical_issue": 1,
"apps": [{
"vendor": "Microsoft Corporation",
"name": "Windows VPN Client",
"health": [{
"status": "VPN Client detected",
"is_issue": 1
}],
"version": "6.1.7600.16385"
}],
"has_issue": 1,
"has_critical_issue": 1
}, {
"category": "Hard Drive",
"critical_issue": -1,
"apps": [{
"vendor": "",
"name": "465.66 GB",
"health": [{
"status": "Hard drive has 9% free (43.54 GB)",
"is_issue": 1
}],
"version": ""
}],
"has_issue": 1,
"has_critical_issue": 0
}, {
"category": "Backup",
"critical_issue": 0,
"apps": [{
"vendor": "Microsoft Corporation",
"name": "Windows Backup and Restore",
"health": [{
"status": "Backup has never been run",
"is_issue": 1
}],
"version": "6.1.7600.16385"
}],
"has_issue": 0,
"has_critical_issue": 0
}, {
"category": "Unclassified PUA",
"critical_issue": 1,
"apps": [{
"vendor": "FileZilla Project",
"name": "FileZilla",
"health": [{
"status": "Unclassified PUA detected",
"is_issue": 1
}],
"version": "3.7.1.1"
}],
"has_issue": 1,
"has_critical_issue": 1
}, {
"category": "User Authentication",
"critical_issue": -1,
"apps": [{
"vendor": "",
"name": "ble",
"health": [{
"status": "User password protection is enabled",
"is_issue": 0
}, {
"status": "Lock screen timeout is under 10 minutes",
"is_issue": 0
}],
"version": ""
}],
"has_issue": 0,
"has_critical_issue": 0
}, {
"category": "Remote Control",
"critical_issue": 1,
"apps": [{
"vendor": "TeamViewer GmbH",
"name": "TeamViewer",
"health": [{
"status": "Remote Control detected",
"is_issue": 1
}],
"version": "10.0"
}],
"has_issue": 1,
"has_critical_issue": 1
}],
"total_critical_issue": 7,
"infections": [{
"category": "malware_scan",
"critical_issue": 0,
"total_threats": 0,
"has_issue": 0,
"threats": [],
"last_scan_time": "2015-06-11T01:13:58Z",
"has_critical_issue": 0,
"total_engines": 41
}, {
"category": "repeated_threats",
"critical_issue": 0,
"last_report": "2015-06-11T11:27:14Z",
"total_threats": 0,
"has_issue": 0,
"threats": [],
"has_critical_issue": 0
}],
"last_seen": "2015-06-11T11:27:00Z",
"user": "",
"remediation_link": "https://gears.opswat.com/gears/remediation/2dac92f8fa8dfe02414835d792fb412f/GJHGUHGUUGI/011G2JGHNGFUGHYGSUPU8GOIA/remediation.html"
}
## [History](/docs/cm/developer-guidelines/device-details-v2-4#history)

| Version | URL |
| --- | --- |
| v2.3 | [Device Details v2.3](/docs/cm/developer-guidelines/device-details-v2-3) |
| v2.2 | [Device Details v2.2](/docs/cm/developer-guidelines/device-details-v2-2) |
| v2.1 | [Device Details v2.1](/docs/cm/developer-guidelines/device-details-v2-1) |
