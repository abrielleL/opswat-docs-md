<!-- source: https://www.opswat.com/docs/macloud-sdp/developer-guide/account-config -->

# Account Config

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

| API version | 3.1 |
| --- | --- |
| Last Update | 10/22/2019 |
| Authentication | YES |
| Response Format | JSON |
| HTTP Method | POST |
| Rate limited | YES |
| Requests per rate limit | 10/min |
| Change History | 10/22/2019: add new regcode section |

Use this API to retrieve account settings.

## [API URL](/docs/cm/developer-guidelines/account-config#api-url)

https://gears.opswat.com/o/api/v3.1/configuration
## [Request Parameters](/docs/cm/developer-guidelines/account-config#request-parameters)

| Key | Datatype | Parameter Type | Required | Description | Default |
| --- | --- | --- | --- | --- | --- |
| access_token | string | URL | Yes | access token which archived from OAuth authentication step |  |
| sections | Array of strings | Body | Yes | Specify which settings to fetch information. Available options:   - cross-domain-api: Cross-domain API setting - regcode: a registration code for mobile devices to enroll to the account |  |

## [Response HTTP Code](/docs/cm/developer-guidelines/account-config#response-http-code)

See details in the Response HTTP Code section in [this page](/docs/cm/developer-guidelines/apis)

## [Response Parameters](/docs/cm/developer-guidelines/account-config#response-parameters)

| Key | Datatype | Description |
| --- | --- | --- |
| <setting_name> | object | a setting name in the request.  Depend on settings, object will have different keys in response |
| cross-domain-api | object | Cross-domain API setting |
| cross-domain-api.enabled | number | Values:   - 1: API is enable on endpoints at the configured port - 0: API is disable on endpoints |
| cross-domain-api.port | number | port number which the cross-domain API is listening on endpoints |
| regcode | string | Account specific registration Shortcode |

## [Example](/docs/cm/developer-guidelines/account-config#example)

**Request Example**

https://gears.opswat.com/o/api/v3.1/configuration?access_token=TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R61234
 
 
Request Body:
{
"sections": ["cross-domain-api","regcode"]
}

**Response Example**

{
"cross-domain-api": {
"enabled": 1,
"port": 11369
},
"regcode": "EZ3ESTSY"
}
## [History](/docs/cm/developer-guidelines/account-config#history)

| Action | Version | URL |
| --- | --- | --- |
| Account Config | 3.0 | [Account Config v3.0](https://www.opswat.com/docs/macloud-sdp/developer-guide/account-config-v3-0) |
