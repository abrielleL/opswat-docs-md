<!-- source: https://www.opswat.com/docs/macloud-sdp/secure-access/configure-sso-settings-on-applications -->

# Configure SSO settings on applications

This step updates IdP certificate on single sign-on settings of your application in order to the application can verify user authentication results from MetaDefender IT-OT Access. Otherwise, the application couldn't trust the authentications and not let your end-user login.

**1.** Log into the MetaDefender IT-OT Access console, navigate to **Secure Access** > **Protected Apps**.

**2.** Select an application you would like to configure, select SSO Setup Instructions tab and click Download Certificate to download a self-signed certificate MetaDefender IT-OT Access generated for your account.

**3.** Log into your application as administrator. Navigate to single sign-on settings on your application where you set up single sign-on settings

**4.** Replace the IdP certificate with OPSWAT certificate you downloaded in step 2

**5.** Save your changes
