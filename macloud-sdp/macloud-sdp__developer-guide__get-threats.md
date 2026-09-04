<!-- source: https://www.opswat.com/docs/macloud-sdp/developer-guide/get-threats -->

# Get Threats

| API version | 3.0 |
| --- | --- |
| Last Update | 10/23/2018 |
| Authentication | YES |
| HTTP Method | POST |
| Content Type | application/json |
| Rate limited | YES |
| Requests per rate limit | 10/min |
| Response Format | JSON |

Use to fetch detected threats on a device

## [API URL](/docs/macloud-sdp/developer-guide/get-threats#api-url)

https://gears.opswat.com/o/api/v3/get_threats
## [Request Parameters](/docs/macloud-sdp/developer-guide/get-threats#request-parameters)

| Key | Datatype | Parameter Type | Required | Description | Default |
| --- | --- | --- | --- | --- | --- |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step |  |
| id | string | Body | Yes | The Device ID or MAC Address of a device you want to fetch detected threats. |  |
| limit | int | URL | Optional | Specific maximum number of threats will be returned in the response. The value should be in [1,50]. | 50 |
| page | int | URL | Optional | Specific page number which threats will be returned in. If the requested page exceeds the number of pages of threats, error code will be 413. It means that the requested page number is too large, no devices will be returned in this case. | 1 |
| verbose | object | Body | Optional | Specify what information you look for |  |
| verbose. antimalware_scan | int | Body | Optional | Specify if threats detected by daily anti-malware scan are included in the response Values can be:   - 0: not include - 1: include | 1 |
| verbose. local_antimalware_threats | int | Body | Optional | Specify if threats detected by local anti-malware products are included in the response Values can be:   - 0: not include - 1: include | 1 |

## [Response HTTP Code](/docs/macloud-sdp/developer-guide/get-threats#response-http-code)

See [APIs](/docs/macloud-sdp/developer-guide/apis)

## [Response Parameters](/docs/macloud-sdp/developer-guide/get-threats#response-parameters)

| Key | DataType | Returned when | Description |
| --- | --- | --- | --- |
| antimalware_scan | array<object> | verbose. antimalware_scan =1 | An array of threats detected by daily anti-malware scan |
| antimalware_scan.critical | int |  | Indicate if the threat is critical based on the defined policy on MetaDefender IT-OT Access console Values are:   - 0 – not critical - 1 – critical |
| antimalware_scan .scan_time | string |  | timestamp when found the threat |
| antimalware_scan .file | string |  | File was found the threat |
| antimalware_scan .hash | string |  | Indicates the hash code of the scanning object if the object is a file or process |
| antimalware_scan .threat_name | string |  | Threat name |
| antimalware_scan .details | array<object> |  | An array of threats found with details information |
| antimalware_scan .details.threat_name | string |  | Threat name which detected on a specific engine |
| antimalware_scan .details.av_name | string |  | Name of an engine which found the threat |
| local_antimalware_threats | array<object> | verbose. local_antimalware_threats =1 | Lists of threats ( threat details detected by local anti-malware applications ) |
| local_antimalware_threats .scan_time | string |  | Last timestamp when the threat was detected |
| local_antimalware_threats .repeat | int |  | Number of times the threat was detected |
| local_antimalware_threats .file | string |  | File was detected as a threat |
| local_antimalware_threats .threat_name | string |  | Threat name |
| local_antimalware_threats .product_name | string |  | product name which found the threat |
| local_antimalware_threats .product_vendor | string |  | Vendor name |
| local_antimalware_threats .product_version | string |  | Product version |
| local_antimalware_threats .action | string |  | Indicate an action the local anti-malware product took Value can be: unknown, cleaned, deleted, quarantined |
| local_antimalware_threats .existing | int |  | to indicate if an infected file still exists on the system when the agent report the data.   - 0 : not existing - 1 : existing |

## [Example](/docs/macloud-sdp/developer-guide/get-threats#example)

**Example Request: using Device ID**

https://gears.opswat.com/o/api/v3/get_threat?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
{
"id" : "device123",
"limit" : 10,
"page": 1
}

**Example Response**

{
"antimalware_scan": [
{
"critical": 0,
"file": "C:\\ProgramData\\WindowsMangerProtect\\ProtectWindowsManager.exe",
"hash": "e152e3ea7c356cfed40306ff946233d0",
"scan_time": "2015-05-13T17:00:34Z",
"threat_name": "Generic6.WQW",
"details": [
{
"threat_name": "ADWARE/ELEX.Gen",
"av_name": "ClamAV"
}
]
}
]
,
"local_antimalware_threats": [
{
"file": "C:\\Windows\\KMSEmulator.exe",
"scan_time": "2015-05-12T23:32:19Z",
"threat_name": "@ApplicUnwnt.Win32/HackKMS.A",
"repeat": 2,
"product_name": "ESET Endpoint Security",
"product_vendor": "ESET",
"product_version": "5.0.2211.0",
"action": "unknown",
"existing": 1
}
]
}
}
