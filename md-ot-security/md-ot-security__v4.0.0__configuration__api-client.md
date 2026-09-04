<!-- source: https://www.opswat.com/docs/md-ot-security/v4.0.0/configuration/api-client -->

# API Client v1

## [Overall](/docs/md-ot-security/v4.0.0/configuration/api-client#overall)

## [Workflow overview](/docs/md-ot-security/v4.0.0/configuration/api-client#workflow-overview)

## [MetaDefender OT Security Configuration](/docs/md-ot-security/v4.0.0/configuration/api-client#metadefender-ot-security-configuration)

### [Create a MetaDefender OT Security User](/docs/md-ot-security/v4.0.0/configuration/api-client#create-a-metadefender-ot-security-user)

MetaDefender OT Security will utilize multiple APIs to communicate with its products. Access to the API is validated via a combination of credentials (Token). This user requires a minimum access level; do not use a Super Administrator account.

Create a user from **Enterprise** -> **User Management** → **User** → **Create User** → {Create a user, ensure that you use the Role of **API-Client** }

Clicking on the Save button → Create user successfully → Copy this API-Client Token to be used for authentication

## [API](/docs/md-ot-security/v4.0.0/configuration/api-client#api)

1. [Device] Get the server IP address

| Title | [Device] Get the server IP address |
| --- | --- |
| URL Path | https://{IP of Enterprise Manager}:3003/neu-exposure/exposure/v1/managements/components |
| Method | GET |
| Authentication method | Bearer Token |
| Request headers | - Bearer Token: retrieved after creating API-Client user (mandatory) - This API requires **Bearer Token Authentication**. You must include a valid Bearer token in the `Authorization` header. - Format: `Authorization: Bearer <token>` |
| Response |  |

- Response, 200 OK

JsonCopy{
"error": false,
"errors": [],
"data": [
{
"siteIp": "10.40.172.144",
"sensorIps": [
"10.40.172.172"
]
}
]
}

- Response, 401 - Unauthorized

JavascriptCopy{
"error": true,
"errors": [
{
"code": "NEM-3003-000204",
"message": "Invalid authentication token"
}
]
}
### [2. [Device] Get device list](/docs/md-ot-security/v4.0.0/configuration/api-client#2-device-get-device-list)

| Title | [Device] Get device list |
| --- | --- |
| URL Path | https://{IP_Enterprise}:3003/neu-exposure/exposure-external/asset-main/exposure/v1/sensor/device/items |
| Method | GET |
| Authentication method | Bearer Token |
| Request headers | - Bearer Token: retrieved after creating API-Client user (mandatory) - This API requires **Bearer Token Authentication**. You must include a valid Bearer token in the `Authorization` header. - Format: `Authorization: Bearer <token>` |
| Params | - **siteIp**:    - **Type**: `string`   - **Description**: The IP address of the site to fetch device data for.   - **Example**: `"10.40.172.144"` - **sensorIp**:    - **Type**: `string`   - **Description**: The IP address of the sensor associated with the site.   - **Example**: `"10.40.172.172"` - **data**:    - **Type**: `Object`   - **Description**: Pagination Info      - “limit”: Number of records     - “**page**”: The value should **ALWAYS** be 1.     - "sortBy": "discovTime"     - "sortType": "desc"   - **Example:**{"limit":20,"page":1,"sortBy":"discovTime","sortType":"desc"} |
| Response | Response, 200 OK Ex: |

