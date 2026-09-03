<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/centrify-idp-with-dropbox -->

# Centrify IdP with Dropbox

My OPSWAT Central Management can be easily integrated with an existing Centrify Dropbox integration to ensure that a device is compliant with the organization's security policy before it is granted access to Dropbox. This ensures that the device is not only authenticated by the IdP, but also tested for risks and vulnerabilities such as infections or unpatched versions of operating systems, BEFORE it accesses an organization's cloud services.

To get started with implementing My OPSWAT Central Management integration to enforce device compliance check before granting a device to access Dropbox with Centrify Single Sign On (SSO) service, you set up SSO between Centrify and Dropbox. If you haven't already done so, please follow the instruction [here](https://docs.centrify.com/en/centrify/appref/index.html?version=1507675723#page/cloudhelp%2Fa-f%2Fsaas_appref_dropbox.html%23) to set it up.

## Step 1. Enable Access Control on your My OPSWAT Central Management account

1. Login to the  My OPSWAT Central Management console.
2. Navigate to **Secure Access > Protected Apps.**
3. Check on the box **"Enable Secure Access ".**
4. Navigate to **Settings > Integrations** and then **Device Identity Tab**, and enable **Enable cross-domain API integration at port xxxx**

## Step 2. Add protected applications with IdP Method

1. Download Centrify IdP certificate: the next step is importing an Centrify X.509 certificate to My OPSWAT Central Management. This allows My OPSWAT Central Management to verify users signing though a trusted IdP, Centrify. Each identity provider has a unique X.509 certificate. Download the Centrify X509 certificate by following these steps:
   1. Login to Centrify as Administrator.
   2. Navigate to **Apps**, then select **Dropbox** application.

![](https://uploads.developerhub.io/prod/97qW/aazxer05nce47say4mmgqbfkezdw7o27av7v89l46z6k41u2om9ya1kxa9xd3o3m.png)

2. From Application Settings, click on the Download button to download Centrify certificate for your account.
3. On SAML Service Provider Settings section, click on Idp Certificate.
4. Click on Download Certificate to download the Centrify certificate.
   1. Collect Dropbox LoginURL: is a Dropbox single sign-on post back URL of your organization's Dropbox, for example                         [https://www.dropbox.com/saml_login](https://www.dropbox.com/saml_login)
   2. Collect Dropbox Logout URL: you can find this URL inside of Dropbox
      1. Log into your organization's Dropbox account.
      2. Click on your avatar, right click on **Sign out** and choose **Copy link address** to get log out URL.
5. Store the log out URL in a note or document file for later use.
   1. Add the Centrify Identity Provider. If you already have Centrify IdP settings on your My OPSWAT Central Management account, go to Step 5 to add Dropbox application.
   2. Login to the My OPSWAT Central Management console
      1. Navigate to **Secure Access > Access Methods > Identity Providers**.
      2. On the **Identity Providers** tab, click **"Create New Identity Provider"** to add your IdP.
      3. Fill in required fields for the Identity Provider:
         1. IdP Name: an IdP name, for example: Centrify
         2. IdP Certificate: upload Centrify certificate you downloaded in **Step 2.1**
   3. Click **SAVE** and confirm with your PIN.
6. Add Dropbox application
   1. Navigate to **Secure Access** > **Protected Apps**. Click **Add Protected Application**. Choose **IdP Method**.
   2. Choose from existing IdPs . Select IdPs from **5.b.d**. Then **Continue**
   3. Enter required field:
      1. _Application name: application name, for example: Dropbox _
      2. *IdP Login URL: application login URL which you have from* ***Step 2.4.a*** __
      3. *Access Mode: pick an access mode you prefer.*
      4. *App ACS URL:  which you have from* ***Step 2.4.a***
   4. Then click **Add**
   5. After saving your changes successfully, click the **SSO Setup Instructions** button of the Dropbox application you have just added and then copy the **ACS URL in the IdP** generated there. This URL is used to replace Dropbox login URL on Centrify in **Step 4**.

Step 3. Configure Access Rules

1. On My OPSWAT Central Management console, navigate to **Secure Access > Rules**
2. On **Rules** tab, click "**ADD NEW RULE**" to add a new rule for this application OR you can update existing access rules to add this application
3. With a new access rule, you need to specify how you would like to block/allow access a device from the application:
   1. *Rule name*: a rule name, for example Block non-compliant devices
   2. *Action*: Block or Allow
   3. Configure conditions to do the action. Details at [Step 3. Configure Access Rules](https://onlinehelp.opswat.com/metaaccess/Step_3._Configure_Access_Rules.html)
4. Click **ADD RULE**

## Step 4. Update Applications settings on Identity Provider

1. Login to Centrify as administrator.
2. Switch to Admin portal.
3. Navigate to **Apps**.
4. Select **Dropbox** application.
5. Select **Advanced** setting.
6. Replace **recipient** URL with the URL My OPSWAT Central Management generated for your app from **Step 2.6.e**

![](https://uploads.developerhub.io/prod/97qW/gl9jvohmrzj0pid20dt0bgmyopzcbktkyefem57i6wg39cur6lfns9blynag9oz2.png)

7. Click **Save.**

## Step 5. Configure SSO settings on applications

1. On My OPSWAT Central Management console, Navigate to **Secure Access > Protected Apps**.
2. Select the Dropbox application and follow the **SSO instructions tab**, you should be prompted to download the **OPSWAT Certificate**.
3. Login to Dropbox as an administrator.
4. Navigate to **Admin Console** > **Settings**, click **Single sign-on.**

![](https://uploads.developerhub.io/prod/97qW/6a3dmgxhncq91cp0737oj9vjzbzokddfgmm2ukml690nn8ly0ewme0blaqjqsmud.png)

5. Click on **Certificate** link and upload the **OPSWAT certificate** generated for your account (you downloaded in **step 5.2**).

![](https://uploads.developerhub.io/prod/97qW/o9k1uizgprlnuh82njv3wscvv1lwnwf98fs58qmaywhvuf6k9vi1n2v2us2aunvr.png)

6. Click **Apply Changes.**

## Step 6: Test your integration

Follow guideline at [Step 6: Test your integration](https://onlinehelp.opswat.com/metaaccess/Step_6__Test_your_integration.html) to test your integration.
