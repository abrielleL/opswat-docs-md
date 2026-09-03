<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/okta-idp-with-o365-using-ws-federation -->

# Okta IdP with O365 using WS-Federation

My OPSWAT Central Management can be easily integrated with an Okta O365 integration to ensure that a device is compliant with the organization's security policy before it is granted access to O365. This ensures that the device is not only authenticated by the IdP, but also tested for risks and vulnerabilities such as infections or unpatched versions of operating systems, BEFORE it access an organization's cloud services.

To get started with implementing My OPSWAT Central Management integration to enforce device posture check before granting a device to access O365 with Okta Single Sign On (SSO) service, you set up SSO between Okta and O365 manually as below steps even you already have SSO set up for O365 on Okta. The built-in O365 application doesn't allow you to modify a LoginURL of O365 .

1. Log into Okta console as an Administrator
2. Switch to Admin view

![](https://uploads.developerhub.io/prod/97qW/piee9tqe14rye0zihxnfdofpz37i3rl4vn9nocjs0k1da4wzwpxg13fw5094tqfv.png)

3. Create new Template WS-Fed application

![](https://uploads.developerhub.io/prod/97qW/u30z1i2wir2ttj0ycxijptevaf6xrplto4vqezscv2rt0wj5ebh21p15i7npok7y.png)

4. Fill in below information and then click **Done:

**- *Realm*: urn:federation:MicrosoftOnline

- *RelyTo Url*: [https://login.microsoftonline.com/login.srf](https://login.microsoftonline.com/login.srf)[ ](https://login.microsoftonline.com/login.srf)- *Audience Restriction*: urn:federation:MicrosoftOnline
- *Custom Attribute Statements*: ImmutableID|{findDirectoryUser().externalId}|urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified,UPN|${user.login}|urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified

And leave the rest as default

![](https://uploads.developerhub.io/prod/97qW/fmzra8wfal2b2rbb0tt05t7uka5metgrjx78y1t2cceidtb5wirji2y9t0tltav4.png)

5. On Assignments tab, click on Assign to assign person you want to allow to access this application

![](https://uploads.developerhub.io/prod/97qW/7zealcxnmhlsua9keszdnl5n0qpq5gyvpeznbbvb2rpovaxkdqz5yqk9hxgiro0e.png)

6. Follow [Microsoft guideline](https://docs.microsoft.com/en-us/powershell/module/MSOnline/?view=azureadps-1.0&redirectedfrom=msdn) to install Windows PowerShell for Azure Active Directory .
7. Follow [Okta guideline](https://help.okta.com/en/prod/Content/Topics/Directory/ad-agent-new-integration.htm) to install Okta Active Directory agent to sync your Active Directory users to Okta.
8. You should test the configuration to make sure that users can log into O365 from the Okta app you just create.

Now it's the time you can integrate My OPSWAT Central Management with your Okta O365 by following below steps. You can learn more details for each step here at [3.1.1. How to set it up?](https://onlinehelp.opswat.com/metaaccess/3.1.1._How_to_set_it_up_.html)

- [Step 1. Enable Access Control on your My OPSWAT Central Management account](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_O365_using_WS-Federation.html#step-1-enable-access-control-on-your-metaaccess-account)
- [Step 2. Add protected applications with IdP Method](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_O365_using_WS-Federation.html#step-2-add-protected-applications-with-idp-method)
- [Step 3. Configure Access Rules](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_O365_using_WS-Federation.html#step-3-configure-access-rules)
- [Step 4. Update Applications settings on Identity Provider](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_O365_using_WS-Federation.html#step-4-update-applications-settings-on-identity-provider)
- [Step 5. Configure SSO settings on Office 365](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_O365_using_WS-Federation.html#step-5-configure-sso-settings-on-office-365)
- [Step 6: Test your integration](https://onlinehelp.opswat.com/metaaccess/Okta_IdP_with_O365_using_WS-Federation.html#step-6-test-your-integration)

## Step 1. Enable Access Control on your My OPSWAT Central Management account

1. Login to the My OPSWAT Central Management console.
2. Navigate to **Access Control** and then **Configurations.**
3. Check on the box **"****Enable access control****"** and configure a port for the cross-domain API. Note that you must select a port which no applications on endpoints is running.

**

![](https://uploads.developerhub.io/prod/97qW/htkk5qnvv9xbvfh2ixlx1czhuv5j3dsclwnhq0rlbrr9u2jkis1c311p47qmm0lc.png)

**

4. Click **SAVE**.

## Step 2. Add protected applications with IdP Method

1. Download Okta IdP: the next step is importing an Okta X.509 certificate to My OPSWAT Central Management. This allows My OPSWAT Central Management to verify users signing though a trusted IdP, Okta. Each identity provider has a unique X.509 certificate. Download the Okta X509 certificate by following these steps:
   1. Login to Okta as Administrator
   2. Switch to Admin mode

![](https://uploads.developerhub.io/prod/97qW/rw6rnw8grns2iz0wqkp9qhfvzqbj0rn0lyvzenr9mhb0h4693zap4w7o9vufiqz2.png)

3.  Go to Applications dashboard

![](https://uploads.developerhub.io/prod/97qW/i2hn1h3idm40ie026d06w29elemdfzyx1fqfn4p0thrrl1zk3ukgi15zfe7kp16j.png)

4.  Select O365 application

5.  Go to **Sign On** tab and click **View Setup Instruction** **

![](https://uploads.developerhub.io/prod/97qW/sg4x6yjomvmg2ny5cb5ixydmic3wfsd13auimfjoyhvjqo4bre9hb74u67si0jzv.png)

**

6.  Click **Download certificate** to download Okta certificate

![](https://uploads.developerhub.io/prod/97qW/jgqgs7jdrs4i4zpchwfdecmyeink8ablglcjeuo06yhq3qvgxfy28legy4jtlhmh.png)

2. Collect Idp Login URL: this is an embed link which Okta generated for the app to embed outside Okta. You can find this URL on General tab, scroll down to the App Embed Link section

![](https://uploads.developerhub.io/prod/97qW/ssi1crpr61uraabs7lpy3nwibhm2bktoabeo1iwwjpjb0cdiwwidfbtp7do856ae.png)

3. Add the Okta Identity Provider. If you already have Okta IdP settings on your My OPSWAT Central Management account, go to 4 to add O365 application.
   1. Login to the My OPSWAT Central Management console
   2. Navigate to **Access Control** and then **Configurations**
   3. On the **Identity Providers** tab, click "**Add New Identity Provider**" to add your IdP
   4. Fill in required fields for the Identity Provider
      1. *IdP Name*: an IdP name, for example: Okta
      2. *IdP Certificate*: upload Okta certificate you downloaded in Step 2.1

![](https://uploads.developerhub.io/prod/97qW/vbo3cblevrp9bgtm548bczv7zlupzdeb4o7yds9nzikk9q5boicf2aunpxl7g9ty.png)

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

![](https://uploads.developerhub.io/prod/97qW/7391viqyco8c13ow90gquoj24twhrelvka31bf3te72vn8kt0dwe2aqzjhme2rj9.png)

4.  Click **SAVE**

5. After saving your changes sucessfully, click the **Setup Instructions** button of the O365 application you have just added and then copy the **URL** My OPSWAT Central Management generated there. This URL is used to replace O365 login URL on Okta.

![](https://uploads.developerhub.io/prod/97qW/a3glnikp1qc1aodk4jhdoo143unbacvaz6n2es0ad2wcqalzc2vwl6dn5fe3axyr.png)

Note: you can add O365 application (step 2.4) when you add Okta IdP settings.

## Step 3. Configure Access Rules

1. On My OPSWAT Central Management console, navigate to **Access Control** and then **Configurations**
2. On **Access Rules** tab, click "**ADD NEW RULE**" to add a new rule for this application OR you can update existing access rules to add this application
3. With a new access rule, you need to specify how you would like to block/allow access a device from the application
   1. *Rule name*: a rule name, for example Block non-compliant devices
   2. *Action*: Block or Allow
   3. Configure conditions to do the action. Details at [Step 3. Configure Access Rules](https://onlinehelp.opswat.com/metaaccess/Step_3._Configure_Access_Rules.html)
4. Click **ADD RULE**

![](https://uploads.developerhub.io/prod/97qW/s6mo1k90uoi7ct10znooej7h7is9kp2k2puoeh1blbtral90b6zdtq8np832ieyz.png)

## Step 4. Update Applications settings on Identity Provider

1. Login to Okta as administrator
2. Go to Applications dashboard
3. Select O365 application
4. On General tab, click Edit
5. Replace **ReplyTo URL** with the My OPSWAT Central Management URL which you got from Step 2.5

![](https://uploads.developerhub.io/prod/97qW/m99fvy8ikepqtyck9rqtgs4yf7vkjbfsa3a6vzo856udjty1zwo237fznuwai1gt.png)

6. Click **Save**

## Step 5. Configure SSO settings on Office 365

1. Get **Issuer** and **Passive Endpoint** from Okta
   1. Login to Okta as administrator
   2. Go to Applications dashboard
   3. Select O365 application
   4. On **Sign On** tab, click **View Setup Instructions**
   5. Get *Issuer* and _Passive Endpoint

![](https://uploads.developerhub.io/prod/97qW/i7nm43zzxj971twndiqb50natx9fqlv40lipa1j7iabilve6ux1za5j8an1iu6yu.png)

_

2. Click **Download OPSWAT certificate** to download a self-signed certificate My OPSWAT Central Management generated for your account

![](https://uploads.developerhub.io/prod/97qW/beyz91mz0hl5wjdho9tlh5bx2vb7o5ugqdaffzsm21lwgkdc4s0i7i86nwk0blrh.png)

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
-IssuerUri <Issuer in step 5.1> `
-PassiveLogOnUri <Passive Endpoint in step 5.1>`
-LogOffUri https://login.microsoftonline.com/logout.srf `
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
