<!-- source: https://www.opswat.com/docs/macloud-sdp/secure-access/microsoft-azure-with-salesforce -->

# Microsoft Azure with Salesforce

OPSWAT MetaDefender IT-OT Access can be easily integrated with an existing Microsoft Azure & Salesforce integration to ensure that a device is compliant with the organization's security policy before it is granted access to Salesforce. This ensures that the user is not only authenticated by Microsoft Azure, but also a device the user uses to access SaaS applications tested for risks and vulnerabilities such as infections or outdated operating systems, BEFORE it access an organization's cloud services.

To get started with implementing OPSWAT MetaDefender IT-OT Access integration to enforce device posture check before granting a device to access Salesforce with Microsoft Azure Single Sign On (SSO) service. You set up SSO between Microsoft Azure and Salesforce as guidelines in [Azure Active Directory integration with Salesforce](https://docs.microsoft.com/en-us/azure/active-directory/saas-apps/salesforce-tutorial)

After configuring SSO, you should test it out to make sure that SSO works as expected.

Now it's the time you can integrate MetaDefender IT-OT Access with your Microsoft Azure & Salesforce by following the below steps. You can learn more details for each step here at [3.1.1. How to set it up?](https://onlinehelp.opswat.com/metaaccess/3.1.1._How_to_set_it_up_.html)

- [Step 1. Enable Access Control on your MetaDefender IT-OT Access account](https://onlinehelp.opswat.com/metaaccess/Microsoft_Azure_with_Salesforce.html#step-1-enable-access-control-on-your-metaaccess-account)
- [Step 2. Add protected applications with IdP Method](https://onlinehelp.opswat.com/metaaccess/Microsoft_Azure_with_Salesforce.html#step-2-add-protected-applications-with-idp-method)
- [Step 3. Configure Access Rules](https://onlinehelp.opswat.com/metaaccess/Microsoft_Azure_with_Salesforce.html#step-3-configure-access-rules)
- [Step 4. Update Applications settings on Identity Provider](https://onlinehelp.opswat.com/metaaccess/Microsoft_Azure_with_Salesforce.html#step-4-update-applications-settings-on-identity-provider)
- [Step 5. Configure SSO settings on applications](https://onlinehelp.opswat.com/metaaccess/Microsoft_Azure_with_Salesforce.html#step-5-configure-sso-settings-on-applications)
- [Step 6: Test your integration](https://onlinehelp.opswat.com/metaaccess/Microsoft_Azure_with_Salesforce.html#step-6-test-your-integration)

## [Step 1. Enable Access Control on your MetaDefender IT-OT Access account](/docs/macloud-sdp/secure-access/microsoft-azure-with-salesforce#step-1-enable-access-control-on-your-metadefender-it-ot-access-account)

1. Log into [the MetaDefender IT-OT Access console](https://gears.opswat.com/console)
2. Navigate to **Secure Access** > **Protected Apps**
3. Check **"**Enable Secure Access**".**
4. Click **SAVE**.
5. Navigate to **Integrations** and then **Device Identity**, and enable **Enable cross-domain API integration at port xxxx**

## [Step 2. Add protected applications with IdP Method](/docs/macloud-sdp/secure-access/microsoft-azure-with-salesforce#step-2-add-protected-applications-with-idp-method)

1. Download Azure Certificate: the next step is importing an Azure X.509 certificate to MetaDefender IT-OT Access. This allows MetaDefender IT-OT Access to verify users signing though a trusted Azure. Each identity provider has a unique X.509 certificate. Download the Azure X509 certificate by following these steps:

   1. Log into Azure Portal as Administrator
   2. Click **Azure Active Directory** on the left navigation

The Azure Active Directory button

3. Navigate to **Enterprise applications > All applications**.

The Enterprise applications blade

4. Select the Salesforce application

5. Select tab Single sign-on. Scroll down to SAML Signing Certificate area and and click on "Certificate (Base64)" to download certificate

2. Collect Idp Login URL and User access URL

   1. Scroll down copy Login URL. Store the URL in somewhere for later use. For example <https://login.microsoftonline.com/60244d0a-5473-4468-b743-f9cc479b7dab/saml2>

2. Select Properties and copy User access URL. Store the URL in somewhere for later use. For example [https://myapps.microsoft.com/signin/Salesforce/549c009f-5f75-4beb-9e53-a754dd43a3f4?tenantId=<your_tenant_id](https://myapps.microsoft.com/signin/Salesforce/549c009f-5f75-4beb-9e53-a754dd43a3f4?tenantId=%3Cyour%5C_tenant%5C_id)>

3. Collect Salesforce Logout URL: you can find this URL inside of Salesforce

   1. Log into your Salesforce account
   2. Click on your avatar, right click on **Log Out** and choose **Copy link address** to get log out URL

3. Store the log out URL in somewhere for later use

4. Add the Azure Identity Provider. If you already have Azure IdP settings on your MetaDefender IT-OT Access account, go to step 2.5 to add Salesforce application.

   1. Log into the [MetaDefender IT-OT Access console](https://gears.opswat.com/console)
   2. Navigate to **Secure Access** > **Protected Apps**
   3. Click Add New Protected App
   4. select IdP Method
   5. Select your IdP if you already added it or add a new IdP and fill in required fields for the Identity Provider

      1. *IdP Name*: an IdP name, for example: Azure
      2. *IdP Certificate*: upload Azure certificate you downloaded in Step 2.1

6. Click **Continue**

5. Add Salesforce application:

   1. Enter required field

      1. *Application*: application name, for example: Salesforce
      2. IdP Login URL: Embedded "User access URL" which you have from Step 2.2
      3. *Login URL*: Embedded "Login URL" which you have from Step 2.2
      4. *Logout URL*: application logout URL which you have from Step 2.3
      5. *Access Mode*: pick an access mode you prefer. See details on the access modes at [Step 2. Add protected applications with IdP Method](https://onlinehelp.opswat.com/metaaccess/Step_2._Add_protected_applications_with_IdP_Method.html)

2. Click **ADD**

6. After saving your changes successfully, a SSO setup instruction will be shown, copy the **ACS URL** MetaDefender IT-OT Access generated there and download OPSWAT Certificate. Note that this information can be found in the protected app's details later .

## [Step 3. Configure Access Rules](/docs/macloud-sdp/secure-access/microsoft-azure-with-salesforce#step-3-configure-access-rules)

Note: This step can be skipped if you have done this step in the past or you can use the default rules

1. In [MetaDefender IT-OT Access console](https://gears.opswat.com/console)
2. Navigate to **Secure Access** > **Rules**
3. click "**ADD NEW RULE**" to add a new rule for this application OR you can update existing access rules to add this application
4. With a new access rule, you need to specify how you would like to block/allow access a device from the application

   1. *Rule name*: a rule name, for example Block non-compliant devices
   2. *Action*: Block or Allow
   3. Configure conditions to do the action. Details at [Step 3. Configure Access Rules](https://onlinehelp.opswat.com/metaaccess/Step_3._Configure_Access_Rules.html)
5. Click **ADD RULE**

## [Step 4. Update Applications settings on Identity Provider](/docs/macloud-sdp/secure-access/microsoft-azure-with-salesforce#step-4-update-applications-settings-on-identity-provider)

1. Log into Azure Portal as administrator
2. Click **Azure Active Directory**.
3. Navigate to **Enterprise applications > All applications**.
4. Select the Salesforce application
5. Select Single sign-on.
6. Click the edit icon (pencil icon) on Basic SAML Configuration section
7. Replace **Reply URL** with the MetaDefender IT-OT Access URL which you got from Step 2.6

8. Click **Save**

## [Step 5. Configure SSO settings on applications](/docs/macloud-sdp/secure-access/microsoft-azure-with-salesforce#step-5-configure-sso-settings-on-applications)

1. Login to Salesforce as an administrator
2. Select Setup
3. Navigate to **Security Controls** > **Single sign-on Settings** and click **Edit** on application

4. Click on **Choose File** to upload the OPSWAT certificate that MetaDefender IT-OT Access generated for your account (you downloaded in step 2.6)

5. Change Identity Provider Login URL to the ACS URL MetaDefender IT-OT Access generated for your application that you got from Step 2.6
6. Select Service Provider Initiated Request Binding to **Redirect**
7. Click **Save**

## [Step 6: Test your integration](/docs/macloud-sdp/secure-access/microsoft-azure-with-salesforce#step-6-test-your-integration)

Follow guideline at [Step 6: Test your integration](https://onlinehelp.opswat.com/metaaccess/Microsoft_Azure_with_Salesforce.html#src-5718783) to test your integration to verify if it works as your expectation.

**DONE! CONGRATULATIONS.**
