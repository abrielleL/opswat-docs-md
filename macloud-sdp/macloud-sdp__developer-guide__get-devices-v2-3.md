<!-- source: https://www.opswat.com/docs/macloud-sdp/developer-guide/get-devices-v2-3 -->

# Get Devices v2.3

| API version | 2.3 |
| --- | --- |
| Last Update | 01/30/2018 |
| Authentication | YES |
| Response Format | JSON |
| HTTP Method | GET |
| Rate limited | YES |
| Requests per rate limit | 10/min |
| Changes | Fixed not return mobile devices when agent_type is managed 01/30/2018: removed agent_type in input parameters. API will ignore agent_type parameter in the input |

Use to get all devices on a given account

## [API URL](/docs/macloud-sdp/developer-guide/get-devices-v2-3#api-url)

https://gears.opswat.com/o/api/v2.3/devices
## [Request Parameters](/docs/macloud-sdp/developer-guide/get-devices-v2-3#request-parameters)

| Key | Datatype | Parameter Type | Required | Description | Default |
| --- | --- | --- | --- | --- | --- |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step |  |
| limit | int | URL | Optional | Specific maximum number of devices will be returned in the response. The value should be in [1,50]. If there are more devices than what the limit asks for, error code will be 406. | 1 |
| page | int | URL | Optional | Specific page number which devices will be returned in. If the requested page exceeds the number of pages of devices, error code will be 413. It means that the requested page number is too large, no devices will be returned in this case. | 1 |
| GroupBy | string | URL | Optional | Specific how to group devices. Values can be: **none** - No need to group devices **hwid** - HWID **host** - hostname **issues** - number of issues | none |
| order | string | URL | Optional | Sort order. Values can be: **des** - descending. **asc** - ascending. | des |

## [Response HTTP Code](/docs/macloud-sdp/developer-guide/get-devices-v2-3#response-http-code)

| HTTP Code | Description |
| --- | --- |
| 200 | Success |
| 401 | Unauthorized. Your access_token is invalid or expired |
| 406 | Too many devices to return |
| 413 | Requested page number exceeds limit |

## [Response Parameters](/docs/macloud-sdp/developer-guide/get-devices-v2-3#response-parameters)

| Key | DataType | Description |
| --- | --- | --- |
| hwid | string | Hardware ID of the device |
| agent_type | string | Agent type that runs on the device. (optional) |
| remediation_link | string | URL on remediation page for given device |
| status | int | Reports the compliance status of the endpoint. This status is based on the defined policy within MetaAccess. Status values are:   - **0** – the endpoint is in compliance with MetaAccess account’s policies - **1** – the endpoint is **not** in compliance with MetaAccess account’s policies - **3** – the endpoint is still sending information to MetaAccess and not yet completed |
| hostname | string | Hostname of the device |
| nickname | string | nickname for the device (admin editable) |
| agent_version | string | Local resident MetaAccess agent version |
| last_seen | string | The last timestamp in GMT format when MetaAccess agent reports its data to Cloud |
| machine_type | string | The type of devices |
| country | string | Region where the device IP geographically represents |
| active | int | 1 - device is connected to Cloud, 0 - disconnected |
| total_issue | int | Number of issues were seen on the device |
| user | string | Username of a group |
| user_info | object | User information block |
| user_info.username | string | Currently logged in username |
| user_info.domain | string | Currently logged in user domain |
| os_info | object | Operation system block |
| os_info.family | string | OS family |
| os_info.name | string | OS name |
| os_info.vendor | string | OS vendor |
| os_info.version | string | OS version |
| os_info.service_pack_version | string | OS Service Pack Version |
| os_info.architecture | string | OS architecture |
| os_info.os_language | string | OS language |
| os_info.user_password_set | string | If user password is set on OS, 1 is set, 0 is not set |
| network_info | array<object> | Network adapter information block |
| network_info.mac_addr | string | MAC address for adapter |
| network_info.ipv4_addr | string | IPV4 address |
| network_info.ipv6_addr | string | IPV6 address |
| total_critical_issue | int | Number of critical issues were seen on the device |
| critical_status | int | This critical status is based on the defined policy within MetaAccess. This status apply for the whole device. Critical status values are:   - **0** – the endpoint doesn't have critical issues - **1** – the endpoint has critical issues - **2** – the endpoint is not found |
| exempt | int | Exempt status of the endpoint device. Exempt values are:   - **0** – Endpoint device is not exempted - **1** – Endpoint device is exempted |

