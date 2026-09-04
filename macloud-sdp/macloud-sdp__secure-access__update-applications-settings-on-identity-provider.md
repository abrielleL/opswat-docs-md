<!-- source: https://www.opswat.com/docs/macloud-sdp/secure-access/update-applications-settings-on-identity-provider -->

# Update Applications settings on Identity Provider

This step is done on your IdP to tell your IdP forward user authentication to OPSWAT MetaDefender IT-OT Access for checking device posture status before granting them log into your applications. Otherwise, IdP will allow the user to your application directly without going through MetaDefender IT-OT Access.

Before implementing this step, you need to add your IdP and applications to your MetaDefender IT-OT Access account by following [Add protected applications with IdP Method](/docs/macloud-sdp/secure-access/add-protected-applications-with-idp-method)

**1.** Log into the MetaDefender IT-OT Access console, navigate to Secure Access > Protected App

**2.** Select a protected application you would like to update, select SSO Setup Instructions tab and copy an ACS URL that MetaDefender IT-OT Access generated for the application. This URL is used to replace the ACS URL of the application on IdP.

**3.** Log into your IdP console as an administrator and navigate to your application single sign-on settings

**4.** Replace ACS URL/LogIn URL of your application on the IdP with the ACS URL on MetaDefender IT-OT Access console for your application that you got from step 2 in this section.

**5.** Save your changed settings
