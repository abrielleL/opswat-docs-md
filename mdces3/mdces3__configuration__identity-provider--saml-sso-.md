<!-- source: https://www.opswat.com/docs/mdces3/configuration/identity-provider--saml-sso- -->

# Identity Provider (SAML SSO)

Summarize Page

**MetaDefender Cloud Email Security ™** uses **OPSWAT Single Sign-On (SSO)** as its default identity provider for user authentication.

## [Use your own Identity Provider](/docs/mdces3/configuration/identity-provider--saml-sso-#use-your-own-identity-provider)

For organizations that prefer to manage authentication through their own identity systems, **MetaDefender Cloud Email Security ™** supports custom Identity Provider (IdP) integration using the SAML 2.0 protocol.

This allows you to centralize authentication, enforce your organization’s security policies, and streamline user access management.

### [Prerequisites](/docs/mdces3/configuration/identity-provider--saml-sso-#prerequisites)

Before configuring a custom Identity Provider, ensure that:

- Your Identity Provider supports **SAML 2.0**
- You have administrative access to:

  - Your Identity Provider (e.g., Okta, Azure AD, etc.)
  - [My OPSWAT portal](https://my.opswat.com/)
- You are familiar with basic SAML configuration concepts (e.g., metadata, assertions, certificates)

### [Detailed Configuration Guide](/docs/mdces3/configuration/identity-provider--saml-sso-#detailed-configuration-guide)

For step-by-step instructions, refer to the official OPSWAT documentation:

[Bring Your Own Identity (BYOI) Integration Guide](https://www.opswat.com/docs/my/get-started/bring-your-own-identity-byoi-integration)