## [Example](/docs/macloud-sdp/developer-guide/get-devices-v2-3#example)

**Example Request**

https://gears.opswat.com/o/api/v2.3/devices?limit=10&groupBy=hwid&order=asc&&access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234

**Example Response**

[{
"hwid": "6WXJURV8QAM0I7KC",
"agent_type": "managed",
"hostname": "Win_7ENTx64_English",
"nickname": "Win_7ENTx64_English",
"agent_version": "6.1.51.0",
"critical_status": 0,
"total_critical_issue": 0,
"last_seen": "2013-12-04T08:00:00Z",
"machine_type": "laptop",
"country": "Unknown",
"active": 1,
"total_issue": 10,
"exempt": 0,
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
}, {
"hwid": "BCDJDHT6JLFIOXIA",
"agent_type": "managed",
"hostname": "tomas-0c8fb945d",
"nickname": "Windows XP VM",
"agent_version": "4.4.5.0",
"critical_status": 1,
"total_critical_issue": 1,
"last_seen": "2013-12-04T08:00:00Z",
"machine_type": "vm",
"country": "United States",
"active": 1,
"total_issue": 5,
"exempt": 1,
"user_info": {
"username": "Administrator",
"domain": "TOMAS-0C8FB945D"
},
"user": "gear",
"os_info": {
"family": "Windows",
"name": "Windows XP Professional",
"vendor": "Microsoft Corp.",
"version": "5.1.2600",
"service_pack_version": "3.0",
"architecture": "32-Bit",
"os_language": "20",
"user_password_set": "1"
},
"network_info": [{
"mac_addr": "00:0C:29:0A:83:0C",
"ipv4_addr": "192.168.159.138",
"ipv6_addr": ""
}],
"status": 1,
"remediation_link": "https://gears.opswat.com/gears/remediation/2dac92f8fa8dfe02414835d792fb412f/BCDJDHT6JLFIOXIA/004APD1FU42/remediation.html"
}]

**Example Response for Mobile devices**

[{
"hwid": "W7ibNr5eVxv3wHlmsAWKo9MazUpkdWQG",
"hostname": "Thang's Phone",
"agent_version": "7.0.250.0",
"machine_type": "phone",
"active": 1,
"critical_status": 0,
"total_critical_issue": 0,
"total_issue": 10,
"status": 1,
"last_seen": "2013-12-04T08:00:00Z",
"remediation_link": "https://gears.opswat.com/gears/remediation/2dac92f8fa8dfe02414835d792fb412f/6WXJURV8QAM0I7KC/009nOa7nMaInXaDnMaZ1J/remediation.html?od=2",
"os_info": {
"family": "android",
"name": "Android",
"vendor": "Google Inc.",
"version": "4.4.2",
"os_language": "English"
},
"network_info": [{
"mac_addr": "00:0c:29:f2:7a:29",
"ipv4_addr": "10.0.50.106",
"ipv6_addr": "fe80::3c64:7e44:4e78:677"
}]
}]
## [History](/docs/macloud-sdp/developer-guide/get-devices-v2-3#history)

| Version | URL |
| --- | --- |
| v2.2 | [Get Devices v2.2](/docs/macloud-sdp/developer-guide/get-devices-v2-2) |
| v2.1 | [Get Devices v2.1](/docs/macloud-sdp/developer-guide/get-devices-v2-1) |
