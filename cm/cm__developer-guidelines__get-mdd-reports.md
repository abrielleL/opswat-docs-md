<!-- source: https://www.opswat.com/docs/cm/developer-guidelines/get-mdd-reports -->

# Get MetaDefender Drive Reports

| API version | 1.0 |
| ---- | ---- |
| Last Update | 06/17/2025 |
| Authentication | YES |
| HTTP Method | POST |
| Content Type | application/json |
| Rate limited | YES |
| Requests per rate limit | 10/min |
| Response Format | JSON |

Receive MetaDefender Drive's reports in the cursor fashion, sorted by reported time in ascending order..

## API URL

```plaintext
https://product.my.us.opswat.com/o/mdd/v1/reports
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
| filter.scanned_host | array<string> | Body | Optional |  |  |
| filter.scanned_by | array<string> | Body | Optional |  |  |
| filter.issue_type | array<string> | Body | Optional | Specify what issue type used to filter along with the field. Value: - VUL: report with vulnerability - COO: report with coo detection - SENSITIVE: report with sensitive files - SKIPPED: report with skipped files - INFECTED: report with infected files |  |

Notes:

- criteria in a same parameter will be combined with OR operator
- criteria in different parameter will be combined with AND operator

## Response HTTP Code

See details in the Response HTTP Code section in [APIs](https://www.opswat.com/docs/cm/developer-guidelines/apis) guidelines.

## Response Parameters

| Key | DataType | Description |
| ---- | ---- | ---- |
| token | string | A pagination token. |
| data | Array Object | The returned reports. |
| data.timestamp | long | timestamp when the report occurs |
| data.sync_time | long | timestamp when the report sent to My Opswat Central Management |
| data.session_id | string | session id of the report |
| data.hardware_model | string | hardware model of a device that the report occurred on |
| data.scan_profile | string | scanning profile |
| data.scanned_host | string |  |
| data.scanned_by | string |  |
| data.device_group | string | A device's group name |
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
https://product.my.us.opswat.com/o/mdd/v1/reports
Content-Type: application/json
Authorization: Bearer ACCESS_TOKEN

{
    "filter": {
			"scanned_host": [ "qa-machine"],
      "scanned_by": ["MSCLyAWEbU6qKF8ULBXwKmj60WBvJsbnnByS"],
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
			"timestamp": 1746618097000,
      "sync_time": 1746618097000,
			"session_id": "qa-virtual-machine__CustomScan_07-May-2025_11-41-37.json.gz",
			"device_group": "Default Drivea",
			"hardware_model": " VMware, VMware Virtual Platform",
			"scan_profile": "Custom Scan",
			"scanned_host": "qa-virtual-machine",
			"scanned_by": "MSCLyAWEbU6qKF8ULBXwKmj60WBvJsbnnByS",
			"total_infected": 0,
			"total_vulnerability": 0,
			"total_sensitive": 57,
			"total_coo": 0,
			"total_skipped": 15,
			"total_files_scanned": 15677,
			"total_sanitized": 0,
			"total_threat": 72
		}
	],
	"token": "681b4976bf684e4a32617a70"
}
```
