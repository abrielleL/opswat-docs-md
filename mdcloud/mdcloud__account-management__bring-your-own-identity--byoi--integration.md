<!-- source: https://www.opswat.com/docs/mdcloud/account-management/bring-your-own-identity--byoi--integration -->

# Bring Your Own Identity (BYOI) Integration

This article applies to MetaDefender Cloud deployed at <https://metadefender.opswat.com/>

If your organization already uses Single Sign-On (SSO) services for user authentication before accessing your cloud services, you can integrate with OPSWAT's IDaaS to prevent unauthorized access to your cloud applications. OPSWAT currently supports leading Identity Providers, including Okta and Entra ID (Azure), as long as they support the Security Assertion Markup Language (SAML) protocol.

Info

Please note, custom IDP integration disables any previously enabled Multi-Factor Authentication within OPSWAT.

### [How to Integrate with OPSWAT's IDaaS](/docs/mdcloud/account-management/bring-your-own-identity--byoi--integration#how-to-integrate-with-opswats-idaas)

Integration between your organization's identity provider and OPSWAT’s service requires an exchange of key configuration details.

**Step 1: Request Integration Support** To begin the integration process, please open a support case with OPSWAT Support and request SSO integration assistance. Our team will guide you through the steps and help with the configuration.

**Step 2: Exchange Information**

OPSWAT → Organization:

- IdP Start URL: Provided for SP-Initiated SSO workflows.
- Assertion Consumer Service (ACS) URL: A unique post-back SSO URL for each application. OPSWAT uses this URL to forward the authentication message from your IdP to the appropriate OPSWAT service after verification.

Organization → OPSWAT:

- Customer Company Name and Domain
- Identity Provider (IdP) metadata file (*.xml), exported from your IdP’s settings console
- Confirmation that the following SAML attributes are configured:

  - NameID Format: Email Address
  - Attribute Statement (included in the SAML token):

    - firstName
    - lastName
    - emailAddress

**Step 3: Authentication Flow**

Once the integration is successfully completed and confirmed by an OPSWAT account representative, users attempting to log in to MetaDefender Cloud will be redirected to <https://id.opswat.com/> for credential verification. After successful authentication, users will gain access to MetaDefender Cloud services seamlessly.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
