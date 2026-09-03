<!-- source: https://www.opswat.com/docs/my/get-started/bring-your-own-identity-byoi-integration -->

# Bring Your Own Identity (BYOI) Integration

To provide your users with a seamless and secure login experience, OPSWAT SSO supports integration with your organization’s Single Sign-On (SSO), enabling your users to access OPSWAT services using their existing corporate credentials. OPSWAT currently supports leading Identity Providers, including Okta, Entra ID (Azure), etc., as long as they support the Security Assertion Markup Language (SAML) 2.0 protocol.

> **Warning**
>
> When your organization integrates its own SSO with OPSWAT SSO, the Multi-Factor Authentication settings configured within My OPSWAT Portal will not apply to your users. In this case, user authentication and MFA enforcement are managed entirely by your organization’s identity provider (IdP). We recommend ensuring that MFA is configured and enforced within your IdP to maintain the desired security level.

This guide walks you through the steps to connect your identity provider (IdP) with OPSWAT SSO. If your organization uses Okta or Microsoft Entra, follow the guides below

- [Set up SSO with Microsoft Entra](https://www.opswat.com/docs/my/get-started/set-up-sso-with-microsoft-entra)
- [Set up SSO with Okta](https://www.opswat.com/docs/my/get-started/set-up-sso-with-okta)

### How to Integrate with OPSWAT SSO

Integration between your organization's identity provider and OPSWAT’s service requires an exchange of key configuration details.

**Step 1: Create an application inside your IdP**

Log into your IdP as an administrator, follow your IdP guideline to add an application. During the process, you can use the below temporary information and update them later when OPSWAT provides:

- Entity ID : [https://id.opswat.com](https://id.opswat.com)
- ACS URL: [https://id-api.opswat.com/saml/acs/{opswat_will](https://id-api.opswat.com/saml/acs/%7Bopswat_will)_ provide}

And make sure that the following SAML attributes are configured:

- NameID Format: Email Address
- Attribute Statement (included in the SAML Assertion):
  - firstName
  - lastName
  - emailAddress

**Step 2: Request Integration Support**

Navigate to [Support ](https://my.opswat.com/support) in My OPSWAT Portal, submit a support case to request SSO integration and provide the below information.

- Company Name: your company name
- Domain name: your company name's domain name.
- Identity Provider (IdP) metadata file (*.xml), exported from the application you created in step 1 inside your IdP console
- OPSWAT will redirect users to your own IdP based on a specific domain or specific users. If you only wants to allow specific users to authenticate via your organization's IdP, please provide emails of those users.

**Step 3: Update the application settings in your IdP**

When OPSWAT receives all required information and has done set up your IdP inside OPSWAT SSO, OPSWAT Support will provide Entify ID and ACS URL for your IdP inside OPSWAT SSO. You need to use these information to update the application you created in step 1

**Step 4: Authentication Flow**

Once the integration is successfully completed, users attempting to log in to My OPSWAT Portal will be redirected to your Identity Provider for user authentication. Upon successful authentication, the user is redirected back to My OPSWAT Portal.
