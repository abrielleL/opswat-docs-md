<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/configuration/microsoft-entra-id--saml- -->

# Microsoft Entra ID (SAML)

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
## [Prerequisites](/docs/mdmft/v3.11.5/configuration/microsoft-entra-id--saml-#prerequisites)

- Access to the Microsoft Entra ID (Azure AD) Administration dashboard
- Administrative privileges to create and configure Enterprise Applications
- Your application's public URL

## [Step 1 — Navigate to Identity](/docs/mdmft/v3.11.5/configuration/microsoft-entra-id--saml-#step-1--navigate-to-identity)

Open the **Administration dashboard** and navigate to the **Identity** section.

## [Step 2 — Open Enterprise Applications](/docs/mdmft/v3.11.5/configuration/microsoft-entra-id--saml-#step-2--open-enterprise-applications)

In the left-hand navigation menu, select **Enterprise applications**.

## [Step 3 — Create a New Application](/docs/mdmft/v3.11.5/configuration/microsoft-entra-id--saml-#step-3--create-a-new-application)

Click the **+ New application** button at the top of the Enterprise applications view.

## [Step 4 — Create Your Own Application](/docs/mdmft/v3.11.5/configuration/microsoft-entra-id--saml-#step-4--create-your-own-application)

In the App Gallery, click **Create your own application**.

## [Step 5 — Configure the Application](/docs/mdmft/v3.11.5/configuration/microsoft-entra-id--saml-#step-5--configure-the-application)

1. Enter a **name** for your application.
2. Select **"Integrate any other application you don't find in the gallery (Non-gallery)"**.
3. Click **Create**.

## [Step 6 — Assign Users and Groups](/docs/mdmft/v3.11.5/configuration/microsoft-entra-id--saml-#step-6--assign-users-and-groups)

In the application overview, select **Users and groups** from the left-hand menu. Add the users and groups that should have access to the application.

## [Step 7 — Select SAML as the SSO Method](/docs/mdmft/v3.11.5/configuration/microsoft-entra-id--saml-#step-7--select-saml-as-the-sso-method)

In the application overview, select **Single sign-on** from the left-hand menu, then choose **SAML** as the sign-on method.

## [Step 8 — Edit Basic SAML Configuration](/docs/mdmft/v3.11.5/configuration/microsoft-entra-id--saml-#step-8--edit-basic-saml-configuration)

In the **SAML-based Sign-on** view, locate the **Basic SAML Configuration** section and click **Edit** .

## [Step 9 — Enter SAML Configuration Values](/docs/mdmft/v3.11.5/configuration/microsoft-entra-id--saml-#step-9--enter-saml-configuration-values)

Provide the following values:

- **Identifier (Entity ID)**: A unique identifier for your application. It can be any string, but using a URL format is recommended.
- **Reply URL (Assertion Consumer Service URL)**: `https://<your-application-url>/vault_rest/authenticate-saml`

## [Step 10 — Save the Configuration](/docs/mdmft/v3.11.5/configuration/microsoft-entra-id--saml-#step-10--save-the-configuration)

Click **Save** to apply the Basic SAML Configuration.

## [Step 11 — Configure Attributes (Optional)](/docs/mdmft/v3.11.5/configuration/microsoft-entra-id--saml-#step-11--configure-attributes-optional)

If needed, configure **Attribute Mapping** and **User Attributes & Claims** to match your application's requirements.

## [Step 12 — Copy the Login URL](/docs/mdmft/v3.11.5/configuration/microsoft-entra-id--saml-#step-12--copy-the-login-url)

In the **Set up** section, copy the **Login URL**. This value will be required when configuring your application to authenticate using Entra ID SAML.

## [Step 13 — Enable SSO in MetaDefender Managed File Transfer™](/docs/mdmft/v3.11.5/configuration/microsoft-entra-id--saml-#step-13--enable-sso-in-product_name)

Open Settings/Authentication sources, choose the Single Sign-On tab and enable SSO.

## [Step 14 — Configure SAML Authority](/docs/mdmft/v3.11.5/configuration/microsoft-entra-id--saml-#step-14--configure-saml-authority)

Select SAML 2.0 and provide a custom provider name and fill in login url from Step 12 into the Authority field.

## [Step 15 — Fill in IP Address or Domain, Client ID](/docs/mdmft/v3.11.5/configuration/microsoft-entra-id--saml-#step-15--fill-in-ip-address-or-domain-client-id)

This IP Address or Domain field is to help generating the correct redirect uri, which we already provided in previous steps.

The client id is the value from Step 9.

## [Step 16 — Save configuration](/docs/mdmft/v3.11.5/configuration/microsoft-entra-id--saml-#step-16--save-configuration)

Click Update to save the configuration, Entra ID SAML based SSO is now configured and can be utilized during login.
