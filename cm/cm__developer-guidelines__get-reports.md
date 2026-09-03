<!-- source: https://www.opswat.com/docs/cm/developer-guidelines/get-reports -->

# Get Reports

| API version | 3.1 |
| ---- | ---- |
| Last Update | 08/02/2019 |
| Authentication | YES |
| Response Format | CSV &#124; ZIP &#124; JSON |
| HTTP Method | GET |
| Rate limited | YES |
| Requests per rate limit | 10/min |
| Change History | 08/02/2019: add one more export type (type parameter in request), scan_threats_log |

Use to download reports such as OS patches summary, devices which missing a specific OS patch, missing OS patches on a specific device, My OPSWAT Central Management agent log

## API URL

```plaintext
https://gears.opswat.com/o/api/v3.1/get_reports
```

## Request Parameters

| Key | Datatype | Parameter Type | Required | Description | Default |
| ---- | ---- | ---- | ---- | ---- | ---- |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step |  |
| type | string | URL | Yes | Specify what report you want to download. Values can be: - os_patch_summary: get OS Patches summary report - device_missing_os_patch: get devices which missing a specific OS Patch report - missing_os_patch: get missing OS Patches on a device - agent_log: download OPSWAT Agent logs which was requested in Device Action - scan_threats_log: download threat scanning log which was requested in Device Action |  |
| command_id | string | URL | Optional | **Must be passed in if the report type is agent_log or scan_threat_log** Command ID which archived from Device Action when you request to retrieve OPSWAT Agent logs |  |
| kb | string | URL | Optional | **Must be passed in with if the report type is device_missing_os_patch** KB Number of an OS patch you would like to download devices which are missing the OS patch. |  |
| id | string | URL | Optional | **Must be passed in if the report type is missing_os_patch** Device ID or D MAC address |  |

## Response HTTP Code

See details in the Response HTTP Code section in [this page](https://www.opswat.com/docs/cm/developer-guidelines/apis)

## Response Parameters

| Key | Datatype | Description |
| ---- | ---- | ---- |
| status | string | _*_Only applied for agent_log, *_scan_threats_log type _ Command status. Value can be - Queued: the command is in queue, has not sent to a device yet - Pending: the command is sent to a device but the device has not responded yet - In Progress: the device responded that it will start scanning - Failed: the device responded that it couldn't upload log |
| message | string | *_This is applied for agent_log type or *_scan_threats_log type Detailed status |
| error | string | *_This is applied for agent_log type or *_scan_threats_log type Indicate what is wrong |
| error_description | string | *_This is applied for agent_log type or *_scan_threats_log type Detailed error |

## Example

## GET OS Patches Summary Report

**Request Example**

```plaintext
https://gears.opswat.com/o/api/v3.1/get_reports?type=os_patch_summary&access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
```

**Example Response**: csv file

| No. | Category | KB Number | Title | Description | Product | Vendor | Severity | No. of Devices |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 1 | critical_update | KB3115040 | Update for Microsoft Project 2013 32-Bit Edition | Microsoft has released an update for Microsoft Project 2013 32-Bit Edition. | Office 2013 | Microsoft Corporation | unknown | 1 |
| 2 | critical_update | KB3115039 | Update for Microsoft OneDrive for Business 32-Bit Edition | Microsoft has released an update for Microsoft OneDrive for Business 32-Bit Edition. | Office 2013 | Microsoft Corporation | unknown | 1 |

## GET Devices Which Missing a Specific OS Patch Report

**Request Example**

```plaintext
https://gears.opswat.com/o/api/v3.1/get_reports?type=device_missing_os_patch&kb=KB3115040&access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
```

**Response Example:** csv file

| KB Number: KB3115040 |  |  |  |
| ---- | ---- | ---- | ---- |
| Title: Update for Microsoft Project 2013 32-Bit Edition |  |  |  |
| No. | Device ID | Device Name | Username |
| 1 | 3AD89B1F7647455889897B5D2A63D15A | WSEVN20 | bob |

## GET Missing OS Patches on Device

**Request Example**

```plaintext
https://gears.opswat.com/o/api/v3.1/get_reports?type=missing_os_patch&id=00:0c:29:cd:c7:b2&access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
```

**Response Example:** csv file

| Last information updated: May 04, 2016 03:23:13 AM UTC |  |  |  |  |  |  |  |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| No. | Category | KB Number | Title | Description | Product | Vendor | Severity |
| 1 | update | KB3013816 | Update for Windows 8.1 for x64-based Systems | Install this update to resolve issues in Windows | Windows 8.1 | Microsoft Corporation | unknown |

## GET Fetch Log Reports

**Request Example**

```plaintext
https://gears.opswat.com/o/api/v3.1/get_reports?type=agent_log&command_id=5c2c59e91e772804e4235319&access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
```

**Response Example:**

- ***Successful***
  - HTTP 200
  - Response: a zip file. It contains OPSWAT Agent's logs
- ***Command ID is valid but agent log is not available***
  - HTTP 202
  - Response: json

```plaintext
//The command is in queue
{
	"status" : "Queued",
	"message" : "Command has not completed"
}
 
//The command is sent to a device but the device has not responded yet
{
	"status" : "Pending",
	"message" : "Command has not completed"
}
 
//A device responded but the device couldn't complete a command
{
	"status" : "Failed",
	"message" : "Command has not been successful"
}
```

- ***Command is invalid or doesn't exist***
  - HTTP 404
  - Response: json

```plaintext
{
	"error" : "invalid_request",
	"error_description" : "Command not found"
}
```

## GET Scan Threats Reports

**Request Example**

```plaintext
https://gears.opswat.com/o/api/v3.1/get_reports?type=scan_threats_log&command_id=5c2c59e91e772804e4235319&access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
```

**Response Example:**

- ***Successful***
  - HTTP 200
  - Response: a zip file. It contains OPSWAT Agent's threat scanning logs
- ***Command ID is valid but scan threat log is not available***
  - HTTP 202
  - Response: json

```plaintext
//The command is in queue
{
	"status" : "Queued",
	"message" : "Command has not completed"
}
 
//The command is sent to a device but the device has not responded yet
{
	"status" : "Pending",
	"message" : "Command has not completed"
}
 
//The device responded that it will start scanning
{
	"status" : "In Progress",
	"message" : "Command has not completed"
}
 
//The device responded that it couldn't upload log
{
	"status" : "Failed",
	"message" : "Failed to upload log"
}
```

- ***Command is invalid or doesn't exist***
  - HTTP 404
  - Response: json

```plaintext
{
	"error" : "invalid_request",
	"error_description" : "Command not found"
}
```

## History

| API | Version | URL |
| ---- | ---- | ---- |
| Get Reports | 3.0 | [Get Reports v3.0](https://www.opswat.com/docs/macloud-sdp/developer-guide/get-reports-v3-0) |
| Get Reports | 2.0 | [Get Reports v2.0](https://www.opswat.com/docs/macloud-sdp/developer-guide/get-reports-v2-0) |
