<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/okta-idp-with-o365-using-saml-2-0 -->

# Okta IdP with O365 using SAML 2.0

My OPSWAT Central Management can be easily integrated with an existing Okta O365 integration to ensure that a device is compliant with the organization's security policy before it is granted access to O365. This ensures that the device is not only authenticated by the IdP, but also tested for risks and vulnerabilities such as infections or unpatched versions of operating systems, BEFORE it access an organization's cloud services.

To get started with implementing My OPSWAT Central Management integration to enforce device posture check before granting a device to access O365 with Okta Single Sign On (SSO) service, you set up SSO between Okta and O365 manually as below steps even you already have SSO set up for O365 on Okta. The built-in O365 application doesn't allow you to modify a LoginURL of O365 .

1. Log into Okta console as an Administrator
2. Switch to Admin view, navigate to Application

![](https://uploads.developerhub.io/prod/97qW/nfuzqabmusrrs9up01jatpp73r6isqa0396q4e2kc1osxbecqa0rgthhbxkexhfd.png)

![](https://uploads.developerhub.io/prod/97qW/noh5s969j28xquoz75gjh4phkh2bahkkiikakchcvsiw5lw0b37fsyu0low3jjml.png)

3. Click **Add Application**

![](https://uploads.developerhub.io/prod/97qW/zw6qf9mfqmvn1n291rfmn4s909bh8wu8b0a8ftd44h1dfizip67fy8vf677nha11.png)

4. Click " **Create New App** " button to create an application manually

![](https://uploads.developerhub.io/prod/97qW/nxdmetfbs5c7z67prbsfglu5e0nhespx1kve596l9g2m2ye3rob6i3dptsry8srk.png)

5. Select **SAML 2.0** option and click **Create

![](https://uploads.developerhub.io/prod/97qW/rm7o426qvcotiv96ubewqjrooh2yq05uaklh0ml3gbxm4ofymus93gnzvd87jfeh.png)

**

6. On the step **1 General Settings**, fill in the app name and upload a new logo for the app if needed, then click Next

![](https://uploads.developerhub.io/prod/97qW/2n6ljd02jtckdl0wbobk3ah11i0g924nbnuen4g23v9v9d80wcv568y46d3kwot1.png)

7. On the step 2 **Configure SAML**, fill in the below information and then click Next
   1. *Single sign-on URL*: [https://login.microsoftonline.com/login.srf](https://login.microsoftonline.com/login.srf)
   2. *Audience URL (SP Entity ID)*: urn:federation:MicrosoftOnline
   3. *Default RelayState*: your organization's URL
   4. *Name ID format*: Unspecified
   5. *Application username*: Okta username
   6. In *Attribute Statement*, you need to add two more attributes "ImmutableID" and "IDPEmail" as the below:

![](https://uploads.developerhub.io/prod/97qW/uwutdibi4wxy043oajzly5ej8l4mo48rx0z87slmhlhzo8a5kdj98fk8go16v4rn.png)

8. On the step 3 Feedback, select the option "I'm an Okta customer adding an internal app" and click Finish

![](https://uploads.developerhub.io/prod/97qW/qw916qs3k20xj69077nit00wlrc0j4mgmdqwbrivn0ywy5fn21vqwtwn7xt1vimd.png)

9. On Assignments tab, click on Assign to assign person you want to allow to access this application

![](https://uploads.developerhub.io/prod/97qW/xqo1ct51r86qggmofxn8wjg6r00mj4nl33vrjd56sjfnw7gw2qwjpivra0figh7r.png)

10. Follow [Microsoft guideline](https://docs.microsoft.com/en-us/powershell/module/MSOnline/?view=azureadps-1.0&redirectedfrom=msdn) to install Windows PowerShell for Azure Active Directory .
11. Follow [Okta guideline](https://help.okta.com/en/prod/Content/Topics/Directory/ad-agent-new-integration.htm) to install Okta Active Directory agent to sync your Active Directory users to Okta.
12. You should test the configuration to make sure that users can log into O365 from the Okta app you just create.

Now it's the time you can integrate My OPSWAT Central Management with your Okta O365 by following below steps. You can learn more details for each step here at [3.1.1. How to set it up?](https://onlinehelp.opswat.com/metaaccess/3.1.1._How_to_set_it_up_.html)

- [Step 1. Enable Access Control on your My OPSWAT Central Management account](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_O365_using_SAML_2.0.html#step-1-enable-access-control-on-your-metaaccess-account)
- [Step 2. Add protected applications with IdP Method](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_O365_using_SAML_2.0.html#step-2-add-protected-applications-with-idp-method)
- [Step 3. Configure Access Rules](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_O365_using_SAML_2.0.html#step-3-configure-access-rules)
- [Step 4. Update Applications settings on Identity Provider](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_O365_using_SAML_2.0.html#step-4-update-applications-settings-on-identity-provider)
- [Step 5. Configure SSO settings on Office 365](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_O365_using_SAML_2.0.html#step-5-configure-sso-settings-on-office-365)
- [Step 6: Test your integration](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_O365_using_SAML_2.0.html#step-6-test-your-integration)

## Step 1. Enable Access Control on your My OPSWAT Central Management account

1. Login to the My OPSWAT Central Management console.
2. Navigate to **Access Control** and then **Configurations.**
3. Check on the box **"****Enable access control****"** and configure a port for the cross-domain API. Note that you must select a port which no applications on endpoints is running.
4. Click **SAVE**.

![](https://uploads.developerhub.io/prod/97qW/uu21jbinojpahoic7j31949lf7g5uvxi8fnlx4lrk25nkzyhxd8ge98qoomp6p5b.png)

## Step 2. Add protected applications with IdP Method

1. Download Okta IdP: the next step is importing an Okta X.509 certificate to My OPSWAT Central Management. This allows My OPSWAT Central Management to verify users signing though a trusted IdP, Okta. Each identity provider has a unique X.509 certificate. Download the Okta X509 certificate by following these steps:
   1. Login to Okta as Administrator
   2. Switch to Admin mode

![](https://uploads.developerhub.io/prod/97qW/co6vv3jup6t2rm95j46h0oycodcbur5okqypql0fvqygi0ji0ulxm0h8os17cknw.png)

3.  Go to Applications dashboard

![](https://uploads.developerhub.io/prod/97qW/am0wecvw8jpkyvfd5y7dt3nijbuenjotkyu6hk4kdmirktioq8arclwzcedwo19t.png)

4.  Select O365 application

5.  Go to **Sign On** tab and click **View Setup Instruction**

![](https://uploads.developerhub.io/prod/97qW/msk68o8zwy2b5bi87l688wlppg2gmavnphex6dpn8t9dy77yvwdfnnvkor41rp9z.png)

6.  Click **Download certificate** to download Okta certificate

![](https://uploads.developerhub.io/prod/97qW/tz4j7o9biq9tu80pgq3v79alqkfwk6db41wfip0qdps7ui0bhf9lm113f41cj694.png)

2. Collect Idp Login URL: this is an embed link which Okta generated for the app to embed outside Okta. You can find this URL on General tab, scroll down to the App Embed Link section

![](https://uploads.developerhub.io/prod/97qW/225tvm4jfiq9smly7ty1mr4e3r725om9vlowkfh7dvth3hvul27egzen89afjxjk.png)

3. Add the Okta Identity Provider. If you already have Okta IdP settings on your My OPSWAT Central Management account, go to 4 to add O365 application.
   1. Login to the My OPSWAT Central Management console.
   2. Navigate to **Access Control** and then **Configurations**
   3. On the **Identity Providers** tab, click "**Add New Identity Provider**" to add your IdP
   4. Fill in required fields for the Identity Provider
      1. *IdP Name*: an IdP name, for example: Okta
      2. *IdP Certificate*: upload Okta certificate you downloaded in Step 2.1

![](https://uploads.developerhub.io/prod/97qW/wwtjdsesvh6hhz8elcnx1i3w8aweivu9fqohef0i185joa0yveyp36hlzii8cevy.png)

5.  Click **Add IDP**

6.  Click **SAVE**

4. Add the O365 application:
   1. Expand the Okta IdP settings you have just added in Step 2.3 above.
   2. Click **Add New Application**
   3. Enter required field
      1. *Application*: application name, for example: O365
      2. *IDP Login URL*: application login URL which you have from Step 2.2
      3. *Login URL*: [https://login.microsoftonline.com/login.srf](https://login.microsoftonline.com/login.srf)
      4. *Logout URL*: [https://login.microsoftonline.com/logout.srf](https://login.microsoftonline.com/logout.srf)
      5. *Access Mode*: pick an access mode you prefer. See details on the access modes at [Step 2. Add protected applications with IdP Method](https://onlinehelp.opswat.com/metaaccess/Step_2._Add_protected_applications_with_IdP_Method.html)

![](https://uploads.developerhub.io/prod/97qW/hlayswdj4mflj283dsa1yzprwu1rfrgud6itvdoomgriyxdiqunyfns80545ayn8.png)

4.  Click **SAVE**

5. After saving your changes sucessfully, click the **Setup Instructions** button of the O365 application you have just added and then copy the **URL** My OPSWAT Central Management generated there. This URL is used to replace O365 Single sign on URL on Okta.

![](https://uploads.developerhub.io/prod/97qW/t8ouu9h8aotgt2h4y6jcp2yx5puvu74v1e2o30v9sl675wusv1so61wqzxtgwm4d.png)

Note: you can add O365 application (step 2.4) when you add Okta IdP settings.

## Step 3. Configure Access Rules

1. On My OPSWAT Central Management console, navigate to **Access Control** and then **Configurations**
2. On **Access Rules** tab, click "**ADD NEW RULE**" to add a new rule for this application OR you can update existing access rules to add this application
3. With a new access rule, you need to specify how you would like to block/allow access a device from the application
   1. *Rule name*: a rule name, for example Block non-compliant devices
   2. *Action*: Block or Allow
   3. Configure conditions to do the action. Details at [Step 3. Configure Access Rules](https://onlinehelp.opswat.com/metaaccess/Step_3._Configure_Access_Rules.html)
4. Click **ADD RULE**

![](https://uploads.developerhub.io/prod/97qW/0p53nso26rtphwmsjdxezar3c0l58annrjc7juy5ezkzp8cysmf7ku9j1js244oe.png)

## Step 4. Update Applications settings on Identity Provider

1. Login to Okta as administrator
2. Go to Applications dashboard
3. Select O365 application
4. On **General** tab, click Edit on the SAML Settings box
5. Click **Next** at the first step
6. Replace **Single sign on URL** with the MetaAccess URL which you got from Step 2.5

![](https://uploads.developerhub.io/prod/97qW/old9nmqj8nexybv0kr0qgajjmrezlxs1spo96i0fvfpp63sfhlc7zlec7qy1j1zs.png)

7. Click **Next** and **Finish**

## Step 5. Configure SSO settings on Office 365

1. Get **IssuerUri** and **PassiveLogOnUri** from Okta
   1. Login to Okta as administrator
   2. Go to Applications dashboard
   3. Select O365 application
   4. On **Sign On** tab, click **View Setup Instructions**
   5. Get **IssuerUri** and **PassiveLogOnUri**_

![](https://uploads.developerhub.io/prod/97qW/oq0c6e2v8ypt5p4qmu9afwtqcu8gncfgfavhhod8rkpwqeivtkrs6xpwdy5pyis1.png)

_

2. Click **Download OPSWAT certificate** to download a self-signed certificate MetaAccess generated for your account

![](https://uploads.developerhub.io/prod/97qW/muhfkxyp3c2w195utos4kpkm0jvyhyrqlow4unyd0u7mlpql8ptklqour64faoiu.png)

3. Converting your domain in Office 365 to federated
   1. Login to a computer installed Windows PowerShell for Azure Active Directory
   2. Start PowerShell and run **Connect-MsolService** cmdlet and enter your administrator credentials for your Office 365 domain when prompted

```plaintext
C:\Windows\system32>Connect-MsolService
```

3.  Run **Set-MsolDomainAuthentication** cmdlet

```plaintext
C:\Windows\system32>Set-MsolDomainAuthentication `
-FederationBrandName MetaAccess `
-DomainName <Your Domain>`
-Authentication Federated `
-IssuerUri <IssuerUri in step 5.1> `
-PassiveLogOnUri <PassiveLogOnUri  in step 5.1>`
-LogOffUri https://login.microsoftonline.com/logout.srf `
-PreferredAuthenticationProtocol SAMLP `
-SigningCertificate <OPSWAT Certificate in step 5.2>
```

**Note**: enter the certificate on a single line without break line

4.  Run following cmdlet to verify configuration

```plaintext
C:\Windows\system32>Get-MsolDomainFederationSettings -DomainName <Your Domain>
```

**Note**: it can take some time for Office 365 to apply new configuration

## Step 6: Test your integration

Follow guideline at [Step 6: Test your integration](https://onlinehelp.opswat.com/metaaccess/Step_6__Test_your_integration.html) to test your integration to verify if it works as your expectation.

**DONE! CONGRATULATIONS.**
