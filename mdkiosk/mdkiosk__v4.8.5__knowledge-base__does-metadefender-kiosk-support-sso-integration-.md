<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/does-metadefender-kiosk-support-sso-integration- -->

# Does MetaDefender Kiosk support SSO Integration?

Yes. MetaDefender Kiosk supports integration with Identity Providers (IdPs) for Single Sign-On (SSO) authentication.

There are two main areas where this integration applies:

## [**Login to the Web Management Console:**](/docs/mdkiosk/v4.8.5/knowledge-base/does-metadefender-kiosk-support-sso-integration-#login-to-the-web-management-console)

The Web Management Console allows administrators to configure the MetaDefender Kiosk settings. This is separate from the kiosk application itself (used for media scanning).

**Steps:**

1. Navigate to **User Management** > **User Directories**
2. Add a new **Microsoft Entra ID** or **SAML Directory**
3. Configure the directory details and test the connection.

**Supports:**

- Microsoft Entra ID
- SAML 2.0

**Additional resources:**

- [Login Settings](https://www.opswat.com/docs/mdkiosk/operating/login-settings)

## [**Login to the Kiosk Application itself:**](/docs/mdkiosk/v4.8.5/knowledge-base/does-metadefender-kiosk-support-sso-integration-#login-to-the-kiosk-application-itself)

In the Workflow Settings, the login method specifies how end-users sign in before they can perform media processing tasks

**Steps:**

1. Navigate to **Workflows** > **Set Default Login Method**
2. Select the **Single-Sign On** login method
3. Configure the connection with the IdP Server
4. The connection will be tested automatically

**Supports:**

- OIDC
- SAML

**Additional resources:**

- [Configuring ADFS as SAML Identity Provider](https://www.opswat.com/docs/mdkiosk/advanced-deployment/configuring-adfs-as-saml-identity-provider)
- [Microsoft Entra ID Integration (SAML)](https://www.opswat.com/docs/mdkiosk/advanced-deployment/microsoft-entra-id-integration)
- [Microsoft Entra ID Integration (OIDC)](https://www.opswat.com/docs/mdkiosk/advanced-deployment/microsoft-entra-id-integration--oidc-)

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
