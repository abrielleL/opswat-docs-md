<!-- source: https://www.opswat.com/docs/macloud-sdp/configuration---management/setup-sso-with-okta -->

# Setup SSO with Okta

**MetaDefender IT Access** offers an integration with a 3rd-party Single Sign-on Service (SSO). This enables an account to provision new users to manage your account. When a user logs into the MetaDefender IT Access console through your own SSO service, MetaDefender IT Access will provision that user as a read-only user on your account. You can update the user's role later.

MetaDefender IT Access uses the secure and widely adopted industry standard Security Assertion Markup Language 2.0 (SAML 2.0), so that you can integrate easily with any large identity provider that supports SAML 2.0.

#### [Prerequisites](/docs/macloud-sdp/configuration---management/setup-sso-with-okta#prerequisites)

The 3rd-party Single Sign-on Service (SSO) feature is available for paid Customers. If you are using a free account, and you would like to use the SSO feature. Please click the "Upgrade Request" button on your Console Management \ Settings \ Global \ Account tab.

#### [Supported features](/docs/macloud-sdp/configuration---management/setup-sso-with-okta#supported-features)

- IdP-initiated SSO
- SP-initiated SSO
- Just-In-Time provisioning

#### [Configuration steps](/docs/macloud-sdp/configuration---management/setup-sso-with-okta#configuration-steps)

1. Log into Okta as an administrator
2. Navigate to **Applications** and click on "Browsers App Catalog" button
3. Search OPSWAT and select OPSWAT MetaDefender IT Access application

4. Click the **Add Integration** button

5. Enter the Application Label, for example **OPSWAT MetaDefender IT Access** and click the **Done** button

6. Navigate to **Sign On** tab.
7. Open the **Metadata URL** on another tab and save the content as **idpmetadata.xml**

8. Login MetaDefender IT Access Console
9. Navigate to **User Management** **> SSO >** **Console Authentication**
10. Check **Enable Single Sign On**
11. Upload idpmetadata.xml from step 7 and click the **SAVE** button

12. Scroll down to the MetaDefender IT Access Login URL and copy the URL

13. Switch to Okta Admin
14. Click the **Edit** button
15. Scroll down to the Advanced Sign-on Settings and paste the MetaDefender IT Access Login URL

16. Click the **Save** button
17. **DONE.** Now you need to assign people/groups who can access this application on Okta.

If You couldn't import the identity provider information from the IdP metadata file, you can get information from the Set up instruction page of the app and copy IdP certificate, Issuer, and IdP SSO URL to the MetaDefender IT Access console

#### [SP-initiated SSO](/docs/macloud-sdp/configuration---management/setup-sso-with-okta#sp-initiated-sso)

Contact [OPSWAT Support](https://www.opswat.com/support/contact-support) to enable SP-initiated SSO for your domain users
