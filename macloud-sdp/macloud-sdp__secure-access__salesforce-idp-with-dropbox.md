<!-- source: https://www.opswat.com/docs/macloud-sdp/secure-access/salesforce-idp-with-dropbox -->

# Salesforce IdP with Dropbox

OPSWAT MetaDefender IT-OT Access can be easily integrated with an existing Salesforce Dropbox integration to ensure that a device is compliant with the organization's security policy before it is granted access to Dropbox. This ensures that the device is not only authenticated by the IdP, but also tested for risks and vulnerabilities such as infections or unpatched versions of operating systems, BEFORE it access an organization's cloud services.

To get started with implementing OPSWAT MetaDefender IT-OT Access integration to enforce device posture check before granting a device to access Dropbox with Salesforce Single Sign On (SSO) service, you set up SSO between Salesforce and Dropbox. If you haven't already done so, please follow the instruction [here](https://www.dropbox.com/guide/admin/security/configure-single-sign-on) to set it up.

You can learn more details for each step here at [3.1.1. How to set it up?](https://onlinehelp.opswat.com/metaaccess/3.1.1._How_to_set_it_up_.html)

- [Step 1. Enable Access Control on your MetaDefender IT-OT Access account](https://onlinehelp.opswat.com/metaaccess/Salesforce_IdP_with_Dropbox.html#step-1-enable-access-control-on-your-metaaccess-account)
- [Step 2. Add protected applications with IdP Method](https://onlinehelp.opswat.com/metaaccess/Salesforce_IdP_with_Dropbox.html#step-2-add-protected-applications-with-idp-method)
- [Step 3. Configure Access Rules](https://onlinehelp.opswat.com/metaaccess/Salesforce_IdP_with_Dropbox.html#step-3-configure-access-rules)
- [Step 4. Update Applications settings on Identity Provider](https://onlinehelp.opswat.com/metaaccess/Salesforce_IdP_with_Dropbox.html#step-4-update-applications-settings-on-identity-provider)
- [Step 5. Configure SSO settings on applications](https://onlinehelp.opswat.com/metaaccess/Salesforce_IdP_with_Dropbox.html#step-5-configure-sso-settings-on-applications)
- [Step 6: Test your integration](https://onlinehelp.opswat.com/metaaccess/Salesforce_IdP_with_Dropbox.html#step-6-test-your-integration)

## [Step 1. Enable Access Control on your MetaDefender IT-OT Access account](/docs/macloud-sdp/secure-access/salesforce-idp-with-dropbox#step-1-enable-access-control-on-your-metadefender-it-ot-access-account)

1. Login to [the MetaDefender IT-OT Access console](https://gears.opswat.com/console)
2. Navigate to **Access Control** and then **Configurations**
3. Check on the box **"**Enable secure access**".**
4. Click **SAVE**.
5. Navigate to **Integrations** and then **Device Identity**, and enable **Enable cross-domain API integration at port xxxx**

## [Step 2. Add protected applications with IdP Method](/docs/macloud-sdp/secure-access/salesforce-idp-with-dropbox#step-2-add-protected-applications-with-idp-method)

1. Download Salesforce IdP certificate: the next step is importing an Salesforce X.509 certificate to MetaDefender IT-OT Access. This allows MetaDefender IT-OT Access to verify users signing though a trusted IdP, Salesforce. Each identity provider has a unique X.509 certificate. Download the Salesforce X509 certificate by following these steps:

   1. Login to Salesforce as Administrator
   2. Navigate to Setup > Manage Apps > Connected Apps

3. Select the Dropbox application to view the application details

4. On SAML Service Provider Settings section, click on Idp Certificate

5. Click on Download Certificate to download the Salesforce certificate

2. Collect Dropbox LoginURL: is a Dropbox single sign-on post back URL of your organization's Dropbox, for example <https://www.dropbox.com/saml_login>
3. Collect Dropbox Logout URL: you can find this URL inside of Dropbox

   1. Log into your organization's Dropbox account
   2. Click on your avatar, right click on **Sign out** and choose **Copy link address** to get log out URL

3. Store the log out URL in somewhere for later use

4. Add the Salesforce Identity Provider. If you already have Salesforce IdP settings on your MetaDefender IT-OT Access account, go to 5 to add Dropbox application.

   1. Login to the [MetaDefender IT-OT Access console](https://gears.opswat.com/console)
   2. Navigate to **Secure Access** and then **Access Methods > IdP**
   3. On the **Identity Providers** tab, click "**Add New Identity Provider**" to add your IdP
   4. Fill in required fields for the Identity Provider

      1. *Identity Provider*: Salesforce
      2. *IdP Name*: an IdP name, for example: Salesforce
      3. *IdP Certificate*: upload Salesforce certificate you downloaded in Step 2.1
   5. Click **Add IDP**
   6. Click **SAVE**
5. Navigate to **Secure Access** and then **Protected Apps**.
6. Add Dropbox application:

   1. Expand the Salesforce IdP settings you have just added in Step 2.4 above.
   2. Click **Add New Application**
   3. Enter required field

      1. *Application*: application name, for example: Dropbox
      2. *Login URL*: application login URL which you have from Step 2.2
      3. *Logout URL*: application logout URL which you have from Step 2.3
      4. *Access Mode*: pick an access mode you prefer. See details on the access modes at [Step 2. Add protected applications with IdP Method](https://onlinehelp.opswat.com/metaaccess/Step_2._Add_protected_applications_with_IdP_Method.html)
   4. Click **SAVE**
7. After saving your changes successfully, click the **Setup Instructions** button of the Dropbox application you have just added and then copy the **URL** MetaDefender IT-OT Access generated there. This URL is used to replace Dropbox login URL on Salesforce in Step 4.

Note: you can add Dropbox application (step 2.5) when you add Salesforce IdP settings in step 2.4.

## [Step 3. Configure Access Rules](/docs/macloud-sdp/secure-access/salesforce-idp-with-dropbox#step-3-configure-access-rules)

1. On [MetaDefender IT-OT Access console](https://gears.opswat.com/console), navigate to **Secure Access** and then Rules
2. On **Rules** tab, click "**ADD NEW RULE**" to add a new rule for this application OR you can update existing access rules to add this application
3. With a new access rule, you need to specify how you would like to block/allow access a device from the application

   1. *Rule name*: a rule name, for example Block non-compliant devices
   2. *Action*: Block or Allow
   3. Configure conditions to do the action. Details at [Step 3. Configure Access Rules](https://onlinehelp.opswat.com/metaaccess/Step_3._Configure_Access_Rules.html)
4. Click **ADD RULE**

## [Step 4. Update Applications settings on Identity Provider](/docs/macloud-sdp/secure-access/salesforce-idp-with-dropbox#step-4-update-applications-settings-on-identity-provider)

1. Login to Salesforce as administrator
2. Navigate to Setup > Manage Apps > Connected Apps
3. Select Dropbox application
4. Click Edit
5. Replace **Start URL and ACS URL** with the MetaDefender IT-OT Access URL which you got from Step 2.6

6. Click **Save**

## [Step 5. Configure SSO settings on applications](/docs/macloud-sdp/secure-access/salesforce-idp-with-dropbox#step-5-configure-sso-settings-on-applications)

1. On MetaDefender IT-OT Access console, navigate to **Secure Access** > **Access Methods > IdP**
2. Download OPSWAT certificate
3. Login to Dropbox as an administrator
4. Navigate to **Admin Console** > **Settings**, click **Single sign-on**

5. Click on **Certificate** link and upload the OPSWAT certificate OPSWAT generated for your account (you downloaded in step 5.1)

6. Click **Apply Changes**

## [Step 6: Test your integration](/docs/macloud-sdp/secure-access/salesforce-idp-with-dropbox#step-6-test-your-integration)

Follow guideline at [Step 6: Test your integration](https://onlinehelp.opswat.com/metaaccess/Step_6__Test_your_integration.html) to test your integration to verify if it works as your expectation.

**DONE! CONGRATULATIONS.**
