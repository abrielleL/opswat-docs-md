<!-- source: https://www.opswat.com/docs/cm/developer-guidelines/get-mdd-report-details -->

# Get MetaDefender Drive Report Details

| API version | 1.0 |
| ---- | ---- |
| Last Update | 06/17/2025 |
| Authentication | YES |
| HTTP Method | POST |
| Content Type | application/json |
| Rate limited | YES |
| Requests per rate limit | 10/min |
| Response Format | JSON |

Retrieve the MetaDefender Drive report details by using the report ID and device ID.

## API URL

```plaintext
https://product.my.us.opswat.com/o/mdd/v1/reports/details
```

## Request Parameters

| Key | Datatype | Parameter Type | Required | Description | Default |
| ---- | ---- | ---- | ---- | ---- | ---- |
| Authorization | string | Header | Yes | Bearer token for Authentication Authorization: Bearer ACCESS_TOKEN |  |
| device_id | string | Body | Yes | the device ID |  |
| report_id | string | Body | Yes | the report ID |  |
| filter | object | Body | Optional | Specify filter criteria |  |
| filter.issue_type | array<string> | Body | Optional | Specify what issue type used to filter along with the field. Value: - VUL: report with vulnerability - COO: report with coo detection - SENSITIVE: report with sensitive files - SKIPPED: report with skipped files - INFECTED: report with infected files |  |

Notes:

- criteria in a same parameter will be combined with OR operator
- criteria in different parameter will be combined with AND operator

## Response HTTP Code

See details in the Response HTTP Code section in [APIs](https://www.opswat.com/docs/cm/developer-guidelines/apis) guidelines.

## Response Parameters

| Key | DataType | Description |
| ---- | ---- | ---- |
| id | string | ID |
| timestamp | long | timestamp when the report occurs |
| sync_time | long | timestamp when the report sent to My Opswat Central Management |
| session_id | string | session id of the report |
| file_path | string | file path |
| threat_type | string | issue type |
| device_group | string | Device group of a device that the report occurred on |
| device_id | string | Device id of a device that the report occurred on |
| sha256 | string | sha256 of the file |

## Example

**Example Request**

```plaintext
https://product.my.us.opswat.com/o/pmp/v1/reports/details
Content-Type: application/json
Authorization: Bearer ACCESS_TOKEN

{
    "filter": {
			"issue_type" : ["VUL", "COO", "SENSITIVE", "SKIPPED", "INFECTED"]
		},
    "device_id": "MSCLyAWEbU6qKF8ULBXwKmj60WBvJsbnnByS",
		"report_id": "qa-virtual-machine__CustomScan_11-Apr-2025_03-34-31.json.gz"
}
```

## Example Response

```plaintext
{
  "id": "67f88dd210db0c74b2da2514",
  "file_path": "/media/Disk2/EFI/ubuntu/shimx64.efi",
  "threat_type": "SKIPPED",
  "timestamp": 1746618097000,
  "sync_time": 1746618097000,
  "session_id": "qa-virtual-machine__CustomScan_11-Apr-2025_03-34-31.json.gz",
  "device_id": "MSCLyAWEbU6qKF8ULBXwKmj60WBvJsbnnByS",
  "device_group": "Default Drivea",
  "sha256": "6fe6e1bcbe6cf6baec8e056d40361ca1aa715cc04ddcc2855351de060b84350b"
}
{
  "id": "67f88dd210db0c74b2da2515",
  "file_path": "/media/Disk2/EFI/BOOT/BOOTX64.EFI",
  "threat_type": "SKIPPED",
  "timestamp": 1746618097000,
  "sync_time": 1746618097000,
  "session_id": "qa-virtual-machine__CustomScan_11-Apr-2025_03-34-31.json.gz",
  "device_id": "MSCLyAWEbU6qKF8ULBXwKmj60WBvJsbnnByS",
  "device_group": "Default Drivea",
  "sha256": "6fe6e1bcbe6cf6baec8e056d40361ca1aa715cc04ddcc2855351de060b84350b"
}
```
