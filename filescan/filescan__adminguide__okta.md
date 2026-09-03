<!-- source: https://www.opswat.com/docs/filescan/adminguide/okta -->

# Okta

Below you can find a step by step tutorial on how to integrate Okta with MetaDefender Aether using the OpenID Connect protocol.

## [Prepare the MetaDefender Sandbox for the OAuth integration](https://www.opswat.com/docs/filescan/adminguide/microsoft-entra#prepare-the-metadefender-sandbox-for-the-oauth-integration)

Let’s prepare the SSO settings in MetaDefender Aether as follows:

1. Go to **Admin panel >** **Settings > Authentication** on MetaDefender Aether page.
2. Click on **+ Add Service** button
3. Fill in the **Name** (e.g. "Okta") and **Service key** (should be **"okta**") values
4. **Do NOT click Save yet**; the remaining values will be filled in later
5. Please note down the **Redirect** **URI** at the bottom of the form

## [Register application in Okta](https://www.opswat.com/docs/filescan/adminguide/microsoft-entra#register-application-in-microsoft-entra-id)

1. Sign into Okta and navigate to admin dashboard
2. Go to **Applications** and select **Create App Integration**

Please copy the Client ID and client secrets from the newly created application.

## [Configure MetaDefender Aether for Okta SSO](https://www.opswat.com/docs/filescan/adminguide/microsoft-entra#configure-metadefender-sandbox-for-entra-id-sso)

Let’s finish the configuration of the MetaDefender Aether SSO settings using the information collected above:

1. Go back to the MetaDefender Aether UI
2. Fill in the form details for the newly created service using the reference below
3. **Save the form**

| Field | Description | Example |
| --- | --- | --- |
| Name | Integration name | Okta |
| Home page | First page after log in | <https://sandbox.mycompany.com> |
| Client ID | Application (client) ID , comes from Okta | 1234-5678-90123-4567 |
| Client secret | Comes from Okta | abcd1234!%# |
| Order | The order of authentication can be specified | 1 |
| Active | Enable or disable the authentication | on |
| Use state | **Generate and validate OIDC state parameter - must be enabled for Okta** | **on** |
| Base URL | Service base url | [**https://mycompany.okta.com**](https://login.microsoftonline.com) |
| Path | Service URL postfix. Format should be: | /.well-known/openid-configuration |
| Service Key | Is used internally in our app and in redirect URI | okta |

## [Testing the integration](https://www.opswat.com/docs/filescan/adminguide/microsoft-entra#testing-the-integration)

1. Log out of MetaDefender Aether
2. You will notice that there is a new **Sign In with Okta** button on the login page

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
