<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/okta-with-github -->

# Okta with Github

My OPSWAT Central Management can be easily integrated with an Okta & Github to ensure that a device is compliant with the organization's security policy before it is granted access to Github. This ensures that the user is not only authenticated by Okta, but also a device the user uses to access SaaS applications tested for risks and vulnerabilities such as infections or outdated operating systems, BEFORE it accesses an organization's cloud services.

Follow below steps to integrate My OPSWAT Central Management with your Okta & Github.

## Step 1. Create Application On Okta

1. Login to Okta Admin Dashboard
2. Navigate to **Applications** -> **Applications** then click on **Create App Integration**

![](https://uploads.developerhub.io/prod/97qW/8sfdhiu28zphohiw399xcwd0pmsz3azx9p59mxvql6h8i6mfqw68xn4xpi10vooy.png)

3. Choose **SAML 2.0** and click **Next**

![](https://uploads.developerhub.io/prod/97qW/2w5hbg5e8s07e4fmwyobst1f7e306hub4edv2eyehd74sbw9b9hioos9ucmv5wkx.png)

4. At the **SAML Settings** step, fill with below information:
   - Single sign-on URL: fill with a placeholder, like [*http://localhost*](http://localhost)
   - Audience URI (SP Entity ID): fill with format [*https://github.com/orgs/<your*](https://github.com/orgs/%3Cyour)* organization>*
   - Name ID format: *EmailAddress*

![](https://uploads.developerhub.io/prod/97qW/retaa6v8g5jwsggcy54rkwbu2u90d0p4o5f2foczxom2jskrm1pllxtbzbbkazwq.png)

5. Click **Next** then click **Finish**
6. Navigate to the Github application and click on **General** tab, then copy **Embed Link**

![](https://uploads.developerhub.io/prod/97qW/a5ldirsr35qlgvxe3ycw4k8f7tn91ns9y9zn84h29ayysjtwzpsq1djl3cd951q2.png)

7. Click on **Sign On tab**
8. Copy **Sign on URL**
9. Copy **Issuer**
10. Download **Signing Certificate**

![](https://uploads.developerhub.io/prod/97qW/18482i2s2yog95ytb217e70b7zfxykde8a26rf2tnkv4puh7l9851acbl24471zb.png)

## Step 2. Add application and configure Access Rules on My OPSWAT Central Management

1. Log in to the My OPSWAT Central Management console.
2. Navigate to **Secure Access** > **Protected Apps.**
3. **Check** **"Enable Secure Access".**
4. Click  **SAVE.**
5. Click **Add Protected Application** then choose **IDP METHOD** option**.**
6. Choose option  **Add new IDP ,** enter the name, and upload the certificate got in step 1.10. Then click  **Continue**

![](https://uploads.developerhub.io/prod/97qW/iiui67gywyw4whn7o62ifdhiepmc1mhow2tncl6sgy31l2wfgnfkuzqsalspcprc.png)

7. Enter the required fields
   1. *Application:* application name, for example: Github
   2. *IdP Login URL*: fill in the link that you have from Step 1.6
   3. *IdP Start URL*: fill with the link that you have from Step 1.8
   4. *App ACS URL*: is the Gihub single sign-on post back URL of your organization's Github, format is [https://github.com/orgs/<your organization name>/saml/consume](https://github.com/orgs/Opswat-Inc/saml/consume)
   5. *Access Mode:* pick an access mode you prefer. See details on the access modes at [Step 2. Add protected applications with IdP Method](https://onlinehelp.opswat.com/metaaccess/Step_2._Add_protected_applications_with_IdP_Method.html)

![](https://uploads.developerhub.io/prod/97qW/sm2ayouy7la5xxoxvgpnz3nhqt48fg6fghosfhgo2t9e5rhbpuhh4tadzb3lgsqa.png)

8. After saving successfully, a SSO setup instruction will be shown, copy the ACS URL My OPSWAT Central Management generated there and download the OPSWAT Certificate. Note that this information can be found in the protected app's details later.

![](https://uploads.developerhub.io/prod/97qW/2txmu5v9v8uhrp1nygn49r2861zg6q3r3z08enobzsutrd1hj0mmuc87h9w1p0lu.png)

## Step 3. Update Okta Application

1. Navigate to the application created in Step 1
2. Click on **General** tab, click **Edit** button under **SAML Settings** section
3. Click Next to go to **SAML Settings** section and fill the **Single sign-on URL** with the ACS URL from Step 2.8. Then click **Next** and **Finish**

![](https://uploads.developerhub.io/prod/97qW/0pg2tgkqp04zfuxmvt26t8e7u3n1nql6sxp7g2u1zv2y4jx93b3dkjx2j3e85l90.png)

## Step 4. Configure SSO On Github

1. Login to your Github account and navigate to **Settings** -> **Security** -> **Authentication security**
2. Click Enable SAML authentication and fill the required fields:
   - *Sign on URL*: fill with the ACS URL from Step 2.8
   - *Issuer*: fill with the Issuer from Step 1.9
   - *Public certificate*: open the certificate file from Step 2.8 and copy the content then paste to the public certificate box

![](https://uploads.developerhub.io/prod/97qW/x9r6a1bm5a37byd1efrn6x4ladksalputjzp3zgms104efq38z97sklibp5ziemr.png)

3. Click **Test SAML Configuration**. If the test is successful, click **Save** to complete the setup.
