<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/salesforce-idp-with-dropbox -->

# Salesforce IdP with Dropbox

My OPSWAT Central Management can be easily integrated with an existing Salesforce Dropbox integration to ensure that a device is compliant with the organization's security policy before it is granted access to Dropbox. This ensures that the device is not only authenticated by the IdP, but also tested for risks and vulnerabilities such as infections or unpatched versions of operating systems, BEFORE it access an organization's cloud services.

To get started with implementing My OPSWAT Central Management integration to enforce device posture check before granting a device to access Dropbox with Salesforce Single Sign On (SSO) service, you set up SSO between Salesforce and Dropbox. If you haven't already done so, please follow the instruction [here](https://www.dropbox.com/guide/admin/security/configure-single-sign-on) to set it up.

You can learn more details for each step here at [Configuration](https://www.opswat.com/docs/cm/secure-access-solution/SAML-SSO-integration-configuration).

## Step 1. Enable Secure Access on your My OPSWAT Central Management account

1. Login to the My OPSWAT Central Management console.
2. Navigate to **Access Control** and then **Configurations.**
3. Check on the box **"Enable Secure Access".**
4. Click **SAVE**.
5. Navigate to **Integrations** and then **Device Identity**, and enable **Enable cross-domain API integration at port xxxx**

![](https://uploads.developerhub.io/prod/97qW/3xcvx8db4yjszpg6r6rz3k7ayx4p42u38pcmurj3vrj94h1bg6hcf3rv1olrynz5.png)

## Step 2. Add protected applications with IdP Method

1. Download Salesforce IdP certificate: the next step is importing an Salesforce X.509 certificate to My OPSWAT Central Management. This allows My OPSWAT Central Management to verify users signing though a trusted IdP, Salesforce. Each identity provider has a unique X.509 certificate. Download the Salesforce X509 certificate by following these steps:
   1. Login to Salesforce as Administrator
   2. Navigate to Setup > Manage Apps > Connected Apps

![](https://uploads.developerhub.io/prod/97qW/s4m8xjm7xzeh5lyqvt6xuy8brnuue1oc5loaioo2kdwy9kt65po6hhzs2o9cjksw.png)

3.  Select the Dropbox application to view the application details

4.  On SAML Service Provider Settings section, click on Idp Certificate

![](https://uploads.developerhub.io/prod/97qW/lmh49euawy7yutkol99waew8gr7zxu8mcpycobxiz2yfksgbibcgdt6n2wrpbi40.png)

5.  Click on Download Certificate to download the Salesforce certificate

![](https://uploads.developerhub.io/prod/97qW/mp5v4ck6qmtmjw8gt6hcjjfkv5alhljc4thhaffv9qca4oryux4jj4tsxu7jtezu.png)

2. Collect Dropbox LoginURL: is a Dropbox single sign-on post back URL of your organization's Dropbox, for example [https://www.dropbox.com/saml_login](https://www.dropbox.com/saml_login)
3. Collect Dropbox Logout URL: you can find this URL inside of Dropbox
   1. Log into your organization's Dropbox account
   2. Click on your avatar, right click on **Sign out** and choose **Copy link address** to get log out URL

![](https://uploads.developerhub.io/prod/97qW/2aijyn4gcb8l8hpeykima2u1gjm5i7nq5uhxi3b6x7zm0cgelrdgtzgkna2252d6.png)

3.  Store the log out URL in somewhere for later use

4. Add the Salesforce Identity Provider. If you already have Salesforce IdP settings on your My OPSWAT Central Management account, go to 5 to add Dropbox application.
   1. Login to the My OPSWAT Central Management console.
   2. Navigate to **Secure Access** and then **Access Methods > IdP**
   3. On the **Identity Providers** tab, click "**Add New Identity Provider**" to add your IdP
   4. Fill in required fields for the Identity Provider
      1. *Identity Provider*: Salesforce
      2. *IdP Name*: an IdP name, for example: Salesforce
      3. *IdP Certificate*: upload Salesforce certificate you downloaded in Step 2.1
   5. Click **Add IDP**
   6. Click **SAVE**
5. Navigate to **Secure Access** and then **Protected Apps**.
6. Add Dropbox application:
   1. Expand the Salesforce IdP settings you have just added in Step 2.4 above.
   2. Click **Add New Application**
   3. Enter required field
      1. *Application*: application name, for example: Dropbox
      2. *Login URL*: application login URL which you have from Step 2.2
      3. *Logout URL*: application logout URL which you have from Step 2.3
      4. *Access Mode*: pick an access mode you prefer. See details on the access modes at [Add Protected Applications with IdP Method](https://www.opswat.com/docs/cm/secure-access-solution/SAML-SSO-add-protected-applications).
   4. Click **SAVE**
7. After saving your changes successfully, click the **Setup Instructions** button of the Dropbox application you have just added and then copy the **URL** My OPSWAT Central Management generated there. This URL is used to replace Dropbox login URL on Salesforce in Step 4.

Note: you can add Dropbox application (step 2.5) when you add Salesforce IdP settings in step 2.4.

## Step 3. Configure Access Rules

1. On My OPSWAT Central Management console, navigate to **Secure Access** and then  Rules
2. On **Rules** tab, click "**ADD NEW RULE**" to add a new rule for this application OR you can update existing access rules to add this application
3. With a new access rule, you need to specify how you would like to block/allow access a device from the application
   1. *Rule name*: a rule name, for example Block non-compliant devices
   2. *Action*: Block or Allow
   3. Configure conditions to do the action. Details at [Configure Access Rules](https://www.opswat.com/docs/cm/secure-access-solution/SAML-SSO-configure-access-rules)
4. Click **ADD RULE**

## Step 4. Update Applications settings on Identity Provider

1. Login to Salesforce as administrator
2. Navigate to Setup > Manage Apps > Connected Apps
3. Select Dropbox application
4. Click Edit
5. Replace **Start URL and ACS URL** with the My OPSWAT Central Management URL which you got from Step 2.6

![](https://uploads.developerhub.io/prod/97qW/uot1am78t6yt059p3bdwjxv28cz6769alogskbcf04vq5ipwx54y9cojwuzys53i.png)

6. Click **Save**

## Step 5. Configure SSO settings on applications

1. On My OPSWAT Central Management console, navigate to **Secure Access** > **Access Methods > IdP**
2. Download OPSWAT certificate
3. Login to Dropbox as an administrator
4. Navigate to **Admin Console** > **Settings**, click **Single sign-on**

![](https://uploads.developerhub.io/prod/97qW/rwayau4fr9n7osyjz3yjpz2uz8jlicnqsqn5u3f0ojz00c176lxxzkg4pun22mh8.png)

5. Click on **Certificate** link and upload the OPSWAT certificate OPSWAT generated for your account (you downloaded in step 5.1)

![](https://uploads.developerhub.io/prod/97qW/hu29y642v8lhnzesjwqeih4so083qh5u74yfa4xd6yaibgkqslr71tc5ye3mjw83.png)

6. Click **Apply Changes**

## Step 6: Test your integration

Follow guideline at [Test Your Integration](https://www.opswat.com/docs/cm/secure-access-solution/test-your-integration) to verify if it works as your expectation.
