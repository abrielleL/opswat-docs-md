<!-- source: https://www.opswat.com/docs/macloud-sdp/developer-guide/apis -->

# APIs

MetaAccess provides different APIs to fetch device information (Hostname, Device ID, MAC/IP Address,...) and device security and compliance status, such as Antivirus, Antiphising, Public File Sharing, and Malware detection as well as account information.

These APIs require an access token as a parameter for security and authentication reasons. Without a valid access token provided, you will get HTTP code as 401 in response for each request. You are able to archive the access token for your application by using [authentication](/docs/macloud-sdp/developer-guide/authentication) methods we provide.

**Request Example**

https://gears.opswat.com/o/api/v2/account?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234

**Response Example**

{
"name": "OPSWAT MetaAccess",
"email": "opswat_metaaccess@opswat.com",
"last_login": "2017-03-09T08:00:00Z",
"date_created": "2013-10-04T08:00:00Z",
"devices_allowed": 500,
"devices_used": 120,
"devices_uncompliant": 5
}

**Response HTTP Code**

| HTTP Code | Description | Note |
| --- | --- | --- |
| 200 | Success |  |
| 400 | Bad request. JSON format is invalid or input values are invalid |  |
| 401 | Unauthorized. Your access_token is invalid or expired |  |
| 404 | Not found |  |
| 405 | Method not allowed | when a query specifies incorrect HTTP method. For example: an OAuth API requires HTTP method as GET, but the query sets HTTP method as POST/PUT/DELETE |
| 406 | "limit" parameter in the request parameter is greater than 50. | This is only applied for old APIs. |
| 413 | Requested page number exceeds page limit There is no data to return |  |
| 415 | Unsupported Media Type |  |
| 429 | The request exceeds the API rate limit. | please limit the number of requests sent per minute |
| 500 | Internal Server Error | Please contact OPSWAT support |

**Response Header**

## [Response Parameters](/docs/macloud-sdp/developer-guide/apis#response-parameters)

| Key | Datatype | Description |
| --- | --- | --- |
| X-RateLimit-Limit | int | rate limit of an account |
| X-RateLimit-Remaining | int | number of calls left in the limit duration |
| X-RateLimit-Reset-Time | int | when the rate limit is reset in second |

**Example**

{
"X-RateLimit-Limit": 20,
"X-RateLimit-Remaining": 10,
"X-RateLimit-Reset-Time": 40 // rate limit will be reset in 40 seconds
}
