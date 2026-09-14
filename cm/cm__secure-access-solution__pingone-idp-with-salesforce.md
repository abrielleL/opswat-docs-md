<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/pingone-idp-with-salesforce -->

# PingOne IdP with Salesforce

My OPSWAT Central Management can be easily integrated with an existing PingOne & Salesforce integration to ensure that a device is compliant with the organization's security policy before it is granted access to Salesforce. This ensures that the device is not only authenticated by the IdP, but also tested for risks and vulnerabilities such as infections or unpatched versions of operating systems, BEFORE it access an organization's cloud services.

To get started with implementing My OPSWAT Central Management integration to enforce device posture check before granting a device to access Salesforce with PingOne Single Sign On (SSO) service, you need to have SSO set up between PingOne and Salesforce. If you haven't already done so, please follow the instructions [here](http://saml-doc.okta.com/SAML_Docs/How-to-Configure-SAML-2.0-in-Salesforce.html) to set it up.

You can learn more details for each step here at [Configuration](https://www.opswat.com/docs/cm/secure-access-solution/SAML-SSO-integration-configuration).

## Step 1. Enable Access Control on your My OPSWAT Central Management account

1. Login to the My OPSWAT Central Management console.
2. Navigate to **Secure Access** and then **Protected Apps.**
3. Check on the box **"****Enable Secure Access****"** and configure a port for the cross-domain API. Note that you must select a port which no applications on endpoints is running.
4. Click **SAVE**.

![](https://uploads.developerhub.io/prod/97qW/3xcvx8db4yjszpg6r6rz3k7ayx4p42u38pcmurj3vrj94h1bg6hcf3rv1olrynz5.png)

## Step 2. Add protected applications with IdP Method

1. The next step is importing an PingOne certificate to My OPSWAT Central Management. This allows My OPSWAT Central Management to verify users signing though a trusted IdP. Each identity provider has a unique X.509 certificate. Download the PingOne certificate by following these steps:
   1. Login to PingOne as Administrator
   2. Go to Applications dashboard
   3. Select Salesforce application
   4. Click **Download** on *Signing Certificate* to download certificate

![](https://uploads.developerhub.io/prod/97qW/2uuwradi69s6b166jbtv7xvb6jzf03m2uc9ukhijwq8jnzv055xvh1m3k3hlwyy1.png)

2. Collect Salesforce Login URL
   1. In PingOne, go to Applications page then select the Salesforce app
   2. Copy **ACS URL**

![](https://uploads.developerhub.io/prod/97qW/16c5h6xeyrj1ygxtr8u5tr0aflan978kgcboa46elni995e1ndv584dbgg4oee1u.png)

3. Collect Salesforce Logout URL: you can find this URL inside of Salesforce
   1. Log in to Salesforce
   2. You can find "**Logout**" link when you click on your name
   3. Right-click **Logout** link and select "**Copy link address**" to copy logout URL

![](https://uploads.developerhub.io/prod/97qW/oo7729lgda7im21l0hkic9jhd72pp3739kmxsjxa0h25x0sbr3970qzlbdx8vfjw.png)

4. Add the PingOne Identity Provider. If you already have PingOne IdP settings on your My OPSWAT Central Management account, go to 5 to add Salesforce application.
   1. Login to the My OPSWAT Central Management console.
   2. Navigate to **Secure Access** and then **Access Methods > IdP**
   3. On the **Identity Providers** tab, click "**Add New Identity Provider**" to add your IdP
   4. Fill in required fields for the Identity Provider
      1. *IdP Name*: an IdP name, for example: PingOne
      2. *IdP Certificate*: upload PingOne certificate you downloaded in Step 2.1

![](https://uploads.developerhub.io/prod/97qW/x22y58qq4c61s31eyxssexzskjhrfdpync1sng2x2sh24npxd97n7nmtll1sdq0z.png)

5.  Click **Add IDP**

6.  Click **SAVE**

5. Add the Salesforce application:
   1. Expand the PingOne IdP settings you have just added in Step 2.4 above.
   2. Click **Secure Access > Protected Apps > Add New Application**
   3. Enter required field
      1. *Application*: application name, for example: Salesforce
      2. *IdP Login URL:* get IdP SSO login URL from your PingOne account
      3. *Application Login URL*: application login URL which you have from Step 2.2
      4. *Application Logout URL*: application logout URL which you have from Step 2.3
      5. *Access Mode*: pick an access mode you prefer. See details on the access modes at [Add Protected Applications with IdP Method](https://www.opswat.com/docs/cm/secure-access-solution/SAML-SSO-add-protected-applications)
   4. Click **SAVE**
6. After saving your changes successfully, click the **Setup Instructions** button of the Salesforce application you have just added and then copy the **URL** My OPSWAT Central Management generated there. This URL is used to replace Salesforce login URL on PingOne in Step 4.

Note: you can add Salesforce application (step 2.5) when you add PingOne IdP settings.

## Step 3. Configure Access Rules

1. On My OPSWAT Central Management console, navigate to **Secure Access** and then **Rules**
2. On **Rules** tab, click "**ADD NEW RULE**" to add a new rule for this application OR you can update existing access rules to add this application
3. With a new access rule, you need to specify how you would like to block/allow access a device from the application
   1. *Rule name*: a rule name, for example Block non-compliant devices
   2. *Action*: Block or Allow
   3. Configure conditions to do the action. Details at [Configure Access Rules](https://www.opswat.com/docs/cm/secure-access-solution/SAML-SSO-configure-access-rules)
4. Click **ADD RULE**

## Step 4. Update Applications settings on Identity Provider

1. Login to PingOne
2. Go to **Applications** then **My Applications**
3. Select Salesforce application and click the **Edit** button
4. Click **Continue to Next Step**
5. Replace **ACS URL** with the My OPSWAT Central Management URL which you got from Step 2.6

![](https://uploads.developerhub.io/prod/97qW/18afwtu8zrlim5ae5v57yz6xz3pgrs4j8ecgg45xu1uxive85kv94hlxtfkj7p3f.png)

6. Click **Save**

## Step 5. Configure SSO settings on applications

1. On My OPSWAT Central Management console, navigate to **Secure Access > Access Methods > IdP**
2. Click **Download OPSWAT certificate** to download a self-signed certificate My OPSWAT Central Management generated for your account
3. Login to Salesforce as administrator
4. Navigate to **Setup** > **Security Controls** > **Single Sign-On Settings**, click **Edit** on the SAML Single Sign-On Settings of the PingOne IdP

![](https://uploads.developerhub.io/prod/97qW/svdwvh877omtxw0xnkxe1w961of74ap2jjo4rynu3ncyyyeawlyqy06tweyneef1.png)

5. Upload OPSWAT certificate from your My OPSWAT Central Management account which you downloaded from Step 5.1
6. Click **Save**

## Step 6: Test your integration

Follow guideline at [Test Your Integration](https://www.opswat.com/docs/cm/secure-access-solution/test-your-integration) to verify if it works as your expectation.
