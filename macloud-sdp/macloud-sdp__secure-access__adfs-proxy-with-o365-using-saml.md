<!-- source: https://www.opswat.com/docs/macloud-sdp/secure-access/adfs-proxy-with-o365-using-saml -->

# ADFS Proxy with O365 using SAML

OPSWAT MetaDefender IT-OT Access can be easily integrated with ADFS Proxy to ensure that a device is compliant with the organization's security policy before it is granted access to O365. This ensures that the device is not only authenticated by the IdP, but also tested for risks and vulnerabilities such as infections or unpatched versions of operating systems, BEFORE it access an organization's cloud services.

To get started with implementing OPSWAT MetaDefender IT-OT Access integration to enforce device posture check before granting a device to access O365 with ADFS Proxy, you set up SSO between AD FS server and O365 manually. You need the following requirements

1. A domain.
2. An Active Directory instance.
3. Add your domain to Office 365.
4. Install Windows PowerShell for Azure Active Directory [here](https://docs.microsoft.com/en-us/powershell/module/MSOnline/?view=azureadps-1.0&redirectedfrom=msdn).
5. Install ADFS server.
6. Using Azure AD Connect to enable Single Sign-On to Office 365.

Configuring, installing ADFS server and enabling SSO to Office 365 is beyond the scope of this tutorial. This tutorial uses screenshots from Server 2012R2, but similar steps should be possible on other versions.

Now it's the time you can integrate MetaDefender IT-OT Access with your ADFS by following below steps. You can learn more details for each step here at [3.1.1. How to set it up?](https://onlinehelp.opswat.com/metaaccess/3.1.1._How_to_set_it_up_.html)

- [Step 1. Enable Access Control on your MetaDefender IT-OT Access account](https://onlinehelp.opswat.com/metaaccess/ADFS_Proxy_with_O365_using_SAML.html#step-1-enable-access-control-on-your-metaaccess-account)
- [Step 2. Add protected applications with IdP Method](https://onlinehelp.opswat.com/metaaccess/ADFS_Proxy_with_O365_using_SAML.html#step-2-add-protected-applications-with-idp-method)
- [Step 3. Configure Access Rules](https://onlinehelp.opswat.com/metaaccess/ADFS_Proxy_with_O365_using_SAML.html#step-3-configure-access-rules)
- [Step 4. Update Office 365 Relying Party Trusts in AD FS Server](https://onlinehelp.opswat.com/metaaccess/ADFS_Proxy_with_O365_using_SAML.html#step-4-update-office-365-relying-party-trusts-in-ad-fs-server)
- [Step 5. Edit SSO settings on Office 365](https://onlinehelp.opswat.com/metaaccess/ADFS_Proxy_with_O365_using_SAML.html#step-5-edit-sso-settings-on-office-365)
- [Step 6: Test your integration](https://onlinehelp.opswat.com/metaaccess/ADFS_Proxy_with_O365_using_SAML.html#step-6-test-your-integration)

## [Step 1. Enable Access Control on your MetaDefender IT-OT Access account](/docs/macloud-sdp/secure-access/adfs-proxy-with-o365-using-saml#step-1-enable-access-control-on-your-metadefender-it-ot-access-account)

1. Login to the MetaDefender IT-OT Access console.
2. Navigate to **Secure Access > Protected Apps.**
3. Check on the box **"Enable Secure Access ".**
4. Navigate to **Integrations** and then **Device Identity**, and enable **Enable cross-domain API integration at port xxxx**

## [Step 2. Add protected applications with IdP Method](/docs/macloud-sdp/secure-access/adfs-proxy-with-o365-using-saml#step-2-add-protected-applications-with-idp-method)

1. The next step is importing an ADFS Signing certificate to MetaDefender IT-OT Access. This allows MetaDefender IT-OT Access to verify users signing though a trusted IdP. Each identity provider has a unique X.509 certificate. Download the ADFS Signing certificate by following these steps:

   1. Login to Windows Server
   2. Open **Server Manager**
   3. Click **Tools**
   4. Click **AD FS Management**
   5. Expand **Service**
   6. Click **Certificates**
   7. Double-click on the "Token-signing" being used to sign your responses

8. Click **Copy to File** to download the certificate. That should open another box, showing the certificate export wizard. Click **Next** and you will be asked which format to export the certificate in. Choose **Base-64 encoded X.509**

2. Collect Idp Login URL In this case, Idp Login URL is <https://login.microsoftonline.com/login.srf>
3. Add the ADFS Identity Provider. If you already have ADFS IdP settings on yourMetaDefender IT-OT Access account, go to 4 to add O365 application.

   1. Login to the [MetaDefender IT-OT Access console](https://gears.opswat.com/console)
   2. Navigate to **Secure Access** and then **Access Methods**
   3. On the **Identity Providers** tab, click "**Create New Identity Provider**" to add your IdP
   4. Fill in required fields for the Identity Provider

      1. *IdP Name*: an IdP name, for example: ADFS
      2. *IdP Certificate*: upload ADFS certificate you downloaded in Step 2.1
4. Click **SAVE**.
5. Add the O365 application:

   1. Expand the ADFS IdP settings you have just added in Step 2.3 above.
   2. Navigate to **Secure Access** and then **Protected Apps**. Click **Add New Application.**
   3. Select **IdP Method** and choose from the existing IdPs, finding the one you just made. Press **Continue**.
   4. Enter required field

      1. *Application*: application name, for example: O365
      2. *IDP Login URL*: application login URL which you have from Step 2.2
      3. *Login URL*: <https://login.microsoftonline.com/login.srf>
      4. *Logout URL*: <https://login.microsoftonline.com/logout.srf>
      5. *Access Mode*: pick an access mode you prefer. See details on the access modes at [Step 2. Add protected applications with IdP Method](https://onlinehelp.opswat.com/metaaccess/Step_2._Add_protected_applications_with_IdP_Method.html)
      6. Click **Add**
      7. After saving your changes successfully, click the **Setup Instructions** button of the O365 application you have just added and then copy the **URL** MetaDefender IT-OT Access generated there. This URL is used to replace O365 login URL on ADFS.
      8. Download the Note: you can add O365 application (step 2.4) when you add ADFS IdP settings.

## [Step 3. Configure Access Rules](/docs/macloud-sdp/secure-access/adfs-proxy-with-o365-using-saml#step-3-configure-access-rules)

1. On [MetaDefender IT-OT Access console](https://gears.opswat.com/console), navigate to **Secure Access** and then **Rules**
2. Click "**ADD NEW RULE**" to add a new rule for this application OR you can update existing access rules to add this application
3. With a new access rule, you need to specify how you would like to block/allow access a device from the application

   1. *Rule name*: a rule name, for example Block non-compliant devices
   2. *Action*: Block or Allow
   3. Configure conditions to do the action. Details at [Step 3. Configure Access Rules](https://onlinehelp.opswat.com/metaaccess/Step_3._Configure_Access_Rules.html)
4. Click **ADD RULE**

## [Step 4. Update Office 365 Relying Party Trusts in AD FS Server](/docs/macloud-sdp/secure-access/adfs-proxy-with-o365-using-saml#step-4-update-office-365-relying-party-trusts-in-ad-fs-server)

1. Update Passive Endpoint

   1. Login to Windows Server
   2. Open **Server Manager**
   3. Click **Tools**
   4. Click **AD FS Management**
   5. Expand **Trust Relationships**
   6. Click **Relying Party Trusts**
   7. Double-click on "Microsoft Office 365 Identity Platform" and choose **Endpoints tab

8. Click **Add SAML** to add new Endpoint

9. Use the URL in step 2.5 as **Trusted URL**:

10. Click **OK**

2. Configure the Active Directory claims-provider trust

   1. Right-click "Microsoft Office 365 Identity Platform" and choose **Edit Claim Rules

2. On the **Issuance Transform Rules** tab, click **Add Rule

3. In the Claim rule template box, select **Send Claims Using a Custom Rule**, and then click **Next

4. In the Claim rule name box type "Issue nameidentifier SAML 2.0", and fill the Custom rule as follow:

c:[Type == "[http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"]](http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID%22%5C%5D) => issue(Type = "[http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier"](http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier%22), Value = c.Value, Properties["[http://schemas.xmlsoap.org/ws/2005/05/identity/claimproperties/format"]](http://schemas.xmlsoap.org/ws/2005/05/identity/claimproperties/format%22%5C%5D) = "urn:oasis:names:tc:SAML:2.0:nameid-format:persistent");

5. Click **Finish**

6. Click **OK**

## [Step 5. Edit SSO settings on Office 365](/docs/macloud-sdp/secure-access/adfs-proxy-with-o365-using-saml#step-5-edit-sso-settings-on-office-365)

After install and configure AD FS server, it will enable SSO for your domain, but you need to replace SigningCertificate in SSO setting to work with MetaDefender IT-OT Access

1. Login to Azure Active Directory via Windows PowerShell

   1. Login to a computer installed Windows PowerShell for Azure Active Directory
   2. Start PowerShell and run **Connect-MsolService** cmdlet and enter your administrator credentials for your Office 365 domain when prompted

C:\Windows\system32>Connect-MsolService

2. Backup current SSO settings

   1. Run **Get-MsolDomainFederationSettings -DomainName <your domain>** cmdlet to get current SSO setting
   2. Get these information

      1. FederationBrandName
      2. IssuerUri
      3. LogOffUri
      4. PassiveLogOnUri
3. Update existing current setting

   1. Run following cmdlet

C:\Windows\system32>Set-MsolDomainAuthentication -DomainName <your domain> -Authentication Managed

2. Run **Set-MsolDomainAuthentication** cmdlet

C:\Windows\system32>Set-MsolDomainAuthentication `
-FederationBrandName <FederationBrandName> `
-DomainName <Your Domain> `
-Authentication Federated `
-IssuerUri <Issuer> `
-PassiveLogOnUri <Passive Endpoint> `
-LogOffUri <LogOffUri> `
-PreferredAuthenticationProtocol SAMLP `
-SigningCertificate <OPSWAT Certificate in step 2>

**Note**: enter the certificate on a single line without break line

3. Run following cmdlet to verify configuration

C:\Windows\system32>Get-MsolDomainFederationSettings -DomainName <Your Domain>

**Note**: It can take some time for Office 365 to apply new configuration

## [Step 6: Test your integration](/docs/macloud-sdp/secure-access/adfs-proxy-with-o365-using-saml#step-6-test-your-integration)

Follow guideline at [Step 6: Test your integration](https://onlinehelp.opswat.com/metaaccess/Step_6__Test_your_integration.html) to test your integration to verify if it works as your expectation.

**DONE! CONGRATULATIONS.**
