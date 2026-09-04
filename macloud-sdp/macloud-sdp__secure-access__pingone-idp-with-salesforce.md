<!-- source: https://www.opswat.com/docs/macloud-sdp/secure-access/pingone-idp-with-salesforce -->

# PingOne IdP with Salesforce

OPSWAT MetaDefender IT-OT Access can be easily integrated with an existing PingOne & Salesforce integration to ensure that a device is compliant with the organization's security policy before it is granted access to Salesforce. This ensures that the device is not only authenticated by the IdP, but also tested for risks and vulnerabilities such as infections or unpatched versions of operating systems, BEFORE it access an organization's cloud services.

To get started with implementing OPSWAT MetaDefender IT-OT Access integration to enforce device posture check before granting a device to access Salesforce with PingOne Single Sign On (SSO) service, you need to have SSO set up between PingOne and Salesforce. If you haven't already done so, please follow the instructiosn [here](http://saml-doc.okta.com/SAML_Docs/How-to-Configure-SAML-2.0-in-Salesforce.html) to set it up.

You can learn more details for each step here at [3.1.1. How to set it up?](https://onlinehelp.opswat.com/metaaccess/3.1.1._How_to_set_it_up_.html)

- [Step 1. Enable Access Control on your MetaDefender IT-OT Access account](https://onlinehelp.opswat.com/metaaccess/PingOne_IdP_with_Salesforce.html#step-1-enable-access-control-on-your-metaaccess-account)
- [Step 2. Add protected applications with IdP Method](https://onlinehelp.opswat.com/metaaccess/PingOne_IdP_with_Salesforce.html#step-2-add-protected-applications-with-idp-method)
- [Step 3. Configure Access Rules](https://onlinehelp.opswat.com/metaaccess/PingOne_IdP_with_Salesforce.html#step-3-configure-access-rules)
- [Step 4. Update Applications settings on Identity Provider](https://onlinehelp.opswat.com/metaaccess/PingOne_IdP_with_Salesforce.html#step-4-update-applications-settings-on-identity-provider)
- [Step 5. Configure SSO settings on applications](https://onlinehelp.opswat.com/metaaccess/PingOne_IdP_with_Salesforce.html#step-5-configure-sso-settings-on-applications)
- [Step 6: Test your integration](https://onlinehelp.opswat.com/metaaccess/PingOne_IdP_with_Salesforce.html#step-6-test-your-integration)

## [Step 1. Enable Access Control on your MetaDefender IT-OT Access account](/docs/macloud-sdp/secure-access/pingone-idp-with-salesforce#step-1-enable-access-control-on-your-metadefender-it-ot-access-account)

1. Login to [the MetaDefender IT-OT Access console](https://gears.opswat.com/console)
2. Navigate to **Secure Access** and then **Protected Apps.**
3. Check on the box **"**Enable access control**"** and configure a port for the cross-domain API. Note that you must select a port which no applications on endpoints is running.
4. Click **SAVE**.

## [Step 2. Add protected applications with IdP Method](/docs/macloud-sdp/secure-access/pingone-idp-with-salesforce#step-2-add-protected-applications-with-idp-method)

1. The next step is importing an PingOne certificate to MetaDefender IT-OT Access. This allows MetaDefender IT-OT Access to verify users signing though a trusted IdP. Each identity provider has a unique X.509 certificate. Download the PingOne certificate by following these steps:

   1. Login to PingOne as Administrator
   2. Go to Applications dashboard
   3. Select Salesforce application
   4. Click **Download** on *Signing Certificate* to download certificate

2. Collect Salesforce Login URL

   1. In PingOne, go to Applications page then select the Salesforce app
   2. Copy **ACS URL**

3. Collect Salesforce Logout URL: you can find this URL inside of Salesforce

   1. Log in to Salesforce
   2. You can find "**Logout**" link when you click on your name
   3. Right-click **Logout** link and select "**Copy link address**" to copy logout URL

4. Add the PingOne Identity Provider. If you already have PingOne IdP settings on your MetaDefender IT-OT Access account, go to 5 to add Salesforce application.

   1. Login to the [MetaDefender IT-OT Access console](https://gears.opswat.com/console)
   2. Navigate to **Secure Access** and then **Access Methods > IdP**
   3. On the **Identity Providers** tab, click "**Add New Identity Provider**" to add your IdP
   4. Fill in required fields for the Identity Provider

      1. *IdP Name*: an IdP name, for example: PingOne
      2. *IdP Certificate*: upload PingOne certificate you downloaded in Step 2.1

5. Click **Add IDP**

6. Click **SAVE**

5. Add the Salesforce application:

   1. Expand the PingOne IdP settings you have just added in Step 2.4 above.
   2. Click **Secure Access > Protected Apps > Add New Application**
   3. Enter required field

      1. *Application*: application name, for example: Salesforce
      2. *IdP Login URL:* get IdP SSO login URL from your PingOne account
      3. *Application Login URL*: application login URL which you have from Step 2.2
      4. *Application Logout URL*: application logout URL which you have from Step 2.3
      5. *Access Mode*: pick an access mode you prefer. See details on the access modes at [Step 2. Add protected applications with IdP Method](https://onlinehelp.opswat.com/metaaccess/Step_2._Add_protected_applications_with_IdP_Method.html)
   4. Click **SAVE**
6. After saving your changes successfully, click the **Setup Instructions** button of the Salesforce application you have just added and then copy the **URL** MetaDefender IT-OT Access generated there. This URL is used to replace Salesforce login URL on PingOne in Step 4.

Note: you can add Salesforce application (step 2.5) when you add PingOne IdP settings.

## [Step 3. Configure Access Rules](/docs/macloud-sdp/secure-access/pingone-idp-with-salesforce#step-3-configure-access-rules)

1. On [MetaDefender IT-OT Access console](https://gears.opswat.com/console), navigate to **Secure Access** and then **Rules**
2. On **Rules** tab, click "**ADD NEW RULE**" to add a new rule for this application OR you can update existing access rules to add this application
3. With a new access rule, you need to specify how you would like to block/allow access a device from the application

   1. *Rule name*: a rule name, for example Block non-compliant devices
   2. *Action*: Block or Allow
   3. Configure conditions to do the action. Details at [Step 3. Configure Access Rules](https://onlinehelp.opswat.com/metaaccess/Step_3._Configure_Access_Rules.html)
4. Click **ADD RULE**

## [Step 4. Update Applications settings on Identity Provider](/docs/macloud-sdp/secure-access/pingone-idp-with-salesforce#step-4-update-applications-settings-on-identity-provider)

1. Login to PingOne
2. Go to **Applications** then **My Applications**
3. Select Salesforce application and click the **Edit** button
4. Click **Continue to Next Step**
5. Replace **ACS URL** with the MetaDefender IT-OT Access URL which you got from Step 2.6

6. Click **Save**

## [Step 5. Configure SSO settings on applications](/docs/macloud-sdp/secure-access/pingone-idp-with-salesforce#step-5-configure-sso-settings-on-applications)

1. On MetaDefender IT-OT Access console, navigate to **Secure Access > Access Methods > IdP**
2. Click **Download OPSWAT certificate** to download a self-signed certificate MetaDefender IT-OT Access generated for your account
3. Login to Salesforce as administrator
4. Navigate to **Setup** > **Security Controls** > **Single Sign-On Settings**, click **Edit** on the SAML Single Sign-On Settings of the PingOne IdP

5. Upload OPSWAT certificate from your MetaDefender IT-OT Access account which you downloaded from Step 5.1
6. Click **Save**

## [Step 6: Test your integration](/docs/macloud-sdp/secure-access/pingone-idp-with-salesforce#step-6-test-your-integration)

Follow guideline at [Step 6: Test your integration](https://onlinehelp.opswat.com/metaaccess/Step_6__Test_your_integration.html) to test your integration to verify if it works as your expectation.

**DONE! CONGRATULATIONS.**
