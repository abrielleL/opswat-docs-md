<!-- source: https://www.opswat.com/docs/cm/developer-guidelines/get-pmp-report-details -->

# Get PMP Report Details

| API version | 1.0 |
| ---- | ---- |
| Last Update | 06/17/2025 |
| Authentication | YES |
| HTTP Method | POST |
| Content Type | application/json |
| Rate limited | YES |
| Requests per rate limit | 10/min |
| Response Format | JSON |

Retrieve the details of a PMP report - including MetaDefender Kiosk, MetaDefender Drive - using the report's session ID.

## API URL

```plaintext
https://product.my.us.opswat.com/o/pmp/v1/reports/details
```

## Request Parameters

| Key | Datatype | Parameter Type | Required | Description | Default |
| ---- | ---- | ---- | ---- | ---- | ---- |
| Authorization | string | Header | Yes | Bearer token for Authentication Authorization: Bearer ACCESS_TOKEN |  |
| session_id | string | Body | Optional | session ID |  |
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
| file_name | string | file name |
| file_path | string | file path |
| pmp_type | string | issue type |
| device_type | string | Device type of a device that the report occurred on |
| device_name | string | Device name of a device that the report occurred on |
| device_id | string | Device id of a device that the report occurred on |
| md5 | string | md5 of the file |
| sha1 | string | sha1 of the file |
| sha256 | string | sha256 of the file |

## Example

**Example Request**

```plaintext
https://gears.opswat.com/o/pmp/v1/reports/details
Content-Type: application/json
Authorization: Bearer ACCESS_TOKEN

{
    "filter": {
			"issue_type" : ["VUL", "COO", "SENSITIVE", "SKIPPED", "INFECTED"]
		},
    "session_id": "phuoc12345678"
}
```

## Example Response

```plaintext
{
  "id": "681a21f3c239c15ff0c16981",
  "file_name": "Exceeded Archive File Number_4.zip",
  "file_path": "E:\\Exceeded Archive File Number_4.zip",
  "pmp_type": "SENSITIVE",
  "device_type": "KIOSK",
  "timestamp": 1712161663000,
  "sync_time": 1747381075000,
  "session_id": "phuoc12345678",
  "device_name": "phuockiosk",
  "device_id": "phuockiosk",
  "md5": "F4C0908C43B07361D9692AB21163E554",
  "sha1": "FB08572F367FD54E6C82C17E6B4FFEFF4A109441",
  "sha256": "3A08843F67A170B0AC9588E7C9C742D4602416140A1FC8D15AE0B6F10C7BF228"
}
{
  "id": "681a21f3c239c15ff0c16983",
  "file_name": "Exceeded Archive Depth.zip",
  "file_path": "E:\\Exceeded Archive Depth.zip",
  "pmp_type": "SENSITIVE",
  "device_type": "KIOSK",
  "timestamp": 1712161663000,
  "sync_time": 1747381075000,
  "session_id": "phuoc12345678",
  "device_name": "phuockiosk",
  "device_id": "phuockiosk",
  "md5": "F4C0908C43B07361D9692AB21163E554",
  "sha1": "FB08572F367FD54E6C82C17E6B4FFEFF4A109441",
  "sha256": "3A08843F67A170B0AC9588E7C9C742D4602416140A1FC8D15AE0B6F10C7BF228"
}
```
