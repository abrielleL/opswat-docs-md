<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/adfs-proxy-with-vdi -->

# ADFS Proxy with VDI

My OPSWAT Central Management can be easily integrated with ADFS Proxy to ensure that a device is compliant with the organization's security policy before it is granted access to a virtual desktop. This ensures that the device is not only authenticated by the IdP, but also tested for risks and vulnerabilities such as threats or unpatched versions of operating systems, BEFORE it access an organization's cloud services.

To get started integrating My OPSWAT Central Management to enforce device posture check before granting a device to access VDI with ADFS Proxy, you set up SSO between ADFS and VDI manually. You need the following requirements

1. A domain.
2. An Active Directory instance.
3. Add your domain to Azure AD.
4. Install Windows PowerShell for Azure Active Directory [here](https://docs.microsoft.com/en-us/powershell/module/MSOnline/?view=azureadps-1.0&redirectedfrom=msdn).
5. Install ADFS server.
6. Using Azure AD Connect to enable Single Sign-On for your domain.

Configuring, installing ADFS server and enabling SSO are beyond the scope of this tutorial. This tutorial uses screenshots from Server 2016, but similar steps should be possible on other versions.

Now it's the time you can integrate My OPSWAT Central Management with your ADFS by following below steps. You can learn more details for each step here at [3.1.1. How to set it up?](https://onlinehelp.opswat.com/metaaccess/3.1.1._How_to_set_it_up_.html)

- [Step 1. Enable Access Control on your MetaAccess account](https://onlinehelp.opswat.com/metaaccess/ADFS_Proxy_with_VDI.html#step-1-enable-access-control-on-your-metaaccess-account)
- [Step 2. Add protected applications with IdP Method](https://onlinehelp.opswat.com/metaaccess/ADFS_Proxy_with_VDI.html#step-2-add-protected-applications-with-idp-method)
- [Step 3. Configure Access Rules](https://onlinehelp.opswat.com/metaaccess/ADFS_Proxy_with_VDI.html#step-3-configure-access-rules)
- [Step 4. Create new Relying Party Trust For VDI in ADFS Server](https://onlinehelp.opswat.com/metaaccess/ADFS_Proxy_with_VDI.html#step-4-create-new-relying-party-trust-for-vdi-in-adfs-server)
- [Step 5. Edit SSO settings on Office 365](https://onlinehelp.opswat.com/metaaccess/ADFS_Proxy_with_VDI.html#step-5-edit-sso-settings-on-office-365)
- [Step 6: Test your integration](https://onlinehelp.opswat.com/metaaccess/ADFS_Proxy_with_VDI.html#step-6-test-your-integration)

## Step 1. Enable Access Control on your My OPSWAT Central Management account

1. Login to the My OPSWAT Central Management console.
2. Navigate to **Access Control** and then **Configurations**
3. Check on the box **"****Enable access control****"** and configure a port for the cross-domain API. Note that you must select a port which no applications on endpoints is running.

![](https://uploads.developerhub.io/prod/97qW/izg5tc3k3ux8v2el9sa5j7jyvlj5jtadgekb4ynbdn119xnk64sh4bk7w2jrso9z.png)

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

![](https://uploads.developerhub.io/prod/97qW/hbsdddzy4hspp7e384ch3b7p7ruedio2da6rh5ze4amrsmjv1fuuvzosaevj2dkd.png)

8.  Click **Copy to File** to download the certificate. That should open another box, showing the certificate export wizard. Click **Next** and you will be asked which format to export the certificate in. Choose **Base-64 encoded X.509**

![](https://uploads.developerhub.io/prod/97qW/p49c83rv9bmn3oewoq78kt8ayl80faldqgpplh5ww49f6u69xwmexsjswwbdtpnm.png)

2. Collect Idp Login URL In this case, Idp Login URL is [https://login.microsoftonline.com/login.srf](https://login.microsoftonline.com/login.srf)
3. Add the ADFS Identity Provider. If you already have ADFS IdP settings on your My OPSWAT Central Management account, go to next step to add an application.
   1. Login to the My OPSWAT Central Management console.
   2. Navigate to **Access Control** and then **Configurations**
   3. On the **Identity Providers** tab, click "**Add New Identity Provider**" to add your IdP
   4. Fill in required fields for the Identity Provider
      1. *IdP Name*: an IdP name, for example: ADFS
      2. *IdP Certificate*: upload ADFS certificate you downloaded in Step 2.1

![](https://uploads.developerhub.io/prod/97qW/ensjpu7y264b86sx9ut1jdoduuezpox7nbvpyelznn7jt4bc903qs0q4rgvzwj0j.png)

5.  Click **Add IDP**

6.  Click **SAVE**

4. Add the application:
   1. Expand the ADFS IdP settings you have just added in Step 2.3 above.
   2. Click **Add New Application**
   3. Enter required field
      1. *Application*: application name, for example: vdi
      2. *IDP Login URL*: application login URL which you have from Step 2.2
      3. *Login URL*: [https://login.microsoftonline.com/login.srf](https://login.microsoftonline.com/login.srf)
      4. *Logout URL*: [https://login.microsoftonline.com/logout.srf](https://login.microsoftonline.com/logout.srf)
      5. *Access Mode*: pick an access mode you prefer. See details on the access modes at [Step 2. Add protected applications with IdP Method](https://onlinehelp.opswat.com/metaaccess/Step_2._Add_protected_applications_with_IdP_Method.html)

![](https://uploads.developerhub.io/prod/97qW/z43ln9j88f715vr34ifr7zb9t30aa9lxeut7kifw69uo0s28cv064jb6oe20f7kd.png)

4.  Click **SAVE**

5. After saving your changes successfully, click the **Setup Instructions** button of the VDI application you have just added and then copy the **URL** My OPSWAT Central Management generated there. This URL is used to replace VDI login URL on ADFS.

![](https://uploads.developerhub.io/prod/97qW/8rvlh6frldbgs07m6anw5r8wbjwp0iqpa57ecgymuq2a93ouyxe2amois6ghw4mt.png)

Note: you can add VDI application (step 2.4) when you add ADFS IdP settings.

## Step 3. Configure Access Rules

1. On My OPSWAT Central Management console, navigate to **Access Control** and then **Settings**
2. On **Access Rules** tab, click "**ADD NEW RULE**" to add a new rule for this application OR you can update existing access rules to add this application
3. With a new access rule, you need to specify how you would like to block/allow access a device from the application
   1. *Rule name*: a rule name, for example Block non-compliant devices
   2. *Action*: Block or Allow
   3. Configure conditions to do the action. Details at [Step 3. Configure Access Rules](https://onlinehelp.opswat.com/metaaccess/Step_3._Configure_Access_Rules.html)
4. Click **ADD RULE**

![](https://uploads.developerhub.io/prod/97qW/1zrfexhyakd68iqodu6hdb19571zqw1mu4qr6xnno5efc5ypd1j4yb6eq9eouios.png)

## Step 4. Create new Relying Party Trust For VDI in ADFS Server

1. Login to Windows Server
2. Open **Server Manager**
3. Click **Tools**
4. Click **AD FS Management**
5. Expand **Trust Relationships**
6. Click **Relying Party Trusts**
7. Follow [this tutorial](https://docs.microsoft.com/en-us/windows-server/identity/ad-fs/operations/create-a-relying-party-trust) to create new Relying Party Trust
8. Change the default Endpoint with the URL in step 2.5

![](https://uploads.developerhub.io/prod/97qW/vngn708ph2zdofnyr9210umnws12yqpgi330adb9ry85cpvb6tilwj5wrdt8ia45.png)

## Step 5. Edit SSO settings on Office 365

After install and configure ADFS server, it will enable SSO for your domain, but you need to replace SigningCertificate in SSO setting to work with My OPSWAT Central Management.

1. Login to Azure Active Directory via Windows PowerShell
   1. Login to a computer installed Windows PowerShell for Azure Active Directory
   2. Start PowerShell and run **Connect-MsolService** cmdlet and enter your administrator credentials for your Azure AD domain when prompted

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

![](https://uploads.developerhub.io/prod/97qW/1wxx7g8v3uy1785zkwhqwa6ygojfue965jnaphszhcwykg3jq2ain7rfk9bhsxhb.png)

3. Click **Download OPSWAT certificate** to download a self-signed certificate My OPSWAT Central Management generated for your account

![](https://uploads.developerhub.io/prod/97qW/x4s9nx5spdsh4ckco85mdg5etagm0nid59savnyi4phvnwg62k9kh8mbuqk3he2t.png)

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

**Note**: It can take some time for Azure AD to apply new configuration

## Step 6: Test your integration

Follow guideline at [Step 6: Test your integration](https://onlinehelp.opswat.com/metaaccess/Step_6__Test_your_integration.html) to test your integration to verify if it works as your expectation.

**DONE! CONGRATULATIONS.**
