<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/okta-idp-with-salesforce -->

# Okta IdP with Salesforce

My OPSWAT Central Management can be easily integrated with an existing Okta Salesforce integration to ensure that a device is compliant with the organization's security policy before it is granted access to Salesforce. This ensures that the device is not only authenticated by the IdP, but also tested for risks and vulnerabilities such as infections or unpatched versions of operating systems, BEFORE it access an organization's cloud services.

To get started with implementing My OPSWAT Central Management integration to enforce device posture check before granting a device to access Salesforce with Okta Single Sign On (SSO) service, you need to have SSO set up between Okta and Salesforce. If you haven't already done so, please follow the instruction [here](http://saml-doc.okta.com/SAML_Docs/How-to-Configure-SAML-2.0-in-Salesforce.html) to set it up.

- [Step 1. Enable Access Control on your My OPSWAT Central Management account](https://www.opswat.com/docs/cm/secure-access-solution/okta-idp-with-salesforce#step-1-enable-access-control-on-your-my-opswat-central-management-account)
- [Step 2. Add protected applications with IdP Method](https://www.opswat.com/docs/cm/secure-access-solution/okta-idp-with-salesforce#step-2-add-protected-applications-with-idp-method)
- [Step 3. Configure Access Rules](https://www.opswat.com/docs/cm/secure-access-solution/okta-idp-with-salesforce#step-3-configure-access-rules)
- [Step 4. Update Applications settings on Identity Provider](https://www.opswat.com/docs/cm/secure-access-solution/okta-idp-with-salesforce#step-4-update-applications-settings-on-identity-provider)
- [Step 5. Configure SSO settings on applications](https://www.opswat.com/docs/cm/secure-access-solution/okta-idp-with-salesforce#step-5-configure-sso-settings-on-applications)
- [Step 6: Test your integration](https://www.opswat.com/docs/cm/secure-access-solution/okta-idp-with-salesforce#step-6-test-your-integration)

## Step 1. Enable Access Control on your My OPSWAT Central Management account

1. Login to the My OPSWAT Central Management console.
2. Navigate to **Access Control** and then **Configurations.**
3. Check on the box **"****Enable access control****"** and configure a port for the cross-domain API. Note that you must select a port which no applications on endpoints is running.
4. Click **SAVE**.

![](https://uploads.developerhub.io/prod/97qW/ew1jgadkuv4hnz5jkov4eobxpdarrpoblgb1aaxh4haoszx3ztcsq90ew4fgc53u.png)

## Step 2. Add protected applications with IdP Method

1. Download Okta IdP: the next step is importing an Okta X.509 certificate to My OPSWAT Central Management. This allows My OPSWAT Central Management to verify users signing though a trusted IdP, Okta. Each identity provider has a unique X.509 certificate. Download the Okta X509 certificate by following these steps:
   1. Login to Okta as Administrator
   2. Switch to Admin mode

![](https://uploads.developerhub.io/prod/97qW/aoxy58cawqmto60clceoyhefrywwf2xvbyv50z03ika9f3vr5uvw6yymbvi772ct.png)

3.  Go to Applications dashboard

![](https://uploads.developerhub.io/prod/97qW/kfo0diwv2iuee5iyq6hqv7upu69kqn437fgopi4whleq2aw4egdowsmka6xuk90z.png)

4.  Select Salesforce application

5.  Go to **Sign On** tab and click **View Setup Instruction** **

![](https://uploads.developerhub.io/prod/97qW/8gzfozjikb8xognu1ueez8b4za9ofoztzdcpwd5caz6ykmo9gfix0n0nzzjdqjal.png)

**

6.  Click **Download certificate** to download Okta certificate

![](https://uploads.developerhub.io/prod/97qW/9vckuti5mel73djdborlnrat5lrowaq25wc8t35fht13dp6gn3e5frp2ssjykok1.png)

2. Collect Salesforce Login URL
   1. In Okta, select the **Sign On** tab for the Salesforce app
   2. Copy **Login URL** under **Avanced Sign-on Settings**

![](https://uploads.developerhub.io/prod/97qW/xbmhdegslnt897ovftpkb2eps8pmywpyjt75zmqd5jzbwxt0ctakwlgg4vhshilb.png)

3. Collect IdP SSO login URL:
   1. In Okta, go to Salesforce app
   2. on General tab, scroll down to App Embed Link section
   3. Copy the embed link there

-

![](https://uploads.developerhub.io/prod/97qW/i3g9asnds0zthm4ntb36eijq7wabhopyecm6aorm0r2qzeau6mgrb0hu987wsxef.png)

4. Collect Salesforce Logout URL: you can find this URL inside of Salesforce
   1. Log in to Salesforce
   2. You can find "**Logout**" link when you click on your name
   3. Right-click **Logout** link and select "**Copy link address**" to copy logout URL

![](https://uploads.developerhub.io/prod/97qW/gvx40f09y8ahj2lllpk6hd3h1u2853hl9fuz6m62l9hzzyuhg72gh644adyu9qpt.png)

5. Add the Okta Identity Provider. If you already have Okta IdP settings on your My OPSWAT Central Management account, go to 5 to add Salesforce application.
   1. Login to the My OPSWAT Central Management console.
   2. Navigate to **Access Control** and then **Configurations**
   3. On the **Identity Providers** tab, click "**Add New Identity Provider**" to add your IdP
   4. Fill in required fields for the Identity Provider
      1. *IdP Name*: an IdP name, for example: Okta
      2. *IdP Certificate*: upload Okta certificate you downloaded in Step 2.1

![](https://uploads.developerhub.io/prod/97qW/bxnlvlmhr87wuu653a3adrts6zhmwdafkmpsrt1uhzxfdaqe7olflitskrh0szmq.png)

5.  Click **Add IDP**

6.  Click **SAVE**

6. Add the Salesforce application:
   1. Expand the Okta IdP settings you have just added in Step 2.4 above.
   2. Click **Add New Application**
   3. Enter required field
      1. *Application*: application name, for example: Salesforce
      2. *IdP Login URL: IdP SSO login URL which you have from step 2.3*
      3. *Application Login URL*: application login URL which you have from Step 2.2
      4. *Application Logout URL*: application logout URL which you have from Step 2.4
      5. *Access Mode*: pick an access mode you prefer. See details on the access modes at [Step 2. Add protected applications with IdP Method](https://onlinehelp.opswat.com/metaaccess/Step_2._Add_protected_applications_with_IdP_Method.html)

![](https://uploads.developerhub.io/prod/97qW/sz0uxgddfv20c5u8vhuxlrok5rpe9pluge56spyggwmin2jzk2jdhnxllxn0n7qf.png)

4.  Click **SAVE**

7. After saving your changes sucessfully, click the **Setup Instructions** button of the Salesforce application you have just added and then copy the **URL** My OPSWAT Central Management generated there. This URL is used to replace Salesforce login URL on Okta in Step 4.

![](https://uploads.developerhub.io/prod/97qW/tbq8w922iqc3iqyxkqrqbu92ozyl0oju5rwopl6xofygy0dx55esw9x9p1lcjr9g.png)

Note: you can add Salesforce application (step 2.5) when you add Okta IdP settings.

## Step 3. Configure Access Rules

1. On My OPSWAT Central Management console, navigate to **Access Control** and then **Configurations**
2. On **Access Rules** tab, click "**ADD NEW RULE**" to add a new rule for this application OR you can update existing access rules to add this application
3. With a new access rule, you need to specify how you would like to block/allow access a device from the application
   1. *Rule name*: a rule name, for example Block non-compliant devices
   2. *Action*: Block or Allow
   3. Configure conditions to do the action. Details at [Step 3. Configure Access Rules](https://onlinehelp.opswat.com/metaaccess/Step_3._Configure_Access_Rules.html)
4. Click **ADD RULE**

![](https://uploads.developerhub.io/prod/97qW/o4f8r5eeli25bpa7pl5w18l4h3uwfntxmk39xfm5gmt2u72mqempee4k3n0wul8z.png)

## Step 4. Update Applications settings on Identity Provider

1. Login to Okta as administrator
2. Go to Applications dashboard
3. Select Salesforce application
4. On **Sign On** tab, click Edit
5. Replace **Login URL** with the My OPSWAT Central Management URL which you got from Step 2.6

![](https://uploads.developerhub.io/prod/97qW/xx5wn6cyzgebb6ced6fo2q454s2i2yaxxyzn2yck1ntz2fqrzgkjb38z9llk8qiw.png)

6. Click **Save**

## Step 5. Configure SSO settings on applications

1. On My OPSWAT Central Management console, navigate to **Access Control** > **Configurations**
2. Click **Download OPSWAT certificate** to download a self-signed certificate My OPSWAT Central Management generated for your account

![](https://uploads.developerhub.io/prod/97qW/02k1p6d70ucyyeaum9w8hmbpk2kbpi3r3ifa7fvpin50llucmii8c2cxhckzz7r2.png)

3. Login to Salesforce as administrator
4. Navigate to **Setup** > **Security Controls** > **Single Sign-On Settings**, click **Edit** on the SAML Single Sign-On Settings of the Okta IdP

![](https://uploads.developerhub.io/prod/97qW/sz54f4es8283th0he0796ko5oljv93kdl87xefrj4u0pcjkgf7w9nai3srraf4dq.png)

5. Upload OPSWAT certificate from your My OPSWAT Central Management account which you downloaded from Step 5.1

![](https://uploads.developerhub.io/prod/97qW/lsom185aauo8vnmpuyggix51epzmsmlqzi2fy3l6e4r6l1ej4x7h2usrc1ei52r0.png)

6. Click **Save**

## Step 6: Test your integration

Follow guideline at [Step 6: Test your integration](https://onlinehelp.opswat.com/metaaccess/Step_6__Test_your_integration.html) to test your integration to verify if it works as your expectation.

**DONE! CONGRATULATIONS.**
