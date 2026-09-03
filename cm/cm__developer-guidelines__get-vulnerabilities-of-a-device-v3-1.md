<!-- source: https://www.opswat.com/docs/cm/developer-guidelines/get-vulnerabilities-of-a-device-v3-1 -->

# Get Vulnerabilities of a Device v3.1

| API version | 3.1 |
| ---- | ---- |
| Last Update | 04/18/2023 |
| Authentication | YES |
| HTTP Method | POST |
| Content Type | application/json |
| Rate limited | YES |
| Requests per rate limit | 10 requests/min |
| Response Format | JSON |
| Change History | Added support multiple CVSS scores on the response data |

Use to fetch detected vulnerabilities that are associated to a device

## API URL

```plaintext
https://gears.opswat.com/o/api/v3.1/get_cves
```

## Request Parameters

| Key | Datatype | Parameter Type | Required | Description | Default |
| ---- | ---- | ---- | ---- | ---- | ---- |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step |  |
| id | string | Body | Yes | The Device ID or MAC Address of a device you want to fetch vulnerabilities |  |
| verbose | int | Body | Optional | 1 - detailed vulnerability information will return in response 0 - response does not include detailed information, only CVE IDs are included in a response | 0 |
| limit | int | Body | Optional | Specific maximum number of vulnerabilities will be returned in the response. The value should be in [1,100]. | 100 |
| page | int | Body | Optional | A page you want to get data | 1 |
| filter | object | Body | Optional | Specify filter criteria |  |
| filter.score_type | string | Body | Optional | Specify what score type used to filter along with the field *filter.score* Value can be: "opswat_score", "cvss2_ score", "cvss3_score" | opswat_score |
| filter.severity | array | Body | Optional | Filter vulnerabilities based on score_type: - cvss2_score: "high", "medium", "low - cvss3_score: "critical", "high", "medium", "low", "none - opswat_score: "critical", "important", "moderate", "low", "unknown" | all based on selected score_type |

## Response HTTP Code

See [APIs](https://www.opswat.com/docs/macloud-sdp/3.54.0/developer-guide/apis)

## Response Parameters

| Key | DataType | Description |
| ---- | ---- | ---- |
| cve_id | string | CVE ID |
| severity | string | vulnerability severity. Value can be: "critical", "important", "moderate", "low", "unknown", "high", "medium" |
| summary | string | Vulnerability summary |
| update_date | string | The last date NIST updated this vulnerability |
| publish_date | string | The date NIST published this vulnerability |
| opswat_score | string | OPSWAT score |
| cvss2_score | string | CVSS 2 score |
| cvss3_score | number | CVSS 3 score |
| remediation | string | Suggestion to remediate the CVE |
| cwe_id | string | A CWE(Common Weakness Enumeration) group identification string. |

## Example

**Example Request:**

```plaintext
https://gears.opswat.com/o/api/v3.1/get_cves?access_token=XXXXXXXXXXXXXXXXXXXXXXXXXXXXX
{
    "id": "device_id",
    "filter": {
        "severity": ["critical"]
    },
    "page": 1,
    "limit": 20
}
```

**Example Response with verbose as OFF**

```plaintext
[
    {
        "cve_id": "CVE-2015-8459",
        "severity": "critical",
        "opswat_score": 9.6,
        "cvss2_score": 10,
        "cvss3_score": 10,
    },
    {
        "cve_id": "CVE-2004-0629",
        "severity": "critical",
        "opswat_score": 5.3,
        "cvss2_score": 7.5
        "cvss3_score": 10,
    }
]
```

**Example Response with verbose as ON**

```plaintext
[
  {
    "cve_id": "CVE-2007-5341",
    "severity": "critical",
    "summary": "Remote code execution in the Venkman script debugger in Mozilla Firefox before 2.0.0.8.",
    "cwe_id": "CWE-119",
    "update_date": "2017-02-17T02:59:08Z",
    "publish_date": "2017-02-17T02:59:08Z",
    "opswat_score": 9.0,
    "cvss2_score": 7.5,
    "cvss3_score": 9.8,
    "remediation": "Mozilla Firefox 0.0: Upgrade to a version higher than 2.0.0.7"
  },
  {
    "cve_id": "CVE-2016-0990",
    "severity": "critical",
    "summary": "Use-after-free vulnerability in Adobe Flash Player before 18.0.0.333 and 19.x through 21.x before 21.0.0.182 on Windows and OS X and before 11.2.202.577 on Linux, Adobe AIR before 21.0.0.176, Adobe AIR SDK before 21.0.0.176, and Adobe AIR SDK & Compiler before 21.0.0.176 allows attackers to execute arbitrary code via unspecified vectors, a different vulnerability than CVE-2016-0987, CVE-2016-0988, CVE-2016-0991, CVE-2016-0994, CVE-2016-0995, CVE-2016-0996, CVE-2016-0997, CVE-2016-0998, CVE-2016-0999, and CVE-2016-1000.",
    "cwe_id": "",
    "update_date": "2017-02-17T02:59:08Z",
    "publish_date": "2017-02-17T02:59:08Z",
    "opswat_score": 8.1,
    "cvss2_score": 10.0,
    "cvss3_score": 9.8,
    "remediation": "Adobe Flash Player (ActiveX) 10.0.32.18: Upgrade to a version higher than 20.0.0.306"
   }
]
```

## History

| Action | Version | URL |
| ---- | ---- | ---- |
| Get Vulnerabilities of a device | 3.0 | [Get Vulnerabilities of a Device v3.0](https://www.opswat.com/docs/cm/developer-guidelines/get-vulnerabilities-of-a-device-v3-0) |
