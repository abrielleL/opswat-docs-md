<!-- source: https://www.opswat.com/docs/macloud-sdp/secure-access/add-protected-applications-with-idp-method -->

# Add protected applications with IdP Method

This steps provides MetaDefender IT-OT Access what Identity Provider (IdP) you want to integrate with and what applications you want to enforce device posture check before granting the device to access the applications. Once you integrate with MetaDefender IT-OT Access, your IdP will forward user authentication result to MetaDefender IT-OT Access after a user logs in successfully for checking device posture. Every request MetaDefender IT-OT Access receives, it will verify if the request comes from a trusted IdP before enforcing device posture check to grant an access to a specified application. Once again, MetaDefender IT-OT Access only processes requests if [Secure Access is enabled on your account.](/docs/macloud-sdp/secure-access/enable-access-control-on-your-metaaccess-account)

We support most Identity Providers who support SAML SSO, for example: Okta, Ping Identity, Centrify, OneLogin,... and applications which supports SAML SSO.

In this step, you need to collect the following information from your IdP and Single Sign-on settings of the applications:

1. IdP certificate which you can get from IdP metadata
2. Application information: log in URL, log out URL

**1. Download IdP certificate**

The next step is importing an IdP X.509 certificate to MetaDefender IT-OT Access. This allows MetaDefender IT-OT Access to verify users signing though a trusted IdP. Each identity provider has a unique X.509 certificate for your account. You can find this certificate from metadata of the IdP on single sign-on setup instructions.

**2 Collect Login URL of the application**

Each application has a unique Assertion Consumer Service (ACS) URL (OR post back single sign on URL) to authenticate users signing through a third-party identity provider. MetaDefender IT-OT Access uses this URL to forward the authentication message from IdP to the application after checking device posture passed.

You are able to find the Login URL of the application from a guideline to configure single sign-on settings for the application.

Or you can figure it out from the application settings on the IdP console.

**3. Collect IdP SSO log in URL**

IdP generates a unique SSO log in URL for each application when you set up SSO for an application. MetaDefender IT-OT Access uses this URL to let a user log into the application when a device is granted temporary access.

**4. Collect Logout URL of the application**

Each application has a unique Logout URL to terminate a user session only for that application. MetaDefender IT-OT Access uses this URL to kick users out if a device is blocked from access the application

You are able to find the Logout URL of the application when you log in to the application. Some application put the logout URL on the Logout button or link and you just simply copy the link.

**4. Add protected applications**

1. Login to the MetaDefender IT-OT Access console
2. Navigate to **Secure Access** and then **Protected Apps**
3. Click Add Protected Apps
4. Select IdP Method to add protected apps with SAML IdP Method.

Note: While enabling this feature, endpoints on your account will be enforced into running the [Cross-Domain API](/docs/macloud-sdp/developer-guide/cross-domain-api) on local endpoints at a configured port. You MUST to pick a port which no applications on endpoints are running,

5. Provide IdP where your application is set up

- Select Add new IdP if you have not added your IdP. You then need to fill in IdP information

  - IdP Name
  - IdP certificate: upload the IdP certificate you downloaded in the step 1. Note that the certificate file is PEM format.
- Select Choose from existing IdPs if you already added the IdP

6. Click Continue
7. Fill in the application information

- *Application*: application name, for example: Salesforce
- *IdP login URL:* an URL IdP generates for your app when you configure single sign on
- IdP Start URL: in case you use SP-Initiated SSO workflow
- *App ACS URL*: an post-back single sign on URL or Assertion Consumer Service (ACS) URL of the application which you have from Step 2.
- *Application Logout URL* *(__optional)*: application logout URL which you have from Step #3.
- Android Package Name and iOS App URL schema: to identify an app on Android/iOS so that OPSWAT Mobile app can redirect end-users back. You can check out the KB [How could I find an app ID of an application?](/docs/macloud-sdp/kb/how-could-i-find-an-app-id-of-an-application-) to know how to get these information.
- *Access Mode(*)*: pick an access mode you prefer.

  - ***Disable*** mode: MetaDefender IT-OT Access always allows all devices to access the application. No access log is recorded for this mode.
  - ***Monitor*** mode: MetaDefender IT-OT Access always allows all devices to access the application. Beside that, it processes [Access rules](/docs/macloud-sdp/secure-access/access-rules) on your account to check what action (Block/Allow) will be applied to the device if you change the application mode to ***Enforce*** mode. An access log will be generated as Monitored (Allow) or Monitored (Block) based on the check.
  - ***Enforce*** mode: MetaDefender IT-OT Access processes [Access rules](/docs/macloud-sdp/secure-access/access-rules) on your account to check what action will be applied to the device.

    - If the action is *Allow*, MetaDefender IT-OT Access allows the device to access the application and records an access log with an action as ***Allowed.***
    - If the action is *Block*, MetaDefender IT-OT Access blocks the device from accessing the application and records an access log with an action as ***Blocked.*** The user will get a page to tell why he/she is blocked from accessing the application.
- Check " Allow MetaDefender IT-OT Access to record a user who is using a device to access an application" to allow MetaDefender IT-OT Access record users who are using devices to access cloud applications. By this way, MetaDefender IT-OT Access can help you address the complex BYOD ownership problem by showing the user identity such like application username with each device they use when accessing cloud applications, increasing unmanaged device control without requiring any IT infrastructure changes, network traffic manipulation, or mobile device management (MDM).
- Enter your PIN
- Click SAVE

8. After saving your changes successfully, the system will show you steps to completely protect your application. You should copy a URL MetaDefender IT-OT Access generates for your application and store it for later use. This URL is used to replace a login URL of the application on IdP console in [Step 4. Update Applications settings on Identity Provider](metaaccess-cloud---sdp/v3.9.0/secure-access/update-applications-settings-on-identity-provider)

(*) MetaDefender IT-OT Access always check if an user authentication result comes from a trusted IdP by using the X.509 certificate you uploaded for the IdP. If it comes from an untrusted IdP, MetaDefender IT-OT Access doesn't allow the user log into your application.
