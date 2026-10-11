<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/configuration/single-sign-on--sso- -->

# Single Sign-On (SSO)

View as Markdown Ask ChatGPT about this page Ask Claude about this page

MetaDefender Core supports Single Sign-On (SSO) authentication where users can configure the product to integrate with various widely used Identity Providers (IdP) on both SAML 2.0 and OpenID Connect protocols.

Info

MetaDefender Core consistently verifies the time frame validity of the sign-in session, so the system time on the device running MetaDefender Core needs to be configured accurately.

Learn more integration guidelines with the following specific IdPs.

| IdP | OIDC | SAML |
| --- | --- | --- |
| Amazon Cognito | [Supported](/docs/mdcore/v5.22.1/configuration/aws-cognito-oidc-single-sign-on) |  |
| ForgeRock | Soon | [Supported](/docs/mdcore/v5.22.1/configuration/forgerock-saml-single-sign-on) |
| Keycloak |  | [Supported](/docs/mdcore/v5.22.1/configuration/keycloak-saml-single-sign-on) |
| Microsoft Active Directory Federation Services (ADFS) | [Supported](/docs/mdcore/v5.22.1/configuration/adfs-oidc-single-sign-on) | [Supported](/docs/mdcore/v5.22.1/configuration/adfs-saml-single-sign-on) |
| Microsoft Entra ID | [Supported](/docs/mdcore/v5.22.1/configuration/entra-oidc-single-sign-on) | [Supported](/docs/mdcore/v5.22.1/configuration/entra-saml-single-sign-on) |
| Okta | [Supported](/docs/mdcore/v5.22.1/configuration/okta) | [Supported](/docs/mdcore/v5.22.1/configuration/okta) |
| OneLogin | [Supported](/docs/mdcore/v5.22.1/configuration/onelogin-oidc-single-sign-on) | [Supported](/docs/mdcore/v5.22.1/configuration/onelogin-saml-single-sign-on) |
| Ping Identity - PingFederate | [Supported](/docs/mdcore/v5.22.1/configuration/pingfederate-oidc-single-sign-on) | [Supported](/docs/mdcore/v5.22.1/configuration/pingfederate-saml-single-sign-on) |
| Ping Identity - PingOne | [Supported](/docs/mdcore/v5.22.1/configuration/pingone-oidc-single-sign-on) | [Supported](/docs/mdcore/v5.22.1/configuration/pingone-saml-single-sign-on) |
