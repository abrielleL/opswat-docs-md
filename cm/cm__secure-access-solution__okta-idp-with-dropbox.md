<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/okta-idp-with-dropbox -->

# Okta IdP with Dropbox

My OPSWAT Central Management can be easily integrated with an existing Okta Dropbox integration to ensure that a device is compliant with the organization's security policy before it is granted access to Dropbox. This ensures that the device is not only authenticated by the IdP, but also tested for risks and vulnerabilities such as infections or unpatched versions of operating systems, BEFORE it access an organization's cloud services.

To get started with implementing My OPSWAT Central Management integration to enforce device posture check before granting a device to access Dropbox with Okta Single Sign On (SSO) service, you set up SSO between Okta and Dropbox manually as below steps even you already have SSO set up for Dropbox on Okta. The built-in Dropbox application doesn't allow you to modify a LoginURL of Dropbox.

Reference: [How to configure](https://www.dropbox.com/guide/admin/security/configure-single-sign-on) [Dropbox](https://www.dropbox.com/guide/admin/security/configure-single-sign-on) [single sgin on with an identity provider](https://www.dropbox.com/guide/admin/security/configure-single-sign-on)

1. Log into the Okta console as an Administrator
2. Switch to Admin view, navigate to Application

![](https://uploads.developerhub.io/prod/97qW/gvpnwnsn3nigcfb233qxd4houqo1dds5raznhdcxfs5pct19wyy4ohjjfhrhetm6.png)

![](https://uploads.developerhub.io/prod/97qW/nziseqot2trww8dt3avso8sqsa7p0igz4oxswzlpdmptf6d1sv69klnokzg5qj7i.png)

3. Click **Add Application**

![](https://uploads.developerhub.io/prod/97qW/phwxmr0rvim6fqhwasj7bny0e8x1feyxxy62e4c6s88phxx5yj8e2jaq3mwbowwx.png)

4. Click "**Create New App**" button to create an application manually

![](https://uploads.developerhub.io/prod/97qW/g1bix03efk9a8xt2znww5wjrelufwyoy8a94ywwiqqt8s3eqqscb8p9uuhyqdfdt.png)

5. Select **SAML 2.0** option and click **Create**

![](https://uploads.developerhub.io/prod/97qW/vet0f37416o4to30vg2j0dq8a97nmy1f6343j5gvbpvqcm0qm4qn5ay0wmllbma6.png)

6. On the step **1 General Settings**, fill in the app name and upload a new logo for the app if needed, then click Next

![](https://uploads.developerhub.io/prod/97qW/ow3qhw1rojowj9nhsic8uaszyu18o78y4qvz96l3qd6p8uehryviwosri7zodcer.png)

7. On the step **2 Configure SAML**, fill in the below information and then click Next
   1. *Single sign-on URL* is a Dropbox single sign-on post back URL: [https://www.dropbox.com/saml_login](https://www.dropbox.com/saml_login)
   2. *Audience URL (SP Entity ID)*: [https://www.dropbox.com](https://www.dropbox.com)
   3. *Name ID format*: EmailAddress
   4. *Application username*: Okta username

![](https://uploads.developerhub.io/prod/97qW/o4p4tg378rywtqzh6toxh1oaw61xpx42me56eib1tjzilqtjks1d7vv4mezj4f50.png)

8. On the step **3 Feedback**, select the option "**I'm an Okta customer adding an internal app**" and click Finish

![](https://uploads.developerhub.io/prod/97qW/hasxkpxp63btegmbzh2e40v14cfpa1xlga9jjgrc6cs7nykqy7nhu76aloywis6h.png)

9. On Sign On tab, you can view Setup instructions to get IdP metadata and follow guideline [here](https://www.dropbox.com/guide/admin/security/configure-single-sign-on) to set up single sign-on settings on Dropbox.
10. On Assignments tab, click on Assign to assign person you want to allow to access this application

![](https://uploads.developerhub.io/prod/97qW/7yqcakeb6zqov7f0hijdjj7ikya2pvpw5x40j08rcimna2aaq6twx8oq0u8esg4u.png)

After configuring SSO, you should test it out to make sure that SSO works as expected.

Now it's the time you can implement integration My OPSWAT Central Management with your Okta Dropbox by following the below steps. You can learn more details for each step here at

## Step 1. Enable Secure Access on your My OPSWAT Central Management account

1. Login to the My OPSWAT Central Management console
2. Navigate to **Secure Access** and then **Configurations**
3. Check on the box **"Enable Secure Access"**
4. Click **SAVE**

![](https://uploads.developerhub.io/prod/97qW/3xcvx8db4yjszpg6r6rz3k7ayx4p42u38pcmurj3vrj94h1bg6hcf3rv1olrynz5.png)

## Step 2. Add protected applications with IdP Method

1. Download Okta IdP: the next step is importing an Okta X.509 certificate to My OPSWAT Central Management. This allows My OPSWAT Central Management to verify users signing though a trusted IdP, Okta. Each identity provider has a unique X.509 certificate. Download the Okta X509 certificate by following these steps:
   1. Login to Okta as Administrator
   2. Switch to Admin mode

![](https://uploads.developerhub.io/prod/97qW/5ie4yuaeuv0ry72fcgviwchbq66uq0n4j1wdiik1d07dbsfonsmr6arb2nj6ya52.png)

3.  Go to Applications dashboard

![](https://uploads.developerhub.io/prod/97qW/yyscgas4wvm3x8b6xpjkairpa17jy3fsrobvxlqkfkun5g4076debh32pn2nwq8g.png)

4.  Select the Dropbox application which you just added above

5.  Go to **Sign On** tab and click **View Setup Instruction**

![](https://uploads.developerhub.io/prod/97qW/b9sh2v0cn417bmbebdmalprd0opphb6jpfdte0bsmyz5tihyz4d3yndjaeeovrii.png)

**

6.  Search for **X.509 Certificate** and c lick **Download certificate** to download Okta certificate

![](https://uploads.developerhub.io/prod/97qW/rr909g2o70nik83zi2655rhmqjqaqw0sv3xyphc3iuj2xyjoq55ef02ewa2to2dh.png)

2. Dropbox LoginURL: is a Dropbox single sign-on post back URL of your organization's Dropbox, for example [https://www.dropbox.com/saml_login](https://www.dropbox.com/saml_login)
3. Collect Dropbox Logout URL: you can find this URL inside of Dropbox
   1. Log into your organization's Dropbox account
   2. Click on your avatar, right click on **Sign out** and choose **Copy link address** to get log out URL

![](https://uploads.developerhub.io/prod/97qW/vgxymvtbq7bpcvywkv9gydacig2ax3tl1cf4xkw2bvft33vfq0g6g6hnrzmcyvpq.png)

3.  Store the log out URL in somewhere for later use

4. Add the Okta Identity Provider. If you already have Okta IdP settings on your My OPSWAT Central Management account, go to 5 to add Dropbox application.
   1. Login to the My OPSWAT Central Management console.
   2. Navigate to **Access Control** and then **Configurations**
   3. On the **Identity Providers** tab, click "**Add New Identity Provider**" to add your IdP
   4. Fill in required fields for the Identity Provider
      1. *IdP Name*: an IdP name, for example: Okta
      2. *IdP Certificate*: upload Okta certificate you downloaded in Step 2.1

![](https://uploads.developerhub.io/prod/97qW/um4xqhns1a15np3805br2g6684njqk021tztof02hp46pgevg1we9v8gzkj9vymy.png)

5.  Click **Add IDP**

6.  Click **SAVE**

5. Add Dropbox application:
   1. Expand the Okta IdP settings you have just added in Step 2.4 above.
   2. Click **Add New Application**
   3. Enter required field
      1. *Application*: application name, for example: Dropbox
      2. *Login URL*: application login URL which you have from Step 2.2
      3. *Logout URL*: application logout URL which you have from Step 2.3
      4. *Access Mode*: pick an access mode you prefer. See details on the access modes at [Add Protected Applications with IdP Method](https://www.opswat.com/docs/cm/secure-access-solution/SAML-SSO-add-protected-applications)

![](https://uploads.developerhub.io/prod/97qW/qzzzlw1bhq598znwvei1iowh26b53j9fq6f78uas2c8yr18ubui08h1kv7cp7vik.png)

4.  Click **SAVE**

6. After saving your changes sucessfully, click the **Setup Instructions** button of the Dropbox application you have just added and then copy the **URL** My OPSWAT Central Management

    generated there. This URL is used to replace Dropbox login URL on Okta in Step 4.

![](https://uploads.developerhub.io/prod/97qW/e3j308x494dan5ax36vhp9892ua7jae3h8piyhbbk6w8wyoc04ct7upjfizhzagg.png)

Note: you can add Dropbox application (step 2.5) when you add Okta IdP settings in step 2.4.

## Step 3. Configure Access Rules

1. On My OPSWAT Central Management console, navigate to **Access Control** and then **Configurations**
2. On **Access Rules** tab, click "**ADD NEW RULE**" to add a new rule for this application OR you can update existing access rules to add this application
3. With a new access rule, you need to specify how you would like to block/allow access a device from the application
   1. *Rule name*: a rule name, for example Block non-compliant devices
   2. *Action*: Block or Allow
   3. Configure conditions to do the action. Details at [Configure Access Rules](https://www.opswat.com/docs/cm/secure-access-solution/SAML-SSO-configure-access-rules)
4. Click **ADD RULE**

![](https://uploads.developerhub.io/prod/97qW/m7kqb803pxtpjl0vv4nwmns9u27fger6dngp9jzkwbu5qhjshex3d994sre2370z.png)

## Step 4. Update Applications settings on Identity Provider

1. Login to Okta as administrator
2. Go to Applications dashboard
3. Select Dropbox application
4. On **General** tab, click Edit on the SAML Settings box
5. Click **Next** at the first step
6. Replace **Single sign on URL** with the My OPSWAT Central Management URL which you got from Step 2.6

![](https://uploads.developerhub.io/prod/97qW/kwtocmw8fsd3lo6s86mpzbahflq8lsfhul9oxd2e1s2bsyyj99taljz60cg825kd.png)

7. Click **Next** and **Finish**

## Step 5. Configure SSO settings on applications

1. On My OPSWAT Central Management console, navigate to **Secure Access **> **Configurations**
2. Download OPSWAT certificate
3. Login to Dropbox as an administrator
4. Navigate to **Admin Console** > **Settings**, click **Single sign-on**

![](https://uploads.developerhub.io/prod/97qW/uvi59f2kcpkbdmdn0rihxgznl54tvif972n010o6os1m4k6w63261d0rzdzshqhn.png)

5. Click on **Certificate** link and upload the OPSWAT certificate OPSWAT generated for your account (you downloaded in step 5.1)

![](https://uploads.developerhub.io/prod/97qW/8t0rbdr9nvfz2apd109ihns6hn1hkvnsw75zpu5qlb6ucto437pncsryp918reuk.png)

6. Click **Apply Changes**

## Step 6: Test your integration

Follow guideline at [Test Your Integration](https://www.opswat.com/docs/cm/secure-access-solution/test-your-integration) to verify if it works as your expectation.
