<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/okta-idp-with-access-gateway -->

# Okta IdP with Access Gateway

My OPSWAT Central Management can be easily integrated with an existing Okta - Access Gateway integration to ensure that a device is compliant with the organization's security policy before it is granted access to applications. This ensures that the device is not only authenticated by the IdP, but also tested for risks and vulnerabilities such as infections or unpatched versions of operating systems BEFORE it accesses an organization's cloud services.

To get started with implementing My OPSWAT Central Management integration to enforce device posture check before granting a device to access applications with Access Gateway with Okta Inbound SAML, you need to have Access Gateway configured with Okta Inbound SAML. If you haven't already done so, please follow the instructions [on Okta Help Center](https://help.okta.com/en/prod/Content/Topics/Access-Gateway/configure-spgw-okta-inbound-saml.htm) to set it up.

You can learn more details for each step here at [3.1.1. How to set it up?](https://onlinehelp.opswat.com/metaaccess/3.1.1._How_to_set_it_up_.html)

- [Step 1. Enable Access Control on your MetaAccess account](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_Access_Gateway.html#step-1-enable-access-control-on-your-metaaccess-account)
- [Step 2. Add protected applications with IdP Method](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_Access_Gateway.html#step-2-add-protected-applications-with-idp-method)
- [Step 3. Configure Access Rules](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_Access_Gateway.html#step-3-configure-access-rules)
- [Step 4. Update Applications settings on Identity Provider](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_Access_Gateway.html#step-4-update-applications-settings-on-identity-provider)
- [https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_Access_Gateway.html#](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_Access_Gateway.html#)
- [Step 5. Configure SSO settings on applications](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_Access_Gateway.html#Step5.ConfigureSSOsettingsonapplications)
- [Step 6: Test your integration](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_Access_Gateway.html#step-6-test-your-integration)

## Step 1. Enable Access Control on your My OPSWAT Central Management account

1. Login to the My OPSWAT Central Management console.
2. Navigate to **Access Control** and then **Configurations.**
3. Check on **"****Enable access control****"** and configure a port for the cross-domain API. Note that you must select a port which no applications on endpoints is running.
4. Click **SAVE**.

![](https://uploads.developerhub.io/prod/97qW/c1w2hiy2dc29vpk0vrc2stoel3ofkaelkofpyjrzyhrapzu9zdrnyd9ophf8ztt2.png)

## Step 2. Add protected applications with IdP Method

1. Download Okta IdP certificate: the next step is importing an Okta X.509 certificate to My OPSWAT Central Management. This allows My OPSWAT Central Management to verify users signing though a trusted IdP, Okta. Each identity provider has a unique X.509 certificate. Download the Okta X509 certificate by following these steps:
   1. Login to Okta as Administrator
   2. Switch to Admin mode

![](https://uploads.developerhub.io/prod/97qW/shikaavkqvwcx0xyd43s2h0hzr36kqz5hlb9u92mogxf5iojcwsanxzsxqkbiilw.png)

3.  Go to Applications dashboard

![](https://uploads.developerhub.io/prod/97qW/g33dgfjny24xeluf41g2ab5b04mnyg8z5yjh3msuh1iytcszmrr015nijdoc1zwt.png)

4.  Select Access Gateway application

5.  Go to **Sign On** tab and click **View Setup Instruction** **

![](https://uploads.developerhub.io/prod/97qW/n4he4b1fsvrep0e1cx6hylvelmpypnqsfpy6i1tpklkvalul2nmle6sfewjclgb1.png)

**

6.  Click **Download certificate** to download Okta certificate

![](https://uploads.developerhub.io/prod/97qW/1oi4gxng9oi8hxb1y88g96fkxj7w3f5e1czgz9mmhd263cu9d9u5l1uvm18mxmna.png)

2. Collect Access Gateway ACS URL
   1. In Okta Administrator console, select Security > Identifier Providers

![](https://uploads.developerhub.io/prod/97qW/5heph2j3f8a75vzjo6phlo05utp1yqyvru9187co2qlvdqq3g0ynlhaaoimjphrg.png)

b. Expand the Okta Inbound SAML you configured for the Access Gateway. Then copy the **Assertion Consumer Service URL**

![](https://uploads.developerhub.io/prod/97qW/nbssbl16bowhf3qaez66yqjy7ctwl3dvtt42dw72s5rm8ja2uor8jjzglhoa8kn0.png)

3. Collect IdP SSO login URL:

- In Okta Administrator console, navigate to Applications > then select Access Gateway app
- on General tab, scroll down to App Embed Link section
- Copy the Embed Link there

![](https://uploads.developerhub.io/prod/97qW/wk71rjh5h4mtvyvgf2eqr0yfu46tsqultwp56kqv9aj1fb1ix35rxl4wvq4g91dz.png)

4. Add the Okta Identity Provider. If you already have Okta IdP settings on your My OPSWAT Central Management account, go to 5 to add Access Gateway application.

- Login to the My OPSWAT Central Management console.
- Navigate to **Access Control** and then **Configurations**
- On the **Identity Providers** tab, click "**Add New Identity Provider**" to add your IdP
- Fill in required fields for the Identity Provider
  - *IdP Name*: an IdP name, for example, Okta
  - *IdP Certificate*: upload Okta certificate you downloaded in Step 2.1

![](https://uploads.developerhub.io/prod/97qW/f8vebg9dwb8sruf8ly1g6yjzc8c4zjedwkjpx3gv1cu3herz2a9jqaehneuz43e4.png)

- Click **Add IDP**
- Click **SAVE CHANGES**

5. Add the Access Gateway application:

- Expand the Okta IdP settings you have just added in Step 2.4 above.
- Click **Add New Application**
- Fill required fields
  - *Application*: application name, for example, Access Gateway
  - *IdP Login URL: IdP SSO login URL which you have from step 2.3*
  - *Application Login URL*: application login URL which you have from Step 2.2
  - *Access Mode*: pick an access mode you prefer. See details on the access modes at [Step 2. Add protected applications with IdP Method](https://onlinehelp.opswat.com/metaaccess/Step_2._Add_protected_applications_with_IdP_Method.html)

![](https://uploads.developerhub.io/prod/97qW/betbwgqpictg04h2h8mkn9t6rqbaltykzwze4bcamulhi1f9b3rbqll8lxbzc8m9.png)

- Click **SAVE CHANGES**

6. After saving your changes successfully, click the **Setup Instructions** button of the Access Gateway application you have just added and then copy the **URL** MetaAccess generated there. This URL is used to replace Single sign on URL of the Access Gateway app on Okta in Step 4.

![](https://uploads.developerhub.io/prod/97qW/82x3kl3g90g9wqciq27qky2njb5tsoezwnzpvmnk4vtqkuxmot708qe83zdqowhu.png)

Note: you can add Access Gateway application (step 2.5) when you add Okta IdP settings.

## Step 3. Configure Access Rules

1. On My OPSWAT Central Management console, navigate to **Access Control** and then **Configurations**
2. On **Access Rules** tab, click "**ADD NEW RULE**" to add a new rule for this application OR you can update existing access rules to add this application
3. With a new access rule, you need to specify how you would like to block/allow access a device from the application
   1. *Rule name*: a rule name, for example Block non-compliant devices
   2. *Action*: Block or Allow
   3. Configure conditions to do the action. Details at [Step 3. Configure Access Rules](https://onlinehelp.opswat.com/metaaccess/Step_3._Configure_Access_Rules.html)
4. Click **ADD RULE**

![](https://uploads.developerhub.io/prod/97qW/x77te1v498zdm2w2tc2kgwn6a7cemg0vioxt56vzltlwtbbx4p7uygaz1db6d8rh.png)

## Step 4. Update Applications settings on Identity Provider

1. Login to Okta as administrator
2. Navigate to Applications dashboard
3. Select Access Gateway application
4. On **General** tab, click Edit on the SAML Settings section

![](https://uploads.developerhub.io/prod/97qW/796fkltd0plkpnegcald9vjlevue92m23ti7jxfg5krh20o64zkxlhwkqiicsdes.png)

5. Click Next on the first screen, then replace Single sign on URL with the My OPSWAT Central Management URL which you got from Step 2.6
6. Click Show Advanced Settings

![](https://uploads.developerhub.io/prod/97qW/rwbpam3utnpdrkxepahoq3so2yxd0iiwwvd158s8kb8vu1atp70qubjm96bl7uok.png)

7. Change Signature Algorithm to RSA-SHA1 and Digest Algorithm to SHA1
8. Click Next
9. Click Finish

## Step 5. Configure SSO settings on applications

1. On My OPSWAT Central Management console, navigate to **Access Control** >**Configurations**
2. Click **Download OPSWAT certificate** to download a self-signed certificate My OPSWAT Central Management generated for your account

![](https://uploads.developerhub.io/prod/97qW/6an0ktmtensyjq6javzca9q21348qs3pjx8rwkaml9ycm7eea2bzurt5fahoorll.png)

3. Log into Okta Administrator console
4. Navigate to **Security** > **Identity Providers**

![](https://uploads.developerhub.io/prod/97qW/vsmovs6ivwqq5m00b1c11dxvpb5ncec4w1tm4ht9jzsnfuqmex5zpv3aajdny4un.png)

5. Click Configure then select Configure Identity Providers on the Okta Inbound SAML you configured for the Access Gateway.

![](https://uploads.developerhub.io/prod/97qW/qghglyliwiyh1ae7vo2k657ddr7fx7kgltqoc9bs0pdfdc2xjdtio82iadpjifpf.png)

6. On the SAML PROTOCOL SETTINGS, replace IdP Signature Certificate to the certificate My OPSWAT Central Management generated for your account as you downloaded at step 5.2
   - Click on x icon to remove the current one
   - upload the new one
7. Click Show Advanced Settings

![](https://uploads.developerhub.io/prod/97qW/83jyo7o5roujq68kiauo0czwb1qmjofck6kwovg64b3a6c5u0sm22xiyg3a4tnyk.png)

8. Change Request Signature Algorithm to SHA-1 and Response Signature Algorithm to SHA-1

![](https://uploads.developerhub.io/prod/97qW/dqkjquqdiwip2nsjhnqmfoq5rdqahp0ht1tlso20va77wwcvuoi7th8ym248fj5m.png)

9. Click Update Identity Provider

## Step 6: Test your integration

Follow guideline at [Step 6: Test your integration](https://onlinehelp.opswat.com/metaaccess/Step_6__Test_your_integration.html) to test your integration to verify if it works as your expectation.

**DONE! CONGRATULATIONS.**
