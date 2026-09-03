<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/okta-idp-with-a-protected-app-through-okta-access-gateway -->

# Okta IdP with a protected app through Okta Access Gateway

My OPSWAT Central Management can be easily integrated with an existing Okta Access Gateway to ensure that a device is compliant with the organization's security policy before it is granted access to protected applications which connected with Okta Access Gateway. This ensures that the device is not only authenticated by the IdP, but also tested for risks and vulnerabilities such as infections or unpatched versions of operating systems BEFORE it accesses an organization's on-premise applications.

To get started with implementing My OPSWAT Central Management integration to enforce device posture check before granting a device to access protected applications with Okta Access Gateway, you need to have your protected app configured on Okta Access Gateway and [configured Okta tenant as an IdP for Okta Access Gateway](https://help.okta.com/en/prod/Content/Topics/Access-Gateway/configure-idp-okta.htm). If you haven't already done so, please follow the instructions [on Okta Help Center](https://help.okta.com/en/prod/Content/Topics/Access-Gateway/admin-ui-console-overview.htm) to add your applications to Okta Access Gateway.

**Note: Please be aware that this integration needs to **[**update SAML settings of the protected app on Okta**](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_a_protected_app_through_Okta_Access_Gateway.html#step-4-update-applications-settings-on-identity-provider)**, and you need to re-do that if you make any changes of the app on Okta Access Gateway to make sure that a connection between Okta and OPSWAT MetaAccess still exists.**

You can learn more details for each step here at [3.1.1. How to set it up?](https://onlinehelp.opswat.com/metaaccess/3.1.1._How_to_set_it_up_.html)

- [Step 1. Enable Access Control on your My OPSWAT Central Management account](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_a_protected_app_through_Okta_Access_Gateway.html#step-1-enable-access-control-on-your-metaaccess-account)
- [Step 2. Add protected applications with IdP Method](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_a_protected_app_through_Okta_Access_Gateway.html#step-2-add-protected-applications-with-idp-method)
- [Step 3. Configure Access Rules](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_a_protected_app_through_Okta_Access_Gateway.html#step-3-configure-access-rules)
- [Step 4. Update Applications settings on Identity Provider](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_a_protected_app_through_Okta_Access_Gateway.html#step-4-update-applications-settings-on-identity-provider)
- [Step 5: Test your integration](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_a_protected_app_through_Okta_Access_Gateway.html#step-5-test-your-integration)

## Step 1. Enable Access Control on your My OPSWAT Central Management account

1. Login to the My OPSWAT Central Management console.
2. Navigate to **Access Control** and then **Configurations**
3. Check on **"****Enable access control****"** and configure a port for the cross-domain API. Note that you must select a port which no applications on endpoints are running.
4. Click **SAVE**.

![](https://uploads.developerhub.io/prod/97qW/94cgl7pcmlg975qqwiper9wes5xa0xvkmwexn83lurdqrlozpyvg9d9oeubl5sgt.png)

## Step 2. Add protected applications with IdP Method

1. Download Okta IdP certificate: the next step is importing an Okta X.509 certificate to My OPSWAT Central Management. This allows My OPSWAT Central Management to verify users signing though a trusted IdP, Okta. Each identity provider has a unique X.509 certificate. Download the Okta X509 certificate by following these steps:
   1. Log into Okta as Administrator
   2. Switch to Admin mode

![](https://uploads.developerhub.io/prod/97qW/82n1fg0xn0njo1yjtd9q3zsglkv04laysjdmqiny3bh2oyqzanrcgvmfvur4p3v8.png)

3.  Go to Applications dashboard

![](https://uploads.developerhub.io/prod/97qW/vp6eafufl70qajvnvoko1fwv321uyaflydkv7f1347bwa6xxo3hiy31c4t5einpl.png)

4.  Select your application

5.  Go to **Sign On** tab and click **View Setup Instruction** **

![](https://uploads.developerhub.io/prod/97qW/qjhlt8bhaqfpjfi726vziri6d7joxaeba95f1abqrto3otg77e2qi5gq29crmnjo.png)

**

6.  Click **Download certificate** to download Okta certificate

![](https://uploads.developerhub.io/prod/97qW/89oe2st1qs4ncc91bnvlrjb3kno6vz5lmtvvv1p3j181stp00aexbwe39ujibbs6.png)

2. Collect the application ACS URL and IdP SSO login URL
   - In Okta Administrator console, select Applications, then select your protected application
   - The **Assertion Consumer Service** URL is the Single sign on URL on the **SAML Settings** section on the General tab

![](https://uploads.developerhub.io/prod/97qW/35isw8bxng4kn4aldbhvu0etlknymclreygpltpwk8obr4gtq83s6jtjnemvrs29.png)

- on the General tab, scroll down to App Embed Link section,
- The IdP SSO login URL is the embed link

![](https://uploads.developerhub.io/prod/97qW/frh9kcbwy0j6v0zcbckel0rr0cif5qosxcs404b4szrx0shqz5rcpeh28q67wdx0.png)

4. Add the Okta Identity Provider. If you already have Okta IdP settings on your My OPSWAT Central Management account, go to step 2.5 to add your application.

- Login to the My OPSWAT Central Management
- Navigate to **Access Control** and then **Configurations**
- On the **Identity Providers** tab, click "**Add New Identity Provider**" to add your IdP
- Fill in required fields for the Identity Provider
  - *IdP Name*: an IdP name, for example, Okta
  - *IdP Certificate*: upload Okta certificate you downloaded in Step 2.1

![](https://uploads.developerhub.io/prod/97qW/8ntramoxk44g7d1nbbbr4bc53viwuto8m7s7a80sulm084ncq68h58c1ej1wxlt5.png)

- Click **Add IDP**
- Click **SAVE CHANGES**

5. Add your protected application:

- Expand the Okta IdP settings you have just added in Step 2.4 above.
- Click **Add New Application**
- Fill required fields. Other optional settings are in the Advanced Settings
  - *Application*: application name, for example, Protected Application
  - *IdP Login URL: IdP SSO login URL which you have from step 2.2*
  - *Application Login URL*: application login URL which you have from Step 2.2
  - *Access Mode*: pick an access mode you prefer. See details on the access modes at [Step 2. Add protected applications with IdP Method](https://onlinehelp.opswat.com/metaaccess/Step_2._Add_protected_applications_with_IdP_Method.html)

![](https://uploads.developerhub.io/prod/97qW/l04bf96gpjv403kcbvf6z8up1c3k6pyoaj2t3sw21eio98m58me31k0ffyw2zmbt.png)

- Click **SAVE CHANGES**

6. After saving your changes successfully, click Setup Instructions of your application, you have just added and then copy the URL My OPSWAT Central Management generated there. This URL is used to replace Single sign on URL of the application on Okta in Step 4.

![](https://uploads.developerhub.io/prod/97qW/k5dhfb53w9z4sj7yiuntt6ylz2wmriwqsb93pnd0cufredlfe9qocucj9dhekq6i.png)

Note: you can add your application (step 2.5) when you add Okta IdP settings.

## Step 3. Configure Access Rules

1. On My OPSWAT Central Management console, navigate to **Access Control** and then **Configurations**
2. On **Access Rules** tab, click "**ADD NEW RULE**" to add a new rule for this application OR you can update existing access rules to add this application
3. With a new access rule, you need to specify how you would like to block/allow access a device from the application
   1. *Rule name*: a rule name, for example Block non-compliant devices
   2. *Action*: Block or Allow
   3. Configure conditions to do the action. Details at [Step 3. Configure Access Rules](https://onlinehelp.opswat.com/metaaccess/Step_3._Configure_Access_Rules.html)
4. Click **ADD RULE**

![](https://uploads.developerhub.io/prod/97qW/w11rrum4143uqfonb5duktg5dg62ksnvu0tqbipr1sol7xuyyu75rv84h7mn5tv2.png)

## Step 4. Update Applications settings on Identity Provider

1. Login to Okta as administrator
2. Navigate to Applications dashboard
3. Select your application
4. On **General** tab, click Edit on the SAML Settings section

![](https://uploads.developerhub.io/prod/97qW/rxo00zg3jzj6duwuso7png58gvznl7ckukb7s30qyqjk8c18szb4roarqjddrxm5.png)

5. Click Next on the first screen

- uncheck " Use this for Recipient URL and Destination URL" option first so that we can configure different URL for Single sign on URL and recipient URL.
- replace **Single sign on URL** with the My OPSWAT Central Management URL which you got from Step 2.6

![](https://uploads.developerhub.io/prod/97qW/qhyj5kbklzp0thjpb92njug00k31wqnqlaid75ux2gkdzjjxish0gapbcveejjrc.png)

6. Click Next
7. Click Finish

## Step 5: Test your integration

Follow guideline [here](https://onlinehelp.opswat.com/metaaccess/Step_6__Test_your_integration.html) to test your integration to verify if it works as your expectation.

**DONE! CONGRATULATIONS.**
