<!-- source: https://www.opswat.com/docs/cm/developer-guidelines/get-access-activities -->

# Get Access Activities

| API version | 3.0 |
| ---- | ---- |
| Last Update | 05/22/2018 |
| Authentication | YES |
| HTTP Method | POST |
| Content Type | application/json |
| Rate limited | YES |
| Requests per rate limit | 10/min |
| Response Format | JSON |

My OPSWAT Central Management records access activities when a device accesses to SaaS applications. To retrieve access activities on your account, you can use this API. You can filter access activities you concern.

**API URL**

```plaintext
https://gears.opswat.com/o/api/v3/activities
```

## Request Parameters

| Key | Datatype | Parameter Type | Required | Description | Default |
| ---- | ---- | ---- | ---- | ---- | ---- |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step |  |
| limit | int | Body | Optional | Specific maximum number of access activities will be returned in the response. The value should be in [1,50]. If there are more event logs than what the limit asks for, error code will be 406. Access activities in response is ordered by date. | 50 |
| page | int | Body | Optional | Specific page number which access activities will be returned in. If the requested page exceeds the number of pages of access activities, error code will be 413. It means that the requested page number is too large, no devices will be returned in this case. | 1 |
| start_date | string | Body | Optional | Specific the start date for the query duration. Starting date of the query. Format: MM/DD/YYYY in UTC timezone |  |
| end_date | string | Body | Optional | Specific the end date for the query duration. It must be greater than start_date. Format: MM/DD/YYYY in UTC timezone |  |
| age | int | Body | Optional | Specify age of the information in last hours. This parameter will be skipped if start_date and end_date parameters are set in the json input For example: if you want to query event access activities in last 5 hours, you need to pass age as 5. | 24 |
| action | array<string> | Body | Optional | Specify what access activities you want to retrieve. Options can be: - *blocked*: activities are blocked from accessing a SaaS application. - *allowed*: activities are allowed to access a SaaS application. - *monitored_block*: activities are monitored and they will be blocked from accessing a SaaS application if you change an access mode of the application to Enforce mode. - *monitored_allow*: activities are monitored and they will be allowed to access a SaaS application if you change an access mode of the application to Enforce mode. - *temporary_allowed*: activities are temporary allowed to access a SaaS application. It's temporary granted by an administrator |  |
| search | string | Body | Optional | a keyword to search. In which, the keyword can be a device name, group name, application user, device id, application name, access control rule name, device status |  |

## Response HTTP Code

See details in the Response HTTP Code section in [this page](https://www.opswat.com/docs/cm/developer-guidelines/apis)

## Response Parameters

| Key | Data Type | Description |
| ---- | ---- | ---- |
| timestamp | string | timestamp when the access activity occurs |
| action | string | Action taken by My OPSWAT Central Management. Values can be: - *blocked*: activities are blocked from accessing a SaaS application. - *allowed*: activities are allowed to access a SaaS application. - *monitored_block*: activities are monitored and they will be blocked from accessing a SaaS application if you change an access mode of the application to Enforce mode. - *monitored_allow*: activities are monitored and they will be allowed to access a SaaS application if you change an access mode of the application to Enforce mode. - *temporary_allowed*: activities are temporary allowed to access a SaaS application. It's temporary granted by an administrator |
| device_id | string | device id of a device which is accessing an application |
| device_name | string | Device name of a device which is accessing an application |
| device_status | string | Device status of a device which is accessing an application |
| device_group | string | group name of a device which is accessing an application |
| app_user | string | application user who is using a device to access an application |
| access_rule | string | access control rule which is applied to this activity |
| app_name | string | application name which a device is accessing |

## Example

**Example Request:**

```plaintext
https://gears.opswat.com/o/api/v3/activities?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
{
  "action": [
    "blocked"
  ],
  "page": 1,
  "limit": 20,
  "start_date": "05/15/2018",
  "end_date": "05/18/2018"
}
```

**Example Response**

```plaintext
[
    {
        "app_name": "Salesforce",
        "device_status": "Non-compliant",
        "device_name": "W8EVN20",
        "device_id": "SGH238TZW5",
        "access_rule": "NON COMPLIANT DEVICES",
        "app_user": "test_user@gmail.com",
        "device_group": "Group only firewall",
        "action": "blocked",
        "timestamp": "May 18, 2018 10:40:00 AM"
    },
    {
        "app_name": "Slack",
        "device_status": "Non-compliant",
        "device_name": "W8EVN20",
        "device_id": "SGH238TZW5",
        "access_rule": "NON COMPLIANT DEVICES",
        "app_user": "test_user@gmail.com",
        "device_group": "Group only firewall",
        "action": "blocked",
        "timestamp": "May 18, 2018 10:37:48 AM"
    }
]
```
