<!-- source: https://www.opswat.com/docs/macloud-sdp/developer-guide/get-groups -->

# Get Groups

Summarize Page    Connect to Cursor Connect to VS Code

| API version | 3.0 |
| --- | --- |
| Last Update | 05/08/2018 |
| Authentication | YES |
| HTTP Method | POST |
| Content Type | application/json |
| Rate limited | YES |
| Requests per rate limit | 10/min |
| Response Format | JSON |

Use to fetch groups in an account

## API URL

https://gears.opswat.com/o/api/v3/groups
## Request Parameters

| Key | Datatype | Parameter Type | Required | Description | Default |
| --- | --- | --- | --- | --- | --- |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step |  |
| limit | number | Body | Optional | Specify a maximum number of groups will be returned in the response. The value should be in [1,50]. If there are more groups than what the limit asks for, HTTP code will be 406. | 10 |
| page | number | Body | Optional | Specify a page number which groups will be returned in. If the requested page exceeds the number of pages of groups, error code will be 413. It means that the requested page number is too large, no groups will be returned in this case. | 1 |
| search | string | Body | Optional | The keyword to search. In which, the keyword can be a group name or an assigned policy |  |
| sort | object | Body | Optional | Specify how to sort groups in result-set By default: sort groups by group_name in ascending order |  |
| sort.field | string | Body | Optional | Specify which field will be sorted by  Values can be: **group_name, domain_name, policy_name, number_of_devices, last_update**. | group_name |
| sort.order | string | Body | Optional | Specify sort order. Values can be:   - asc: sort devices in ascending order. - desc: sort devices in descending order. | asc |

## Response HTTP Code

See details in the Response HTTP Code section in [this page](/developer-guidelines/apis)

## Response Parameters

| Key | DataType | Description |
| --- | --- | --- |
| group_id | string | a unique group identification |
| group_name | string | group name |
| domain_name | string | domain name of a domain controller where this group is synchronized |
| auto_join | boolean | specify if a device can auto-join this group when it registers to the account |
| policy_id | string | assigned policy id |
| policy_name | string | assigned policy name |
| number_of_devices | int | number of devices assigned to this group |
| description | string | group description |
| created_date | string | A timestamp in GMT format when this group is created |
| last_modified | string | The last timestamp in GMT format when this group is updated |

## Example

**Example Request**

https://gears.opswat.com/o/api/v3/groups?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
{
"limit": 10,
"page": 1,
"sort": {
"order": "desc",
"field": "group_name"
},
"search": "antivirus"
}

**Example Response**

[
{
"domain_name": "",
"auto_join": false,
"policy_id": "35010615",
"number_of_devices": 10,
"group_name": "Default",
"policy_name": "Policy Antivirus-critical",
"description": "This is a default group",
"group_id": "167641719",
"created_date": "Jun 12, 2017 01:49:39 AM",
"last_modified": "Jun 12, 2017 01:50:29 AM"
},
{
"domain_name": "your_domain.com",
"auto_join": true,
"policy_id": "33010675",
"number_of_devices": 100,
"group_name": "San Francisco",
"policy_name": "Policy Antivirus-critical",
"description": "This is a group synchronized from an active directory",
"group_id": "260854829",
"created_date": "Jul 17, 2017 07:56:22 AM",
"last_modified": "Aug 04, 2017 07:01:33 AM"
}
]
