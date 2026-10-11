<!-- source: https://www.opswat.com/docs/filescan/3.2.0/adminguide/microsoft-entra -->

# Microsoft Entra

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Below you can find a step-by-step tutorial on how to integrate Microsoft Azure Active Directory with MetaDefender Aether using the OpenID Connect protocol.

Info

**Prerequisites**: An Entra Tenant (quick guide: <https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-create-new-tenant> )

## [Prepare the MetaDefender Sandbox for the OAuth integration](/docs/filescan/3.2.0/adminguide/microsoft-entra#prepare-the-metadefender-sandbox-for-the-oauth-integration)

Let’s prepare MetaDefender Aether SSO settings as follows:

1. Go to **Admin panel >** **Settings > Authentication** on the MetaDefender Aether page.
2. Click on **+ Add Service** button
3. Fill in the **Name** (e.g., "MS Entra") and **Service key** (should be **"entra**") values
4. **Do NOT click Save yet**; the remaining values will be filled in later
5. Please note down the **Redirect** **URI** at the bottom of the form

## [Register application in Microsoft Entra ID](/docs/filescan/3.2.0/adminguide/microsoft-entra#register-application-in-microsoft-entra-id)

1. Sign into Microsoft Entra ID and navigate to the admin dashboard
2. Go to **App registrations** and select **New registration**

3. Let’s configure the application settings.

   1. Give the application a name. for example, “MetaDefender Aether”. In the following examples, we will use "OPSWAT Sandbox - Staging" as the application name
   2. Configure the **Redirect URI** (`https://<host>:<port>/`auth/signin/<service_key>/callback) - Use the value you noted down in the previous section.

Warning

*Microsoft Entra ID* supports only **HTTPS** protocol for redirect URI

4. Note down **Application (client) ID** and **Directory (tenant) ID** of the newly created application as it will be needed in a later step

## [Generate Secret key for Entra ID SSO](/docs/filescan/3.2.0/adminguide/microsoft-entra#generate-secret-key-for-entra-id-sso)

Go to **Certificates & Secrets** and generate a new **client secret** string (also referred to as an application password). Record the client secret.

Warning

You will not be able to retrieve **client secret** at a later time because it will be hidden. You need to generate a new secret in this case.

## [Configure MetaDefender Sandbox for Entra ID SSO](/docs/filescan/3.2.0/adminguide/microsoft-entra#configure-metadefender-sandbox-for-entra-id-sso)

Let’s finish the configuration of the MetaDefender Aether SSO settings using the information collected above:

1. Go back to the MetaDefender Aether UI
2. Fill in the form details for the newly created service using the reference below
3. **Save the form**

| Field | Description | Example |
| --- | --- | --- |
| Name | Integration name | MS Entra |
| Home page | First page after log in | <https://sandbox.mycompany.com> |
| Client ID | Application (client) ID , comes from Entra | 1234-5678-90123-4567 |
| Client secret | Comes from Entra | abcd1234!%# |
| Order | The order of authentication can be specified | 1 |
| Active | Enable or disable the authentication | on |
| Base URL | Service base url | [**https://login.microsoftonline.com**](https://login.microsoftonline.com) |
| Path | Service URL postfix. Format should be:  **/<tenant_id>/v2.0/.well-known/openid-configuration**  Tenant id comes from Entra: Directory (tenant) id | **/*12314*/v2.0/.well-known/openid-configuration** |
| Service Key | Is used internally in our app and in redirect URI | entra |

## [Login as an Entra organization admin](/docs/filescan/3.2.0/adminguide/microsoft-entra#login-as-an-entra-organization-admin)

Depending on Entra ID configuration, and organization admin should approve/allow a new application beforehand.

Log in to MetaDefender Aether SSO with the Entra ID administrative account and accept the newly created application:

## [Testing the integration](/docs/filescan/3.2.0/adminguide/microsoft-entra#testing-the-integration)

1. Log out of MetaDefender Aether
2. You will notice that there is a new **Sign In with SSO** button on the login page

3. Click Sign In with SSO. You should be redirected to Microsoft Entra ID to login. Once logged in, you will be redirected back to MetaDefender Aether and automatically logged in.

Warning

In some cases, the following warning might be displayed even though the login is successful. This is a known issue and will be fixed in the next version of the product.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
