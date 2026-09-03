<!-- source: https://www.opswat.com/docs/cm/developer-guidelines/get-logs-v3-1 -->

# Get Logs v3.1

| API version | 3.1 |
| ---- | ---- |
| Last Update | 04/21/2021 |
| Authentication | YES |
| HTTP Method | POST |
| Content Type | application/json |
| Rate limited | YES |
| Requests per rate limit | 10/min |
| Response Format | JSON |

MetaAccess records events on your account. There are 3 types of event logs: admin event logs, device event logs, and webhook event logs. To retrieve event logs on your account, you can use this API. You can set filters in parameters to filter event logs you concern.

## API URL

```plaintext
https://gears.opswat.com/o/api/v3.1/logs
```

## Request Parameters

| Key | Datatype | Parameter Type | Required | Description | Default |
| ---- | ---- | ---- | ---- | ---- | ---- |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step |  |
| event_category | string | Body | Yes | Specify what event logs you want to retrieve. Possible values can be: - device: Device event logs - admin: Admin event logs - webhook: webhook's event logs |  |
| limit | int | Body | Optional | Specify a maximum number of event logs will be returned in the response. The value should be in [1,50]. If there are more event logs than what the limit asks for, HTTP code in a response will be 406. Event logs in the response are sorted by timestamp. | 20 |
| page | int | Body | Optional | Specify a page number that event logs will be returned in. If the requested page exceeds the number of pages of event logs, HTTP code in a response will be 413. It means that the requested page number is too large, no event logs will be returned. | 1 |
| start_time | long | Body | Optional | Specify a start time of the query's duration. The format should be Unix epoch time in milliseconds |  |
| end_time | long | Body | Optional | Specify an end time of the query's duration. The format should be Unix epoch time in milliseconds |  |
| age | int | Body | Optional | Specify age of the information in seconds. Maximum value is 86400 (1 day) For example: if you want to query event logs in last 5 minutes, you need set the "age" parameter to 300. |  |
| filter | object | Body | Optional | Specify filter criteria |  |
| filter.events | string | Body | Optional | Specify which events you want to retrieve. Values for admin event logs *(event_category = admin)* can be: - *cac_change*: an admin changed configuration for Secure Access module - *config*: an admin changed configuration - *failed_auth*: an admin failed authenticate with OPSWAT SSO. - *login*: an admin logged into MetaAccess console - *rev_mobile_code*: an admin revoked a registration code - *submit_ticket*: an admin summited a support ticket to OPSWAT through MetaAccess console - *whitelist*: an admin updated allowlist settings for CVEs Values for device event logs (event_category=*device)* can be: - *access_granted:* a device was granted temporary access to a protected app - *access_revoked:* a device was revoked a temporary access to a protected app - *added*: a device was enrolled to an account - *added_duplicate_mac:* a device was enrolled to an account with a duplicated MAC address. - *compliance_check:* an admin performed an on-demand compliance check on the device - *compliant*: a device was considered as COMPLIANT - *deleted*: a device was deleted by an admin - *deleted_user*: OPSWAT Client was uninstalled by a local user on a device - *exempt_all:* an admin exempted a device - *fetch_log:* an admin fetched the OPSWAT Client's log remotely - *noncompliant*: a device was considered as NON-COMPLIANT - *scan_threat:* an admin requested an on-demand malware scan on a device - *unexempt:* an admin unexempted a device - *unseen*: a device was deleted by Lost Devices feature Values for category *webhook* can be: - *added* : a device was enrolled to an account - *deleted* : a device was deleted - *status_changed_to_compliant*: a device was considered as COMPLIANT - *status_changed_to_exempted:* a device was exempted - *status_changed_to_non_compliant*: a device was considered as NON-COMPLIANT |  |
| filter.agent_types | array<int> | Body | Optional | *Only valid for device event logs (event_category = device).* To filter event logs by an agent type. Values can be: - 0: OPSWAT Client - 2: OPSWAT Domain Controller Client |  |
| filter.search | string | Body | Optional | Only valid for device event logs (event_category = device) or webhook event logs (event_category = *webhook)* Search by device name, device id. |  |

## Response HTTP Code

See [APIs](https://www.opswat.com/docs/macloud-sdp/3.54.0/developer-guide/apis)

## Response Parameters for admin event logs (event_category = admin):

| Key | DataType | Description |
| ---- | ---- | ---- |
| timestamp | string | timestamp when the event occurs |
| event | string | Event text |
| details | string | Event details |
| admin_name | string | Name of an admin who is related to the event |
| admin_email | string | Email of an admin who is related to the event |

## Response Parameters for Device event logs (event_category = device):

| Key | DataType | Description |
| ---- | ---- | ---- |
| timestamp | string | timestamp when the event occurs |
| event | string | Event text |
| details | string | Event details |
| device_id | string | Device id of a device that the event occurred on |
| device_name | string | Device name that the event occurred on |
| device_username | string | User logged-in ID who logged into a device when the event occurred |
| device_group | string | A device's group name |

## Response Parameters for Webhook event logs (event_category = webhook):

| Key | DataType | Description |
| ---- | ---- | ---- |
| timestamp | string | timestamp when the event log occurs |
| event | string | Event text |
| details | string | Event details |
| device_id | string | Device id of a device that the event occurred on |
| device_name | string | Device name that the event occurred on |
| response_code | string | Response code from a webhoook API |
| response_body | string | Response body from a webhoook API |

## Example

**Example Request**

```plaintext
https://gears.opswat.com/o/api/v3.1/logs?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
{
    "filter": {
		events: ["added","added_duplicate_mac","compliance_check","compliant","deleted","deleted_user"]
	},
    "start_time": 1617662410591,
    "end_time": 1618267210591,
    "page": 1,
    "limit" : 30,
	"event_category": "device"
}
```

**Example Response**

```plaintext
{
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
    }
}
```

**Example Request**

```plaintext
https://gears.opswat.com/o/api/v3.1/logs?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
{
    "start_time": 1617662410591,
    "end_time": 1618267210591,
    "page": 1,
    "limit" : 30,
	"event_category": "admin"
}
```

**Example Response**

```plaintext
{
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
    }
}
```

**Example Request**

```plaintext
https://gears.opswat.com/o/api/v3.1/logs?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
{
    "start_time": 1617662410591,
    "end_time": 1618267210591,
    "page": 1,
    "limit" : 30,
	"event_category": "webhook"
}
```

**Example Response**

```plaintext
{
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
}
```

## History

| Version | URL |
| ---- | ---- |
| v3.0 | [Get Logs v3.0](https://www.opswat.com/docs/cm/developer-guidelines/get-logs-v3-0) |
| v2.0 | [Get Logs v2.0](https://www.opswat.com/docs/cm/developer-guidelines/get-logs-v2-0) |
