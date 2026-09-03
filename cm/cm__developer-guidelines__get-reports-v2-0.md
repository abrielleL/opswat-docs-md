<!-- source: https://www.opswat.com/docs/cm/developer-guidelines/get-reports-v2-0 -->

# Get Reports v2.0

| API version | 2.0 |
| ---- | ---- |
| Last Update | 05/16/2016 |
| Authentication | YES |
| Response Format | CSV |
| HTTP Method | POST |
| Rate limited | YES |
| Requests per rate limit | 10/min |

Use to download reports such as OS patches summary, devices which missing a specific OS patch, missing OS patches on a specific device.

## API URL

```plaintext
https://gears.opswat.com/o/api/v2/get_reports
```

## Request Parameters

| Key | Datatype | Parameter Type | Required | Description | Default |
| ---- | ---- | ---- | ---- | ---- | ---- |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step |  |
| type | string | URL | Yes | Specify what report you want to download. Values can be: - OSPatchSummary: get OS Patches summary report - DeviceMissingOSPatch: get devices which missing a specific OS Patch report - MissingOSPatch: get missing OS Patches on a device |  |
| kb | string | URL | Optional | Must be passed in with if the report type is *DeviceMissingOSPatch* Value: KB Number |  |
| id | string | URL | Optional | Must be passed in if the report type is *MissingOSPatch* Value: device's id or MAC address |  |

Response HTTP Code

See [APIs](https://www.opswat.com/docs/macloud-sdp/3.54.0/developer-guide/apis)

## Example

## Get OS Patches Summary Report

**Request Example**

```plaintext
Request:https://gears.opswat.com/o/api/v2/get_reports?type=OSPatchSummary&access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
```

**Example Response**: csv file

| No. | Category | KB Number | Title | Description | Product | Vendor | Severity | No. of Devices |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 1 | critical_update | KB3115040 | Update for Microsoft Project 2013 32-Bit Edition | Microsoft has released an update for Microsoft Project 2013 32-Bit Edition. | Office 2013 | Microsoft Corporation | unknown | 1 |
| 2 | critical_update | KB3115039 | Update for Microsoft OneDrive for Business 32-Bit Edition | Microsoft has released an update for Microsoft OneDrive for Business 32-Bit Edition. | Office 2013 | Microsoft Corporation | unknown | 1 |

## Get Devices Which Missing a Specific OS Patch Report

**Request Example**

```plaintext
https://gears.opswat.com/o/api/v2/get_reports?type=DeviceMissingOSPatch&kb=KB3115040&access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
```

**Response Example:** csv file

| KB Number: KB3115040 |  |  |  |
| ---- | ---- | ---- | ---- |
| Title: Update for Microsoft Project 2013 32-Bit Edition |  |  |  |
| No. | Device ID | Device Name | Username |
| 1 | 3AD89B1F7647455889897B5D2A63D15A | WSEVN20 | ctran |

## Get Missing OS Patches on Device

**Request Example**

```plaintext
https://gears.opswat.com/o/api/v2/get_reports?type=MissingOSPatch&id=00:0c:29:cd:c7:b2&access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
```

**Response Example:** csv file

| Last information updated: May 04, 2016 03:23:13 AM UTC |  |  |  |  |  |  |  |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| No. | Category | KB Number | Title | Description | Product | Vendor | Severity |
| 1 | update | KB3013816 | Update for Windows 8.1 for x64-based Systems | Install this update to resolve issues in Windows | Windows 8.1 | Microsoft Corporation | unknown |
