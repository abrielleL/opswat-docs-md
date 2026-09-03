<!-- source: https://www.opswat.com/docs/macloud-sdp/developer-guide/account-details-v3-1 -->

# Account Details v3.1

| API version | 3.1 |
| --- | --- |
| Last Update | 01/09/2019 |
| Authentication | YES |
| HTTP Method | GET |
| Rate limited | YES |
| Requests per rate limit | 10/min |
| Response Format | JSON |

Use this API to fetch your account details

## [API URL](/docs/macloud-sdp/developer-guide/account-details-v3-1#api-url)

https://gears.opswat.com/o/api/v3.1/account
## [Request Parameters](/docs/macloud-sdp/developer-guide/account-details-v3-1#request-parameters)

| Key | Datatype | Parameter Type | Required | Description | Default |
| --- | --- | --- | --- | --- | --- |
| access_token | string | Header | Yes | access token which archived from OAuth authentication step |  |

## [Response HTTP Code](/docs/macloud-sdp/developer-guide/account-details-v3-1#response-http-code)

See [APIs](/docs/macloud-sdp/developer-guide/apis)

## [Response Parameters](/docs/macloud-sdp/developer-guide/account-details-v3-1#response-parameters)

| Key | DataType | Description |
| --- | --- | --- |
| name | string | Account Name |
| email | string | Owner email address |
| last_login | string | The last date when the owner user logged into MetaAccess console |
| date_created | string | Date when the account was created |
| devices_allowed | int | Maximal number of devices is allowed to be monitored by on the account |
| devices_used | int | Number of monitored devices on the account |
| license_key | string | Account license key |
| devices_by_status | Array <object> |  |
| devices_by_status.status | string | - compliant : device is compliance with policy - non-compliant : device is non-compliance with policy - exempted : device is exempted - unknown : device is not installed MetaAccess agent |
| devices_by_status.number_of_devices | int | Number of devices by status |
| devices_by_issue_severity | Array <object> |  |
| devices_by_issue_severity.severity | string | - critical : device has critical issues - warning : device has warning issues - no_issue: device doesn't have any issues |
| devices_by___issue_severity.number_of_devices | int | Number of devices by issue severity |
| devices_by_vulnerability_severity | Array <object> |  |
| devices_by_vulnerability_severity.severity | string | Vulnerability severity: Value can be: "critical", "important", "moderate", "low", "unknown" |
| devices_by_vulnerability_severity.number_of_devices | int | Number of devices by vulnerability severity |

## [Example](/docs/macloud-sdp/developer-guide/account-details-v3-1#example)

**Example request**

https://gears.opswat.com/o/api/v3.1/account?access_token=TEST7P9ZMJ2LBF8AMOMJLNPMMLO953AVQ4C9YFF52R61234

**Example Response**

{
"name": "OPSWAT IT",
"email": "opswat_it@opswat.com",
"last_login": "2017-03-09T08:00:00Z",
"date_created": "2013-10-04T08:00:00Z",
"devices_allowed": 500,
"devices_used": 120,
"devices_by_status": [
{
"status": "compliant",
"number_of_devices": 110
},
{
"status": "non-compliant",
"number_of_devices": 5
},
{
"status": "exempted",
"number_of_devices": 5
},
{
"status": "unknown",
"number_of_devices": 25
}
],
"devices_by_issue_severity": [
{
"severity": "critical",
"number_of_devices": 2
},
{
"severity": "warning",
"number_of_devices": 50
},
{
"severity": "no_issue",
"number_of_devices": 68
}
],
"devices_by_vulnerability_severity": [
{
"severity": "critical",
"number_of_devices": 20
},
{
"severity": "important",
"number_of_devices": 50
},
{
"severity": "moderate",
"number_of_devices": 23
},
{
"severity": "low",
"number_of_devices": 17
},
{
"severity": "unknown",
"number_of_devices": 10
}
],
"license_key": "testcccd3e7201ee83e2c4b9f6dfc96c"
}
## [History](/docs/macloud-sdp/developer-guide/account-details-v3-1#history)

| Action | Version | URL |
| --- | --- | --- |
| Account Details | 3.0 | [Account Details v3.0](/docs/macloud-sdp/developer-guide/account-details-v3-0) |
| Account Details | 2.0 | [Account Details v2.0](/docs/macloud-sdp/developer-guide/account-details-v2-0) |
