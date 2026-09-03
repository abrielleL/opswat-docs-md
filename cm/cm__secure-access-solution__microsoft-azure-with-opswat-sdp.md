<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/microsoft-azure-with-opswat-sdp -->

# Microsoft Azure with OPSWAT SDP

My OPSWAT Central Management can be easily integrated with an existing Microsoft Azure & legacy OPSWAT SDP integration to ensure that a device is compliant with the organization's security policy before it is granted access to OPSWAT SDP. This ensures that the user is not only authenticated by Microsoft Azure, but also a device the user uses to access SaaS applications tested for risks and vulnerabilities such as infections or outdated operating systems, BEFORE it access an organization's cloud services.

Follow below steps to integrate My OPSWAT Central Management with your Microsoft Azure & Legacy OPSWAT SDP. You can learn more details for each step here at [3.1.1. How to set it up?](https://onlinehelp.opswat.com/metaaccess/3.1.1._How_to_set_it_up_.html)

- [Step 1. Enable Access Control on your MetaAccess account](https://onlinehelp.opswat.com/metaaccess/Microsoft_Azure_with_OPSWAT_SDP.html#step-1-enable-access-control-on-your-metaaccess-account)
- [Step 2. Create SDP app on Microsoft Azure](https://onlinehelp.opswat.com/metaaccess/Microsoft_Azure_with_OPSWAT_SDP.html#step-2-create-sdp-app-on-microsoft-azure)
- [Step 3. Configure Application and Access Rules on MetaAccess](https://onlinehelp.opswat.com/metaaccess/Microsoft_Azure_with_OPSWAT_SDP.html#step-3-configure-application-and-access-rules-on-metaaccess)
- [Step 4. Configure SSO settings on SDP](https://onlinehelp.opswat.com/metaaccess/Microsoft_Azure_with_OPSWAT_SDP.html#step-4-configure-sso-settings-on-sdp)
- [Step 5. Update Applications settings on Identity Provider](https://onlinehelp.opswat.com/metaaccess/Microsoft_Azure_with_OPSWAT_SDP.html#step-5-update-applications-settings-on-identity-provider)
- [Step 6: Test your integration](https://onlinehelp.opswat.com/metaaccess/Microsoft_Azure_with_OPSWAT_SDP.html#step-6-test-your-integration)

## Step 1. Enable Access Control on your My OPSWAT Central Management account

1. Log into the My OPSWAT Central Management console.
2. Navigate to **Secure Access** > **Protected Apps**
3. Check **"****Enable Secure Access****".**
4. Click **SAVE**.

![](https://uploads.developerhub.io/prod/97qW/4f7eu5wx494bdnkroje3cl5udvkeg7gec8u29u094s7hytb1wd8c3om7616ql4n3.png)

## Step 2. Create SDP app on Microsoft Azure

1. Log into Azure Portal as Administrator
2. Click **Azure Active Directory** on the left navigation

![](https://uploads.developerhub.io/prod/97qW/othtqjk2hl5yvlpmfolvnb1buvqe454cttstroqxzm6664iad6lzsmxlsneollu4.png)

The Azure Active Directory button

3. Navigate to **Enterprise applications >** **All applications**.

![](https://uploads.developerhub.io/prod/97qW/kz0ou5015owdc92857zezk3hewwg9d68wh2zq0y0aguayjv1yul2ht70grqfnb15.png)

The Enterprise applications blade

4. Create a Non-gallery application

![](https://uploads.developerhub.io/prod/97qW/81z657v6jh4uvhdnd3o3u6rro6k8p5xh5fal65izlbr98nmswlau2vnygxmwnzxs.png)

5. Enter some placeholder value for fields in Basic SAML Configuration, then click save. You will need to to update these fields in later steps.

![](https://uploads.developerhub.io/prod/97qW/8zbj2afulb7let249qb9g5c3743xw17nvh9qxvp2mleymm8ab6hg1fqsmwonozjk.png)

6. Add group claim for SAML Response
   1. Click *Edit* on section _User Attributes & Claims

![](https://uploads.developerhub.io/prod/97qW/xb7i8479fdlv0mlvusk50c9nw2ze7r14bk0pexc50silu8tie7j8pcxxpqj4zaj3.png)

_

2.  Click on "Add a group claim", choose "All groups" options(or you can choose what group you want to include in the SAML response) then click **Save

![](https://uploads.developerhub.io/prod/97qW/c3p26egtnc13ztl809i8wmzuqq3pdf2vl4q6vjipmdk1264r0g9iyn1jtur5i4i0.png)

**

7. Download Azure Certificate: this allows My OPSWAT Central Management to verify users signing though a trusted Azure. Each identity provider has a unique X.509 certificate Select Single sign-on on the left navigation, scroll down to SAML Signing Certificate section and and click "Certificate (Base64)" to download the Azure certificate. You need to upload this cert to My OPSWAT Central Management console later.

![](https://uploads.developerhub.io/prod/97qW/40383jmtdvtiq2c86zgmdnro6atb319e5nkkxfdqrr89rd68crymcuyybrpu03if.png)

8. Download Azure metadata for the SDP app. This data will be used to upload to OPSWAT SDP to enable single sign on for your users. Select Single sign-on on the left navigation, scroll down to SAML Signing Certificate section and and click on " Federation Metadata XML " to download IDP metadata file

![](https://uploads.developerhub.io/prod/97qW/e5yd6c96rzuhqzffuh2o1ss7risy1jqlufshfhncgrhis70kd0ul4c5fwl4gwpsj.png)

9. Collect Idp Login URL. Scroll down copy Login URL. Store the URL in somewhere for later use. For example [https://login.microsoftonline.com/60244d0a-5473-4468-b743-f9cc479b7dab/saml2](https://login.microsoftonline.com/60244d0a-5473-4468-b743-f9cc479b7dab/saml2)

![](https://uploads.developerhub.io/prod/97qW/mxij31oni1gmy4c3pb7rzyjevship3wfln59wzoaqbpzn97q57he5e4yic67vzyo.png)

10. Collect *User access URL.* Select Properties and copy User access URL

![](https://uploads.developerhub.io/prod/97qW/7p060xmf16xudoelm6k6smhe5ilnzwujcqakxit5012w1duvtdho55gsn6y8bagi.png)

11. Assign your users/groups to this application

## Step 3. Configure Application and Access Rules on My OPSWAT Central Management

1. Add the Azure Identity Provider. If you already have Azure IdP settings on your My OPSWAT Central Management account, go to step 3.2 to add SDP application.
   1. Log into the My OPSWAT Central Management console.
   2. Navigate to **Secure Access** > **Protected Apps**
   3. Click Add Protected App
   4. Select IdP Method
   5. Select Add new IdP if you have not added your IdP or select your IdP from existing IdP
      1. *IdP Name*: an IdP name, for example: Azure
      2. *IdP Certificate*: upload Azure certificate you downloaded in Step 2.7

![](https://uploads.developerhub.io/prod/97qW/i95ehxiw7oohdicfzo4z3cvbuvzyksw9bztbwhb3yh5f0m8508259mgdi4eagcc8.png)

6.  Click **Continue**

2. Add SDP application:
   1. Expand the Azure IdP settings you have just added in Step 3.1 above.
   2. Click **Add New Application**
   3. Enter required field
      1. *Application*: application name, for example: Demo App
      2. *IdP Login URL*: Embedded " *User access URL* " which you have from Step 2.10
      3. *Application ACS URL*: Embedded "Login URL" which you have from Step 2.9
      4. *Access Mode*: pick an access mode you prefer. See details on the access modes at [Step 2. Add protected applications with IdP Method](https://onlinehelp.opswat.com/metaaccess/Step_2._Add_protected_applications_with_IdP_Method.html)

![](https://uploads.developerhub.io/prod/97qW/97r7jlp6xd35o66pmvm9pkxt2e1f9sakcc8d6ny1m0t5d35ll7lvui38g7un5uio.png)

4.  Click **SAVE** and confirm the change with your PIN

3. After saving your changes successfully, a SSO setup instruction will be shown, copy the **ACS URL** My OPSWAT Central Management generated there and download OPSWAT Certificate. Note that this information can be found in the protected app's details later.

![](https://uploads.developerhub.io/prod/97qW/oilhsn82fj6lq0pk5ia7duki2ze4fptn40h2m191du4lpcps8zpmvrs50f1ptbja.png)

4. Configure Access Rules (this step can be skipped if you have done this step in the past or you can use the default rules):
   1. Navigate to **Secure Access > Rules**, click "**ADD NEW RULE**" to add a new rule for this application OR you can update existing access rules to add this application
   2. With a new access rule, you need to specify how you would like to block/allow access a device from the application
      1. *Rule name*: a rule name, for example Block non-compliant devices
      2. *Action*: Block or Allow
      3. Configure conditions to do the action. Details at [Step 3. Configure Access Rules](https://onlinehelp.opswat.com/metaaccess/Step_3._Configure_Access_Rules.html)
   3. Click **ADD RULE**

![](https://uploads.developerhub.io/prod/97qW/pxxtndizpxi5o9vfe2imzvod187799emz41vrnh0yj1oji9sicmb7xr2tag07ji7.png)

## Step 4. Configure SSO settings on SDP

1. Prepare IdP Metadata File to upload to OPSWAT SDP.
   1. Open the Azure metadata for the SDP app file, you download in step 2.8
   2. Replace all sections **X509Certificate** in the file with the My OPSWAT Central Management certificate downloaded in step 3.3
   3. Replace all sections **SingleSignOnService.Location** in the file with the URL get in step 3.3
   4. Save all changes
2. Login to SDP console ([https://<your account name>.sdp.cloud.impulse.com/login](https://sdp.cloud.impulse.com/login))
3. Go to **Users** and click **Add** button in the section **SAML** to add new IdP

![](https://uploads.developerhub.io/prod/97qW/femic1x29r1oow4qnyu3i72tt9jmhn7xjxs46jwwkdkp5dd66cnmfswk2ixxym3z.png)

4. Choose **Custom IDP** then Click **Next.

![](https://uploads.developerhub.io/prod/97qW/rnki9muk3y9j9s6lun3kq9crklo7bkeko5d0wasj37365vdf8fl5n2zoihku99kk.png)

**

5. On this the Provide SP details to SAML Identity Provide screen, copy value of " Audience / SP Identity" for later use t hen click **Next**

![](https://uploads.developerhub.io/prod/97qW/3ynkfw7gmtnxjh7z2pi5un30ux6ttyyas57u33r9ph9zpnwirmg45r84trhfq8xy.png)

6. Upload the modified Azure metadata for SDP app file, you prepared in the step 4.2 then click **Next**

![](https://uploads.developerhub.io/prod/97qW/27xl3nbbtzkb5grp73hjdtzl7s88q8c4jcbzuz2yf6odxobyurcch1jcippxszez.png)

7. Enter "[http://schemas.microsoft.com/ws/2008/06/identity/claims/groups](http://schemas.microsoft.com/ws/2008/06/identity/claims/groups)" for Group Attribute then click **Next**
8. Click **Create**

## Step 5. Update Applications settings on Identity Provider

1. Log into Azure Portal as administrator
2. Click **Azure Active Directory**.
3. Navigate to **Enterprise applications >** **All applications**.
4. Select the SDP application
5. Select Single sign-on.
6. Click the edit icon (pencil icon) on Basic SAML Configuration section
7. Replace **Identifier** with value got from step 4.6. Replace **Reply URL** with the MetaAccess URL which you got from Step 3.3

![](https://uploads.developerhub.io/prod/97qW/yl59toku0qf6muera80bzg5kcn6205xjetz7w3jgdd67cl4x7yuri98ci07x22cm.png)

8. Click **Save**

## Step 6: Test your integration

Follow guideline at [Step 6: Test your integration](https://onlinehelp.opswat.com/metaaccess/Microsoft_Azure_with_OPSWAT_SDP.html#src-5718880) to test your integration to verify if it works as your expectation.

**DONE! CONGRATULATIONS.**
