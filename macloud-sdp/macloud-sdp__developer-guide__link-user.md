<!-- source: https://www.opswat.com/docs/macloud-sdp/developer-guide/link-user -->

# Link User

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

| API version | 2.0 |
| --- | --- |
| Last Update | 0 8/28/2014 |
| Authentication | YES |
| Response Format | JSON |
| HTTP Method | POST |
| Rate limited | YES |
| Requests per rate limit | 10/min |

Use to associate user with given MAC address or HWID.

## API URL

https://gears.opswat.com/o/api/v2/devices/:value/link_user
## Request Parameters

| Key | Datatype | Parameter Type | Required | Description | Default |
| --- | --- | --- | --- | --- | --- |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step |  |
| value | string | URL | Yes | HWID of MAC address of the device |  |
| opt | int | URL | Optional | Specific which kind of data we put in *value* parameter  0 - MAC address 1 - HWID | 0 |
| username | string | Body | Yes | User associates to the device. Length of *username* parameter should be in [1..256] |  |
| group | string | Body | Optional | Group name of the user who associated to the device. Length of *group* parameter should be in [1..256] |  |

## Response HTTP Code

See details in the Response HTTP Code section in [this page](/developer-guidelines/apis)

## Response Parameters

| Key | DataType | Description |
| --- | --- | --- |
| result | int | **0** - failure **1** - success |
| msg | string | Result details |

## Example

**Example Request:**

https://gears.opswat.com/o/api/v2/devices/00:0c:29:f2:7a:29/link_user?opt=0&access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
JSON body:
{
"username" : "testinguser",
"group" : "testinggroup"
}

**Example Response**

//Successful
{
"result": 1,
"msg": "OK"
}
 
 
//Failed
{
"result": 0,
"msg": "Device not found"
}
