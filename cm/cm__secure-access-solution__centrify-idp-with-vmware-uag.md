<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/centrify-idp-with-vmware-uag -->

# Centrify IdP with VMware UAG

My OPSWAT Central Management can be easily integrated with an existing Centrify & VMware UAG SSO workflow to ensure that a device complies with the organization's My OPSWAT Central Management policy before it is granted access to VMware UAG. This ensures that the device is not only authenticated by Centrify, but is also tested for risks and vulnerabilities (such as infections or unpatched versions of operating systems) *before* it accesses an organization's services.

To get started with implementing My OPSWAT Central Management integration to enforce device compliance check before granting a device to access VMware UAG with Centrify Single Sign On (SSO) service, you need to set up SSO between Centrify and VMware UAG.

You can learn more details for each step [here](https://docs.opswat.com/macloud-sdp/secure-access/configuration).

## Step 1. Enable Access Control on your My OPSWAT Central Management account

1. Login to My OPSWAT Central Management console.
2. Navigate to **Secure Access** and then **Protected Apps.**
3. Check on the box **Enable Secure Access .**
4. Click **SAVE**.

## Step 2. Add protected applications with IdP Method

1. Download Centrify IdP certificate. This allows My OPSWAT Central Management to verify users signing though a trusted IdP, Centrify. Each identity provider has a unique X.509 certificate. Download the Centrify X509 certificate by following these steps:
   1. Login to Centrify as Administrator
   2. Navigate to **Apps**, then select the VMware UAG application
2. Go to Trust > Identity Provider Configuration > Signing Certificate

![](https://uploads.developerhub.io/prod/97qW/lq9p2fnlmt4vj3jhjowwrhoqz5nelfvz2ol08418tpaohv8v13qmwkw3u6m8v8iq.png)

3. Click on **Download Certificate** to download the Centrify certificate.
4. Collect Single Sign On URL:
   1. Go to **Trust**** ****> Identity Provider Configuration***.* Then click on **Manual**** ****Configuration**
   2. Copy **Single Sign On** URL field
5. Add the Centrify Identity Provider. If you already have Centrify IdP settings on your My OPSWAT Central Management account, go to step 6 to add VMware UAG application.
   1. Login to the My OPSWAT Central Management console.
   2. Navigate to **Secure Access** and then **Protected Apps**.
   3. Click **Add a Protected Application** and select **IdP Method**.
   4. Fill in required fields for the Identity Provider:
      1. *Identity Provider*: Centrify
      2. *IdP__Name*: an IdP name, for example: Centrify
      3. *IdP__Certificate*: upload Centrify certificate you downloaded**.**
      4. Click **Continue**.
6. Add VMware UAG application by expanding  the Centrify IdP settings you have just added.
   1. *Application*_:_ application name, for example: UAG
   2. *IdP__Login URL*: login UAG Portal URL, for example: https://<UAG port domain:port>/portal_Application_
   3. *ACS URL*: URL which you have from Step 2.4
   4. *Access Mode*: pick an access mode you prefer. See details on the[ access modes](https://docs.opswat.com/macloud-sdp/secure-access/add-protected-applications-with-idp-method)
   5. Click **Save.**
7. After saving your changes successfully, click the **Setup Instructions** button of the VMware UAG application you have just added and then copy the **URL** MetaAccess generated there.
8. Download the OPSWAT Certificate as you will need this for later.

![](https://uploads.developerhub.io/prod/97qW/6drj5q5ak8n065w0zawxknzkd40om79nr0jotyb255kl2b7gsu78kprc1v1aqise.png)

*Note: you can add VMware UAG application when you add Centrify IdP settings.*

## Step 3. Configure Access Rules

1. On My OPSWAT Central Management console, navigate to **Secure Access** and then **Rules**
2. Click "**ADD NEW RULE**" to add a new rule for this application OR you can update existing access rules to add this application
3. With a new access rule, you need to specify how you would like to block/allow access a device from the application
   1. *Rule name*: a rule name, for example Block non-compliant devices
   2. *Action*: Block or Allow
   3. Configure conditions to do the action. Details at [Configure Access Rules](https://docs.opswat.com/macloud-sdp/secure-access/access-rules)
4. Click **ADD RULE**

![](https://uploads.developerhub.io/prod/97qW/cktlvpd0pbr7r9bbgi80t4xrwtpseoalkne51e4376s84jsv1ae9ulfunipzmpx5.png)

## Step 4. Update Applications settings on Identity Provider

1. Login to Centrify as administrator
2. Switch to Admin portal
3. Navigate to Apps
4. Select VMware UAG application
5. Go to **Trust > Service Provider Configuration***,* select **Manual Configuration**
6. Replace **Assertion Consumer Service (ACS) URL** with the URL MetaAccess generated for your app.

![](https://uploads.developerhub.io/prod/97qW/z6mahgwgc9kut70el4hw7qxa26evgiej2pju6wm7r6wa2lic9q5wixsjucmq9qba.png)

7. Click **Save**

## Step 5. Configure SSO settings on VMware UAG

1. Using the certificate you downloaded earlier, edit the IDP metadata file you used to configured SSO on VMware UAG with Centrify in the past
   1. Replace X509Certificate with the certificate downloaded in step 5.1
   2. Replace *SingleSignOnService.Location* with the link you get in step 2.5

![](https://uploads.developerhub.io/prod/97qW/frsq53ky0fxfxh60lhsnnxch8o15vj3kn29vf1bxwez57ackevh0jpp1i4g7zrp0.png)

2. Login to VMware UAG admin console
3. Navigate to Identity Bridging Settings > Upload Identity Provider Metadata and upload the                 IdP metadata file you modified.
4. Then click **Save.**

![](https://uploads.developerhub.io/prod/97qW/5tz242b5dmy82rfalumx3v8gtimjqtk29zrndm3nodc025b41ayr4otd46pvyodw.png)

## Step 6: Test your integration

Follow guideline at [Step 6: Test your integration](https://docs.opswat.com/macloud-sdp/secure-access/test-your-integration) to test your integration.
