<!-- source: https://www.opswat.com/docs/mdcloud/account-management/oauth -->

# Secure API Authentication Using OAuth

OAuth is available to both Organization and Individual Users.

## [Why OAuth?](/docs/mdcloud/account-management/oauth#why-oauth)

API Keys are used to authenticate users. While they are a good mechanism for that, adding OAuth in addition to authenticate user requests makes the requests even more secure.

## [How OAuth Works](/docs/mdcloud/account-management/oauth#how-oauth-works)

Let's start with some terminology:

**Client Credentials Grant**

_MD Cloud API _- Meta defender cloud REST API *Client APP* - any application that requires access to our MD Cloud API resources *OAuth Tenant* - Dedicated Authorization Server for MD Cloud API

Here are the steps (plus a diagram below) that details how the OAuth authentication mechanism works:

1. The Client APP requests an access token from our OAuth Tenant
2. The OAuth Tenant validates the Application Id and Application Secret and generates an Access token
3. The OAuth Tenant sends the token information back to the Client APP
4. The Client APP can make requests to our MD Cloud API using the authorization token
5. The MD Cloud API verifies the JWT token
6. If the token is valid the MD Cloud API can process the request

## [How to Set Up OAuth in the MetaDefender Cloud UI](/docs/mdcloud/account-management/oauth#how-to-set-up-oauth-in-the-metadefender-cloud-ui)

## [Example Code](/docs/mdcloud/account-management/oauth#example-code)

Below are some code snippets to help you get started using OAuth

#### [Authentication Request](/docs/mdcloud/account-management/oauth#authentication-request)

`POST https://api.metadefender.com/v4/oauth2/token`

BashCopyHeaders:
- Authorization: Basic BASE64(<CLIENT_ID>:<CLIENT_SECRET>)

- CLIENT_ID: application client id
- CLIENT_SECRET_ : application client secret

#### [Authentication Response](/docs/mdcloud/account-management/oauth#authentication-response)

BashCopy{
"access_token": string, // a valid access token
"expires_in": number, // time in seconds,
"token_type": string, // Set to "Bearer"
}
#### [API Request](/docs/mdcloud/account-management/oauth#api-request)

`https://api.metadefender.com/v4/<endpoint>`

BashCopyHeaders:
- Authorization: Bearer <ACCESS_TOKEN>
#### [API Error Response](/docs/mdcloud/account-management/oauth#api-error-response)

**Expired token**

If you receive an expired token response please submit an authentication request again to receive a new token

BashCopy{
"error": {
"code": 401009,
"messages": [
"OAuth token has expired"
]
}
}

**Invalid token**

BashCopy{
"error": {
"code": 401010,
"messages": [
"OAuth token is invalid"
]
}
}
## [How to Set Up OAuth in the MetaDefender Cloud UI for Individuals](/docs/mdcloud/account-management/oauth#how-to-set-up-oauth-in-the-metadefender-cloud-ui-for-individuals)

First log into your account at metadefender.opswat.com and navigate to the security page

From there, you can then name your first OAuth client. Once you have named your OAuth client, click the "add" button at the right of the text box

Once you have added your OAuth client name, you will be given a client ID.

You can also remove OAuth clients if necessary by clicking the checkbox to the right of your client information and then clicking the red "Remove" button as shown below:

## [How to Set Up OAuth in the MetaDefender Cloud UI for Organizations](/docs/mdcloud/account-management/oauth#how-to-set-up-oauth-in-the-metadefender-cloud-ui-for-organizations)

First log into your account at **metadefender.opswat.com/settings/profile**

Click on **Organization Settings** then click on __Organization __ -> **Security**

__ __

You can also remove OAuth clients if necessary by clicking the checkbox to the right of your client information and then clicking the red "Remove" button.
