<!-- source: https://www.opswat.com/docs/cm/developer-guidelines/get-logs -->

# Get Logs

| API version | 3.3 |
| ---- | ---- |
| Last Update | 04/19/2023 |
| Authentication | YES |
| HTTP Method | POST |
| Content Type | application/json |
| Rate limited | YES |
| Requests per rate limit | 10/min |
| Response Format | JSON |
| Changes | Changes compared with v3.2 - add new filter *deleted_api* for filter.events |

My OPSWAT Central Management records events on your account. There are 3 types of event logs: admin event logs, device event logs, and webhook event logs. To retrieve event logs on your account, you can use this API. You can set filters in parameters to filter event logs you concern.

## API URL

`https://gears.opswat.com/o/api/v3.3/logs`

## Request Parameters

| Key | Datatype | Parameter Type | Required | Description | Default |
| ---- | ---- | ---- | ---- | ---- | ---- |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step |  |
| event_category | string | Body | Yes | Specify what event logs you want to retrieve. Possible values can be: - device: Device event logs - admin: Admin event logs - webhook: webhook's event logs - device_report: Device report event log |  |
| limit | int | Body | Optional | Specify a maximum number of event logs will be returned in the response. The value should be in [1,100]. If there are more event logs than what the limit asks for, HTTP code in a response will be 406. Event logs in the response are sorted by timestamp. | 20 |
| token | string | Body | Optional | Specify a pagination token that event logs will be returned in. It can be used to return the next set of items in the list. |  |
| age | int | Body | Optional | Specify age of the information in seconds. Maximum value is 86400 (1 day) For example: if you want to query event logs in last 5 minutes, you need set the "age" parameter to 300. | 3600 |
| start_time | long | Body | Optional | Specify a start time of the query's duration. The format should be Unix epoch time in milliseconds |  |
| end_time | long | Body | Optional | Specify an end time of the query's duration. The format should be Unix epoch time in milliseconds |  |
| filter | object | Body | Optional | Specify filter criteria (does not apply to device_report event_category) |  |
| filter.events | string | Body | Optional | Specify which events you want to retrieve. Values for admin event logs *(event_category = admin)* can be: - *cac_change*: an admin changed configuration for Secure Access module - *config*: an admin changed configuration - *failed_auth*: an admin failed authenticate with OPSWAT SSO. - *login*: an admin logged into MetaDefender IT Access console - *rev_mobile_code*: an admin revoked a registration code - *submit_ticket*: an admin summited a support ticket to OPSWAT through MetaDefender IT Access console - *whitelist*: an admin updated allowlist settings for CVEs - *changed_password*: an admin changed password with OPSWAT SSO Values for device event logs (event_category=*device)* can be: - *access_granted:* a device was granted temporary access to a protected app - *access_revoked:* a device was revoked a temporary access to a protected app - *added*: a device was enrolled to an account - *added_duplicate_mac:* a device was enrolled to an account with a duplicated MAC address. - *compliance_check:* an admin performed an on-demand compliance check on the device - *compliant*: a device was considered as COMPLIANT - *deleted*: a device was deleted by an admin - *deleted_user*: MetaDefender Endpoint was uninstalled by a local user on a device - *deleted_api*: a device was deleted via API - *exempt_all:* an admin exempted a device - *fetch_log:* an admin fetched the MetaDefender Endpoint's log remotely - *noncompliant*: a device was considered as NON-COMPLIANT - *scan_threat:* an admin requested an on-demand malware scan on a device - *unexempt:* an admin unexempted a device - *unseen*: a device was deleted by Lost Devices feature Values for category *webhook* can be: - *added*: a device was enrolled to an account - *deleted*: a device was deleted - *status_changed_to_compliant*: a device was considered as COMPLIANT - *status_changed_to_exempted:* a device was exempted - *status_changed_to_non_compliant*: a device was considered as NON-COMPLIANT |  |
| filter.agent_types | array<int> | Body | Optional | *Only valid for device event logs (event_category = device).* To filter event logs by an agent type. Values can be: - 0: MetaDefender Endpoint - 2: OPSWAT Domain Controller Client |  |
| filter.search | string | Body | Optional | Only valid for device event logs (event_category = device or event_category=device_report) or webhook event logs (event_category = *webhook)* Search by device name, device id. |  |