JsonCopy{
{
"error": false,
"errors": [],
"data": [
{
"createdAt": "2024-11-05T03:07:41.880Z",
"updatedAt": "2024-11-05T03:07:41.980Z",
"dataKey": "tbfh1730774204596",
"id": 62,
"redisKey": ["00:1E:BD:0E:C0:C2"],
"properties": {
"name": "Network Device Cisco 059",
"mode": "discovery",
"isInLearningProcess": true,
"totalLearningMinutes": 0,
"currentLearningMinutes": 1440,
"startLearningTime": "2024-11-05T03:07:41.863Z",
"assetId": null,
"type": "Network Device",
"subtype": null,
"level": null,
"typeId": 53,
"subtypeId": null,
"purdueModelIds": [6],
"purdueModels": [5],
"countryOfOrigin": "US",
"criticality": "low",
"status": "inactive",
"baseline": "accepted",
"discovAgentId": 1,
"discovTime": "2024-11-05T03:07:41.863Z",
"lastUpdateTime": "2024-11-05T03:08:23.174Z",
"isSensor": false,
"isBroadcast": false,
"isOTfuse": false,
"exposureLevel": "none",
"exposureScore": 0,
"isMonitorMode": false,
"hardware": {
"model": "",
"manufacturer": "Cisco",
"version": "",
"cpu": "",
"partNumber": ""
},
"operatingSystem": {
"name": null,
"description": null,
"version": null,
"revision": null,
"kernel": null,
"update": null
},
"orderId": 59,
"webPassword": null,
"timeZone": null,
"nics": [
{
"createdAt": "2024-11-05T03:07:41.880Z",
"updatedAt": "2024-11-05T03:07:41.993Z",
"dataKey": "tbfh1730774204596",
"id": 64,
"mac": "00:1E:BD:0E:C0:C2",
"ipv4": "192.168.2.253",
"ipv6": "",
"resource": "zeek"
}
],
"sensorDataDifference": {
"countryOfOrigin": {
"isModifiable": true,
"data": null
},
"name": {
"isModifiable": true,
"data": null
},
"type": {
"isModifiable": true,
"data": null
},
"subType": {
"isModifiable": true,
"data": null
},
"purdueModels": {
"isModifiable": true,
"data": null
},
"typeId": {
"isModifiable": true,
"data": null
},
"subTypeId": {
"isModifiable": true,
"data": null
},
"purdueModelIds": {
"isModifiable": true,
"data": null
},
"criticality": {
"isModifiable": true,
"data": null
},
"ipRanges": {
"isModifiable": true,
"data": null
},
"hardwareVersion": {
"isModifiable": true,
"data": null
},
"hardwareManufacturer": {
"isModifiable": true,
"data": null
},
"hardwareModel": {
"isModifiable": true,
"data": null
},
"hardwareCPU": {
"isModifiable": true,
"data": null
},
"hardwarePartNumber": {
"isModifiable": true,
"data": null
},
"osVersion": {
"isModifiable": true,
"data": null
},
"osFirmware": {
"isModifiable": true,
"data": null
},
"osRevision": {
"isModifiable": true,
"data": null
},
"osDescription": {
"isModifiable": true,
"data": null
},
"osKernel": {
"isModifiable": true,
"data": null
}
},
"currentLearningProcess": "207/1440"
},
"isOsScanned": true,
"isHardwareScanned": false,
"resources": null,
"origin": "ecat_arp_info.log",
"reScannedData": {}
}
]
}
### [3. [Device] Get a device list by site id](/docs/md-ot-security/v4.0.0/configuration/api-client#3-device-get-a-device-list-by-site-id)

| Title | [Device] Get device list by site id |
| --- | --- |
| URL Path | https://{IP_Enterprise}:3003/neu-exposure/exposure/v1/devices/items?siteId=[2]&data={"isAll":false} |
| Method | GET |
| Authentication method | Bearer Token |
| Request headers | - Bearer Token: retrieved after creating API-Client user (mandatory) - This API requires **Bearer Token Authentication**. You must include a valid Bearer token in the `Authorization` header. - Format: `Authorization: Bearer <token>` |
| Params | - **siteId**:    - **Type**: `number[]`   - **Description**: The IP address of the site to fetch device data for.   - **Example**: `[1,2]` - **data**:    - **Type**: `Object`   - **Description**: Pagination Info      - “limit”: Number of records     - “**page**”: The value should **ALWAYS** be 1.     - "sortBy": "discovTime"     - "sortType": "desc"   - **Example:**   {"limit":20,"page":1,"sortBy":"discovTime","sortType":"desc"} |
| Response | Response, 200 OK Ex: |

JsonCopy{
"error": false,
"errors": [],
"data": {
"current": 1,
"pages": 1,
"total": 1,
"data": [
{
"createdAt": "2025-06-17T08:30:42.399Z",
"updatedAt": "2025-06-17T09:30:42.979Z",
"id": 141,
"properties": {
"name": "Virtual Machine VMware, Inc. 138",
"mode": "protected",
"isInLearningProcess": false,
"totalLearningMinutes": 60,
"currentLearningMinutes": 0,
"startLearningTime": null,
"assetId": null,
"type": "Virtual Machine",
"subtype": "",
"level": null,
"purdueModels": [
5
],
"countryOfOrigin": "US",
"criticality": "low",
"status": "inactive",
"baseline": "accepted",
"discovAgentId": null,
"discovTime": "2025-06-17T08:30:42.384Z",
"lastUpdateTime": "2025-06-17T08:30:42.384Z",
"isSensor": false,
"isBroadcast": false,
"isOTfuse": false,
"exposureLevel": "none",
"exposureScore": 0,
"hardware": {
"model": "",
"manufacturer": "VMware, Inc.",
"manufacturerId": 24424,
"version": "",
"cpu": "",
"partNumber": ""
},
"operatingSystem": {
"name": null,
"description": null,
"version": null,
"revision": null,
"kernel": null
},
"hostname": "",
"systemDescription": "Ubuntu 22.04.5 LTS Linux 6.8.0-48-generic #48~22.04.1-Ubuntu SMP PREEMPT_DYNAMIC Mon Oct 7 11:24:13 UTC 2 x86_64",
"protectedBy": null,
"isTemporaryDevice": false,
"nics": [
{
"id": 148,
"mac": "00:0C:29:49:00:17",
"ipv4": "",
"ipv6": "",
"isTemporaryNic": false
}
],
"sensorDataDifference": {},
"customFields": [],
"currentProductStateLifecycle": {},
"currentLearningProcess": "60/60"
},
"networkProperties": {}
}
]
}
}
### [4. [Device] Get a device alert list](/docs/md-ot-security/v4.0.0/configuration/api-client#4-device-get-a-device-alert-list)

| Title | [Device] Get a device alert list |
| --- | --- |
| URL Path | https://{IP_Enterprise}:3003/neu-exposure/exposure-external/alert-main/exposure/v1/sensor/device-alert/items? |
| Method | GET |
| Authentication method | Bearer Token |
| Request headers | - Bearer Token: retrieved after creating API-Client user (mandatory) - This API requires **Bearer Token Authentication**. You must include a valid Bearer token in the `Authorization` header. - Format: `Authorization: Bearer <token>` |
| Params | - **siteIp**:    - **Type**: `string`   - **Description**: The IP address of the site to fetch conn alert list data for.   - **Example**: `"10.40.172.144"` - **sensorIp**:    - **Type**: `string`   - **Description**: The IP address of the sensor associated with the site.   - **Example**: `"10.40.172.172"` - **data**:    - **Type**: `Object`   - **Description**: Pagination Info      - “limit”: {Number of records}     - “**page**”: The value should **ALWAYS** be 1.     - "sortBy":"alertStarted"     - "sortType": "desc"   - **Example**:{"limit":200,"page":1,"sortBy":"alertStarted","sortType":"desc"} |
| Response | Response, 200 OK Ex: |

JsonCopy{
"error": false,
"errors": [],
"data": {
"current": 1,
"total": "1",
"data": [
{
"id": 38,
"name": "Industrial Device Siemens 080",
"nics": [
{
"id": 89,
"mac": "00:1C:06:0F:BD:E5",
"ipv4": "192.168.25.131",
"ipv6": "",
"dataKey": "arsu1750131077955",
"resource": "zeek",
"createdAt": "2025-06-17T04:07:40.587Z",
"updatedAt": "2025-06-17T04:33:20.926Z",
"isTemporaryNic": false
}
],
"type": "Industrial Device",
"model": "",
"status": "inactive",
"assetId": null,
"subtype": "",
"deviceId": 83,
"hardware": "Siemens",
"policyId": 1,
"alertType": "country-of-origin",
"alertEnded": null,
"alertGroup": "device-pbl-supply-chain",
"alertState": "active",
"discovTime": "2025-06-14T13:20:22.739Z",
"partNumber": "",
"policyName": "DEVICE.SUPPLY.CHAIN.250618.075304.749",
"alertReason": null,
"alertStatus": "pending-acknowledged",
"criticality": "high",
"alertComment": null,
"alertStarted": "2025-06-18T07:53:04.816+00:00",
"purdueModels": [
1
],
"alertMessages": "Device with network adapter from China is detected. China is in the supply chain blocklist",
"alertResolved": "pending-acknowledged",
"discovAgentId": null,
"countryOfOrigin": "CN",
"operatingSystem": "",
"alertCriticality": "severe"
}
],
"remainingPage": "1"
}
}
### [5. [Device] Get the connection alert list](/docs/md-ot-security/v4.0.0/configuration/api-client#5-device-get-the-connection-alert-list)

| Title | [Device] Get the connection alert list |
| --- | --- |
| URL Path | https://{IP_Enterprise}:3003/neu-exposure/exposure-external/alert-main/exposure/v1/sensor/conn-alert/items |
| Method | GET |
| Authentication method | Bearer Token |
| Request headers | - Bearer Token: retrieved after creating API-Client user (mandatory) - This API requires **Bearer Token Authentication**. You must include a valid Bearer token in the `Authorization` header. - Format: `Authorization: Bearer <token>` |
| Params | - **siteIp**:    - **Type**: `string`   - **Description**: The IP address of the site to fetch conn alert list data for.   - **Example**: `"10.40.172.144"` - **sensorIp**:    - **Type**: `string`   - **Description**: The IP address of the sensor associated with the site.   - **Example**: `"10.40.172.172"` - **data**:    - **Type**: `Object`   - **Description**: Pagination Info      - “limit”: {Number of records}     - “**page**”: The value should **ALWAYS** be 1.     - "sortBy":"alertStarted"     - "sortType": "desc"   - **Example**:{"limit":200,"page":1,"sortBy":"alertStarted","sortType":"desc"} |
| Response | Response, 200 OK Ex: |

JavascriptCopy{
"error": false,
"errors": [],
"data": {
"current": 1,
"total": "1",
"data": [
{
"id": 6615,
"source": "Virtual Machine VMware, Inc. 119//192.168.1.191//00:0C:29:18:28:93",
"duration": "1.83",
"policyId": 12,
"alertType": "unauthorized",
"startTime": "2025-06-18T09:26:45.363Z",
"alertEnded": null,
"alertGroup": "conn-pbl-unauthorized",
"alertState": "active",
"policyName": "CONN.UNAUTHORIZED.250617.033314.430",
"sourcePort": "45209",
"alertReason": null,
"alertStatus": "pending-acknowledged",
"destination": "PLC Siemens S7-1200 010//192.168.1.103//E0:DC:A0:C4:6A:43,E0:DC:A0:C4:6A:42",
"alertComment": null,
"alertStarted": "2025-06-18T09:26:43.03+00:00",
"alertMessages": "Connection violates unauthorized policy from Purdue level 5 to Purdue level 1 ",
"alertResolved": "pending-acknowledged",
"connDataLength": null,
"sourceDeviceId": "122",
"destinationPort": "102",
"serviceProtocol": "S7COMM-PLUS",
"alertCriticality": "high",
"destinationDeviceId": "13"
}
],
"remainingPage": "1"
}
}
### [6. [Device] Get the Suricata alert list](/docs/md-ot-security/v4.0.0/configuration/api-client#6-device-get-the-suricata-alert-list)

| Title | [Device] Get the Suricata alert list |
| --- | --- |
| URL Path | https://{IP_Enterprise}:3003/neu-exposure/exposure-external/alert-main/exposure/v1/sensor/suricata-alert/items |
| Method | GET |
| Authentication method | Bearer Token |
| Request headers | - Bearer Token: retrieved after creating API-Client user (mandatory) - This API requires **Bearer Token Authentication**. You must include a valid Bearer token in the `Authorization` header. - Format: `Authorization: Bearer <token>` |
| Params | - **siteIp**:    - **Type**: `string`   - **Description**: The IP address of the site to fetch conn alert list data for.   - **Example**: `"10.40.172.144"` - **sensorIp**:    - **Type**: `string`   - **Description**: The IP address of the sensor associated with the site.   - **Example**: `"10.40.172.172"` - **data**:    - **Type**: `Object`   - **Description**: Pagination Info      - “limit”: {Number of records}     - “**page**”: The value should **ALWAYS** be 1.     - "sortBy":"alertStarted"     - "sortType": "desc"   - **Example**:{"limit":200,"page":1,"sortBy":"alertStarted","sortType":"desc"} |
| Response | Response, 200 OK Ex: |

JavascriptCopy{
"error": false,
"errors": [],
"data": {
"current": 1,
"total": "2",
"data": [
{
"id": 2,
"source": "SCADA Dell 004//192.168.1.241//8C:EC:4B:AB:B7:5C",
"eventId": 2,
"duration": null,
"policyId": 209,
"alertType": "unauthorized",
"startTime": "2025-06-19T08:32:12.587Z",
"alertEnded": null,
"alertGroup": "suricata-pbl-unauthorized",
"alertState": "active",
"policyName": "SURICATA.UNAUTHORIZED.250619.083149.087",
"sourcePort": "49497",
"alertReason": null,
"alertStatus": "pending-acknowledged",
"destination": "Industrial Device Delta Electronic 017//192.168.1.105//00:18:23:12:39:19",
"alertComment": null,
"alertStarted": "2025-06-19T08:32:11.137+00:00",
"connectionId": null,
"alertMessages": "Connection violates suricata policy from Any to Any (Automation)",
"alertResolved": "pending-acknowledged",
"sourceDeviceId": "6",
"destinationPort": "502",
"serviceProtocol": "Modbus-TCP",
"alertCriticality": "severe",
"destinationDeviceId": "45"
},
{
"id": 1,
"source": "SCADA Dell 004//192.168.1.241//8C:EC:4B:AB:B7:5C",
"eventId": 1,
"duration": null,
"policyId": 209,
"alertType": "unauthorized",
"startTime": "2025-06-19T08:31:56.510Z",
"alertEnded": null,
"alertGroup": "suricata-pbl-unauthorized",
"alertState": "active",
"policyName": "SURICATA.UNAUTHORIZED.250619.083149.087",
"sourcePort": "49422",
"alertReason": null,
"alertStatus": "pending-acknowledged",
"destination": "Industrial Device Delta Electronic 017//192.168.1.105//00:18:23:12:39:19",
"alertComment": null,
"alertStarted": "2025-06-19T08:31:55.185+00:00",
"connectionId": null,
"alertMessages": "Connection violates suricata policy from Any to Any (Automation)",
"alertResolved": "pending-acknowledged",
"sourceDeviceId": "6",
"destinationPort": "502",
"serviceProtocol": "Modbus-TCP",
"alertCriticality": "severe",
"destinationDeviceId": "45"
}
],
"remainingPage": "1"
}
}
### [7. [Device] Get CVE list](/docs/md-ot-security/v4.0.0/configuration/api-client#7-device-get-cve-list)

| Title | [Device] Get the list of CVEs for the device |
| --- | --- |
| URL Path | https://{IP of Enterprise Manager}:3003/neu-exposure/exposure-external/asset-report/exposure/v1/sensor/device-cves/items |
| Method | GET |
| Authentication method | Bearer Token |
| Request headers | - Bearer Token: retrieved after creating API-Client user (mandatory) - This API requires **Bearer Token Authentication**. You must include a valid Bearer token in the `Authorization` header. - Format: `Authorization: Bearer <token>` |
| Params | - **siteIp**:    - **Type**: `string`   - **Description**: The IP address of the site to fetch conn alert list data for.   - **Example**: `"10.40.172.144"` - **sensorIp**:    - **Type**: `string`   - **Description**: The IP address of the sensor associated with the site.   - **Example**: `"10.40.172.172"` - **data**:    - **Type**: `Object`   - **Description**: Pagination Info      - “limit”: {Number of records}     - “**page**”: The value should **ALWAYS** be 1.     - "sortBy":"alertStarted"     - "sortType": "desc"   - **Example**:{"limit":250,"page":1,"sortBy":"name","sortType":"desc"} |
| Response | Response, 200 OK Ex: |

JavascriptCopy{
"error": false,
"errors": [],
"data": {
"current": 1,
"pages": 2,
"total": 28,
"data": [
{
"createdAt": "2025-06-19T04:00:18.101Z",
"updatedAt": "2025-06-19T07:51:04.450Z",
"id": "19",
"cve": {
"id": 197167,
"cveCode": "CVE-2022-40227",
"description": "A vulnerability has been identified in SIMATIC HMI Comfort Panels (incl. SIPLUS variants) (All versions < V17 Update 4), SIMATIC HMI KTP Mobile Panels (All versions < V17 Update 4), SIMATIC HMI KTP1200 Basic (All versions < V17 Update 5), SIMATIC HMI KTP400 Basic (All versions < V17 Update 5), SIMATIC HMI KTP700 Basic (All versions < V17 Update 5), SIMATIC HMI KTP900 Basic (All versions < V17 Update 5), SIPLUS HMI KTP1200 BASIC (All versions < V17 Update 5), SIPLUS HMI KTP400 BASIC (All versions < V17 Update 5), SIPLUS HMI KTP700 BASIC (All versions < V17 Update 5), SIPLUS HMI KTP900 BASIC (All versions < V17 Update 5). Affected devices do not properly validate input sent to certain services over TCP. This could allow an unauthenticated remote attacker to cause a permanent denial of service condition (requiring a device reboot) by sending specially crafted TCP packets.",
"nistData": {
"cvssV2": {
"vectorString": null,
"baseSeverity": null,
"baseScore": null
},
"cvssV3": {
"vectorString": "CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H",
"baseSeverity": "HIGH",
"baseScore": 7.5
}
},
"remediations": [
{
"url": "cves/CVE-2022-40227/reference_0.pdf"
}
]
},
"status": "unpatched",
"lastDetectedTime": "2025-06-19T07:50:57.569Z",
"nics": [
{
"id": 42,
"mac": "8C:F3:19:3F:3D:26",
"ipv4": "192.168.1.203",
"ipv6": "",
"isTemporaryNic": false
}
],
"deviceId": 38,
"manufacturer": "Siemens",
"name": "HMI Siemens HMI 041",
"type": "HMI",
"subtype": "",
"deviceStatus": "active",
"securityNotificationPaths": [
"/security-notifications/cves/CVE-2022-40227/reference_0.pdf"
]
}
]
}
}
### [8. [Device] Get the list of CVEs for the device by site id](/docs/md-ot-security/v4.0.0/configuration/api-client#8-device-get-the-list-of-cves-for-the-device-by-site-id)

| Title | [Device] Get the list of CVEs for the device by site id |
| --- | --- |
| URL Path | https://{IP of Enterprise Manager}:3003/neu-exposure/exposure/v1/devices/items?siteId=[2]&data={"isAll":false} |
| Method | GET |
| Authentication method | Bearer Token |
| Request headers | - Bearer Token: retrieved after creating API-Client user (mandatory) - This API requires **Bearer Token Authentication**. You must include a valid Bearer token in the `Authorization` header. - Format: `Authorization: Bearer <token>` |
| Params | - **siteIp**:    - **Type**: `string`   - **Description**: The IP address of the site to fetch conn alert list data for.   - **Example**: `"10.40.172.144"` - **data**: - - **Type**: `Object`   - **Description**: Pagination Info      - “limit”: {Number of records}     - “**page**”: The value should **ALWAYS** be 1.     - "sortBy":"alertStarted"     - "sortType": "desc"   - **Example**:{"limit":20,"page":1,"sortBy":"discovTime","sortType":"desc"} |
| Response | Response, 200 OK Ex: |

JavascriptCopy{
"error": false,
"errors": [],
"data": {
"current": 1,
"pages": 2,
"total": 28,
"data": [
{
"createdAt": "2025-06-19T04:00:18.101Z",
"updatedAt": "2025-06-19T07:51:04.450Z",
"id": "19",
"cve": {
"id": 197167,
"cveCode": "CVE-2022-40227",
"description": "A vulnerability has been identified in SIMATIC HMI Comfort Panels (incl. SIPLUS variants) (All versions < V17 Update 4), SIMATIC HMI KTP Mobile Panels (All versions < V17 Update 4), SIMATIC HMI KTP1200 Basic (All versions < V17 Update 5), SIMATIC HMI KTP400 Basic (All versions < V17 Update 5), SIMATIC HMI KTP700 Basic (All versions < V17 Update 5), SIMATIC HMI KTP900 Basic (All versions < V17 Update 5), SIPLUS HMI KTP1200 BASIC (All versions < V17 Update 5), SIPLUS HMI KTP400 BASIC (All versions < V17 Update 5), SIPLUS HMI KTP700 BASIC (All versions < V17 Update 5), SIPLUS HMI KTP900 BASIC (All versions < V17 Update 5). Affected devices do not properly validate input sent to certain services over TCP. This could allow an unauthenticated remote attacker to cause a permanent denial of service condition (requiring a device reboot) by sending specially crafted TCP packets.",
"nistData": {
"cvssV2": {
"vectorString": null,
"baseSeverity": null,
"baseScore": null
},
"cvssV3": {
"vectorString": "CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H",
"baseSeverity": "HIGH",
"baseScore": 7.5
}
},
"remediations": [
{
"url": "cves/CVE-2022-40227/reference_0.pdf"
}
]
},
"status": "unpatched",
"lastDetectedTime": "2025-06-19T07:50:57.569Z",
"nics": [
{
"id": 42,
"mac": "8C:F3:19:3F:3D:26",
"ipv4": "192.168.1.203",
"ipv6": "",
"isTemporaryNic": false
}
],
"deviceId": 38,
"manufacturer": "Siemens",
"name": "HMI Siemens HMI 041",
"type": "HMI",
"subtype": "",
"deviceStatus": "active",
"securityNotificationPaths": [
"/security-notifications/cves/CVE-2022-40227/reference_0.pdf"
]
}
]
}
}

- Response, 401 - Unauthorized

JavascriptCopy{
"error": true,
"errors": [
{
"code": "NEM-3003-000201",
"message": "Unauthorized Common Gateway"
}
]
}JavascriptCopy{
"error": true,
"errors": [
{
"code": "NEM-3003-000404",
"message": "Site ip is invalid"
}
]
}
### [9. [Components] Get component info](/docs/md-ot-security/v4.0.0/configuration/api-client#9-components-get-component-info)

| Title | [Components] Get the list of Site and Sensor infor |
| --- | --- |
| URL Path | https://{IP of Enterprise Manager}:3003/neu-exposure/exposure/v1/managements/components |
| Method | GET |
| Authentication method | Bearer Token |
| Request headers | - Bearer Token: retrieved after creating API-Client user (mandatory) - This API requires **Bearer Token Authentication**. You must include a valid Bearer token in the `Authorization` header. - Format: `Authorization: Bearer <token>` |
| Params |  |
| Response | Response, 200 OK Ex: |

JavascriptCopy{
"error": false,
"errors": [],
"data": [
{
"siteIp": "10.40.172.190",
"sensorIps": [
"127.0.0.1"
]
},
{
"siteIp": "10.40.172.188",
"sensorIps": [
"10.40.176.61",
"10.40.172.187"
]
}
]
}

- Response, 401 - Unauthorized

JavascriptCopy{
"error": true,
"errors": [
{
"code": "NEM-3003-000201",
"message": "Unauthorized Common Gateway"
}
]
}JavascriptCopy{
"error": true,
"errors": [
{
"code": "NEM-3003-000404",
"message": "Site ip is invalid"
}
]
}
### [10. [Components] Get sites address](/docs/md-ot-security/v4.0.0/configuration/api-client#10-components-get-sites-address)

| Title | [Device] Get sites address |
| --- | --- |
| URL Path | https://{IP of Enterprise Manager}:3003/neu-exposure/exposure/v1/managements/sites |
| Method | GET |
| Authentication method | Bearer Token |
| Request headers | - Bearer Token: retrieved after creating API-Client user (mandatory) - This API requires **Bearer Token Authentication**. You must include a valid Bearer token in the `Authorization` header. - Format: `Authorization: Bearer <token>` |
| Params |  |
| Response | Response, 200 OK Ex: |

JavascriptCopy{
"error": false,
"errors": [],
"data": [
{
"id": 1,
"name": "Site Manager"
},
{
"id": 2,
"name": "Site Bundle Manager"
}
]
}

- Response, 401 - Unauthorized

JavascriptCopy{
"error": true,
"errors": [
{
"code": "NEM-3003-000201",
"message": "Unauthorized Common Gateway"
}
]
}JavascriptCopy{
"error": true,
"errors": [
{
"code": "NEM-3003-000404",
"message": "Site ip is invalid"
}
]
}
## [API Patching PLC Device](/docs/md-ot-security/v4.0.0/configuration/api-client#api-patching-plc-device)

### [Enterprise Manager - Update PLC Firmware by getting from the Cloud Repo or uploading Manualy](/docs/md-ot-security/v4.0.0/configuration/api-client#enterprise-manager---update-plc-firmware-by-getting-from-the-cloud-repo-or-uploading-manualy)

Navigate to the Enterprise Manager → Settings → Update Signatures & Definitions → PLC Firmware

**Get from Cloud Repo**: we can filter by a specific **Article/Part No**.

### [1.[Device Firmware File] Get available version](/docs/md-ot-security/v4.0.0/configuration/api-client#1device-firmware-file-get-available-version)

| Title | [Device Firmware File] Get available version |
| --- | --- |
| URL Path | https://{IP of Enterprise Manager}:3003/neu-exposure/exposure/v1/device-firmware-files/check-available-version |
| Method | POST |
| Authentication method | Bearer Token |
| Request headers | - Bearer Token: retrieved after creating API-Client user (mandatory) - This API requires **Bearer Token Authentication**. You must include a valid Bearer token in the `Authorization` header. - Format: `Authorization: Bearer <token>` |

Request body:

- Raw format:

JavascriptCopy[
{
"manufacturer": "Siemens", //Vendor of PLC device
"partNumber": "6ES7211-1AE40-0XB0" //Part number of PLC
}
]

Response:

- Response, 200 OK

JavascriptCopy{
"error": false,
"errors": [],
"data": [
{
"manufacturer": "Siemens",
"partNumber": "6ES7211-1AE40-0XB0",
"availableVersion": [
{
"version": "4.4.0",
"fileName": "0ecd6f50f36b1f60ae21b2e43b89f30e.upd"
},
{
"version": "4.5.0",
"fileName": "366518a81bd9b611ea880fe873b614d4.upd"
}
]
}
]
}

- Response, 401 - Unauthorized

JavascriptCopy{
"error": true,
"errors": [
{
"code": "NEM-3003-000201",
"message": "Unauthorized Common Gateway"
}
]
}
### [2. [Device] Get the *device ID* for patching](/docs/md-ot-security/v4.0.0/configuration/api-client#2-device-get-the-device-id-for-patching)

| Title | [Device] Get the ***device ID*** for patching |
| --- | --- |
| URL Path | https://{IP of Enterprise Manager}:3003/neu-exposure/exposure-external/asset-main/exposure/v1/sensor/device/items |
| Method | GET |
| Authentication method | Bearer Token |
| Request headers | - Bearer Token: retrieved after creating API-Client user (mandatory) - This API requires **Bearer Token Authentication**. You must include a valid Bearer token in the `Authorization` header. - Format: `Authorization: Bearer <token>` |
| Params | Get based on IPv4 or the MAC address of the Device   - **siteIp**:    - **Type**: `string`   - **Description**: The IP address of the site to fetch device data for.   - **Example**: `"10.40.172.144"` - **sensorIp**:    - **Type**: `string`   - **Description**: The IP address of the sensor associated with the site.   - **Example**: `"10.40.172.172"` - **data**:    - **Type**: `Object`   - **Description**: Pagination Info      - “limit”: Number of records     - “**page**”: The value should **ALWAYS** be 1.     - "sortBy": "discovTime"     - "sortType": "desc"     - “properties“: {"ipv4":"", "mac":""}   - **Example:**   - {"limit":20,"page":1,"sortBy":"discovTime","sortType":"desc","properties":{"ipv4":"192.168.1.103","mac":"E0:DC:A0:C4:6A:42"}} |
| Response | Response, 200 OK Ex: |

JavascriptCopy{
"error": false,
"errors": [],
"data": {
"current": 1,
"pages": 1,
"total": 1,
"data": [
{
"createdAt": "2025-06-14T04:07:04.780Z",
"updatedAt": "2025-06-18T07:51:00.393Z",
"id": 13, // This is device ID
"properties": {
"name": "PLC Siemens S7-1200 010",
"mode": "protected",
"isInLearningProcess": false,
"totalLearningMinutes": 60,
"currentLearningMinutes": 0,
"startLearningTime": null,
"assetId": null,
"type": "Industrial Device",
"subtype": "PLC",
"level": null,
"purdueModels": [
1
],
"countryOfOrigin": "CN",
"criticality": "high",
"status": "active",
"baseline": "accepted",
"discovAgentId": 1,
"discovTime": "2025-06-14T04:07:04.780Z",
"lastUpdateTime": "2025-06-18T04:44:53.934Z",
"isSensor": false,
"isBroadcast": false,
"isOTfuse": false,
"exposureLevel": "high",
"exposureScore": 80,
"hardware": {
"model": "S7-1200",
"manufacturer": "Siemens",
"manufacturerId": 8261,
"version": "10.0.0",
"cpu": "CPU 1212C AC/DC/Rly",
"partNumber": "6ES7212-1BE40-0XB0"
},
"operatingSystem": {
"name": "",
"description": "",
"version": "4.5.2",
"revision": "",
"kernel": ""
},
"hostname": "phân+loại sản phẩm=plc-siemens_103",
"systemDescription": "Siemens, SIMATIC S7, CPU-1200, 6ES7 212-1BE40-0XB0, HW: 10, FW: V.4.5.2, S V-M5BL0194",
"protectedBy": "OPSWAT Industrial Firewall 112",
"isTemporaryDevice": false,
"nics": [
{
"id": 18,
"mac": "E0:DC:A0:C4:6A:42",
"ipv4": "192.168.1.103",
"ipv6": "",
"isTemporaryNic": false
},
{
"id": 19,
"mac": "E0:DC:A0:C4:6A:43",
"ipv4": "",
"ipv6": "",
"isTemporaryNic": false
}
],
"sensorDataDifference": {},
"customFields": [],
"currentProductStateLifecycle": {
"id": 2,
"manufacturerId": 8261,
"state": "DeliveryRelease",
"normalizedState": "Delivery Release",
"description": null,
"data": null
},
"currentLearningProcess": "60/60"
},
"networkProperties": {}
}
]
}
}

- Response, 401 - Unauthorized

JavascriptCopy{
"error": true,
"errors": [
{
"code": "NEM-3003-000201",
"message": "Unauthorized Common Gateway"
}
]
}JavascriptCopy{
"error": true,
"errors": [
{
"code": "NEM-3003-000404",
"message": "Site ip is invalid"
}
]
}
### [3. [Device] Get the list of CVEs for device](/docs/md-ot-security/v4.0.0/configuration/api-client#3-device-get-the-list-of-cves-for-device)

| Title | [Device] Get the list of CVEs for the device |
| --- | --- |
| URL Path | https://{IP of Enterprise Manager}:3003/neu-exposure/exposure-external/asset-main/exposure/v1/sensor/device/cves |
| Method | GET |
| Authentication method | Bearer Token |
| Request headers | - Bearer Token: retrieved after creating API-Client user (mandatory) - This API requires **Bearer Token Authentication**. You must include a valid Bearer token in the `Authorization` header. - Format: `Authorization: Bearer <token>` |
| Params | - **siteIp**:    - **Type**: `string`   - **Description**: The IP address of the site to fetch device data for.   - **Example**: `"10.40.172.144"` - **sensorIp**:    - **Type**: `string`   - **Description**: The IP address of the sensor associated with the site.   - **Example**: `"10.40.172.172"` - **data**:    - **Type**: `Object`   - **Description**: Pagination Info      - “id”: the device ID     - “status”: /unpatched/patched/potential or ““ to get all   - **Example:**   - {"id":1, "status": ""} |
| Response | Response, 200 OK Ex: |

JavascriptCopy{
"error": false,
"errors": [],
"data": [
{
"createdAt": "2025-06-17T07:39:10.862Z",
"updatedAt": "2025-06-18T04:44:45.492Z",
"id": "39",
"cve": {
"id": 201761,
"cveCode": "CVE-2021-40365",
"description": "Affected devices don't process correctly certain special crafted packets sent to port 102/tcp, which could allow an attacker to cause a denial of service in the device.",
"nistData": {
"cvssV2": {
"vectorString": null,
"baseSeverity": null,
"baseScore": null
},
"cvssV3": {
"vectorString": "CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H",
"baseSeverity": "HIGH",
"baseScore": 7.5
}
},
"remediations": [
{
"url": "cves/CVE-2021-40365/reference_0.pdf"
}
]
},
"status": "unpatched",
"lastDetectedTime": "2025-06-18T04:44:53.934Z",
"securityNotificationPaths": [
"security-notifications/cves/CVE-2021-40365/reference_0.pdf"
]
},
{
"createdAt": "2025-06-17T03:35:02.219Z",
"updatedAt": "2025-06-17T04:41:29.500Z",
"id": "11",
"cve": {
"id": 56029,
"cveCode": "CVE-2013-0700",
"description": "Siemens SIMATIC S7-1200 PLCs 2.x and 3.x allow remote attackers to cause a denial of service (defect-mode transition and control outage) via crafted packets to TCP port 102 (aka the ISO-TSAP port).",
"nistData": {
"cvssV2": {
"vectorString": "AV:N/AC:L/Au:N/C:N/I:N/A:C",
"baseSeverity": null,
"baseScore": 7.8
},
"cvssV3": {
"vectorString": null,
"baseSeverity": null,
"baseScore": null
}
},
"remediations": [
{
"url": "cves/CVE-2013-0700/reference_1.pdf"
}
]
},
"status": "patched",
"lastDetectedTime": "2025-06-17T04:40:25.269Z",
"lastPatchedTime": "2025-06-17T04:41:27.108Z",
"securityNotificationPaths": ["security-notifications/cves/CVE-2013-0700/reference_1.pdf"]
}
]
}

- Response, 401 - Unauthorized

JavascriptCopy{
"error": true,
"errors": [
{
"code": "NEM-3003-000201",
"message": "Unauthorized Common Gateway"
}
]
}JavascriptCopy{
"error": true,
"errors": [
{
"code": "NEM-3003-000404",
"message": "Site ip is invalid"
}
]
}
### [4. [Request Patching] Get list](/docs/md-ot-security/v4.0.0/configuration/api-client#4-request-patching-get-list)

| Title | [Request Patching] Get list |
| --- | --- |
| URL Path | https://{IP of Enterprise Manager}:3003/neu-exposure/exposure-external/asset-main/exposure/v1/sensor/request-patching/items |
| Method | GET |
| Authentication method | Bearer Token |
| Request headers | - Bearer Token: retrieved after creating API-Client user (mandatory) - This API requires **Bearer Token Authentication**. You must include a valid Bearer token in the `Authorization` header. - Format: `Authorization: Bearer <token>` |
| Params | - **siteIp**:    - **Type**: `string`   - **Description**: The IP address of the site to fetch device data for.   - **Example**: `"10.40.172.144"` - **sensorIp**:    - **Type**: `string`   - **Description**: The IP address of the sensor associated with the site.   - **Example**: `"10.40.172.172"` |
| Response | Response, 200 OK Ex: |

JavascriptCopy{
"error": false,
"errors": [],
"data": {
"current": 1,
"pages": 1,
"total": 2,
"data": [
{
"id": 3,
"type": "immediately",
"requestedAt": "2025-06-19T08:49:49.219Z",
"scheduleDate": "2025-06-19T08:49:49.349Z",
"scheduleTimeoutInMinutes": 1440,
"totalAsset": 1,
"status": "pending",
"approver": null,
"approverId": null,
"approverUserDirectoryId": null,
"approverUserDirectoryName": null,
"statusUpdatedAt": "2025-06-19T08:49:49.219Z",
"note": "Automation 4.5.1 to 4.5.2",
"isDeleted": false,
"requester": "api-patching",
"requesterId": 3,
"requesterUserDirectoryId": 1,
"requesterUserDirectoryName": null,
"updatedBy": "api-patching",
"updatedById": 3,
"updatedByUserDirectoryId": 1,
"updatedByUserDirectoryName": "Local",
"devices": []
},
{
"id": 1,
"type": "immediately",
"requestedAt": "2025-06-19T08:49:48.651Z",
"scheduleDate": "2025-06-19T08:49:48.643Z",
"scheduleTimeoutInMinutes": 1440,
"totalAsset": 1,
"status": "rejected",
"approver": null,
"approverId": null,
"approverUserDirectoryId": null,
"approverUserDirectoryName": null,
"statusUpdatedAt": "2025-06-19T08:49:48.891Z",
"note": "Automation 4.1.2",
"isDeleted": false,
"requester": "api-patching",
"requesterId": 3,
"requesterUserDirectoryId": 1,
"requesterUserDirectoryName": null,
"updatedBy": "api-patching",
"updatedById": 3,
"updatedByUserDirectoryId": 1,
"updatedByUserDirectoryName": "Local",
"devices": []
}
]
}
}

- Response, 401 - Unauthorized

JavascriptCopy{
"error": true,
"errors": [
{
"code": "NEM-3003-000201",
"message": "Unauthorized Common Gateway"
}
]
}JavascriptCopy{
"error": true,
"errors": [
{
"code": "NEM-3003-000404",
"message": "Site ip is invalid"
}
]
}
### [5. [Request Patching] Get detail](/docs/md-ot-security/v4.0.0/configuration/api-client#5-request-patching-get-detail)

| Title | [Request Patching] Get detail |
| --- | --- |
| URL Path | https://{IP of Enterprise Manager}:3003/neu-exposure/exposure-external/asset-report/exposure/v1/sensor/device-cves/items |
| Method | GET |
| Authentication method | Bearer Token |
| Request headers | - Bearer Token: retrieved after creating API-Client user (mandatory) - This API requires **Bearer Token Authentication**. You must include a valid Bearer token in the `Authorization` header. - Format: `Authorization: Bearer <token>` |
| Params | - **siteIp**:    - **Type**: `string`   - **Description**: The IP address of the site to fetch device data for.   - **Example**: `"10.40.172.144"` - **sensorIp**:    - **Type**: `string`   - **Description**: The IP address of the sensor associated with the site.   - **Example**: `"10.40.172.172"` - **data**:    - **Type**: `Object`   - **Description**:      - “id”: the id of the request patching   - **Example:**{"id": 3} |
| Response | Response, 200 OK Ex: |

JavascriptCopy{
"error": false,
"errors": [],
"data": {
"id": 3,
"type": "immediately",
"requestedAt": "2025-06-19T08:49:49.219Z",
"scheduleDate": "2025-06-19T08:49:49.349Z",
"scheduleTimeoutInMinutes": 1440,
"totalAsset": 1,
"status": "pending",
"approver": null,
"approverId": null,
"approverUserDirectoryId": null,
"approverUserDirectoryName": null,
"statusUpdatedAt": "2025-06-19T08:49:49.219Z",
"note": "Automation 4.5.1 to 4.5.2",
"isDeleted": false,
"requester": "api-patching",
"requesterId": 3,
"requesterUserDirectoryId": 1,
"requesterUserDirectoryName": null,
"updatedBy": "api-patching",
"updatedById": 3,
"updatedByUserDirectoryId": 1,
"updatedByUserDirectoryName": "Local",
"devices": [
{
"id": 4,
"deviceId": 19,
"status": "waiting-for-approve",
"updateStatus": null,
"updateStatusDescription": null,
"currentVersion": "",
"dataKey": "iabc1750304160282",
"requestId": 3,
"userName": "",
"password": "",
"manufacturerId": 8261,
"manufacturer": "Siemens",
"partNumber": "6ES7212-1BE40-0XB0",
"updateVersion": "4.5.2",
"updateFileName": "c2c4473c6e8cb61176603a945112021a.upd",
"nics": [
{
"ipv4": "192.168.1.103",
"mac": "E0:DC:A0:C4:6A:42"
}
]
}
]
}
}

- Response, 401 - Unauthorized

JavascriptCopy{
"error": true,
"errors": [
{
"code": "NEM-3003-000201",
"message": "Unauthorized Common Gateway"
}
]
}JavascriptCopy{
"error": true,
"errors": [
{
"code": "NEM-3003-000404",
"message": "Site ip is invalid"
}
]
}
### [6. [Request Patching] Create request](/docs/md-ot-security/v4.0.0/configuration/api-client#6-request-patching-create-request)

| Title | [Request Patching] Create request |
| --- | --- |
| URL Path | https://{IP of Enterprise Manager}:3003/neu-exposure/exposure-external/asset-main/exposure/v1/sensor/request-patching/item |
| Method | POST |
| Authentication method | Bearer Token |
| Request headers | - Bearer Token: retrieved after creating API-Client user (mandatory) - This API requires **Bearer Token Authentication**. You must include a valid Bearer token in the `Authorization` header. - Format: `Authorization: Bearer <token>` |
| Params | - **siteIp**:    - **Type**: `string`   - **Description**: The IP address of the site to fetch conn alert list data for.   - **Example**: `"10.40.172.144"` - **sensorIp**:    - **Type**: `string`   - **Description**: The IP address of the sensor associated with the site.   - **Example**: `"10.40.172.172"` |

Request body

- Raw format

JavascriptCopy{
"type": "immediately",
"note": "test api client",
"isDevicePasswordNotEncrypted": true,
"devices": [
{
"deviceId": 19, //The device ID
"manufacturer": "Siemens", // Vendor of PLC device
"partNumber": "6ES7212-1BE40-0XB0", // The part number of PLC device
"currentVersion": "4.5.1", //Current version of device
"updateVersion": "4.5.2", //Version wana to update
"updateFileName": "c2c4473c6e8cb61176603a945112021a.upd", //The update file name corresponding
"userName": "",
"password": "" //Optional if device need password
}
]
}

Response

- Response, 200 OK

JavascriptCopy{
"error": false,
"errors": [],
"data": {
"id": 5,
"type": "immediately",
"requestedAt": "2025-06-19T09:00:55.792Z",
"scheduleDate": "2025-06-19T09:00:55.737Z",
"scheduleTimeoutInMinutes": 1440,
"totalAsset": 1,
"status": "pending",
"approver": null,
"approverId": null,
"approverUserDirectoryId": null,
"approverUserDirectoryName": null,
"statusUpdatedAt": "2025-06-19T09:00:55.792Z",
"note": "test api client",
"requester": "api-patching",
"requesterId": 3,
"requesterUserDirectoryId": 1,
"requesterUserDirectoryName": null,
"updatedBy": null,
"updatedById": null,
"updatedByUserDirectoryId": null,
"updatedByUserDirectoryName": null,
"devices": [
{
"id": 6,
"deviceId": 19,
"status": "waiting-for-approve",
"updateStatus": null,
"updateStatusDescription": null,
"currentVersion": "4.5.1",
"dataKey": "iabc1750304160282",
"requestId": 5,
"userName": "",
"password": "",
"manufacturerId": 8261,
"manufacturer": "Siemens",
"partNumber": "6ES7212-1BE40-0XB0",
"updateVersion": "4.5.2",
"updateFileName": "c2c4473c6e8cb61176603a945112021a.upd",
"nics": []
}
]
}
}

- Response, 401 - Unauthorized

JavascriptCopy{
"error": true,
"errors": [
{
"code": "NEM-3003-000201",
"message": "Unauthorized Common Gateway"
}
]
}JavascriptCopy{
"error": true,
"errors": [
{
"code": "NEM-3003-000404",
"message": "Site ip is invalid"
}
]
}
### [7. [Request Patching] Update request](/docs/md-ot-security/v4.0.0/configuration/api-client#7-request-patching-update-request)

| Title | [Request Patching] Create request |
| --- | --- |
| URL Path | https://{IP of Enterprise Manager}:3003/neu-exposure/exposure-external/asset-main/exposure/v1/sensor/request-patching/item |
| Method | PUT |
| Authentication method | Bearer Token |
| Request headers | - Bearer Token: retrieved after creating API-Client user (mandatory) - This API requires **Bearer Token Authentication**. You must include a valid Bearer token in the `Authorization` header. - Format: `Authorization: Bearer <token>` |
| Params | - **siteIp**:    - **Type**: `string`   - **Description**: The IP address of the site to fetch conn alert list data for.   - **Example**: `"10.40.172.144"` - **sensorIp**:    - **Type**: `string`   - **Description**: The IP address of the sensor associated with the site.   - **Example**: `"10.40.172.172"` |

Request body

- Raw format

JavascriptCopy{
"id": 5, //The ID of Request Patching
"type": "immediately",
"note": "test api client",
"isDevicePasswordNotEncrypted": true,
"devices": [
{
"deviceId": 5, //The device ID
"manufacturer": "Siemens", // Vendor of PLC device
"partNumber": "6ES7212-1BE40-0XB0", // The part number of PLC device
"currentVersion": "4.5.1", //Current version of device
"updateVersion": "4.5.2", //Version wana to update
"updateFileName": "c2c4473c6e8cb61176603a945112021a.upd", //The update file name corresponding
"userName": "",
"password": "" //Optional if device need password
}
]
}

Response

- Response, 200 OK

JavascriptCopy{
"error": false,
"errors": [],
"data": {
"id": 5,
"type": "immediately",
"requestedAt": "2025-06-19T09:00:55.792Z",
"scheduleDate": "2025-06-19T09:05:14.441Z",
"scheduleTimeoutInMinutes": 1440,
"totalAsset": 1,
"status": "pending",
"approver": null,
"approverId": null,
"approverUserDirectoryId": null,
"approverUserDirectoryName": null,
"statusUpdatedAt": "2025-06-19T09:00:55.792Z",
"note": "test api client",
"isDeleted": false,
"requester": "api-patching",
"requesterId": 3,
"requesterUserDirectoryId": 1,
"requesterUserDirectoryName": null,
"updatedBy": "api-patching",
"updatedById": 3,
"updatedByUserDirectoryId": 1,
"updatedByUserDirectoryName": "Local",
"devices": [
{
"id": 7,
"deviceId": 19,
"status": "waiting-for-approve",
"updateStatus": null,
"updateStatusDescription": null,
"currentVersion": "4.5.1",
"dataKey": "iabc1750304160282",
"requestId": 5,
"userName": "",
"password": "",
"manufacturerId": 8261,
"manufacturer": "Siemens",
"partNumber": "6ES7212-1BE40-0XB0",
"updateVersion": "4.5.2",
"updateFileName": "c2c4473c6e8cb61176603a945112021a.upd",
"nics": []
}
]
}
}

- Response, 401 - Unauthorized

JavascriptCopy{
"error": true,
"errors": [
{
"code": "NEM-3003-000201",
"message": "Unauthorized Common Gateway"
}
]
}JavascriptCopy{
"error": true,
"errors": [
{
"code": "NEM-3003-000404",
"message": "Site ip is invalid"
}
]
}
### [8. [Request Patching] Approve request](/docs/md-ot-security/v4.0.0/configuration/api-client#8-request-patching-approve-request)

| Title | [Request Patching] Approve request |
| --- | --- |
| URL Path | https://{IP of Enterprise Manager}:3003/neu-exposure/exposure-external/asset-main/exposure/v1/sensor/request-patching/approve |
| Method | PUT |
| Authentication method | Bearer Token |
| Request headers | - Bearer Token: retrieved after creating API-Client user (mandatory) - This API requires **Bearer Token Authentication**. You must include a valid Bearer token in the `Authorization` header. - Format: `Authorization: Bearer <token>` |
| Params | - **siteIp**:    - **Type**: `string`   - **Description**: The IP address of the site to fetch device data for.   - **Example**: `"10.40.172.144"` - **sensorIp**:    - **Type**: `string`   - **Description**: The IP address of the sensor associated with the site.   - **Example**: `"10.40.172.172"` - **data**:    - **Type**: `Object`   - **Description**:      - “id”: the id of the request patching   - **Example:**   - `{"id": 6}` |
| Response | Response, 200 OK Ex: |

JavascriptCopy{
"error": false,
"errors": [],
"data": {
"id": 6,
"type": "immediately",
"requestedAt": "2025-06-19T09:09:10.338Z",
"scheduleDate": "2025-06-19T09:09:10.269Z",
"scheduleTimeoutInMinutes": 1440,
"totalAsset": 1,
"status": "approved",
"approver": "api-patching",
"approverId": 3,
"approverUserDirectoryId": 1,
"approverUserDirectoryName": "Local",
"statusUpdatedAt": "2025-06-19T09:09:38.282Z",
"note": "test api client",
"isDeleted": false,
"requester": "api-patching",
"requesterId": 3,
"requesterUserDirectoryId": 1,
"requesterUserDirectoryName": "Local",
"updatedBy": "api-patching",
"updatedById": 3,
"updatedByUserDirectoryId": 1,
"updatedByUserDirectoryName": "Local",
"devices": [
{
"id": 8,
"deviceId": 19,
"status": "approved",
"updateStatus": "in-queue",
"updateStatusDescription": null,
"currentVersion": "4.5.1",
"dataKey": "iabc1750304160282",
"requestId": 6,
"userName": "",
"password": "",
"manufacturerId": 8261,
"manufacturer": "Siemens",
"partNumber": "6ES7212-1BE40-0XB0",
"updateVersion": "4.5.2",
"updateFileName": "c2c4473c6e8cb61176603a945112021a.upd",
"nics": []
}
]
}
}

- Response, 401 - Unauthorized

JavascriptCopy{
"error": true,
"errors": [
{
"code": "NEM-3003-000201",
"message": "Unauthorized Common Gateway"
}
]
}JavascriptCopy{
"error": true,
"errors": [
{
"code": "NEM-3003-000404",
"message": "Site ip is invalid"
}
]
}
### [9. [Request Patching] Reject request](/docs/md-ot-security/v4.0.0/configuration/api-client#9-request-patching-reject-request)

| Title | [Request Patching] Reject request |
| --- | --- |
| URL Path | https://{IP of Enterprise Manager}:3003/neu-exposure/exposure-external/asset-main/exposure/v1/sensor/request-patching/reject |
| Method | PUT |
| Authentication method | Bearer Token |
| Request headers | - Bearer Token: retrieved after creating API-Client user (mandatory) - This API requires **Bearer Token Authentication**. You must include a valid Bearer token in the `Authorization` header. - Format: `Authorization: Bearer <token>` |
| Params | - **siteIp**:    - **Type**: `string`   - **Description**: The IP address of the site to fetch device data for.   - **Example**: `"10.40.172.144"` - **sensorIp**:    - **Type**: `string`   - **Description**: The IP address of the sensor associated with the site.   - **Example**: `"10.40.172.172"` - **data**:    - **Type**: `Object`   - **Description**:      - “id”: the id of the request patching   - **Example:**   - `{"id": 5}` |
| Response | Response, 200 OK Ex: |

JavascriptCopy{
"error": false,
"errors": [],
"data": {
"id": 5,
"type": "immediately",
"requestedAt": "2025-06-19T09:00:55.792Z",
"scheduleDate": "2025-06-19T09:05:14.441Z",
"scheduleTimeoutInMinutes": 1440,
"totalAsset": 1,
"status": "rejected",
"approver": null,
"approverId": null,
"approverUserDirectoryId": null,
"approverUserDirectoryName": null,
"statusUpdatedAt": "2025-06-19T09:07:27.298Z",
"note": "test api client",
"isDeleted": false,
"requester": "api-patching",
"requesterId": 3,
"requesterUserDirectoryId": 1,
"requesterUserDirectoryName": null,
"updatedBy": "api-patching",
"updatedById": 3,
"updatedByUserDirectoryId": 1,
"updatedByUserDirectoryName": "Local",
"devices": [
{
"id": 7,
"deviceId": 19,
"status": "rejected",
"updateStatus": null,
"updateStatusDescription": null,
"currentVersion": "4.5.1",
"dataKey": "iabc1750304160282",
"requestId": 5,
"userName": "",
"password": "",
"manufacturerId": 8261,
"manufacturer": "Siemens",
"partNumber": "6ES7212-1BE40-0XB0",
"updateVersion": "4.5.2",
"updateFileName": "c2c4473c6e8cb61176603a945112021a.upd",
"nics": []
}
]
}
}

- Response, 401 - Unauthorized

JavascriptCopy{
"error": true,
"errors": [
{
"code": "NEM-3003-000201",
"message": "Unauthorized Common Gateway"
}
]
}JavascriptCopy{
"error": true,
"errors": [
{
"code": "NEM-3003-000404",
"message": "Site ip is invalid"
}
]
}
### [10. [Request Patching] Delete request](/docs/md-ot-security/v4.0.0/configuration/api-client#10-request-patching-delete-request)

| Title | [Request Patching] Delete request |
| --- | --- |
| URL Path | https://{IP of Enterprise Manager}:3003/neu-exposure/exposure-external/asset-main/exposure/v1/sensor/request-patching/item |
| Method | DELETE |
| Authentication method | Bearer Token |
| Request headers | - Bearer Token: retrieved after creating API-Client user (mandatory) - This API requires **Bearer Token Authentication**. You must include a valid Bearer token in the `Authorization` header. - Format: `Authorization: Bearer <token>` |
| Params | - **siteIp**:    - **Type**: `string`   - **Description**: The IP address of the site to fetch device data for.   - **Example**: `"10.40.172.144"` - **sensorIp**:    - **Type**: `string`   - **Description**: The IP address of the sensor associated with the site.   - **Example**: `"10.40.172.172"` - **data**:    - **Type**: `Object`   - **Description**:      - “id”: the id of the request patching   - **Example:**   - `{"id": 5}` |
| Response | Response, 200 OK Ex: |

JavascriptCopy{
"error": false,
"errors": [],
"data": {
"id": 5,
"type": "immediately",
"requestedAt": "2025-06-19T09:00:55.792Z",
"scheduleDate": "2025-06-19T09:05:14.441Z",
"scheduleTimeoutInMinutes": 1440,
"totalAsset": 1,
"status": "rejected",
"approver": null,
"approverId": null,
"approverUserDirectoryId": null,
"approverUserDirectoryName": null,
"statusUpdatedAt": "2025-06-19T09:08:21.800Z",
"note": "test api client",
"isDeleted": true,
"requester": "api-patching",
"requesterId": 3,
"requesterUserDirectoryId": 1,
"requesterUserDirectoryName": null,
"deletedAt": "2025-06-19T09:08:21.800Z",
"updatedBy": "api-patching",
"updatedById": 3,
"updatedByUserDirectoryId": 1,
"updatedByUserDirectoryName": "Local",
"devices": [
{
"id": 7,
"deviceId": 19,
"status": "deleted",
"updateStatus": null,
"updateStatusDescription": null,
"currentVersion": "4.5.1",
"dataKey": "iabc1750304160282",
"requestId": 5,
"userName": "",
"password": "",
"manufacturerId": 8261,
"manufacturer": "Siemens",
"partNumber": "6ES7212-1BE40-0XB0",
"updateVersion": "4.5.2",
"updateFileName": "c2c4473c6e8cb61176603a945112021a.upd",
"nics": []
}
]
}
}

- Response, 401 - Unauthorized

JavascriptCopy{
"error": true,
"errors": [
{
"code": "NEM-3003-000201",
"message": "Unauthorized Common Gateway"
}
]
}JavascriptCopy{
"error": true,
"errors": [
{
"code": "NEM-3003-000404",
"message": "Site ip is invalid"
}
]
}
