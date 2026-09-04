<!-- source: https://www.opswat.com/docs/macloud-sdp/secure-access/okta-idp-with-atlassian -->

# Okta IdP with Atlassian

OPSWAT MetaDefender IT-OT Access can be easily integrated with an existing Okta Atlassian integration to ensure that a device is compliant with the organization's security policy before it is granted access to Atlassian. This ensures that the device is not only authenticated by the IdP, but also tested for risks and vulnerabilities such as infections or unpatched versions of operating systems, BEFORE it access an organization's cloud services.

To get started with implementing OPSWAT MetaDefender IT-OT Access integration to enforce device posture check before granting a device to access Atlassian with Okta Single Sign On (SSO) service, you set up SSO between Okta and Atlassian manually as below steps even you already have SSO set up for Atlassian on Okta. The built-in Atlassian application doesn't allow you to modify a LoginURL of Atlassian.

Reference: [How to configure Atlassian SAML Single Sign On with an Identity Provider](https://confluence.atlassian.com/cloud/saml-single-sign-on-939718272.html)

1. Log into the Okta console as an Administrator
2. Switch to Admin view, navigate to Application

3. Click **Add Application**

4. Click "**Create New App**" button to create an application manually

5. Select **SAML 2.0** option and click **Create**

6. On the step **1 General Settings**, fill in the app name and upload a new logo for the app if needed, then click Next

7. On the step **2 Configure SAML**, fill in the below information and then click Next

   1. *Single sign-on URL* is a Atlassian single sign-on post back URL: <https://id.atlassian.com/login>
   2. *Audience URL (SP Entity ID)*: <https://id.atlassian.com/login>
   3. *Default RelayState:* your organization's URL, for example: [https://your_domain.atlassian.net](https://your%5C_domain.atlassian.net)
   4. *Name ID format*: Unspecified
   5. *Application username*: Okta username
   6. In Attribute Statement, you need to add 3 more attributes as the below

| Name | Name format | Value |
| --- | --- | --- |
| <http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname> | Unspecified | user.firstName |
| <http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname> | Unspecified | user.lastName |
| <http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name> | Unspecified | user.email |

8. On the step **3 Feedback**, select the option "**I'm an Okta customer adding an internal app**" and click Finish

9. On Sign On tab, you can view Setup instructions to get IdP metadata and follow guideline [here](https://confluence.atlassian.com/cloud/saml-single-sign-on-939718272.html) to set up single sign-on settings on Atlassian.
10. On Assignments tab, click on Assign to assign person you want to allow to access this application

After configuring SSO, you should test it out to make sure that SSO works as expected.

Now it's the time you can implement integration MetaDefender IT-OT Access with your Okta Atlassian by following the below steps. You can learn more details for each step here at [3.1.1. How to set it up?](https://onlinehelp.opswat.com/metaaccess/3.1.1._How_to_set_it_up_.html)

- [Step 1. Enable Access Control on your MetaDefender IT-OT Access account](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_Atlassian.html#step-1-enable-access-control-on-your-metaaccess-account)
- [Step 2. Add protected applications with IdP Method](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_Atlassian.html#step-2-add-protected-applications-with-idp-method)
- [Step 3. Configure Access Rules](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_Atlassian.html#step-3-configure-access-rules)
- [Step 4. Update Applications settings on Identity Provider](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_Atlassian.html#step-4-update-applications-settings-on-identity-provider)
- [Step 5. Configure SSO settings on applications](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_Atlassian.html#step-5-configure-sso-settings-on-applications)
- [Step 6: Test your integration](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_Atlassian.html#step-6-test-your-integration)

## [Step 1. Enable Access Control on your MetaDefender IT-OT Access account](/docs/macloud-sdp/secure-access/okta-idp-with-atlassian#step-1-enable-access-control-on-your-metadefender-it-ot-access-account)

1. Login to [the MetaDefender IT-OT Access console](https://gears.opswat.com/console)
2. Navigate to **Secure Access** and then **Protected Apps**
3. Check on the box **"**Enable secure access**".**
4. Click **SAVE**.
5. Navigate to **Integrations** and then **Device Identity**, and enable **Enable cross-domain API integration at port xxxx**

## [Step 2. Add protected applications with IdP Method](/docs/macloud-sdp/secure-access/okta-idp-with-atlassian#step-2-add-protected-applications-with-idp-method)

1. Download Okta IdP: the next step is importing an Okta X.509 certificate to MetaDefender IT-OT Access. This allows MetaDefender IT-OT Access to verify users signing though a trusted IdP, Okta. Each identity provider has a unique X.509 certificate. Download the Okta X509 certificate by following these steps:

   1. Login to Okta as Administrator
   2. Switch to Admin mode

3. Go to Applications dashboard

4. Select the Atlassian application which you just added above

5. Go to **Sign On** tab and click **View Setup Instruction** **

**

6. Search for **X.509 Certificate** and c lick **Download certificate** to download Okta certificate

2. IdP Login URL: this is an embed link which Okta generated for the app to embed outside Okta. You can find this URL on General tab, scroll down to the App Embed Link section

3. Atlassian LoginURL: is a Atlassian single sign-on post back URL of your organization's Atlassian, for example <https://id.atlassian.com/login>
4. Collect Atlassian Logout URL: you can find this URL inside of Atlassian

   1. Log into your organization's Atlassian account
   2. Click on your avatar, right click on **Log Out** and choose **Copy link address** to get log out URL

Store the log out URL in somewhere for later use.

6. Add the Okta Identity Provider. If you already have Okta IdP settings on your MetaDefender IT-OT Access account, go to 5 to add Atlassian application.

   1. Login to the [MetaDefender IT-OT Access console](https://gears.opswat.com/console)
   2. Navigate to **Secure Access** and then **Access Methods**
   3. On the **Identity Providers** tab, click "**Add New Identity Provider**" to add your IdP
   4. Fill in required fields for the Identity Provider

      1. *IdP Name*: an IdP name, for example: Okta
      2. *IdP Certificate*: upload Okta certificate you downloaded in Step 2.1
7. Click **SAVE.**
8. Navigate to **Secure Access** and then **Protected Apps**.
9. Add Atlassian application:

   1. Expand the Okta IdP settings you have just added in Step 2.4 above.
   2. Click **Add New Application**
   3. Enter required field

      1. *Application*: application name, for example: Atlassian
      2. *Login URL*: application login URL which you have from Step 2.2
      3. *Logout URL*: application logout URL which you have from Step 2.3
      4. *Access Mode*: pick an access mode you prefer. See details on the access modes at [Step 2. Add protected applications with IdP Method](https://onlinehelp.opswat.com/metaaccess/Step_2._Add_protected_applications_with_IdP_Method.html)
   4. Click **SAVE**
10. After saving your changes sucessfully, click the **SSO Setup Instructions** button of the Atlassian application you have just added and then copy the **URL** MetaDefender IT-OT Access generated there. This URL is used to replace Atlassian login URL on Okta in Step 4. Download the OPSWAT Certificate as well.

Note: you can add Atlassian application (step 2.5) when you add Okta IdP settings in step 2.4.

## [Step 3. Configure Access Rules](/docs/macloud-sdp/secure-access/okta-idp-with-atlassian#step-3-configure-access-rules)

1. On [MetaDefender IT-OT Access console](https://gears.opswat.com/console), navigate to **Secure Access** and then **Rules**
2. Click "**ADD NEW RULE**" to add a new rule for this application OR you can update existing access rules to add this application
3. With a new access rule, you need to specify how you would like to block/allow access a device from the application

   1. *Rule name*: a rule name, for example Block non-compliant devices
   2. *Action*: Block or Allow
   3. Configure conditions to do the action. Details at [Step 3. Configure Access Rules](https://onlinehelp.opswat.com/metaaccess/Step_3._Configure_Access_Rules.html)
4. Click **ADD RULE**

## [Step 4. Update Applications settings on Identity Provider](/docs/macloud-sdp/secure-access/okta-idp-with-atlassian#step-4-update-applications-settings-on-identity-provider)

1. Login to Okta as administrator
2. Go to Applications dashboard
3. Select Atlassian application
4. On **General** tab, click Edit on the SAML Settings box
5. Click **Next** at the first step
6. Replace **Single sign on URL** and Audience URL with the MetaDefender IT-OT Access URL which you got from Step 2.6

7. Click **Next** and **Finish**

## [Step 5. Configure SSO settings on applications](/docs/macloud-sdp/secure-access/okta-idp-with-atlassian#step-5-configure-sso-settings-on-applications)

3. Login to Atlassian as an administrator
4. Navigate to **Atlassian Site Administration > Your organization > SAML single sign-on.**
5. Click **Edit Configuration**
6. Replace **Public x509-certificate** with the OPSWAT certificate which OPSWAT generated for your account (you downloaded already)
7. Click **Save Changes**

## [Step 6: Test your integration](/docs/macloud-sdp/secure-access/okta-idp-with-atlassian#step-6-test-your-integration)

Follow guideline at [Step 6: Test your integration](https://onlinehelp.opswat.com/metaaccess/Step_6__Test_your_integration.html) to test your integration to verify if it works as your expectation.

**DONE! CONGRATULATIONS.**
