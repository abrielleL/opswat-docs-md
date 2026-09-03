<!-- source: https://www.opswat.com/docs/cm/developer-guidelines/get-devices-v3-6 -->

# Get Devices v3.6

| API version | 3.6 |
| ---- | ---- |
| Last Update | 09/28/2023 |
| Authentication | YES |
| HTTP Method | POST |
| Content Type | application/json |
| Rate limited | YES |
| Requests per rate limit | 10/min |
| Response Format | JSON |
| Changes | Changes compare with v3.5 - Added *host_name* field into the API response. |

Receiving devices in the cursor fashion, with ascending order of enrolling time.

## API URL

```plaintext
https://gears.opswat.com/o/api/v3.6/devices
```

## Request Parameters

| Key | Datatype | Parameter Type | Required | Description | Default |
| ---- | ---- | ---- | ---- | ---- | ---- |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step |  |
| token | string | Body | Optional | Specify a pagination token that devices will be returned in. It can be used to return the next set of items in the list. **Return the oldest items in case the token is missing.** |  |
| limit | int | Body | Optional | Specify maximum number of devices will be returned in the response. The value should be in [1,50]. | 20 |

Notes:

- criteria in a same parameter will be combined with OR operator
- criteria in different parameter will be combined with AND operator

## Response HTTP Code

