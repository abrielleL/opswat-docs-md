<!-- source: https://www.opswat.com/docs/mdcore/configuration/single-sign-on--sso- -->

# Single Sign-On (SSO)

MetaDefender Core supports Single Sign-On (SSO) authentication where users can configure the product to integrate with various widely used Identity Providers (IdP) on both SAML 2.0 and OpenID Connect protocols.

Info

MetaDefender Core consistently verifies the time frame validity of the sign-in session, so the system time on the device running MetaDefender Core needs to be configured accurately.

Learn more integration guidelines with the following specific IdPs.

| IdP | OIDC | SAML |
| --- | --- | --- |
| Amazon Cognito | [Supported](/docs/mdcore/configuration/aws-cognito-oidc-single-sign-on) |  |
| ForgeRock | Soon | [Supported](/docs/mdcore/configuration/forgerock-saml-single-sign-on) |
| Keycloak |  | [Supported](/docs/mdcore/configuration/keycloak-saml-single-sign-on) |
| Microsoft Active Directory Federation Services (ADFS) | [Supported](/docs/mdcore/configuration/adfs-oidc-single-sign-on) | [Supported](/docs/mdcore/configuration/adfs-saml-single-sign-on) |
| Microsoft Entra ID | [Supported](/docs/mdcore/configuration/entra-oidc-single-sign-on) | [Supported](/docs/mdcore/configuration/entra-saml-single-sign-on) |
| Okta | [Supported](/docs/mdcore/configuration/okta) | [Supported](/docs/mdcore/configuration/okta) |
| OneLogin | [Supported](/docs/mdcore/configuration/onelogin-oidc-single-sign-on) | [Supported](/docs/mdcore/configuration/onelogin-saml-single-sign-on) |
| Ping Identity - PingFederate | [Supported](/docs/mdcore/configuration/pingfederate-oidc-single-sign-on) | [Supported](/docs/mdcore/configuration/pingfederate-saml-single-sign-on) |
| Ping Identity - PingOne | [Supported](/docs/mdcore/configuration/pingone-oidc-single-sign-on) | [Supported](/docs/mdcore/configuration/pingone-saml-single-sign-on) |
