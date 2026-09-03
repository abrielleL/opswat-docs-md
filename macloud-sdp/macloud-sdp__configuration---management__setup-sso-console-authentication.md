<!-- source: https://www.opswat.com/docs/macloud-sdp/configuration---management/setup-sso-console-authentication -->

# Setup SSO - Console Authentication

Provision users through your own IdP is only available for Enterprise MetaDefender IT Access customers.

MetaDefender IT Access offers an integration with a 3rd-party Single Sign-on Service (SSO). This enables an account to provision new users to manage your account. When a user logs into the MetaDefender IT Access console through your own SSO service, MetaDefender IT Access will provision that user as a read-only user on your account. You can update the user's role later.

MetaDefender IT Access uses the secure and widely adopted industry standard Security Assertion Markup Language 2.0 (SAML 2.0), so that you can integrate easily with any large identity provider that supports SAML 2.0.

To get started, go to your identity provider's site and follow the instructions to configure a SSO application for MetaDefender IT Access. **Note: that** **MetaDefender IT Access** **only accepts username as email address so that you have to configure user identify on IdP as email**

To integrate MetaDefender IT Access with your own SSO service,

1. Log into the MetaDefender IT Access console with admin permissions
2. Navigate to User Management > SSO > Console Authentication
3. On the Console tab, enable "Enable Single Sign On"
4. Enter an IdP Name. This is for your reference
5. Click the **Choose File** button to upload an IdP X.509 certificate .pem file that you got from the Identity Provider.
6. Enter Issuer you got earlier from the identity provider
7. Enter the IdP SSO URL you got earlier from the identity provider
8. Enter the IdP Log out URL and Error URL you got earlier from the identity provider if any
9. Click the **Save** button.
10. After you save your changes successfully, MetaDefender IT Access generates a MetaDefender IT Access Login URL, you need to copy this URL and update a postback SSO URL (also called the Assertion Consumer Service URL) of the SSO application for MetaDefender IT Access in your identity provider.
11. Create IdP Mappings from your external provider in MetaDefender IT Access (more information [here](https://docs.opswat.com/macloud-sdp/configuration---management/idp-method)) and assign users/groups you allow them to log into MetaDefender IT Access console to that application on your IdP. Note that, you don't need to invite those users to MetaDefender IT Access console under User Management; whenever they log into MetaDefender IT Access console, their account will be set up and assigned to your account as a Read-Only user. You can update their role after that.

Note: You can import information from step #5 through #8 from the IdP metadata file that you got earlier from the identity provider if it's available

You can find detailed setup guideline for some identity providers below

[Setup SSO with Okta](/docs/macloud-sdp/configuration---management/setup-sso-with-okta)

[Setup SSO with Microsoft Azure](/docs/macloud-sdp/configuration---management/setup-sso-with-microsoft-azure)

[Setup SSO with PingOne](/docs/macloud-sdp/configuration---management/setup-sso-with-pingone)