See [APIs](https://www.opswat.com/docs/macloud-sdp/3.54.0/developer-guide/apis)

## Response Parameters

| Key | DataType | Description |
| ---- | ---- | ---- |
| next_token | string | A pagination token. |
| devices | Array Object | The returned devices. |
| devices.device_id | string | HWID of a device |
| devices.severity | string | Issue severity of the device Values can be: "critical", "warning", "no_issues" |
| devices.enrolled_at | string | Timestamp in GMT format when a device enrolled to an account |
| devices.status | string | device status Values can be: "compliant", "non_compliant", "exempted", "out_of_license_usage", "unknown", "ignored", "installed", "pending", "quarantined" |
| devices.device_name | string | device name |
| devices.host_name | string | hostname |
| devices.nickname | string | device nickname (editable on the cloud console) |
| devices.device_type | string | device type Values can be "desktop","laptop","phone","tablet","server","vm" |
| devices.last_seen | string | The last timestamp in GMT format when an agent reports its data to Cloud |
| devices.last_reboot | string | The last timestamp in GMT format when the device reboots |
| devices.agent_version | string | agent version |
| devices.remediation_link | string | URL of remediation page for the given device |
| devices.group_name | string | Group name which a device is assigned to |
| devices.issue | object | Summary of issues a device has |
| devices.issue.total_issue | int | number of issues a device has |
| devices.issue.total_critical | int | number of critical issues a device has |
| devices.issue.total_warning | int | number of warning issues a device has |
| devices.geo_info | object | Location details of the device where the device was in the last report |
| devices.geo_info.country | string | country of the device where the device was in the last report |
| devices.network_info | array<object> | Network adapter information block |
| devices.network_info.mac | string | MAC address of a network adapter |
| devices.network_info.ipv4 | string | IPV4 address of a network adapter |
| devices.os_info | array<object> | Operation system block |
| devices.os_info.family | string | OS family |
| devices.os_info.name | string | OS name |
| devices.os_info.vendor | string | OS vendor |
| devices.os_info.version | string | OS version |
| devices.os_info.type | string | OS type. Values can be: "windows","mac", "linux", "ios", "android" |
| devices.cves | object | Summary of CVEs a device has |
| devices.cves.total | int | Total number of CVEs in device |
| devices.link_user | object | Linked user details |
| devices.link_user.username | string | Username |
| devices.link_user.group | string | group which the user is associated to |
| devices.user_info | object | User information block |
| devices.user_info.username | string | Currently logged in username |
| devices.user_info.domain | string | Currently logged in user domain |
| device.in___grace_period | int | Grace-period status of the device: - 0: Device is not in grace period - 1: Device is in grace period |

## Example

**Example Request**

```plaintext
https://gears.opswat.com/o/api/v3.5/devices?access_token=YOUR_ACCESS_TOKEN
{
    "token": "62bd0dea3f05657d0e8a0cc2",
    "limit": 20
}
```

## Example Response

```plaintext
{
    "next_token": "610a47f4667e833f918e48bf",
    "devices": [
    {
          "device_id": "839219d384a64dc6c93954a61fe74648",
          "severity": "critical",
          "status": "non_compliant",
          "device_name": "WE10-D2739",
          "host_name": "WE10-D2739",
          "nickname": "WE10-D2739",
          "device_type": "desktop",
          "last_seen": "2022-07-05T10:24:10Z",
          "agent_version": "7.6.478.0",
          "remediation_link": "https://metaaccess-testing.opswat.com/remediation/0051a0000026otR/839219d384a64dc6c93954a61fe74648/EF1C5DDC78F3207F93E052DE7D4BDA7108072210",
          "group_name": "Default",
          "geo_info": {
            "country": "Unknown"
          },
          "network_info": [
            {
              "mac": "8c:ec:4b:62:75:20",
              "ipv4": "10.40.50.42"
            },
            {
              "mac": "0a:00:27:00:00:16",
              "ipv4": "192.168.77.2"
            },
            {
              "mac": "0a:00:27:00:00:11",
              "ipv4": "192.168.56.1"
            },
            {
              "mac": "00:50:56:c0:00:08",
              "ipv4": "192.168.19.1"
            },
            {
              "mac": "00:50:56:c0:00:01",
              "ipv4": "192.168.145.1"
            },
            {
              "mac": "00:ff:dd:c9:df:02",
              "ipv4": "N/A"
            },
            {
              "mac": "5c:ea:1d:bc:09:ad",
              "ipv4": "N/A"
            }
          ],
          "os_info": {
            "family": "Windows",
            "name": "Microsoft Windows 10 Enterprise",
            "vendor": "Microsoft Corp.",
            "version": "10.0.19044",
            "type": "windows"
          },
          "link_user": {
            "username": "",
            "group": ""
          },
          "user_info": {
            "username": "tuoi.dinh",
            "domain": "us.opswat.com"
          },
          "issue": {
            "total_issue": 4,
            "total_critical": 2,
            "total_warning": 2
          },
          "last_reboot": "2022-06-27T02:05:00Z",
          "cves": {
            "total": 559
          },
          "enrolled_at": "2022-07-04T04:46:48Z"
        }
    ]
}
```

## History

| Version | URL |
| ---- | ---- |
| v3.5 | [Get Devices v3.5](https://www.opswat.com/docs/cm/developer-guidelines/get-devices-v3-5) |
| v3.3 | [Get Devices v3.3](https://www.opswat.com/docs/cm/developer-guidelines/get-devices-v3-3) |
| v3.2 | [Get Devices v3.2](https://www.opswat.com/docs/cm/developer-guidelines/get-devices-v3-2) |
| v3.1 | [Get Devices v3.1](https://www.opswat.com/docs/cm/developer-guidelines/get-devices-v3-1) |
| v3.0 | [Get Devices v3.0](https://www.opswat.com/docs/cm/developer-guidelines/get-devices-v3-0) |
| v2.3 | [Get Devices v2.3](https://www.opswat.com/docs/cm/developer-guidelines/get-devices-v2-3) |
| v2.2 | [Get Devices v2.2](https://www.opswat.com/docs/cm/developer-guidelines/get-devices-v2-2) |
| v2.1 | [Get Devices v2.1](https://www.opswat.com/docs/cm/developer-guidelines/get-devices-v2-1) |
| v2.1 | [Search Devices v2.1](https://www.opswat.com/docs/cm/developer-guidelines/search-devices-v2-1) |
