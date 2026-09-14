<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/adfs-proxy-with-o365-using-ws-federation -->

# ADFS Proxy with O365 using WS-Federation

My OPSWAT Central Management can be easily integrated with ADFS Proxy to ensure that a device is compliant with the organization's security policy before it is granted access to O365. This ensures that the device is not only authenticated by the IdP, but also tested for risks and vulnerabilities such as infections or unpatched versions of operating systems, BEFORE it access an organization's cloud services.

To get started with implementing OMy OPSWAT Central Management integration to enforce device posture check before granting a device to access O365 with ADFS Proxy, you set up SSO between AD FS and O365 manually. You need the following requirements

1. A domain.
2. An Active Directory instance.
3. Add your domain to Office 365.
4. Install Windows PowerShell for Azure Active Directory [here](https://docs.microsoft.com/en-us/powershell/module/MSOnline/?view=azureadps-1.0&redirectedfrom=msdn).
5. Install ADFS server.
6. Using Azure AD Connect to enable Single Sign-On to Office 365.

Configuring, installing ADFS server and enabling SSO to Office 365 is beyond the scope of this tutorial. This tutorial uses screenshots from Server 2012R2, but similar steps should be possible on other versions.

Now it's the time you can integrate My OPSWAT Central Management with your ADFS by following below steps. You can learn more details for each step here at [Configuration.](https://www.opswat.com/docs/cm/secure-access-solution/SAML-SSO-integration-configuration)

## Step 1. Enable Access Control on your My OPSWAT Central Management account

1. Login to the My OPSWAT Central Management console.
2. Navigate to **Access Control** and then **Configurations**
3. Check on the box **"****Enable access control****"** and configure a port for the cross-domain API. Note that you must select a port which no applications on endpoints is running.

![](https://uploads.developerhub.io/prod/97qW/056lvqktwa7w04g4sbs4y03m2v4xr8bthpgkxe2rff1kumumgzlwfdnhz5vi5fap.png)

4. Click **SAVE**.

## Step 2. Add protected applications with IdP Method

1. The next step is importing an ADFS Signing certificate to My OPSWAT Central Management. This allows My OPSWAT Central Management to verify users signing though a trusted IdP. Each identity provider has a unique X.509 certificate. Download the ADFS Signing certificate by following these steps:
   1. Login to Windows Server
   2. Open **Server Manager**
   3. Click **Tools**
   4. Click **AD FS Management**
   5. Expand **Service**
   6. Click **Certificates**
   7. Double-click on the "Token-signing" being used to sign your responses

![](https://uploads.developerhub.io/prod/97qW/84genaqf3plb5rfupevzo16gincvr332fl3ad20cd4ww77zmfct7gsccwad8hfes.png)

8.  Click **Copy to File** to download the certificate. That should open another box, showing the certificate export wizard. Click **Next** and you will be asked which format to export the certificate in. Choose **Base-64 encoded X.509**

![](https://uploads.developerhub.io/prod/97qW/itpf1zf90bw0r23zhgulfaoy3bcet9o0mjd88c5ss59mqghd907aoo88dm2heghq.png)

2. Collect Idp Login URL In this case, Idp Login URL is [https://login.microsoftonline.com/login.srf](https://login.microsoftonline.com/login.srf)
3. Add the ADFS Identity Provider. If you already have ADFS IdP settings on your My OPSWAT Central Management account, go to 4 to add O365 application.
   1. Login to the My OPSWAT Central Management console.
   2. Navigate to **Access Control** and then **Configurations**
   3. On the **Identity Providers** tab, click "**Add New Identity Provider**" to add your IdP
   4. Fill in required fields for the Identity Provider
      1. *IdP Name*: an IdP name, for example: ADFS
      2. *IdP Certificate*: upload ADFS certificate you downloaded in Step 2.1

![](https://uploads.developerhub.io/prod/97qW/73uwdiahw06ektnnzq2yjnu1gpphqmws46hog63b0bu4angw79b49pwik4596t6o.png)

5.  Click **Add IDP**

6.  Click **SAVE**

4. Add the O365 application:
   1. Expand the ADFS IdP settings you have just added in Step 2.3 above.
   2. Click **Add New Application**
   3. Enter required field
      1. *Application*: application name, for example: O365
      2. *IDP Login URL*: application login URL which you have from Step 2.2
      3. *Login URL*: [https://login.microsoftonline.com/login.srf](https://login.microsoftonline.com/login.srf)
      4. *Logout URL*: [https://login.microsoftonline.com/logout.srf](https://login.microsoftonline.com/logout.srf)
      5. *Access Mode*: pick an access mode you prefer. See details on the access modes at [Add Protected Applications with IdP Method](https://www.opswat.com/docs/cm/secure-access-solution/SAML-SSO-add-protected-applications).

![](https://uploads.developerhub.io/prod/97qW/cvmyw3z46qht2fb6048vhfi5zo8g60bxqqrqu9jlbx5lszbh0l3glo7arvghasxa.png)

4.  Click **SAVE**

5. After saving your changes sucessfully, click the **Setup Instructions** button of the O365 application you have just added and then copy the **URL** My OPSWAT Central Management generated there. This URL is used to replace O365 login URL on ADFS.

![](https://uploads.developerhub.io/prod/97qW/jzw29uim11mxog5o1qufwc44b9as8gqijrbroqa29kfvzfyg31zfv3w4qv2r3efo.png)

Note: you can add O365 application (step 2.4) when you add ADFS IdP settings.

## Step 3. Configure Access Rules

1. On My OPSWAT Central Management console, navigate to **Access Control** and then **Settings**
2. On **Access Rules** tab, click "**ADD NEW RULE**" to add a new rule for this application OR you can update existing access rules to add this application
3. With a new access rule, you need to specify how you would like to block/allow access a device from the application
   1. *Rule name*: a rule name, for example Block non-compliant devices
   2. *Action*: Block or Allow
   3. Configure conditions to do the action. Details at [Configure Access Rules](https://www.opswat.com/docs/cm/secure-access-solution/SAML-SSO-configure-access-rules)
4. Click **ADD RULE**

![](https://uploads.developerhub.io/prod/97qW/xvxrcmo5uvaq4d2y9smre4p1htcg7tfabd9hgbor4qknblrmzea37cuf80e0jv3e.png)

## Step 4. Update Passive Endpoints For Office 365 in AD FS Server

1. Login to Windows Server
2. Open **Server Manager**
3. Click **Tools**
4. Click **AD FS Management**
5. Expand **Trust Relationships**
6. Click **Relying Party Trusts**
7. Double-click on "Microsoft Office 365 Identity Platform" and choose **Endpoints** tab**

![](https://uploads.developerhub.io/prod/97qW/5asyn6vl9nblx5mtng1gsc1zqwg7svsjufwpi9cturzwrf5yudkwdf3n1spm8sqc.png)

**

8. Double-click on the default Endpoint and replace **Trusted URL** with the URL in step 2.5

![](https://uploads.developerhub.io/prod/97qW/uegpxk9mpveiwje06xscscgfuc7zpuupiho7e8n5zyt56ktf1p6304qxe1cpj5sg.png)

## Step 5. Edit SSO settings on Office 365

After install and configure AD FS server, it will enable SSO for your domain, but you need to replace SigningCertificate in SSO setting to work with My OPSWAT Central Management.

1. Login to Azure Active Directory via Windows PowerShell
   1. Login to a computer installed Windows PowerShell for Azure Active Directory
   2. Start PowerShell and run **Connect-MsolService** cmdlet and enter your administrator credentials for your Office 365 domain when prompted

```plaintext
C:\Windows\system32>Connect-MsolService
```

2. Backup current SSO settings
   1. Run **Get-MsolDomainFederationSettings -DomainName <your domain>** cmdlet to get current SSO setting
   2. Get these information
      1. FederationBrandName
      2. IssuerUri
      3. LogOffUri
      4. PassiveLogOnUri

![](https://uploads.developerhub.io/prod/97qW/5loe1dl28rmb644d76k8w29m43d44o0u8yqtwmm5xc4h8eu3warzd44fztf33tra.png)

3. Click **Download OPSWAT certificate** to download a self-signed certificate My OPSWAT Central Management generated for your account

![](https://uploads.developerhub.io/prod/97qW/h62byembr333aznzvowftdybc7i62xruv2tmomw6ve3asv51d45hyfnu7dtf9t0x.png)

4. Update existing current setting
   1. Run following cmdlet

```plaintext
C:\Windows\system32>Set-MsolDomainAuthentication -DomainName <your domain> -Authentication Managed
```

2.  Run **Set-MsolDomainAuthentication** cmdlet

```plaintext
C:\Windows\system32>Set-MsolDomainAuthentication `
-FederationBrandName <FederationBrandName in step 5.2> `
-DomainName <Your Domain> `
-Authentication Federated `
-IssuerUri <Issuer in step 5.2> `
-PassiveLogOnUri <Passive Endpoint in step 5.2> `
-LogOffUri <LogOffUri in step 5.2> `
-SigningCertificate <OPSWAT Certificate in step 5.3>
```

**Note**: enter the certificate on a single line without break line

3.  Run following cmdlet to verify configuration

```plaintext
C:\Windows\system32>Get-MsolDomainFederationSettings -DomainName <Your Domain>
```

**Note**: It can take some time for Office 365 to apply new configuration

## Step 6: Test your integration

Follow guideline at [Test Your Integration ](https://www.opswat.com/docs/cm/secure-access-solution/test-your-integration)to verify if it works as your expectation.
