<!-- source: https://www.opswat.com/docs/cm/developer-guidelines/device-policy-check -->

# Device Policy Check

| API version | 2.2 |
| ---- | ---- |
| Last Update | 05/28/2015 |
| Authentication | YES |
| Response Format | JSON |
| HTTP Method | GET |
| Rate limited | YES |
| Requests per rate limit | 10/min |

Use to fetch compliance status of a given device

## API URL

```plaintext
https://gears.opswat.com/o/api/v2.2/devices/:value/policy_check
```

## Request Parameters

| Key | Datatype | Parameter Type | Required | Description | Default |
| ---- | ---- | ---- | ---- | ---- | ---- |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step |  |
| verbose | int | URL | Optional | 1 - extra detailed information will return in response 0 - response does not include detailed information | 0 |
| opt | int | URL | Optional | **0 -** MAC address **1** - HWID **3** - SSID | 0 |

## Response HTTP Code

| HTTP Code | Description |
| ---- | ---- |
| 200 | Success |
| 401 | Unauthorized. Your access_token is invalid or expired |
| 404 | Not found |

## Response Parameters

| Key | Datatype | Description |
| ---- | ---- | ---- |
| policy_name | string | (Not available, reserved for future) policy name in Policy manager |
| user | string | (Not available, reserved for future) user in Policy manager. |
| location | string | (Not available, reserved for future) location in Policy manager. |
| device_type | string | device type (laptop, desktop, vm, server, phone) of device. |
| os_type | string | operating system type |
| status | int | Device status. This status is based on the defined policy within My OPSWAT Central Management. Status values are: - **0** – the endpoint is in compliance with My OPSWAT Central Management account’s policies - **1** – the endpoint is **not** in compliance with My OPSWAT Central Management account’s policies - **2** – the endpoint is not found, it means that the endpoint does not have the My OPSWAT Central Management installed - **3** – the endpoint is still sending information to My OPSWAT Central Management and not yet completed |
| total_issue | int | Number of issues were seen on the device |
| total_critical_issue | int | Number of critical issues were seen on the device |
| critical_status | int | This critical status is based on the defined policy within My OPSWAT Central Management. This status apply for the whole device. Critical status values are: - **0** – the endpoint doesn't have critical issues - **1** – the endpoint has critical issues |
| last_seen | string | timestamp of the last time when the endpoint device sent a health report to the server. |
| issues | array<object> | Lists any/all issues of given endpoint device. If a device is without issue, the issues array will appear blank (as shown in the example below). For those devices with issues, each issue will be listed out within *issue_text* (as shown in the example below). |
| issues.<category_group> | array<object> | issues found in a category group on the device |
| issues.<category_group>.category | string | category name |
| issues.<category_group>.issues | array<string> | issue descriptions |
| remediation | string | (Not available, reserved for future) remediation, in Policy manager |
| remediation_link | string | URL on remediation page for given device |
| notification | string | (Not available, reserved for future) notification can be no notification with just background log/notification using sms/notification using email, in Policy manager |
| infections | arrays<object> | Infection details |
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
| infections.threats.link | string | a URL to view scan details on [Metadefender Cloud](http://metadefender.com/) |
| infections.threats.ip_address | string | IP which a device connecting to |
| infections.threats.status | string | indicates the scanning object is clear, dirty or in-progress |
| infections.threats.details | array<object> | details of IP connections |
| infections.threats.details.source_name | string | Source of the feed, usually the domain where the feed is from (e.g., [example.com](http://example.com)) |
| infections.threats.details.assessment | string | Type of threat detected |
| infections.threats.details.confident | string | Represents the reliability of the detection based on several factors. The higher the score, the more reliable the result. |
| infections.threats.geo_info | object | An object represents the geolocation of address |
| infections.threats.geo_info.city | string | Country name of the network address (e.g., Brazil) |
| infections.threats.geo_info.country_name | string | Country name of the network address (e.g., BR) |
| infections.threats.geo_info.country_code | string | Region name of the network address (e.g., San Paulo) |
| infections.threats.geo_info.region_name | string | Region code of the network address (e.g., 27) |
| infections.threats.geo_info.region_code | string | City name of the network address (e.g., San Paulo) |
| infections.last_scan_time | string | The timestamp in GMT format when the agent did a scan |
| infections.total_engines | int | number of engines scanned a file |
| infections.total_sources | int | number of source of the feed |
| infections.last_report | string | the timestamp in GMT format when agent reported threat log from local anti-malware products |

## Example

**Example Request (verbose = 0)**

```plaintext
https://gears.opswat.com/o/api/v2.2/devices/TEST-59EHS/policy_check?opt=1&access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
```

**Example Response **(verbose = 0)

```plaintext
{
	"status": 0,
	"last_seen ": "2013-12-04T08:00:00Z",
	"total_issue": 0 "critical_status": 0,
	"total_critical_issue": 0,
	"critical_status": 0
}
```

**Example Request **(verbose = 1)

```plaintext
https://gears.opswat.com/o/api/v2.2/devices/TEST-59EHS/policy_check?verbose=1&opt=1&access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
```

**Example Response for Wins/macOS devices **(verbose = 1)

```plaintext
{
  "last_seen": "2017-03-22T02:36:00Z",
  "policy_name": "",
  "device_type": "laptop",
  "critical_status": 1,
  "remediation_link": "https://gears-beta.opswat.com/console/remediation/b62ba487df821d8a5194136f99da1cca/Vy43/004VAyA4L3Y/remediation.html",
  "issues": [
    {
      "protection": [
        {
          "category": "3rd Party Patch Mgmt.",
          "issues": [
            "No product detected"
          ]
        },
        {
          "category": "Antivirus",
          "issues": [
            "The last full system scan was more than 7 day(s) ago"
          ]
        },
        {
          "category": "Firewall",
          "issues": [
            "Not enabled"
          ]
        },
        {
          "category": "Firewall",
          "issues": [
            "Not enabled"
          ]
        }
      ]
    },
    {
      "system": [
        {
          "category": "Hard Drive",
          "issues": [
            "Hard drive has 2% free (4.24 GB)"
          ]
        }
      ]
    },
    {
      "threat": [
        {
          "category": "Advanced Threats",
          "issues": [
            "Advanced threats detected"
          ]
        }
      ]
    }
  ],
  "agent_type": 0,
  "remediation": "",
  "notification": "",
  "total_issue": 6,
  "total_critical_issue": 4,
  "os_type": "Windows 7 Enterprise",
  "infections": [
    {
      "category": "malware_scan",
      "last_scan_time": "2016-08-05T08:58:56Z",
      "total_engines": 14,
      "total_threats": 5,
      "threats": [
        {
          "ThreatName": "Trojan.Win32.Heur.Gen",
          "File": "c:\\program files\\avast software\\avast\\avastsvc.exe",
          "FoundTime": "2016-07-04T00:11:12Z",
          "hash": "98F2F312F273C52653DC72F8A69ACBD79F588FF1B53CC7DFA85C26B6F7EF620B",
          "link": "https://www.metadefender.com/#!/results/file/98F2F312F273C52653DC72F8A69ACBD79F588FF1B53CC7DFA85C26B6F7EF620B/hash"
        }
      ],
      "has_issue": 1,
      "critical_issue": 1,
      "has_critical_issue": 1
    },
    {
      "category": "repeated_threats",
      "last_report": "2017-03-22T02:36:42Z",
      "threats": [
        {
          "threat_name": "Suspicious.Cloud.5",
          "file": "C:\\ProgramData\\Symantec\\Symantec Endpoint Protection\\12.1.4013.4013.105\\SRTSP\\Quarantine\\APQ629A.tmp",
          "found_time": "2017-03-20T10:37:48Z",
          "engine_name": "Symantec Endpoint Protection",
          "times_detected": 3,
          "action": "deleted"
        }
      ],
      "total_threats": 1,
      "has_issue": 1,
      "critical_issue": 1,
      "has_critical_issue": 1
    }
  ],
  "location": "",
  "status": 1
}
```

**Example Response for iOS/Android devices **(verbose = 1)

```plaintext
{
  "last_seen": "2017-03-22T02:25:38Z",
  "policy_name": "",
  "device_type": "phone",
  "critical_status": 1,
  "remediation_link": "https://gears-beta.opswat.com/console/remediation/b62ba487df821d8a5194136f99da1cca/76BfVPhEbDDTFhMm3Q2MwtoAPVJcLMAw/0327Z6UBTfZV4P3hAELbED2DDT7FThFMHm93JQS25MPwLtHoNA6P3VSJEcEL8MRAGwK/remediation.html",
  "issues": [
    {
      "system": [
        {
          "category": "Security & Health",
          "issues": [
            "Device's operating system does not meet minimum version",
            "Screen lock and passcode are disabled"
          ]
        }
      ]
    }
  ],
  "agent_type": 1,
  "remediation": "",
  "notification": "",
  "total_issue": 2,
  "total_critical_issue": 1,
  "os_type": "android",
  "infections": [
    {
      "category": "ip_scan",
      "critical_issue": 0,
      "total_threats": 1,
      "has_issue": 1,
      "threats": [
        {
          "ip_address": "104.238.102.226",
          "status": "dirty",
          "details": [
            {
              "source_name": "MalwareDomainList",
              "assessment": "malware",
              "confident": "40"
            }
          ],
          "geo_info": {
            "city": "",
            "country_name": "Canada",
            "country_code": "CA",
            "region_name": "",
            "region_code": ""
          }
        }
      ],
      "last_scan_time": "",
      "has_critical_issue": 0,
      "total_sources": 12
    }
  ],
  "location": "",
  "user": "",
  "status": 1
}
```

## History

| Version | URL |
| ---- | ---- |
| 2.0 | [Device Policy Check v2.0](https://www.opswat.com/docs/macloud-sdp/developer-guide/device-policy-check-v2-0) |
