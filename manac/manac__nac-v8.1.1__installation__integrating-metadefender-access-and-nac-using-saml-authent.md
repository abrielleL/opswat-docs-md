<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/installation/integrating-metadefender-access-and-nac-using-saml-authent -->

# Integrating MetaDefender IT Access and NAC Using SAML Authentication

If end-user devices are being assessed by MetaDefender IT Access, and the network is being managed by NAC, you may want to restrict the internet access for devices that MetaDefender IT Access indicates are not compliant with all policies. One way to accomplish this is via the use of a SAML authentication policy in NAC linked to MetaDefender IT Access. When end-user devices are seen by NAC they are blocked until they authenticate. When MetaDefender ITvAccess indicates that these devices are not yet compliant, the NAC captive portal shows the MetaDefender ITvAccess remediation instructions.

## [**Step 1. To Integrate MetaDefender IT Access and NAC using SAML authentication**](/docs/manac/nac-v8.1.1/installation/integrating-metadefender-access-and-nac-using-saml-authent#step-1-to-integrate-metadefender-it-access-and-nac-using-saml-authentication)

1. Before beginning, [contact OPSWAT support](https://www.opswat.com/support) and request that the SAML authentication feature be enabled on your appliance. Also tell them what Identity Provider you intend to use so they can make the necessary remediation resources available to quarantined users.
2. Complete the MetaDefender IT Access setup by referring to [3.1.1. How to set it up?](https://onlinehelp.opswat.com/metaaccess/3.1.1._How_to_set_it_up_.html)
3. Only continue once you receive confirmation from OPSWAT support that SAML integration has been enabled on the NAC appliance.

## [Step 2. Get SAML Information from NAC](/docs/manac/nac-v8.1.1/installation/integrating-metadefender-access-and-nac-using-saml-authent#step-2-get-saml-information-from-nac)

NAC is operating as the Service Provider in a SAML authentication system. Some information needs to be retrieved from the NAC appliance before continuing.

1. Log in to the appliance, use the hamburger in the upper left to navigate to the "Configuration" page, and click "SAML" on the left-hand panel.
2. Click on the "Service Provider Configuration" tab and note the "Entity ID" at the top of the page. This should be "urn:impulse:saml:auth". You will also need to know your Single Sign-On URL. If you are using the default hostname for your NAC appliance, this will be "[https://portal.myweblogon.com:8443/saml/SSO](https://portal.myweblogon.com:8443/saml/SSO+)". If you are using a custom hostname, you would replace "[portal.myweblogon.com](http://portal.myweblogon.com)" with your custom hostname, and replace "8443" with "9443". Many Identity Providers support more-or-less hands-off configuration with the upload of a metadata xml file. If your Identity Provider supports this, you can download this file from NAC by scrolling to the bottom of the "Service Provider Configuration" page and clicking "Download Metadata". If your Identity Provider requires that you enter Service Provider information manually, you’ll need to download the certificate used so that it can be uploaded to the Identity Provider by clicking "Download Certificate".

## [Step 3. Identity Provider Configuration](/docs/manac/nac-v8.1.1/installation/integrating-metadefender-access-and-nac-using-saml-authent#step-3-identity-provider-configuration)

The exact steps for adding a Service Provider will vary by Identity Provider. The steps below use [Okta.com](http://okta.com/), but your Identify Provider may have different steps.

1. Navigate to your Okta organization dashboard as a user with admin privileges. Then click "Admin" in the upper right.
2. Click "Add App"
3. On the next page, click "Create New App", select "Web" and "SAML 2.0" on the dialog this brings up, then click "Create".
4. On the "General Settings" page set "App Name" to "NAC" and upload a custom logo if you would like. Then click "Next".
5. On the "SAML Settings" page, set "Single sign on URL" and "Audience URI (SP Entity ID)" to the values you got from the NAC "Service Provider Configuration" tab. Then scroll to the bottom and click "Next" then "Finish" on the next page.
6. Click "View Setup Instructions" to be taken to the page where we'll get the last piece of information we need to finish setting up the NAC SAML configuration.
7. Scroll to the bottom of the page to find a text box referred to as the IDP "metadata", and NAC will use this to configure itself to use this particular Identity Provider. Copy all of the text from the text box and save it to a .xml file.

## [Step 4. NAC Configuration](/docs/manac/nac-v8.1.1/installation/integrating-metadefender-access-and-nac-using-saml-authent#step-4-nac-configuration)

1. Back in the NAC UI, under "Configuration" > "SAML" > "Identity Provider Configuration", click on the "New IDP" button.
2. Give the new Identity Provider a name, check the "Default IDP" box, select the .xml file with the metadata you got from your Identify Provider, and click Upload.
3. (Optional) Click "Delete" on the "testSaml" IDP panel.
4. Very that SAML authentication is working by setting up a group to use the "SAML Single Sign On Service" authentication policy, and having a member of that group authenticate with NAC using SAML credentials. For best results we recommend making sure that this authentication policy requires users to authenticate every session. This ensures that compliance changes on the MetaDefender IT Access side are reflected in NAC network access as often as possible.

## [Step 5. MetaDefender IT Access Integration](/docs/manac/nac-v8.1.1/installation/integrating-metadefender-access-and-nac-using-saml-authent#step-5-metadefender-it-access-integration)

1. From your MetaDefender IT Access console, navigate to "Secure Access" > "Protected Apps"
2. Check "Enable secure access" if it's not already checked
3. Before we can add a new protected app for this integration, we'll need to get some more information from the Identity Provider. For the case of Okta, navigate back to the "New Setup Instructions" page from earlier in a new tab. Download Okta's certificate and locate the IPD Login URL in the metadata text. It should be inside a "<md:SingSignOnService/>" tag.
4. Back in the MetaDefender IT Access UI, select to add a protected app and choose IdP Method

   - select add new IdP option
   - fill in the "IdP Name" field with the name of your IDP
   - upload the certificate you downloaded in the previous step
   - name the application "NAC"
   - set "IDP Login URL" to the URL you just got from the metadata your IDP provided
   - set "Application ACS URL" to the "Single sign on URL" from earlier (e.g. [https://portal.myweblogon.com:8843/saml/SSO](https://portal.myweblogon.com:8843/saml/SSO+))
   - set access mode to "Enforce"
   - click "ADD"
5. Once the application is saved, the “Setup Instruction” button will show you the login URL that the IDP should be using. Keep track of that URL.
6. This URL can be taken to your IDP and used to replace the URL that the IDP will forward successful authentication attempts to. For example, Okta calls this the “Single sign on URL”
7. We need to replace the certificate included in the IDP metadata we provided to NAC with a certificate OPSWAT generates for us. To get this certificate, click the "Download OPSWAT Certificate" button.
8. Open up this file in a text editor and copy the certificate into your clipboard, excluding the "----BEGIN CERTIFICATE---", "---END CERTIFICATE----", and any unnecessary newline characters.
9. Make a duplicate of the metadata file from your IDP, and rename it to something like "idp_metadata_opswat_cert.xml". Then open it in a text editor, select the certificate text as you did before, selecting no extra characters, and press Ctrl-V to overwrite it with the OPSWAT-provided certificate. Save the file.
10. Back in the NAC UI under "Configuration" > "SAML" > "Identify Provider Configuration", choose the new metadata file and click "Upload" again.

## [Step 6. Test The Integration](/docs/manac/nac-v8.1.1/installation/integrating-metadefender-access-and-nac-using-saml-authent#step-6-test-the-integration)

You should have a policy group in NAC that requires users authenticate against SAML. When a device is online and is put in that group, it should be presented with a captive portal that requires they authenticate against the SAML IDP.

When that login is successful, traffic should then be forwarded to MetaDefender IT Access for compliance checking. A compliant device should be presented with the NAC redirect URL (by default a placeholder indicating that network access is now permitted). If the device is not compliant they should be presented with a MetaDefender IT Access remediation page.
