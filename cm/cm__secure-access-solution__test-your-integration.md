<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/test-your-integration -->

# Test Your Integration

How to test?

Now, it's time to validate your work. Before testing your integration, please make sure you have done all steps to [to protect an app with idP method](https://www.opswat.com/docs/cm/secure-access-solution/SAML-SSO-integration-configuration).

**1.** Use a device and login to your cloud application as you do everyday.

After entering correct username and password on your SSO service (IdP), you should be redirect to an OPSWAT page (from the URL bar of your browser, you can see it's redirected to [https://cac.opswat.com/](https://cac.opswat.com/)....). From there, OPSWAT will process device compliance check before granting you to access the application.

![](https://image-archive.developerhub.io/image/upload/v2_5265/sa3o4r6k49qzpd52ksgd/1628792859.png)

**2.** If a device is blocked from accessing the application, you should expect to see a remediation page which tells you why you are blocked.

![](https://uploads.developerhub.io/prod/97qW/xvxoavviv1dvmvw79h36aii7gg70ltt2smrrzkvufdfhq5v4s28qw5tgrg1bwkxj.png)

If a device is allowed to access the application, you should expect that you are able to log in to the application.

## Common Errors

There are some common mis-configuration you may enter. Here are some use cases you may face during your testing.

### Case 1: You are not redirected to OPSWAT page after logging successfully

This happens when you have not updated the application settings on your IdP to enforce the IdP forward user authentications to My OPSWAT Central Management after a user logs in successfully. To fix this issue, please check out [Update Applications Settings on Identity Provider.](https://www.opswat.com/docs/cm/secure-access-solution/update-applications-settings-on-identity-provider)

### Case 2: You are redirected to an other application after logging successfully

You have at least 2 applications which are integrated to My OPSWAT Central Management. However, after a user logs in successfully, the user is redirected to an other application instead of the application he/she is trying to log in. This happens when you replace wrong ACS/login URL of the application on IdP. Please verify again the ACS/login URL you used to replace the ACS/login URL of the application on IdP. More details is at  [Update Applications Settings on Identity Provider.](https://www.opswat.com/docs/cm/secure-access-solution/update-applications-settings-on-identity-provider)

### Case 3: The application doesn't let me login due to a certificate issue

The application throws an error message to tell that it couldn't validate the authentication like the below screenshot

On Salesforce:

![](https://image-archive.developerhub.io/image/upload/v2_5265/kdpa8hnsp4bobplhuqrj/1628792862.png)

On Dropbox:

![](https://image-archive.developerhub.io/image/upload/v2_5265/iekpqvs5nq4n0m8l2zhu/1628792864.png)

A root cause for this case is your application doesn't trust a SAML message which OPSWAT sends to your application. This issue happens when you has not imported OPSWAT certificate to SSO settings on your application. Follow steps in [Configure SSO Settings on Applications](https://www.opswat.com/docs/cm/secure-access-solution/configure-sso-settings-on-applications) to update it.

### Case 4: The application doesn't let me log in due to a wrong login URL

The application throws an error to say that you log in from a wrong URL like the below screenshot

![](https://image-archive.developerhub.io/image/upload/v2_5265/nn78687aw08ysld1dftd/1628792865.png)

The root cause is you configured wrong ACS URL on the My OPSWAT Central Management console. The URL there should be a ACS/post-back SSO URL of the application.

### Case 5: OPSWAT blocks a device from accessing an application because no agent installed but the device already installed an agent

A user can get the below error message

![](https://uploads.developerhub.io/prod/97qW/g4tl4b81zr2jdj9nvrrtukaaflgq53qd4wtlwlex85wj1trclv4mkimlww43zzdu.jpeg)

This can happen in one of the following cases:

1. The agent is connecting to other account. Solution: uninstall the agent on the device and install a new with the new installer which can be downloaded from the block page.
2. The agent is running an old agent version which has not supported this feature. The agent should be 7.6.121.0+ for Windows and 10.4.147.0+ for macOS. We have not supported Linux/iOS/Android devices, as a result, we allow these devices to access the application no matter what. Solution: this issue can happen
   1. Your account disables auto-upgrade for agent. If that is the case, just need to enable it. Agent will uptake the last version in 1 hour. You also able to reinstall the agent too.
   2. The agent on the device couldn't connect to our server to check the last version. You can check by downloading the file at the URL [https://agent-update.opswat.com/windows_installer/gears_config.wak](https://agent-update.opswat.com/windows_installer/gears_config.wak). If you couldn't download, please check your proxy/firewall settings to resolve it. You can follow [How do I configure MetaDefender Endpoint to work with a proxy or outbound firewall?](https://www.opswat.com/docs/cm/knowledge-base/how-do-i-configure-metadefender-endpoint-to-work-with-a-proxy) to allow our server addresses.
3. OR the device is using proxy to access website. When you enable access control on your account, devices will open a cross-domain API on local for our cloud to query device id. This API is running with the domain epai.opswatgears.com (127.0.0.1). Solution: add exception for the domain [epai.opswatgears.com](http://epai.opswatgears.com) not go through proxy servers

![](https://image-archive.developerhub.io/image/upload/v2_5265/vzpetn7974hylcllfkkm/1628792869.png)

4. OR your DNS couldn't resolve the domain eapi.opswatgears.com. Try to resolve the domain eapi.opswatgears.com on the device and make sure it's resolved as 127.0.0.1

### Case 6: OPSWAT doesn't block or allow a device as expected

In this case, you should check the following settings:

1. Make sure you already enable Secure Access on your My OPSWAT Central Management account at Secure Access > Protected App
2. Verify IdP and applications settings on your My OPSWAT Central Management account. Make sure you already imported the IdP's certificate and configured applications' mode as expected. Check more details at [Add Protected Applications with IdP Method](https://www.opswat.com/docs/cm/secure-access-solution/SAML-SSO-add-protected-applications)
3. Exercise your [Access Rules](https://www.opswat.com/docs/cm/secure-access-solution/access-rules) on your My OPSWAT Central Management account by yourself to see what rule your device meets and what action it will be taken. Note that access rules are processed by order.
4. We have not supported Linux/iOS/Android devices, as a result, we allow these devices to access the application no matter what.
