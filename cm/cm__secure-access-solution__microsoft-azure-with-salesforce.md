<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/microsoft-azure-with-salesforce -->

# Microsoft Azure with Salesforce

My OPSWAT Central Management can be easily integrated with an existing Microsoft Azure & Salesforce integration to ensure that a device is compliant with the organization's security policy before it is granted access to Salesforce. This ensures that the user is not only authenticated by Microsoft Azure, but also a device the user uses to access SaaS applications tested for risks and vulnerabilities such as infections or outdated operating systems, BEFORE it access an organization's cloud services.

To get started with implementing My OPSWAT Central Management integration to enforce device posture check before granting a device to access Salesforce with Microsoft Azure Single Sign On (SSO) service. You set up SSO between Microsoft Azure and Salesforce as guidelines in [Azure Active Directory integration with Salesforce](https://docs.microsoft.com/en-us/azure/active-directory/saas-apps/salesforce-tutorial)

After configuring SSO, you should test it out to make sure that SSO works as expected.

Now it's the time you can integrate My OPSWAT Central Management with your Microsoft Azure & Salesforce by following the below steps. You can learn more details for each step at [Configuration.](https://www.opswat.com/docs/cm/secure-access-solution/SAML-SSO-integration-configuration)

## Step 1. Enable Access Control on your My OPSWAT Central Management account

1. Log into the My OPSWAT Central Management console.
2. Navigate to **Secure Access** > **Protected Apps**
3. Check **"****Enable Secure Access****".**
4. Click **SAVE**.
5. Navigate to **Integrations** and then **Device Identity**, and enable **Enable cross-domain API integration at port xxxx**

![](https://uploads.developerhub.io/prod/97qW/3xcvx8db4yjszpg6r6rz3k7ayx4p42u38pcmurj3vrj94h1bg6hcf3rv1olrynz5.png)

## Step 2. Add protected applications with IdP Method

1. Download Azure Certificate: the next step is importing an Azure X.509 certificate to My OPSWAT Central Management. This allows My OPSWAT Central Management to verify users signing though a trusted Azure. Each identity provider has a unique X.509 certificate. Download the Azure X509 certificate by following these steps:
   1. Log into Azure Portal as Administrator
   2. Click **Azure Active Directory** on the left navigation

![](https://uploads.developerhub.io/prod/97qW/uvcbmdbx88coq0klmuagxskj4yxj3shp85t4svhr28s1es001evrjkoeazfu859z.png)

The Azure Active Directory button

2. Navigate to **Enterprise applications > All applications**.

![](https://uploads.developerhub.io/prod/97qW/d2yaunxtc7xnbebjvpef0n1kl15b3e5csq6i7w837n5dw6y9c51h7ukvedch856w.png)

The Enterprise applications blade

3. Select the Salesforce application
4. Select tab Single sign-on. Scroll down to SAML Signing Certificate area and and click on "Certificate (Base64)" to download certificate

![](https://uploads.developerhub.io/prod/97qW/5uygilg0jltcz01g5qkwn01x0vg7znkk13mapkrxjs4scoigxia9io1i5vbvlkiq.png)

6. Collect Idp Login URL and User access URL
   1. Scroll down copy Login URL. Store the URL in somewhere for later use. For example [https://login.microsoftonline.com/60244d0a-5473-4468-b743-f9cc479b7dab/saml2](https://login.microsoftonline.com/60244d0a-5473-4468-b743-f9cc479b7dab/saml2)
   2. Select Properties and copy User access URL. Store the URL in somewhere for later use. For example [https://myapps.microsoft.com/signin/Salesforce/549c009f-5f75-4beb-9e53-a754dd43a3f4?tenantId=<your_tenant_id](https://myapps.microsoft.com/signin/Salesforce/549c009f-5f75-4beb-9e53-a754dd43a3f4?tenantId=%3Cyour%5C_tenant%5C_id)>

![](https://uploads.developerhub.io/prod/97qW/egqsbyozrrfl9aldw72i9py96ysh9jmdw2nueeiq3jgmo6y9sepz6tmn1wg58xve.png)

![](https://uploads.developerhub.io/prod/97qW/rfevmospxp5limgj8gio9p7s78usjztl53pp13pqu9zd6u7fc7b7j26r4mtajddi.png)

7. Collect Salesforce Logout URL: you can find this URL inside of Salesforce
   1. Log into your Salesforce account
   2. Click on your avatar, right click on **Log Out** and choose **Copy link address** to get log out URL
   3.  Store the log out URL in somewhere for later use

![](https://uploads.developerhub.io/prod/97qW/4mdo1orkctgtej2jeq0b4ahp3f3gj5djokyabgb3fi40a0icm25glhzb66cx4yve.png)

8. Add the Azure Identity Provider. If you already have Azure IdP settings on your My OPSWAT Central Management account, go to step 2.5 to add Salesforce application.
   1. Log into the My OPSWAT Central Management console.
   2. Navigate to **Secure Access** > **Protected Apps**
   3. Click Add New Protected App
   4. select IdP Method
   5. Select your IdP if you already added it or add a new IdP and fill in required fields for the Identity Provider
   6. *IdP Name*: an IdP name, for example: Azure
   7. *IdP Certificate*: upload Azure certificate you downloaded in Step 2.1
   8. Click **Continue**

![](https://uploads.developerhub.io/prod/97qW/6ojwyakcgrml65439im5dqj1k4dnwmoztukm7t0l4h9ygco7rkla64ifqqjb4l4q.png)

9. Add Salesforce application:
   1. Enter required field
   2. *Application*: application name, for example: Salesforce
   3. IdP Login URL: Embedded "User access URL" which you have from Step 2.2
   4. *Login URL*: Embedded "Login URL" which you have from Step 2.2
   5. *Logout URL*: application logout URL which you have from Step 2.3
   6. *Access Mode*: pick an access mode you prefer. See details on the access modes at [Add Protected Applications with IdP Method](https://www.opswat.com/docs/cm/secure-access-solution/SAML-SSO-add-protected-applications).
   7.  Click **ADD**

![](https://uploads.developerhub.io/prod/97qW/2xid06w2a4yc4hdn3n0fxs1abkax8v43a5dax803wrdq2xirarvztgg0wgnkg9if.jpg)

10. After saving your changes successfully, a SSO setup instruction will be shown, copy the **ACS URL** My OPSWAT Central Management generated there and download OPSWAT Certificate. Note that this information can be found in the protected app's details later .

![](https://uploads.developerhub.io/prod/97qW/intumy1zz4ft1386dnmss0bgnvui1j8tdtmyydprkyv8nznneuxp4tnxdpvp6ist.png)

## Step 3. Configure Access Rules

Note: This step can be skipped if you have done this step in the past or you can use the default rules

1. In My OPSWAT Central Management console.
2. Navigate to **Secure Access** > **Rules**
3. click "**ADD NEW RULE**" to add a new rule for this application OR you can update existing access rules to add this application
4. With a new access rule, you need to specify how you would like to block/allow access a device from the application
   1. *Rule name*: a rule name, for example Block non-compliant devices
   2. *Action*: Block or Allow
   3. Configure conditions to do the action. Details at [Configure Access Rules](https://www.opswat.com/docs/cm/secure-access-solution/SAML-SSO-configure-access-rules).
5. Click **ADD RULE**

![](https://uploads.developerhub.io/prod/97qW/vkfys7fnyjzhka7e4jdnn2pqa0qr1l0bpi6prnasmwdwvkl1ek6f7h75eek38whh.png)

## Step 4. Update Applications settings on Identity Provider

1. Log into Azure Portal as administrator
2. Click **Azure Active Directory**.
3. Navigate to **Enterprise applications > All applications**.
4. Select the Salesforce application
5. Select Single sign-on.
6. Click the edit icon (pencil icon) on Basic SAML Configuration section
7. Replace **Reply URL** with the My OPSWAT Central Management URL which you got from Step 2.6

![](https://uploads.developerhub.io/prod/97qW/wkgibff0px3vsbqsm2r4m55wq79iqgmpnjycsc2eqqnfzt9m3yxy8a8dz4fgjc0o.png)

8. Click **Save**

## Step 5. Configure SSO settings on applications

1. Login to Salesforce as an administrator
2. Select Setup
3. Navigate to **Security Controls** > **Single sign-on Settings** and click **Edit** on application

![](https://uploads.developerhub.io/prod/97qW/ttn6dmx94kdzmjyi7ti041nmnfebxyg1msqd5v9a86ubo8blemhbo7z9180z3h03.png)

4. Click on **Choose File** to upload the OPSWAT certificate that My OPSWAT Central Management generated for your account (you downloaded in step 2.6)

![](https://uploads.developerhub.io/prod/97qW/pk2t2r6wk1kenoly9j2ssm8g6c6b06ec8ewsl2kn799qb9lkx20adgk2mwlgecva.png)

5. Change Identity Provider Login URL to the ACS URL My OPSWAT Central Management generated for your application that you got from Step 2.6
6. Select Service Provider Initiated Request Binding to **Redirect**
7. Click **Save**

## Step 6: Test your integration

Follow guideline at [Test Your Integration ](https://www.opswat.com/docs/cm/secure-access-solution/test-your-integration)to verify if it works as your expectation.
