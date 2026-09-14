<!-- source: https://www.opswat.com/docs/cm/user-management/through-your-own-idp -->

# Through your own IdP

> **Info**
>
> Provision users through your own IdP is only available for Enterprise My OPSWAT Central Management customers.

My OPSWAT Central Management offers an integration with a 3rd-party Single Sign-on Service (SSO). This enables an account to provision new users to manage your account. When a user logs into the My OPSWAT Central Management console through your own SSO service, My OPSWAT Central Management will provision that user as a read-only user on your account. You can update the user's role later.

My OPSWAT Central Management uses the secure and widely adopted industry standard Security Assertion Markup Language 2.0 (SAML 2.0), so that you can integrate easily with any large identity provider that supports SAML 2.0.

To get started, go to your identity provider's site and follow the instructions to configure a SSO application for My OPSWAT Central Management.

Note** My OPSWAT Central Management** **only accepts username as email address, so you have to configure user identify on IdP as email.**

To integrate My OPSWAT Central Management with your own SSO service,

1. Log into the My OPSWAT Central Management console with admin permissions
2. Navigate to User Management > SSO > Console Authentication
3. On the Console tab, enable "Enable Single Sign On"
4. Enter an IdP Name. This is for your reference
5. Click the **Choose File** button to upload an IdP X.509 certificate .pem file that you got from the Identity Provider.
6. Enter Issuer you got earlier from the identity provider
7. Enter the IdP SSO URL you got earlier from the identity provider
8. Enter the IdP Log out URL and Error URL you got earlier from the identity provider if any
9. Click the **Save** button.
10. After you save your changes successfully, My OPSWAT Central Management generates a *My OPSWAT Central Management Login URL* and *My OPSWAT Central Management Entity ID.* In your identity provider, open the SSO application for My OPSWAT Central Management and update the following values: Postback SSO URL (also called the Assertion Consumer Service URL) with *My OPSWAT Central Management Login URL* and SP Entity ID with *My OPSWAT Central Management Entity ID*.
11. Create IdP Mappings from your external provider in My OPSWAT Central Management (more information [here)](https://www.opswat.com/docs/cm/secure-access-solution/introduction) and assign users/groups you allow them to log into My OPSWAT Central Management console to that application on your IdP. Note that, you don't need to invite those users to My OPSWAT Central Management console under User Management; whenever they log into My OPSWAT Central Management console, their account will be set up and assigned to your account as a Read-Only user. You can update their role after that.

Note You can import information from step #5 through #8 from the IdP metadata file that you got earlier from the identity provider if it's available

You can find detailed setup guideline for some identity providers below:

- [Provision console users via Microsoft EntraID](https://www.opswat.com/docs/cm/user-management/with-azure)
- [Provision console users via Okta](https://www.opswat.com/docs/cm/user-management/with-okta)
- [Provision console users via PingOne](https://www.opswat.com/docs/cm/user-management/with-pingone)
- [Provision console users via ADFS](https://www.opswat.com/docs/cm/user-management/with-adfs)
