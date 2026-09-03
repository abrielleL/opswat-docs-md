<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/okta-idp-with-atlassian -->

# Okta IdP with Atlassian

My OPSWAT Central Management can be easily integrated with an existing Okta Atlassian integration to ensure that a device is compliant with the organization's security policy before it is granted access to Atlassian. This ensures that the device is not only authenticated by the IdP, but also tested for risks and vulnerabilities such as infections or unpatched versions of operating systems, BEFORE it access an organization's cloud services.

To get started with implementing My OPSWAT Central Management integration to enforce device posture check before granting a device to access Atlassian with Okta Single Sign On (SSO) service, you set up SSO between Okta and Atlassian manually as below steps even you already have SSO set up for Atlassian on Okta. The built-in Atlassian application doesn't allow you to modify a LoginURL of Atlassian.

Reference: [How to configure Atlassian SAML Single Sign On with an Identity Provider](https://confluence.atlassian.com/cloud/saml-single-sign-on-939718272.html)

1. Log into the Okta console as an Administrator
2. Switch to Admin view, navigate to Application

![](https://uploads.developerhub.io/prod/97qW/efs968u28rj4yb79qcgtu485g3dobrq7z8yr31gxxugwhkvqilzrpddfgqaq72cl.png)

![](https://uploads.developerhub.io/prod/97qW/clq64f0nb26dsnawgdnmaxwx3srxogql1wjayws5qu21spgno8o3s7uxkxvubv91.png)

3. Click **Add Application**

![](https://uploads.developerhub.io/prod/97qW/hyb529nw5dcyl4mfhlc85xg03ak21iby6n8eykrflfcnty7fsp4euryq313b5u2m.png)

4. Click "**Create New App**" button to create an application manually

![](https://uploads.developerhub.io/prod/97qW/mw1dywijrtfpbwlvae8i5m9czrno1ir7r8j9nzlbhocrbp8lw7tkscbdkmc2xhky.png)

5. Select **SAML 2.0** option and click **Create**

![](https://uploads.developerhub.io/prod/97qW/x4l4uacjct21s9ydm5l3s63hvyr3qqou7pbmcd0mfdza2l9wrz3ru34n821vgkk2.png)

6. On the step **1 General Settings**, fill in the app name and upload a new logo for the app if needed, then click Next

![](https://uploads.developerhub.io/prod/97qW/o0nevjsqjf0ecg1cgfowmr12t9uadb06lxn7v9mjda3x9e001e1340r6y8ft8xev.png)

7. On the step **2 Configure SAML**, fill in the below information and then click Next
   1. *Single sign-on URL* is a Atlassian single sign-on post back URL: [https://id.atlassian.com/login](https://id.atlassian.com/login)
   2. *Audience URL (SP Entity ID)*: [https://id.atlassian.com/login](https://id.atlassian.com/login)
   3. *Default RelayState:* your organization's URL, for example: [https://your_domain.atlassian.net](https://your%5C_domain.atlassian.net)
   4. *Name ID format*: Unspecified
   5. *Application username*: Okta username
   6. In Attribute Statement, you need to add 3 more attributes as the below

| Name | Name format | Value |
| ---- | ---- | ---- |
| [http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname](http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname) | Unspecified | user.firstName |
| [http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname](http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname) | Unspecified | user.lastName |
| [http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name](http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) | Unspecified | user.email |

![](https://uploads.developerhub.io/prod/97qW/h047uiuc1tr6lo0gxyyifl4eoii9sef40hj9rzy0zkl2kv1wadzmd3b4z31co1zg.png)

8. On the step **3 Feedback**, select the option "**I'm an Okta customer adding an internal app**" and click Finish

![](https://uploads.developerhub.io/prod/97qW/rimyou13eb0dcc04841mdr5fj5w4rz8ak3yqd0qisal8wofqnquy51y38et99n8t.png)

9. On Sign On tab, you can view Setup instructions to get IdP metadata and follow guideline [here](https://confluence.atlassian.com/cloud/saml-single-sign-on-939718272.html) to set up single sign-on settings on Atlassian.
10. On Assignments tab, click on Assign to assign person you want to allow to access this application

![](https://uploads.developerhub.io/prod/97qW/ydt39opcfmbkrr8vv7oc6l6q9hu7xfrnwkix6e3xr9b244tzblc5t8n3jcmbqlbe.png)

After configuring SSO, you should test it out to make sure that SSO works as expected.

Now it's the time you can implement integration My OPSWAT Central Management with your Okta Atlassian by following the below steps. You can learn more details for each step here at [3.1.1. How to set it up?](https://onlinehelp.opswat.com/metaaccess/3.1.1._How_to_set_it_up_.html)

- [Step 1. Enable Access Control on your My OPSWAT Central Management](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_Atlassian.html#step-1-enable-access-control-on-your-metaaccess-account) account
- [Step 2. Add protected applications with IdP Method](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_Atlassian.html#step-2-add-protected-applications-with-idp-method)
- [Step 3. Configure Access Rules](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_Atlassian.html#step-3-configure-access-rules)
- [Step 4. Update Applications settings on Identity Provider](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_Atlassian.html#step-4-update-applications-settings-on-identity-provider)
- [Step 5. Configure SSO settings on applications](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_Atlassian.html#step-5-configure-sso-settings-on-applications)
- [Step 6: Test your integration](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_Atlassian.html#step-6-test-your-integration)

## Step 1. Enable Access Control on your My OPSWAT Central Management account

1. Login to the My OPSWAT Central Management console.
2. Navigate to **Secure Access** and then **Protected Apps**
3. Check on the box **"****Enable secure access****".**
4. Click **SAVE**.
5. Navigate to **Integrations** and then **Device Identity**, and enable **Enable cross-domain API integration at port xxxx**

## Step 2. Add protected applications with IdP Method

1. Download Okta IdP: the next step is importing an Okta X.509 certificate to My OPSWAT Central Management. This allows My OPSWAT Central Management to verify users signing though a trusted IdP, Okta. Each identity provider has a unique X.509 certificate. Download the Okta X509 certificate by following these steps:
   1. Login to Okta as Administrator
   2. Switch to Admin mode

![](https://uploads.developerhub.io/prod/97qW/x696l2ldrnsa899weu33cd297d9no23n3z7p301za91fhbb8d93kmq7j8ou93819.png)

3.  Go to Applications dashboard

![](https://uploads.developerhub.io/prod/97qW/b818vk4d7p1ecqyvwy8y2fiplwo85ddbr1i3d37b2omzqle376ti60tydvusr5z3.png)

4.  Select the Atlassian application which you just added above

5.  Go to **Sign On** tab and click **View Setup Instruction** **

![](https://uploads.developerhub.io/prod/97qW/pqmtgyftxz4xtynqu6767kqnztlygapt32k04k6481f9xrnwin3atatyi2w6zhdt.png)

**

6.  Search for **X.509 Certificate** and c lick **Download certificate** to download Okta certificate

![](https://uploads.developerhub.io/prod/97qW/qhrpbbqak49mld0hxeyj41zdpe9pzb3hq1xtj9ij1npcfqn6x7vx8re40uhp9gxx.png)

2. IdP Login URL: this is an embed link which Okta generated for the app to embed outside Okta. You can find this URL on General tab, scroll down to the App Embed Link section

![](https://uploads.developerhub.io/prod/97qW/24q1pzevvw1swmzm8b2m0j6w8g5bhsw4i0yzry7xyyyfikirgj2tks3sapde81f0.png)

3. Atlassian LoginURL: is a Atlassian single sign-on post back URL of your organization's Atlassian, for example [https://id.atlassian.com/login](https://id.atlassian.com/login)
4. Collect Atlassian Logout URL: you can find this URL inside of Atlassian
   1. Log into your organization's Atlassian account
   2. Click on your avatar, right click on **Log Out** and choose **Copy link address** to get log out URL

![](https://uploads.developerhub.io/prod/97qW/jxyqhpxwnp0hs4o568oyr43wrwpkh7q61tuzt19f2vn78r8rrsjy9np3u2s30z7m.png)

Store the log out URL in somewhere for later use.

6. Add the Okta Identity Provider. If you already have Okta IdP settings on your My OPSWAT Central Management account, go to 5 to add Atlassian application.
   1. Login to the My OPSWAT Central Management console.
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
10. After saving your changes sucessfully, click the **SSO Setup Instructions** button of the Atlassian application you have just added and then copy the **URL** MetaDefender IT Access generated there. This URL is used to replace Atlassian login URL on Okta in Step 4. Download the OPSWAT Certificate as well.

Note: you can add Atlassian application (step 2.5) when you add Okta IdP settings in step 2.4.

## Step 3. Configure Access Rules

1. On My OPSWAT Central Management console, navigate to **Secure Access** and then **Rules**
2. Click "**ADD NEW RULE**" to add a new rule for this application OR you can update existing access rules to add this application
3. With a new access rule, you need to specify how you would like to block/allow access a device from the application
   1. *Rule name*: a rule name, for example Block non-compliant devices
   2. *Action*: Block or Allow
   3. Configure conditions to do the action. Details at [Step 3. Configure Access Rules](https://onlinehelp.opswat.com/metaaccess/Step_3._Configure_Access_Rules.html)
4. Click **ADD RULE**

## Step 4. Update Applications settings on Identity Provider

1. Login to Okta as administrator
2. Go to Applications dashboard
3. Select Atlassian application
4. On **General** tab, click Edit on the SAML Settings box
5. Click **Next** at the first step
6. Replace **Single sign on URL** and Audience URL with the My OPSWAT Central Management URL which you got from Step 2.6

![](https://uploads.developerhub.io/prod/97qW/zq5ck7fun41eswjhkpkd44dervyg06pqoayu2hz9merr5mkn4btpw897d31r66jl.png)

7. Click **Next** and **Finish**

## Step 5. Configure SSO settings on applications

3. Login to Atlassian as an administrator
4. Navigate to **Atlassian Site Administration > Your organization > SAML single sign-on.**
5. Click **Edit Configuration**
6. Replace **Public x509-certificate** with the OPSWAT certificate which OPSWAT generated for your account (you downloaded already)
7. Click **Save Changes**

## Step 6: Test your integration

Follow guideline at [Step 6: Test your integration](https://onlinehelp.opswat.com/metaaccess/Step_6__Test_your_integration.html) to test your integration to verify if it works as your expectation.

**DONE! CONGRATULATIONS.**