## Response HTTP Code

[this page](https://www.opswat.com/docs/cm/my-opswat-central-management/10.0.2506/developer-guidelines/apis)

## Response Parameters for admin event logs (event_category = admin):

| Key | DataType | Description |
| ---- | ---- | ---- |
| data | array<object> | Admin event logs |
| data.timestamp | string | timestamp when the event occurs |
| data.event | string | Event text |
| data.details | string | Event details |
| data.admin_name | string | Name of an admin who is related to the event |
| data.admin_email | string | Email of an admin who is related to the event |
| token | string | A pagination token |

## Response Parameters for Device event logs (event_category = device):

| Key | DataType | Description |
| ---- | ---- | ---- |
| data | array<object> | Device event logs |
| data.timestamp | string | timestamp when the event occurs |
| data.event | string | Event text |
| data.details | string | Event details |
| data.device_id | string | Device id of a device that the event occurred on |
| data.device_name | string | Device name that the event occurred on |
| data.device_username | string | User logged-in ID who logged into a device when the event occurred |
| data.device_group | string | A device's group name |
| token | string | A pagination token |

## Response Parameters for Device event logs (event_category = device_report):

| Key | DataType | Description |
| ---- | ---- | ---- |
| data | array<object> | Device event logs |
| data.timestamp | string | Timestamp when the event occurs |
| data.event | string | Event text |
| data.details | string | Event details |
| data.device_id | string | Device id of a device that the event occurred on |
| data.device_name | string | Device name that the event occurred on |
| data.device_username | string | User logged-in ID who logged into a device when the event occurred |
| data.device_group | string | A device's group name |
| data.status | string | Status of device |
| data.severity | string | Severity level |
| data.policy_name | string | Policy name which a device is assigned to |
| data.last_seen | string | The last timestamp in GMT format when the agent reports data to the Cloud |
| data.public_ip | string | Public IP of the device in the last report |
| token | string | A pagination token |

## Response Parameters for Webhook event logs (event_category = webhook):

| Key | DataType | Description |
| ---- | ---- | ---- |
| data | array<object> | Webhook event logs |
| data.timestamp | string | timestamp when the event log occurs |
| data.event | string | Event text |
| data.details | string | Event details |
| data.device_id | string | Device id of a device that the event occurred on |
| data.device_name | string | Device name that the event occurred on |
| data.response_code | string | Response code from a webhoook API |
| data.response_body | string | Response body from a webhoook API |
| token | string | A pagination token |

## Example

**Example Request**

```plaintext
https://gears.opswat.com/o/api/v3.3/logs?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
{
    "filter": {
		"events": []
	},
    "start_time": 1617662410591,
    "end_time": 1618267210591,
    "token":"59ed8afd62585c75b2d5b551"
    "limit" : 30,
	"event_category": "device_report"
}
```

**Example Response**

```plaintext
{
    "data": [
		{
			"timestamp": "2021-09-08T02:44:32Z",
			"event": "noncompliant",
			"details": "Changes status to NON-COMPLIANT. Device severity is warning in 1 consecutive data report(s)",
			"device_name": "WE10-D2739",
			"device_id": "683Z9P2",
			"device_username": "admin",
			"device_group": "Default",
			"status": "non_compliant",
			"severity": "warning",
			"policy_name": "Default",
			"last_seen": "2021-09-08T02:44:32Z",
			"public_ip": "203.205.57.108"
		}
	],
    "token": "60ed8afd62585c75b2d5b551"
}
```

**Example Request**

```plaintext
https://gears.opswat.com/o/api/v3.3/logs?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
{
    "filter": {
		"events": ["added","added_duplicate_mac","compliance_check","compliant","deleted","deleted_user","deleted_api"]
	},
    "start_time": 1617662410591,
    "end_time": 1618267210591,
    "limit" : 30,
	"event_category": "device"
}
```

**Example Response**

```plaintext
{
    "data": [
          {
              "timestamp": "2021-04-12T07:58:57Z",
			   "event": "noncompliant",
              "details": "Changes status to NON-COMPLIANT. A policy this device is assigned to was changed as a result of an admin action or an API call",
              "device_name": "WET9-D3S89",
              "device_id": "Rose0403202001",
              "device_username": "test",
              "device_group": "Default"
          },
          {
              "timestamp": "2021-04-12T07:58:57Z",
			  "event": "compliant",
              "details": "Changes status to COMPLIANT. A policy this device is assigned to was changed as a result of an admin action or an API call",
              "device_name": "TD10-C6828",
              "device_id": "mac100701",
              "device_username": "test",
			  "device_group": "Default"
          },
          {
              "timestamp": "2023-04-12T08:00:31Z",
              "event": "deleted_api",
              "details": "Was deleted by admin N/A (admin@opswat.com) via API",
              "device_name": "347547593954a61fe71365",
              "device_id": "Linux1658803392",
              "device_username": "ssssss",
              "device_group": "Default"
          }
    ],
    "token": "60ed8afd62585c75b2d5b551"
}
```

**Example Request**

```plaintext
https://gears.opswat.com/o/api/v3.3/logs?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
{
    "start_time": 1617662410591,
    "end_time": 1618267210591,
    "limit" : 30,
    "token": "60ed8afd62585c75b2d5b551",
	  "event_category": "admin"
}
```

**Example Response**

```plaintext
{
    "data": [
            {
                "timestamp": "2021-04-12T20:01:52Z",
                "details": "Admin (admin@opswat.com) updated the policy ANTC - Laptops/Desktops - Device Compliance - Custom Check - Windows",
                "event": "Settings Change",
                "admin_name": "Admin",
                "admin_email": "admin@opswat.com"
            },
            {
                "timestamp": "2021-04-12T09:28:29Z",
                "details": "Admin logged On",
                "event": "Logged On",
                "admin_name": "Admin",
                "admin_email": "admin@opswat.com"
            },
            {
                "timestamp": "2022-03-16T06:19:51Z",
                "event": "Admin Changed Password",
                "details": "Administrator admin (admin@opswat.com) changed password",
                "admin_name": "admin",
                "admin_email": "admin@opswat.com"
            }
    ],
    "token": "60ed8afd62585c75b2d5b551"
}
```

**Example Request**

```plaintext
https://gears.opswat.com/o/api/v3.3/logs?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
{
    "start_time": 1617662410591,
    "end_time": 1618267210591,
    "token": "60ed8afd62585c75b2d5b551",
    "limit" : 30,
	"event_category": "webhook"
}
```

**Example Response**

```plaintext
{
    "data": [
            {
                "timestamp": "2021-04-07T06:51:46Z",
				"event": "status_changed_to_non_compliant",
                "details": "Changed status to non-compliant (retry 1)",
                "device_name": "WET9-D3S89",
                "response_code": "405",
                "response_body": "",
                "device_id": "Rose0403202001"
            },
            {
                "timestamp": "2021-04-07T06:51:42Z",
				"event": "status_changed_to_non_compliant",
                "details": "Changed status to non-compliant",
                "device_name": "WET9-D3S89",
                "response_code": "405",
                "response_body": "",
                "device_id": "Rose0403202001"
            }
    ],
    "token": "60ed8afd62585c75b2d5b551"
}
```

## History

| Version | URL |
| ---- | ---- |
| v3.2 | [Get Logs v3.2](https://www.opswat.com/docs/macloud-sdp/developer-guide/get-logs-v3-2) |
| v3.1 | [Get Logs v3.1](https://www.opswat.com/docs/macloud-sdp/developer-guide/get-logs-v3-1) |
| v3.0 | [Get Logs v3.0](https://www.opswat.com/docs/macloud-sdp/developer-guide/get-logs-v3-0) |
| v2.0 | [Get Logs v2.0](https://www.opswat.com/docs/macloud-sdp/developer-guide/get-logs-v2-0) |
