<!-- source: https://www.opswat.com/docs/cm/developer-guidelines/get-pmp-reports -->

# Get PMP Reports

| API version | 1.0 |
| ---- | ---- |
| Last Update | 06/17/2025 |
| Authentication | YES |
| HTTP Method | POST |
| Content Type | application/json |
| Rate limited | YES |
| Requests per rate limit | 10/min |
| Response Format | JSON |

Retrieve reports of PMP devices - including MetaDefender Kiosk, MetaDefender Endpoint - in the cursor fashion, sorted by reported time in ascending order.

## API URL

```plaintext
https://product.my.us.opswat.com/o/pmp/v1/reports
```

## Request Parameters

| Key | Datatype | Parameter Type | Required | Description | Default |
| ---- | ---- | ---- | ---- | ---- | ---- |
| Authorization | string | Header | Yes | Bearer token for Authentication Authorization: Bearer ACCESS_TOKEN |  |
| token | string | Body | Optional | Specify a pagination token that devices will be returned in. It can be used to return the next set of items in the list. **Return the oldest items in case the token is missing.** |  |
| limit | int | Body | Optional | Specify maximum number of devices will be returned in the response. The value should be in [1,100]. | 20 |
| start_time | long | Body | Yes | Specify a start time of the query's duration. The format should be Unix epoch time in milliseconds The value must be greater than zero, and it must not be more than 30 days from the current date. |  |
| end_time | long | Body | Optional | Specify an end time of the query's duration. The format should be Unix epoch time in milliseconds |  |
| filter | object | Body | Optional | Specify filter criteria |  |
| filter.device_type | array<string> | Body | Optional | Specify what device type used to filter along with the field. Value: - EM - KIOSK - MK5 |  |
| filter.media_type | array<string> | Body | Optional | Specify what media type used to filter along with the field. |  |
| filter.issue_type | array<string> | Body | Optional | Specify what issue type used to filter along with the field. Value: - VUL: report with vulnerability - COO: report with coo detection - SENSITIVE: report with sensitive files - SKIPPED: report with skipped files - INFECTED: report with infected files |  |

Notes:

- criteria in a same parameter will be combined with OR operator
- criteria in different parameter will be combined with AND operator

## Response HTTP Code

See details in the Response HTTP Code section in [this page](https://www.opswat.com/docs/cm/developer-guidelines/apis)

## Response Parameters

| Key | DataType | Description |
| ---- | ---- | ---- |
| token | string | A pagination token. |
| data | Array Object | The returned reports. |
| data.timestamp | long | timestamp when the report occurs |
| data.sync_time | long | timestamp when the report sent to My Opswat Central Management |
| data.session_id | string | session id of the report |
| data.report_id | string | report id of the report |
| data.user_name | string | User logged-in ID who logged into a device when the report occurred |
| data.device_name | string | Device name that the report occurred on |
| data.device_id | string | Device id of a device that the report occurred on |
| data.device_type | string | Device type of a device that the event occurred on |
| data.device_group | string | A device's group name |
| data.media_type | string | media type |
| data.total_infected | int | total infected files in the report |
| data.total_vulnerability | int | total vulnerable files in the report |
| data.total_sensitive | int | total sensitive files in the report |
| data.total_coo | int | total coo detection files in the report |
| data.total_skipped | int | total skipped files in the report |
| data.total_files_scanned | int | total scanned files in the report |
| data.total_sanitized | int | total sanitized files in the report |
| data.total_threat | int | total issued files in the report |

## Example

**Example Request**

```plaintext
https://product.my.us.opswat.com/o/pmp/v1/reports
Content-Type: application/json
Authorization: Bearer ACCESS_TOKEN

{
    "filter": {
			"device_type": ["KIOSK"],
			"media_type" : ["USB Device"],
			"issue_type" : ["VUL", "COO", "SENSITIVE", "SKIPPED", "INFECTED"]
		},
    "start_time": 1617662410591,
    "end_time": 1618267210591,
    "limit" : 1,
		"token": "60ed8afd62585c75b2d5b551"
}
```

## Example Response

```plaintext
{
	"data": [
		{
			"timestamp": 1712161663000,
      "sync_time": 1747381075000,
			"session_id": "phuoc123456789x",
			"report_id": "phuoc123456789x",
			"user_name": "Guest",
			"device_name": "phuockiosk",
			"device_id": "phuockiosk",
			"device_type": "KIOSK",
			"device_group": "Default Kiosk Windows",
			"media_type": "SCSI Device",
			"total_infected": 1,
			"total_vulnerability": 0,
			"total_sensitive": 4,
			"total_coo": 0,
			"total_skipped": 0,
			"total_files_scanned": 14,
			"total_sanitized": 4,
			"total_threat": 5
		}
	],
	"token": "60ed8afd62585c75b2d5b551"
}
```
