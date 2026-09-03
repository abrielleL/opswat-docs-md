<!-- source: https://www.opswat.com/docs/cm/developer-guidelines/account-details-v3-0 -->

# Account Details v3.0

| API version | 3.0 |
| ---- | ---- |
| Last Update | 11/27/2018 |
| Authentication | YES |
| HTTP Method | GET |
| Rate limited | YES |
| Requests per rate limit | 10/min |
| Response Format | JSON |
| Change History | 11/27/2018: added "license_key" into the json response |

Use this API to fetch your account details

## API URL

```plaintext
https://gears.opswat.com/o/api/v3/account
```

## Response Parameters

| Key | DataType | Description |
| ---- | ---- | ---- |
| name | string | Account Name |
| email | string | Owner email address |
| last_login | string | The last date when the owner user logged into MetaAccess console |
| date_created | string | Date when the account was created |
| devices_allowed | int | Maximal number of devices is allowed to be monitored by on the account |
| devices_used | int | Number of monitored devices on the account |
| devices_uncompliant | int | Number of non-compliant devices |
| devices_critical | int | Number of devices with critical issues |
| devices_issues | int | Number of devices with issues |
| devices_unknown | int | Number of unknown devices |
| license_key | string | Account license key |

## Request Parameters

| Key | Datatype | Parameter Type | Required | Description | Default |
| ---- | ---- | ---- | ---- | ---- | ---- |
| access_token | string | Header | Yes | access token which archived from OAuth authentication step |  |

## Response HTTP Code

See [APIs](https://www.opswat.com/docs/macloud-sdp/3.54.0/developer-guide/apis)

## Example

**Example Request:**

```plaintext
https://gears.opswat.com/o/api/v3/account?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
```

**Example Response**

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
   "devices_issues": 10,
   "devices_unknown": 0,
   "license_key": "testcccd3e7201ee83e2c4b9f6dfc96c"
}
```

## History

| Action | Version | URL |
| ---- | ---- | ---- |
| Account Details | 2.0 | [Account Details v2.0](https://www.opswat.com/docs/cm/developer-guidelines/account-details-v2-0) |
