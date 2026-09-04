<!-- source: https://www.opswat.com/docs/macloud-sdp/secure-access/test-your-integration -->

# Test your integration

How to test?

Now, it's time to validate your work. Before testing your integration, please make sure you have done all steps [to protect an app with IdP method](/docs/macloud-sdp/secure-access/configuration)

**1.** Use a device and login to your cloud application as you do everyday.

After entering correct username and password on your SSO service (IdP), you should be redirect to an OPSWAT page (from the URL bar of your browser, you can see it's redirected to <https://cac.opswat.com/>....). From there, OPSWAT will process device compliance check before granting you to access the application.

**2.** If a device is blocked from accessing the application, you should expect to see a remediation page which tells you why you are blocked.

If a device is allowed to access the application, you should expect that you are able to log in to the application.

## [Common Errors](/docs/macloud-sdp/secure-access/test-your-integration#common-errors)

There are some common mis-configuration you may enter. Here are some use cases you may face during your testing.

### [Case 1: You are not redirected to OPSWAT page after logging successfully](/docs/macloud-sdp/secure-access/test-your-integration#case-1-you-are-not-redirected-to-opswat-page-after-logging-successfully)

This happens when you have not updated the application settings on your IdP to enforce the IdP forward user authentications to OPSWAT MetaDefender IT-OT Access after a user logs in successfully. To fix this issue, please check out [Update Applications settings on Identity Provider](/docs/macloud-sdp/secure-access/update-applications-settings-on-identity-provider)

### [Case 2: You are redirected to an other application after logging successfully](/docs/macloud-sdp/secure-access/test-your-integration#case-2-you-are-redirected-to-an-other-application-after-logging-successfully)

You have at least 2 applications which are integrated to MetaDefender IT-OT Access. However, after a user logs in successfully, the user is redirected to an other application instead of the application he/she is trying to log in. This happens when you replace wrong ACS/login URL of the application on IdP. Please verify again the ACS/login URL you used to replace the ACS/login URL of the application on IdP. More details is at [Update Applications settings on Identity Provider](/docs/macloud-sdp/secure-access/update-applications-settings-on-identity-provider)

### [Case 3: The application doesn't let me login due to a certificate issue](/docs/macloud-sdp/secure-access/test-your-integration#case-3-the-application-doesnt-let-me-login-due-to-a-certificate-issue)

The application throws an error message to tell that it couldn't validate the authentication like the below screenshot

On Salesforce:

On Dropbox:

A root cause for this case is your application doesn't trust a SAML message which OPSWAT sends to your application. This issue happens when you has not imported OPSWAT certificate to SSO settings on your application. Follow steps in [Configure SSO settings on applications](/docs/macloud-sdp/secure-access/configure-sso-settings-on-applications) to update it.

### [Case 4: The application doesn't let me log in due to a wrong login URL](/docs/macloud-sdp/secure-access/test-your-integration#case-4-the-application-doesnt-let-me-log-in-due-to-a-wrong-login-url)

The application throws an error to say that you log in from a wrong URL like the below screenshot

The root cause is you configured wrong ACS URL on the MetaDefender IT-OT Access console. The URL there should be a ACS/post-back SSO URL of the application.

## [Case 5: OPSWAT blocks a device from accessing an application because no agent installed but the device already installed an agent](/docs/macloud-sdp/secure-access/test-your-integration#case-5-opswat-blocks-a-device-from-accessing-an-application-because-no-agent-installed-but-the-device-already-installed-an-agent)

A user can get the below error message

This can happen in one of the following cases:

1. The agent is connecting to other account. Solution: uninstall the agent on the device and install a new with the new installer which can be downloaded from the block page.
2. The agent is running an old agent version which has not supported this feature. The agent should be 7.6.121.0+ for Windows and 10.4.147.0+ for macOS. We have not supported Linux/iOS/Android devices, as a result, we allow these devices to access the application no matter what. Solution: this issue can happen

   1. Your account disables auto-upgrade for agent. If that is the case, just need to enable it. Agent will uptake the last version in 1 hour. You also able to reinstall the agent too.
   2. The agent on the device couldn't connect to our server to check the last version. You can check by downloading the file at the URL <https://agent-update.opswat.com/windows_installer/gears_config.wak>. If you couldn't download, please check your proxy/firewall settings to resolve it. You can follow [our KB](/docs/macloud-sdp/metaaccess-cloud---sdp/v3.9.0/kb/how-do-i-configure-opswat-client-to-work-with-a-proxy-or-outbound) to allow our server addresses.
3. OR the device is using proxy to access website. When you enable access control on your account, devices will open a cross-domain API on local for our cloud to query device id. This API is running with the domain epai.opswatgears.com (127.0.0.1). Solution: add exception for the domain [epai.opswatgears.com](http://epai.opswatgears.com) not go through proxy servers

4. OR your DNS couldn't resolve the domain eapi.opswatgears.com. Try to resolve the domain eapi.opswatgears.com on the device and make sure it's resolved as 127.0.0.1

### [Case 6: OPSWAT doesn't block or allow a device as expected](/docs/macloud-sdp/secure-access/test-your-integration#case-6-opswat-doesnt-block-or-allow-a-device-as-expected)

In this case, you should check the following settings:

1. Make sure you already enable Secure Access on your MetaDefender IT-OT Access account at Secure Access > Protected App
2. Verify IdP and applications settings on your MetaDefender IT-OT Access account. Make sure you already imported the IdP's certificate and configured applications' mode as expected. Check more details at [Add protected applications with IdP Method](/docs/macloud-sdp/secure-access/add-protected-applications-with-idp-method)
3. Exercise your [Access rules](/docs/macloud-sdp/secure-access/access-rules) on your MetaDefender IT-OT Access account by yourself to see what rule your device meets and what action it will be taken. Note that access rules are processed by order.
4. We have not supported Linux/iOS/Android devices, as a result, we allow these devices to access the application no matter what.
