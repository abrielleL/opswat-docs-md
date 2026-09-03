<!-- source: https://www.opswat.com/docs/macloud-sdp/developer-guide/authentication -->

# Authentication

MetaDefender IT-OT Access APIs use the [OAuth 2.0](http://oauth.net/2) protocol for authentication and authorization. The simplicity of OAuth 2.0 allows developers to start using and developing against MetaDefender IT-OT Access APIs almost immediately, the only thing which has to be done, before starting integration, is to [register your application](https://console.metaaccess-b.opswat.com/o/app/register) and obtain an unique set of *Client Key* and *Client Secret* from MetaDefender IT-OT Access [OAuth Portal](https://console.metaaccess-b.opswat.com/o/app).

This step provides you ways to authorize with our platform to archive an access token which is required in each API as a parameter for security and authentication reasons.

We support authorization through the Client Credentials grant type.

Info

Note that the URL we used in this document is documented based on MetaDefender IT-OT Access Tenant B. If you are using different MetaDefender IT-OT Access Tenant, you should replace the MetaDefender IT-OT Access URLs accordingly

## [Client Credentials grant type - No log in required from a user](https://docs.opswat.com/macloud-sdp/developer-guide/authentication#client-credentials-grant-type---no-log-in-required-from-a-user)

Client credentials grant type is beneficial for use cases such as service calls or calls on behalf of the user who created the client application and has implicit access to the resources.

The client credentials grant type must be used by only confidential clients and has to be always used through a secure connection.

curl -X POST 'https://gears.opswat.com/o/oauth/token' -d 'client_id=YOUR_CLIENT_KEY&client_secret=YOUR_CLIENT_SECRET&grant_type=client_credentials'
## [Request Example](https://docs.opswat.com/macloud-sdp/developer-guide/authentication#request-example)

curl -X POST https://gears.opswat.com/o/oauth/token -d 'grant_type=client_credentials&client_id=TestnFZFEjr1zCsicMWpAA&client_secret=E9SRTVJ93AASEWVXOJ3PRY1K7KFDEEQ679IX5SJMEMG2Y8AE'
## [Response Example](https://docs.opswat.com/macloud-sdp/developer-guide/authentication#response-example)

{
"access_token": "TEST7P9ZMJ2LBF8AMOMJLFNPMMLO953AVQ4C9YFF52R64567",
"token_type": "bearer",
"expires_in": 43199,
"scope": "read",
"client_id": "2YotnFZFEjr1zCsicMWpAA"
}

If you provide invalid client credentials, the server will return the following error:

{
"error": "invalid_client",
"error_description": "Bad client credentials"
}
