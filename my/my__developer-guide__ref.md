<!-- source: https://www.opswat.com/docs/my/developer-guide/ref -->

## Overview

This is the API documentation for My OPSWAT Public API.

Serverhttps://apiv1.my.opswat.com

My OPSWAT Portal Server

Server Variables## Authenticationhttp bearerAuth

A token can be generated from a secret key that is managed on My OPSWAT Portal.

This token is used as an API Key for protected APIs.

Format:
Authorization: Bearer

### Important Notes

- Token has expiration time
- Must regenerate when expired
## Auth

API for generating access token

Endpoints[POST/portal/oauth2/token](/docs/my/developer-guide#getaccesstoken)
### Get access token

Generate access token using client credentials.

**Rate Limit Note**: The API rate limit is set to **5** requests per minute per organization.

Auth NoneHeaders

| Content-Type | string | application/json |  |
| --- | --- | --- | --- |

Request Body application/json

| object | object |  |  |
| --- | --- | --- | --- |
| client_id | string | Identifier for your application |  |
| client_secret | string | Secret key used to authenticate your application |  |
| grant_type | string | OAuth 2.0 grant type  Enum: `client_credentials` |  |

POST /portal/oauth2/tokencURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Access token generated successfully

| object | object | Response returned when an access token is successfully generated. |  |
| --- | --- | --- | --- |
| data3 fields | object | Contains access token information. |  |
| access_token | string | Token used to authenticate requests to protected APIs. |  |
| token_type | string | Token type (typically Bearer). |  |
| expires_in | integer | Lifetime of the access token in seconds. |  |

400

Validation error

401

Authentication failed due to invalid credentials

429

Rate limit exceeded. Retry after the specified time.

500

Internal server error occurred

 Response
## Product

APIs related to products and licenses management.

Endpoints[GET/portal/product/license/active-deployments](/docs/my/developer-guide#getactivedeployments)
### Get active license deployment

Retrieve deployment information for an active license key.

**Note:**
The license data is synchronized from a third-party system and may be delayed by up to 24 hours.

### Product Mapping

| Licensed Product Id | Product Name | Platform |
| --- | --- | --- |
| 1 | MetaDefender Core | Linux |
| 2 | MetaDefender Core | Windows |
| 3 | MetaDefender ICAP Server |  |
| 4 | MetaDefender Storage Security |  |
| 5 | MetaDefender Endpoint, OPSWAT Central Management |  |
| 6 | MetaDefender Email Gateway Security |  |
| 7 | MetaDefender Managed File Transfer |  |
| 8 | MetaDefender Drive Toolkit |  |
| 9 | MetaDefender Kiosk, MetaDefender Kiosk Windows |  |
| 11 | MetaDefender NetWall |  |
| 13 | MetaDefender Kiosk, MetaDefender Kiosk Linux |  |
| 15 | MetaDefender Industrial Firewall & IPS |  |
| 16 | MetaDefender Aether |  |
| 17 | My OPSWAT Central Management |  |
| 18 | MetaDefender OT Security |  |
| 19 | MetaDefender Software Supply Chain |  |
| 20 | MetaDefender Industrial Firewall |  |
| 21 | My OPSWAT On-premises |  |
| 22 | MetaDefender OT Access On-premises |  |

**Rate Limit Note**: The API rate limit is set to **10** requests per minute per organization.

Auth bearerAuthQuery String

| activation_key | string | The activation key string |  |
| --- | --- | --- | --- |
| product_id | integer | Licensed Product Id |  |

GET /portal/product/license/active-deploymentscURLRequestRequestsnet/httpGuzzleHttpClientOkHttpResponses application/json 200

Successfully retrieved deployment information

| object | object | Response containing deployment information for an active license key. |  |
| --- | --- | --- | --- |
| success | boolean | Indicates whether the request was successful. |  |
| data8 fields | object | License and deployment details. |  |
| license_key | string | License key string. |  |
| note | string | Optional note associated with the license. |  |
| type | string | Type of the license key.  Enum: `PURCHASED`,`EVALUATED` |  |
| expiry | date | Expiration date of the license. |  |
| product | string | Product associated with the license. |  |
| platform | string | Supported platforms of the license. |  |
| generated_at | date-time | Timestamp when this data was generated. |  |
| deployments5 fields | array[object] | List of deployments associated with the license. |  |
| deployment_id | string | Unique deployment identifier. |  |
| description | string | Deployment note. |  |
| expiration | date | Deployment expiration date. |  |
| activated_at | date-time | Activation timestamp. |  |
| quantity | integer | Number of activations. |  |

400

Validation Error

401

Unauthorized - invalid or missing token

403

Forbidden - insufficient permissions

404

Active license key / Product id not found

429

Rate limit exceeded. Retry after the specified time.

500

Internal server error occurred

 Response
