<!-- source: https://www.opswat.com/docs/cm/developer-guidelines/get-vulnerabilities -->

# Get Vulnerabilities

| API version | 3.2 |
| ---- | ---- |
| Last Update | 08/15/2023 |
| Authentication | YES |
| HTTP Method | POST |
| Content Type | application/json |
| Rate limited | YES |
| Requests per rate limit | 10/min |
| Response Format | JSON |
| Change History | Added support for Known Exploited Vulnerabilities |

Use to query vulnerabilities which devices on an account have .

## API URL

```plaintext
https://gears.opswat.com/o/api/v3.2/cves
```

## Request Parameters

| Key | Datatype | Parameter Type | Required | Description | Default |
| ---- | ---- | ---- | ---- | ---- | ---- |
| access_token | string | URL | Yes | Access token which archived from OAuth authentication step |  |
| search | string | Body | Optional | A key word to search vulnerabilities. |  |
| filter | object | Body | Optional | Specify filter criteria |  |
| filter.severity | array | Body | Optional | Filter vulnerabilities based on score_type: - cvss2_score: "high", "medium", "low - cvss3_score: "critical", "high", "medium", "low", "none - opswat_score: "critical", "important", "moderate", "low", "unknown" | all based on selected score_type |
| filter.score | double | Body | Optional | Define a score to filter vulnerabilities My OPSWAT Central Management returns vulnerabilities that have a score greater or equal to this value. You need to specify what score type in the field *filter.score_type;* otherwise, the error code 400 is returned |  |
| filter.score_type | string | Body | Optional | Specify what score type used to filter along with the field *filter.score* Value can be: "opswat_score", "cvss2_score", "cvss3_score" | opswat_score |
| filter.kev | number | Body | Optional | 0: Return all CVEs 1: Only return CVEs in the KEV list | 0 |
| sort | object | Body | Optional | Specify how to sort devices in result-set By default: sort by CVE-ID in ASC order. |  |
| sort.order | string | Body | Optional | Specify how to sort vulnerabilities in result-set Value can be: "asc", "desc" | asc |
| sort.field | string | Body | Optional | Specify which field is used to sort vulnerabilities in result-set. Value can be: "opswat_score", "cvss2_score", "cvss3_score", "severity", "cve_id" | cve_id |
| page | number | Body | Optional | Specify page number which vulnerabilities will be returned in. If the requested page exceeds the number of pages of devices, error code will be 413. It means that the requested page number is too large, no vulnerability will be returned in this case. | 1 |
| limit | number | Body | Optional | Define maximum number of devices which will be returned in the response. The value should be in [1,50]. | 50 |

## Response HTTP Code

[this page](https://www.opswat.com/docs/cm/my-opswat-central-management/10.0.2506/developer-guidelines/apis)

## Response Parameters

| Key | DataType | Required | Description |
| ---- | ---- | ---- | ---- |
| cve_id | string | Yes | CVE ID |
| severity | string | Yes | vulnerability severity. Value can be: "critical", "important", "moderate", "low", "unknown", "high", "medium". |
| summary | string | Yes | vulnerability summary |
| updated_date | string | Yes | The last date NIST updated this vulnerability |
| opswat_score | double | Optional | Opswat score |
| cvss2_score | double | Optional | CVSS 2 score |
| cvss3_score | double | Optional | CVSS 3 score |
| total_devices | int | Yes | Number of devices has this vulnerability |
| kev.due_date | string | Optional | The due date to fix this vulnerability |
| kev.published_date | string | Optional | The date CISA published this vulnerability |

## Example

**Example Request: using Product ID**

```plaintext
https://gears.opswat.com/o/api/v3.2/cves?access_token=XXXXXXXXXXXXXXXXXXXXXXXXXXXXX
{
    "search": "",
    "filter": {
        "score": 5,
        "score_type": "opswat_score",
        "severity": ["critical"],
        "kev": 1
    },
    "sort": {
        "order": "asc",
        "field": "cve_id"
    },
    "page": 1,
    "limit": 20
}
```

**Example Response**

```plaintext
[
    {
        "cve_id": "CVE-2015-8459",
        "severity": "critical",
        "summary": "Adobe Flash Player before 18.0.0.324 and 19.x and 20.x before 20.0.0.267 on Windows and OS X and before 11.2.202.559 on Linux, Adobe AIR before 20.0.0.233, Adobe AIR SDK before 20.0.0.233, and Adobe AIR SDK & Compiler before 20.0.0.233 allow attackers to execute arbitrary code or cause a denial of service (memory corruption) via unspecified vectors, a different vulnerability than CVE-2015-8460, CVE-2015-8636, and CVE-2015-8645.",
        "updated_date": "2017-02-17T02:59:08Z",
        "opswat_score": 9.6,
        "cvss2_score": 10,
        "cvss3_score": 10,
        "total_devices": 182,
        "kev": {
          "due_date": "2023-06-12T00:00:00Z",
          "published_date": "2023-05-22T00:00:00Z"
        }
    },
	{
        "cve_id": "CVE-2004-0629",
        "severity": "critical",
        "summary": "Buffer overflow in the ActiveX component (pdf.ocx) for Adobe Acrobat 5.0.5 and Acrobat Reader, and possibly other versions, allows remote attackers to execute arbitrary code via a URI for a PDF file with a null terminator (%00) followed by a long string.",
        "updated_date": "2017-07-11T01:30:19Z",
        "opswat_score": 5.3,
        "cvss2_score": 7.5,
        "total_devices": 1
    }
]
```

## History

| Action | Version | URL |
| ---- | ---- | ---- |
| Get Vulnerabilities | 3.1 | [Get Vulnerabilities v3.1](https://www.opswat.com/docs/macloud-sdp/developer-guide/get-vulnerabilities-v3-1) |
| Get Vulnerabilities | 3.0 | [Get Vulnerabilities v3.0](https://www.opswat.com/docs/macloud-sdp/developer-guide/get-vulnerabilities-v3-0) |
