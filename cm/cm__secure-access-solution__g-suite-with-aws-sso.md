<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/g-suite-with-aws-sso -->

# G-Suite with AWS SSO

My OPSWAT Central Management can be easily integrated with an existing G-Suite & AWS SSO integration to ensure that a device is compliant with the organization's security policy before it is granted access to AWS Console. This ensures that the user is not only authenticated by G-Suite, but also a device the user uses to access SaaS applications tested for risks and vulnerabilities such as infections or outdated operating systems, BEFORE it access an organization's cloud services.

To get started with implementing My OPSWAT Central Management integration to enforce device posture check before granting a device to access AWS with G-Suite service.

After configuring SSO, you should test it out to make sure that SSO works as expected.

Now it's the time you can integrate My OPSWAT Central Management with your G-Suite & AWS SSO by following the below steps. You can learn more details for each step here at [Configuration.](https://www.opswat.com/docs/cm/secure-access-solution/SAML-SSO-integration-configuration)

## Step 1. Enable Access Control on your My OPSWAT Central Management account

1. Log into the My OPSWAT Central Management console.
2. Navigate to **Secure Access** > **Protected Apps**
3. Check **"Enable Secure Access".**
4. Click **SAVE**.
5. Navigate to **Integrations** and then **Device Identity**, and enable **Enable cross-domain API integration at port xxxx**

## Step 2. Add protected applications with IdP Method on My OPSWAT Central Management

1. Log into G-Suite admin console
2. Go to **Apps > Web and mobile apps** then click on your application. For example: AWS

![](https://uploads.developerhub.io/prod/97qW/lx9ym6yqnpv12idumc0fetx4ygv8lllphsk8qewz1uhp84843ygc7wj0xb6l2xfi.png)

3. Download G-Suite certificate: the next step is importing an G-Suite certificate to My OPSWAT Central Management. This allows My OPSWAT Central Management to verify users signing though a trusted G-Suite. Download the certificate by following these steps:
   1. Click on **Download Metadata** on the left and click the download button to download the certificate

![](https://uploads.developerhub.io/prod/97qW/zx2heyvcomojdbfrhdhm9z42gwitz7fb0vrpg9jwyjwhfjy7d2p2tfz5a0o7m81z.png)

4. Collect Idp Login URL
   1. In the **Download Metadata** popup, scroll down and copy **SSO URL**

![](https://uploads.developerhub.io/prod/97qW/mmwvso2lj22z8ei9fxtocd7p3r3bglbii50f7kbjpj7d5vtgka1u3oex4ls9x9jw.png)

5. Collect **AWS SSO Sign-in URL**
   1. Login to your AWS console then go to **AWS SSO > Settings** then click on the **Change** link in the section **Identity source

![](https://uploads.developerhub.io/prod/97qW/ccob24rwojf3lbjh63rbaofjbel7ycx0aj4w1ue78y1seufkxkhmlsphpmqglovv.png)

6. **Show individual metadata values** then copy **AWS SSO Sign-in URL

![](https://uploads.developerhub.io/prod/97qW/2tbiv6g04agq8z9r1nf3v7gkgyztg2lbpdb1eptmnj26y8znk890qc60a89s8tnm.png)

**

7. Add AWS application on My OPSWAT Central Management:
8. Log into the My OPSWAT Central Management console.
9. Navigate to **Secure Access** > **Protected Apps**
10. Click **Add Protected Application** then choose **IDP METHOD** option
11. Choose option **Add new IDP**, enter name and upload the certificate got in step 2.3. Then **Continue**
12. Enter required field

- *Application*_:_ application name, for example: aws
- *IDP*: choose the IDP created in the previous step
- *IdP Login URL*: fill with the link which you have from Step 2.5
- *App ACS URL*: fill with the link which you have from Step 2.4
- *Access Mode*: pick an access mode you prefer. See details on the access modes at [Add Protected Applications with IdP Method](https://www.opswat.com/docs/cm/secure-access-solution/SAML-SSO-add-protected-applications).

8. Enter your pin then click **SAVE**
9. After saving your changes successfully, it shows a popup, copy the **URL** My OPSWAT Central Management generated there and download                     Opswat Certificate.
10. *Configure Access Rules*. This step can be skipped if you have done this step in the past or you can use the default rules

- Navigate to **Secure Access > Rules**
- Click **"ADD NEW RULE"**
- With a new access rule, you need to specify how you would like to block/allow access a device from the application
  - *Rule name*: a rule name, for example Block non-compliant devices
  - *Action*: Block or Allow
  - Configure conditions to do the action. Details at [Configure Access Rules](https://www.opswat.com/docs/cm/secure-access-solution/SAML-SSO-configure-access-rules)
- Click **ADD RULE**

![](https://uploads.developerhub.io/prod/97qW/lcuk0481irhknc8333mc3zvyugwy7jtd16uy9pn3vno6yg0pcndk6nrj5v87ajzv.png)

## Step 3. Update Applications settings on G-Suite

1. Log into G-Suite admin console
2. Navigate to your application
3. Click to section **Service provider details** then replace the **ACS URL** with the link got in step 2.7

![](https://uploads.developerhub.io/prod/97qW/xhoy2gy8wlh68g8zhej38vlacmzo4x346plk6ygbg1k8hnheqa1zac1ga9h7hm2i.png)

4. Click **Save**

## Step 4. Configure SSO settings on AWS SSO

1. Login to your AWS console then go to **AWS SSO > Settings** then click on the **Change** link in the section **Identity source**
2. Go to the section **Identity provider metatdata**
3. Fill **IdP sign-in URL** with the URL link got in step 2.7
4. Upload OPSWAT certificate got in step 2.7 to **IdP certificate**
5. Click **Next Review**

![](https://uploads.developerhub.io/prod/97qW/hye0ovlbaubrisk4ep2gzfl2ta1k6smbtnalmkon9qulhelagyp2ebqigkst2e0p.png)

## Step 5: Test your integration

Follow guideline at [Test Your Integration ](https://www.opswat.com/docs/cm/secure-access-solution/test-your-integration)to verify if it works as your expectation.
