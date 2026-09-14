<!-- source: https://www.opswat.com/docs/cm/developer-guidelines/account-details-v2-0 -->

# Account Details v2.0

| API version | 2.0 |
| ---- | ---- |
| Last Update | 01/30/2018 |
| Authentication | YES |
| Response Format | JSON |
| HTTP Method | GET |
| Rate limited | YES |
| Requests per rate limit | 10/min |
| Changes | 01/30/2018: add two parameters to response json: devices_critical, devices_issues |

Use this API to fetch your account details

## API URL

```plaintext
https://gears.opswat.com/o/api/v2/account
```

## Request Parameters

| Key | Datatype | Parameter Type | Required | Description | Default |
| ---- | ---- | ---- | ---- | ---- | ---- |
| access_token | string | Header | Yes | access token which archived from OAuth authentication step |  |

## Response HTTP Code

See [APIs guidelines.](https://www.opswat.com/docs/macloud-sdp/3.54.0/developer-guide/apis)

## Response Parameters

| Key | Datatype | Description |
| ---- | ---- | ---- |
| name | string | Account Name |
| email | string | Owner email address |
| last_login | string | The last date when the owner user logged into My OPSWAT Central Management console |
| date_created | string | Date when the account was created |
| devices_allowed | int | Maximal number of devices is allowed to be monitored by on the account |
| devices_used | int | Number of monitored devices on the account |
| devices_uncompliant | int | Number of non-compliant devices |
| devices_critical | int | Number of devices with critical issues |
| devices_issues | int | Number of devices with issues |

## Example

**Request Example**

```plaintext
https://gears.opswat.com/o/api/v2/account?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
```

**Response Example**

```plaintext
{
   "name": "OPSWAT IT",
   "email": "opswat_it@opswat.com",
   "last_login": "2017-03-09T08:00:00Z",
   "date_created": "2013-10-04T08:00:00Z",
   "devices_allowed": 500,
   "devices_used": 120,
   "devices_uncompliant": 5,
   "devices_critical": 0,
   "devices_issues": 10
}
```
