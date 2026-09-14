<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/okta-idp-with-slack -->

# Okta IdP with Slack

My OPSWAT Central Management can be easily integrated with an existing Okta Slack integration to ensure that a device is compliant with the organization's security policy before it is granted access to Slack. This ensures that the device is not only authenticated by the IdP, but also tested for risks and vulnerabilities such as infections or unpatched versions of operating systems, BEFORE it access an organization's cloud services.

o get started with implementing My OPSWAT Central Management integration to enforce device posture check before granting a device to access Salesforce with Okta Single Sign On (SSO) service, you need to have SSO set up between Okta and Salesforce. If you haven't already done so, please follow the instruction [here](http://saml-doc.okta.com/SAML_Docs/How-to-Configure-SAML-2.0-for-Slack.html) to set it up.

You can learn more details for each step here at [Configuration.](https://www.opswat.com/docs/cm/secure-access-solution/SAML-SSO-integration-configuration)

## Step 1. Enable Secure Access on your My OPSWAT Central Management account

1. Login to the My OPSWAT Central Management console.
2. Navigate to **Access Control** and then **Configurations**
3. Select "**Enable Secure Access**"  and configure a port for the cross-domain API. Note that you must select a port which no applications on endpoints is running.
4. Click **SAVE**.

![](https://uploads.developerhub.io/prod/97qW/3xcvx8db4yjszpg6r6rz3k7ayx4p42u38pcmurj3vrj94h1bg6hcf3rv1olrynz5.png)

## Step 2. Add protected applications with IdP Method

1. Download Okta IdP: the next step is importing an Okta X.509 certificate to My OPSWAT Central Management. This allows My OPSWAT Central Management to verify users signing though a trusted IdP, Okta. Each identity provider has a unique X.509 certificate. Download the Okta X509 certificate by following these steps:
   1. Login to Okta as Administrator
   2. Switch to Admin mode

![](https://uploads.developerhub.io/prod/97qW/y02e4x4u57aa65prcumy5zch57kv9wlfn524chtcyhb6mwpazu3d5417odzdlq7f.png)

3.  Go to Applications dashboard

![](https://uploads.developerhub.io/prod/97qW/bz0xu7b3yver6lr33ify3yczc0tlf2q95cco80l79mmh31388aolru709sxqezk3.png)

4.  Select the Slack application which you just added above

5.  Go to **Sign On** tab and click **View Setup Instruction** **

![](https://uploads.developerhub.io/prod/97qW/7atx3nv2qzu3ky8hgiw0lehugwzy8seji1fygt9xze08rwfrc44ojkzsxhhkev3e.png)

**

6.  Copy the Okta certificate and save it to a file, for example okta.cert. Note that the certificate string should be begin with "-----BEGIN CERTIFICATE-----" and end with "-----END CERTIFICATE-----" as the below screenshot.

![](https://uploads.developerhub.io/prod/97qW/lpb0q1sqd7oplfemhik3tvv0nfv3dxh6ev9dyisd1tzsdk5hpcpzk3pi8lzjoz3x.png)

2. Slack LoginURL: is a Slack single sign-on post back URL of your organization's Slack, for example [https://yoursubdomain.slack.com/sso/saml](https://yoursubdomain.slack.com/sso/saml)
3. Collect Slack Logout URL: you can find this URL inside of Slack
   1. Log in to Slack
   2. You can find "**Sign out of <your_subdomain>**" link when you click on your name
   3. Right-click **Sign out of <your_subdomain>** link and select "**Copy link address**" to copy logout URL

![](https://uploads.developerhub.io/prod/97qW/ww0p0z5pw0livn1dwzwzfey6f1rsrslla0riy0z9gusc9gotvv5mdg1dt2wr4mxn.png)

4. Add the Okta Identity Provider. If you already have Okta IdP settings on your My OPSWAT Central Management account, go to 5 to add Slack application.
   1. Login to the My OPSWAT Central Management console.
   2. Navigate to **Access Control** and then **Configurations**
   3. On the **Identity Providers** tab, click "**Add New Identity Provider**" to add your IdP
   4. Fill in required fields for the Identity Provider
      1. *IdP Name*: an IdP name, for example: Okta
      2. *IdP Certificate*: upload Okta certificate you downloaded in Step 2.1

![](https://uploads.developerhub.io/prod/97qW/rt9gz2apc452hreqo6wl4767tzrit3c54q4nqa87q2hz0smtmom50axxn9xls306.png)

5.  Click **Add IDP**

6.  Click **SAVE**

5. Add the Slack application:
   1. Expand the Okta IdP settings you have just added in Step 2.4 above.
   2. Click **Add New Application**
   3. Enter required field
      1. *Application*: application name, for example: Slack
      2. *Login URL*: application login URL which you have from Step 2.2
      3. *Logout URL*: application logout URL which you have from Step 2.3
      4. *Access Mode*: pick an access mode you prefer. See details on the access modes at [Add Protected Applications with IdP Method](https://www.opswat.com/docs/cm/secure-access-solution/SAML-SSO-add-protected-applications)

![](https://uploads.developerhub.io/prod/97qW/gi66soedvfesjc99l7usvuunswlne1jc4hpujic4hoqgcmxz0e8ljmjt4dkwrar7.png)

4.  Click **SAVE**

6. After saving your changes sucessfully, click the **Setup Instructions** button of the Slack application you have just added and then copy the **URL** My OPSWAT Central Management generated there. This URL is used to replace Slack domain on Okta in Step 4.

![](https://uploads.developerhub.io/prod/97qW/zls5vlljrv7eu4zzicjhoiwqij3uict33nf9rxo2kcpi5kjliy793m8lm9387xt6.png)

Note: you can add Slack application (step 2.5) when you add Okta IdP settings.

## Step 3. Configure Access Rules

1. On My OPSWAT Central Management console, navigate to **Access Control** and then **Configurations**
2. On **Access Rules** tab, click "**ADD NEW RULE**" to add a new rule for this application OR you can update existing access rules to add this application
3. With a new access rule, you need to specify how you would like to block/allow access a device from the application
   1. *Rule name*: a rule name, for example Block non-compliant devices
   2. *Action*: Block or Allow
   3. Configure conditions to do the action. Details at [Configure Access Rules](https://www.opswat.com/docs/cm/secure-access-solution/SAML-SSO-configure-access-rules)
4. Click **ADD RULE**

![](https://uploads.developerhub.io/prod/97qW/cqn38bvo4csmxug2c4tfir1ht6qr17u85urzy7wkjazp3yuk94g9aytu6my9zi2o.png)

## Step 4. Update Applications settings on Identity Provider

1. Login to Okta as administrator
2. Go to Applications dashboard
3. Select Slack application
4. On **General** tab, click Edit on the App Settings box

![](https://uploads.developerhub.io/prod/97qW/flvpbzsr9by3wgxp80f7dpccj074yvdazkgjutcutnywbzky9vihjjevae0h9fui.png)

5. Replace **Domain** with the My OPSWAT Central Management URL which you got from Step 2.6 and click **SAVE**

![](https://uploads.developerhub.io/prod/97qW/vcjew5iik9rx68lemiwtvxu9uuf0vpqwqn3ujznnjscoxggorjquajw66uzp6tv3.png)

## Step 5. Configure SSO settings on applications

1. On My OPSWAT Central Management console, navigate to **Access Control** > **Configurations**
2. Click **Download OPSWAT certificate** to download a self-signed certificate My OPSWAT Central Management generated for your account

![](https://uploads.developerhub.io/prod/97qW/1caa8xkk4oy8vrt3zl5b2s49xaklhyh9v6poc15afnf4zmjbrcsaldbdu44ad0yq.png)

3. Login to Slack as a workspace owner
4. Navigate to **Workspace settings** > **Authentication**, click **Change Settings** on the *SAML Authentication Settings*

![](https://uploads.developerhub.io/prod/97qW/34od18vqsj36zwaljr9imxq7j27yauphq3hxzfjkdd5hoci18scakg0lxnfqchf6.png)

5. Click Edit on Public Certificate and copy your OPSWAT certificate from your My OPSWAT Central Management account which you downloaded from Step 5.1

![](https://uploads.developerhub.io/prod/97qW/waqcsr8cjxbkkjswaxaptqeqekai0lut9fuz705d77i958qimfartz1d2k99r7jy.png)

6. Click **Save Configuration**

## Step 6: Test your integration

Follow guideline at [Test Your Integration](https://www.opswat.com/docs/cm/secure-access-solution/test-your-integration) to verify if it works as your expectation.

**Known issues**

- My OPSWAT Central Management couldn't do on-going monitor if a user logs into Slack by Slack app
