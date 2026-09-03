<!-- source: https://www.opswat.com/docs/macloud-sdp/configuration---management/setup-sso-with-pingone -->

# Setup SSO with PingOne

MetaDefender IT Access offers an integration with a 3rd-party Single Sign-on Service (SSO). This enables an account to provision new users to manage your account. When a user logs into the MetaDefender IT Access console through your own SSO service, MetaDefender IT Access will provision that user as a read-only user on your account. You can update the user's role later.

MetaDefender IT Access uses the secure and widely adopted industry standard Security Assertion Markup Language 2.0 (SAML 2.0), so that you can integrate easily with any large identity provider that supports SAML 2.0.

**To get started, log into PingOne and create an application for** **MetaDefender IT Access.**

1. Log into PingOne as an administrator
2. Navigate to **Applications**
3. Click **Add Application** **>** **New SAML Application**
4. Fill in required information and click Continue to Next Step

5. Provide SAML details as below:

   1. Protocol version: select SAML v2.0
   2. Assertion Consumer Service (ACS) & Entity ID: your MetaDefender IT Access/OPSWAT Central Management URL, for example: if your account is connecting to US tenant, it should be [https://gears.opswat.com](https://gears.opswat.com/)

6. Click **Continue to Next Step**
7. **Click** **Save and Exit . You can continue to next steps if you would like to grant access to users and groups or you can do this later.**
8. Expand the app again and download the metadata to import it to MetaDefender IT Access later, named it *saml2metadata PingOne,xml*

**Configure PingOne on MetaDefender IT Access:**

9. Log into the MetaDefender IT Access console with an admin permission. Navigate to User management > SSO
10. On Control tab, enable "**Enable Single Sign On**" checkbox
11. Click **Choose File** to import the identity provider metadata you got earlier in step #8, saml2_metadata_PingOne,xml. If the file is valid then IdP certificate, Issuer, and IdP SSO URL will be popped up.
12. Enter an IdP Name, for example: PingOne

13. Click the **Save** button and enter your PIN to confirm the action.
14. After you save your changes successfully, MetaDefender IT Access generates a MetaDefender IT Access Login URL. Copy this URL

**Go back to PingOne to update ACS URL for the OPSWAT** **MetaDefender IT Access** **app**

15. Switch to PingOne Admin
16. Navigate to Applications, then select the application OPSWAT MetaDefender IT Access application you created earlier.
17. Click Edit and Continue to Next Step
18. Replace the ACS URL with the URL the MetaDefender IT Access generated in step #14

19. Click Continue to Next Step until the end and click Finish.

**DONE.** Now you need to assign people/groups who can access this application on PingOne.

If You couldn't import the identity provider information from the IdP metadata file, you can copy IdP certificate, Issuer, and IdP SSO URL to the MetaDefender IT Access console
