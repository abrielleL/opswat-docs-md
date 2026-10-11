<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/configuration/sso-multiple-login-urls -->

# Multiple Login URLs

View as Markdown Ask ChatGPT about this page Ask Claude about this page
### [Overview](/docs/mdcore/v5.22.1/configuration/sso-multiple-login-urls#overview)

MD Core now supports **multiple** login/redirect URLs as part of the SSO authentication flow. This enhancement allows deployments spanning multiple domains or client applications to dynamically route users to the correct redirect endpoint during login.

### [Key benefits](/docs/mdcore/v5.22.1/configuration/sso-multiple-login-urls#key-benefits)

- Supports multi-domain SSO scenarios.
- Enables multiple client application redirects.
- Improves authentication flexibility without custom logic.

Info

- The URLs must be registered on both MD Core and the Identity Provider.
- Unregistered redirect URLs are rejected for security reasons.
### [Configuration Steps](/docs/mdcore/v5.22.1/configuration/sso-multiple-login-urls#configuration-steps)

1. Sign in to the MD Core dashboard using an administrator account.
2. Go to `User Management` > `Directories`.
3. Click `Add Directory` , or choose an existing SSO directory to modify.
4. If you are adding a new directory, select **OIDC** or **SAML** as `Directory Type` and fill in the required configuration fields.
5. Under the `Host or IP` section, enter your login URL and click `Add` .
6. In your Identity Provider configuration panel, add the **same login URL** as the **redirect/callback URL**.
7. Repeat steps 5–6 for any additional login URLs you need to support.
