<!-- source: https://www.opswat.com/docs/macloud-sdp/developer-guide/application-details -->

# Application Details

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

| API version | 3.0 |
| --- | --- |
| Last Update | 06/14/2018 |
| Authentication | YES |
| HTTP Method | POST |
| Content Type | application/json |
| Rate limited | YES |
| Requests per rate limit | 10/min |
| Response Format | JSON |

Use to get application details which installed on endpoints on an account.

## [API URL](/docs/cm/developer-guidelines/application-details#api-url)

https://gears.opswat.com/o/api/v3/apps/details
## [Request Parameters](/docs/cm/developer-guidelines/application-details#request-parameters)

| Key | Datatype | Parameter Type | Required | Description | Default |
| --- | --- | --- | --- | --- | --- |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step |  |
| product_id | string | body | Yes | OPSWAT signature id of a product |  |
| version | string | body | Yes | Product version |  |
| verbose.cves | interger | body | No | Specify if CVEs information is included on the response  Values can be:   - 0: not include - 1: include | 0 |

## [Response HTTP Code](/docs/cm/developer-guidelines/application-details#response-http-code)

See details in the Response HTTP Code section in [this page](/docs/cm/developer-guidelines/apis)

## [Response Parameters](/docs/cm/developer-guidelines/application-details#response-parameters)

| Key | DataType | Description |
| --- | --- | --- |
| product_id | int | OPSWAT signature id of a product |
| name | string | Name of the product |
| version | string | Product version |
| vendor | string | Name of the product vendor |
| total_devices | int | Total device have install application |
| total_cves | int | Total CVEs of application |
| total_critical | int | Total critical issues of CVE |
| total_important | int | Total important issues of CVE |
| total_moderate | int | Total moderate issues of CVE |
| total_low | int | Total low issues of CVE |
| total_unknown | int | Total unknown issues of CVE |
| cves | Array Object | Top 100 CVEs (sort by severity from Important to Unknown) |
| cves.cve_id | string | ID of CVE |
| cves.severity | string | The severity of CVE |
| cves.summary | string | Summary of CVE |
| cves.update_date | String | Timestamp when the CVE update. |
| cves.opswat_score | double | OPSWAT Security Score |
| cves.cvss2_score | double | Common vulnerability scoring system v2.0 |
| cves.cvss3_score | double | Common vulnerability scoring system v3.0 |

## [Example](/docs/cm/developer-guidelines/application-details#example)

**Example Request with verbose as 0**

https://gears.opswat.com/o/api/v3/apps/details?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
 
{
"product_id":6005,
"version":"5.0.2211.0",
"verbose": {
"cves": 0
}
}

**Example Response verbose = 0**

{
"product_id": 25,
"name": "ESET Endpoint Security",
"version": "5.0.2211.0",
"vendor": "ESET",
"total_devices": 1,
"total_cves": 1,
"total_critical": 0,
"total_important": 0,
"total_moderate": 1,
"total_low": 0,
"total_unknown": 0
}

**Example Request with verbose as 1**

https://gears.opswat.com/o/api/v3/cves/apps/details?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
 
{
"product_id":6005,
"version":"5.0.2211.0",
"verbose": {
"cves": 1
}
}

**Example Response verbose = 1**

{
"product_id": 25,
"name": "ESET Endpoint Security",
"version": "5.0.2211.0",
"vendor": "ESET",
"total_devices": 1,
"total_cves": 1,
"total_critical": 0,
"total_important": 0,
"total_moderate": 1,
"total_low": 0,
"total_unknown":0
"cves": [
{
"cve_id": "CVE-2012-3982",
"severity": "CRITICAL",
"summary": "Multiple unspecified vulnerabilities in the browser engine in Mozilla Firefox before 16.0",
"update_date": 1524195758,
"opswat_score": 0.5,
"cvss2_score": 10,
"cvss3_score": 10
}
]
}
