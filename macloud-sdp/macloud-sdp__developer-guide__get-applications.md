<!-- source: https://www.opswat.com/docs/macloud-sdp/developer-guide/get-applications -->

# Get Applications

Summarize Page    Connect to Cursor Connect to VS Code

| API version | 3.0 |
| --- | --- |
| Last Update | 05/21/2018 |
| Authentication | YES |
| HTTP Method | POST |
| Content Type | application/json |
| Rate limited | YES |
| Requests per rate limit | 10/min |
| Response Format | JSON |

Use to get applications installed on endpoints on a specific account.

## [API URL](/docs/cm/developer-guidelines/get-applications#api-url)

https://gears.opswat.com/o/api/v3/apps
## [Request Parameters](/docs/cm/developer-guidelines/get-applications#request-parameters)

| Key | Datatype | Parameter Type | Required | Description | Default |
| --- | --- | --- | --- | --- | --- |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step |  |
| search | string | Body | No | The key word to search. |  |
| filter | object | Body | No | Indicate criteria you want to filter applications |  |
| filter.severity | array | Body | No | The severity level to filter. |  |
| filter.category | array | Body | No | The category ID to filter. |  |
| sort | object | Body | No | Indicate how you want to sort applications |  |
| sort.order | string | Body | No | The direction to sort. | desc |
| sort.field | string | Body | No | which field | name |
| page | number | Body | No | A page you want to get data | 1 |
| limit | number | Body | No | The limited number of how many records to be returned. | 50 |

## [Response HTTP Code](/docs/cm/developer-guidelines/get-applications#response-http-code)

See details in the Response HTTP Code section in [this page](/docs/cm/developer-guidelines/apis)

## [Response Parameters](/docs/cm/developer-guidelines/get-applications#response-parameters)

| Key | DataType | Description |
| --- | --- | --- |
| category_id | string | The category ID |
| category_name | string | The category name |
| severity | string | The app's severity level |
| product_id | string | Product Signature ID |
| name | string | Product name |
| vendor | string | Product vendor |
| version | string | Product version |
| number_of_devices | int | A number determines how many devices install the product |
| number_of_cves | int | A number determines how many cve issues that product exposures |

## [Example](/docs/cm/developer-guidelines/get-applications#example)

**Example Request: using Product ID**

https://gears.opswat.com/o/api/v3/apps?access_token=XXXXXXXXXXXXXXXXXXXXXXXXXXXXX
{
"search": "",
"filter": {
"severity": [],
"category": [
"Antivirus"
]
},
"sort": {
"order": "desc",
"field": "name"
},
"page": 1,
"limit": 50
}

**Example Response**

[
{
"number_of_devices": 2,
"severity": "unknown",
"category_name": "Anti-Malware",
"category_id": "Antivirus",
"vendor": "Microsoft Corporation",
"product_id": 236,
"name": "avast! Free Antivirus",
"version": "6.1.7600.16385",
"number_of_cves": 0
},
{
"number_of_devices": 20,
"severity": "unknown",
"category_name": "Anti-Malware",
"category_id": "Antivirus",
"vendor": "AVAST Software a.s.",
"product_id": 236,
"name": "avast! Free Antivirus",
"version": "12.3.3154.23",
"number_of_cves": 0
},
{
"number_of_devices": 20,
"severity": "unknown",
"category_name": "Anti-Malware",
"category_id": "Antivirus",
"vendor": "Microsoft Corporation",
"product_id": 477,
"name": "Windows Defender",
"version": "6.1.7600.16385",
"number_of_cves": 0
},
{
"number_of_devices": 1,
"severity": "unknown",
"category_name": "Anti-Malware",
"category_id": "Antivirus",
"vendor": "Microsoft Corporation",
"product_id": 477,
"name": "Windows Defender",
"version": "4.13.17134.1",
"number_of_cves": 0
},
{
"number_of_devices": 4,
"severity": "unknown",
"category_name": "Anti-Malware",
"category_id": "Antivirus",
"vendor": "Apple Inc.",
"product_id": 100141,
"name": "Gatekeeper",
"version": "10.11",
"number_of_cves": 0
}
]
