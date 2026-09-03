<!-- source: https://www.opswat.com/docs/mdmft/configuration/trusted-network-automatic-authentication -->

# Trusted Network Automatic Authentication

Summarize Page    Connect to Cursor Connect to VS Code

Trusted Network List allows MetaDefender Managed File Transfer™ to automatically handle authentication using either Single Sign-On (SSO) or Integrated Windows Authentication (IWA). When a user accesses the MetaDefender Managed File Transfer™ login page, they are seamlessly redirected to the SSO provider’s login page or authenticated through IWA, depending on the configuration.

### [Single Sign-On](/docs/mdmft/configuration/trusted-network-automatic-authentication#single-sign-on)

Enabling this option will automatically redirect users to the SSO provider for login when they access the MetaDefender Managed File Transfer™ login page.

### [Integrated Windows Authentication](/docs/mdmft/configuration/trusted-network-automatic-authentication#integrated-windows-authentication)

When this option is enabled, authentication starts automatically. If it succeeds, the user is redirected to My Files. if it fails, an error message is displayed.

Info

When using an Incognito/Private browsing window, the browser cannot reuse the user's existing Windows session. In this case, the user will be prompted to enter their PC credentials manually for authentication.
