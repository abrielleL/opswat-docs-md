<!-- source: https://www.opswat.com/docs/mdmft/configuration/mft-integrate-microsoft-entra-id -->

# Microsoft Entra ID

Summarize Page    Connect to Cursor Connect to VS Code

Below is a step-by-step guide on integrating *Microsoft Azure Active Directory* (now Microsoft Entra ID) with MetaDefender Managed File Transfer™ using the OpenID Connect protocol.

Info

**Prerequisites**: An Entra Tenant (quick guide: <https://learn.microsoft.com/en-us/entra/identity-platform/quickstart-create-new-tenant> )

Info

*Microsoft Azure with Active Directory* **name changed** **to** **Microsoft Entra ID***.*

Credentials and other sensitive information are blurred in the below examples for security purposes.

### [Register Application in Microsoft Entra ID](/docs/mdmft/configuration/mft-integrate-microsoft-entra-id#register-application-in-microsoft-entra-id)

1. Sign in to Microsoft Entra ID and navigate to the admin dashboard.
2. Go to "App registrations" and select "New registration."

3. Configure the application settings:

   1. Provide a name for the application, e.g., “OPSWAT Managed File Transfer.”
   2. Configure the Redirect URL (`https://host:port/vault_rest/authenticate-sso`), which can also be found in MetaDefender Managed File Transfer™ → "Settings" → "Authentication" → "Single Sign-On" after filling in "IP Address or Domain."

Warning

Microsoft Entra ID only supports HTTPS protocol for redirect URI.

4. Record the "Application (client) ID" and "Directory (tenant) ID."

### [Generate Secret Key for Entra ID SSO](/docs/mdmft/configuration/mft-integrate-microsoft-entra-id#generate-secret-key-for-entra-id-sso)

Go to "Certificates & Secrets" and generate a new "client secret" string (also referred to as an "application password"). Record the client secret. Repeat if necessary.

Warning

Client secrets will be hidden and invisible after generation. A new secret will need to be generated.

### [Configure Managed File Transfer for Entra ID SSO](/docs/mdmft/configuration/mft-integrate-microsoft-entra-id#configure-managed-file-transfer-for-entra-id-sso)

Configure MetaDefender Managed File Transfer SSO using the above information.

1. Go to MetaDefender Managed File Transfer web console and navigate to "Settings" **→ "**Authentication" **→** "Single Sign-On."
2. Turn on "Enable Single Sign-On."
3. Disable "Ignore Certificate Issues," as Entra ID will provide a trusted certificate.
4. Turn on "Load User Profile" to allow MetaDefender Managed File Transfer™ to acquire the following claims:

   - name
   - email
   - preferred_username
   - given_name
   - family_name
   - phone_number
5. Set the "Authority" to the Microsoft Azure AD URL. This URL can be found in the Azure AD dashboard under application endpoints. The format is:
6. `https://login.microsoftonline.com/{directory (tenant) ID}/v2.0`
7. Set the "IP Address or Domain" to the location of the Managed File Transfer instance. Once this information is provided, Managed File Transfer will automatically generate the Redirect URI.

8. Use the "Redirect URI" in Azure AD Application Settings (step 3) - This field is auto-generated.
9. Copy the "Entra ID Application (client) ID" (step 4) into the "Client ID" field.
10. Copy the "Entra ID Client secret -> Value" (step 5) into the "Client Secret" field.
11. For "Administrator Emails," enter a list of emails for Microsoft Entra ID users who should have administrative rights in MetaDefender Managed File Transfer™. MetaDefender Managed File Transfer™ will compare the email of users logging in from Microsoft Entra ID against the provided list to determine administrative rights.
12. Additional integration scopes are not required.
13. Microsoft Entra ID requires adding two additional endpoints:

    1. `https://login.microsoftonline.com/{Directory (tenant) ID}/`
    2. `https://graph.microsoft.com/oidc/userinfo`

14. Review the final configuration.
15. Once all configurations are complete, click "Update."

### [Log in as an Entra Organization Admin](/docs/mdmft/configuration/mft-integrate-microsoft-entra-id#log-in-as-an-entra-organization-admin)

Depending on the Entra ID configuration, an organization admin should approve/allow a new application beforehand.

Log in to Managed File Transfer SSO with the Entra ID administrative account, and accept the newly created application.

### [Testing the Integration](/docs/mdmft/configuration/mft-integrate-microsoft-entra-id#testing-the-integration)

1. Log out of MetaDefender Managed File Transfer.
2. A new "Sign In with SSO" button will appear on the login page.

3. Click "Sign In with SSO" to be redirected to Microsoft Entra ID for login. Once logged in, you will be redirected back to MetaDefender Managed File Transfer.
