<!-- source: https://www.opswat.com/docs/macloud-sdp/configuration---management/setup-sso-with-microsoft-azure -->

# Setup SSO with Microsoft Azure

MetaDefender IT Access offers an integration with a 3rd-party Single Sign-on Service (SSO). This enables an account to provision new users to manage your account. When a user logs into the MetaDefender IT Access console through your own SSO service, MetaDefender IT Access will provision that user as a read-only user on your account. You can update the user's role later.

MetaDefender IT Access uses the secure and widely adopted industry standard Security Assertion Markup Language 2.0 (SAML 2.0), so that you can integrate easily with any large identity provider that supports SAML 2.0.

**To get started, log into Azure Portal and create an application for** **MetaDefender IT Access . Details can be found** [**here**](https://docs.microsoft.com/en-us/azure/active-directory/manage-apps/configure-single-sign-on-non-gallery-applications)

1. Log into Azure Portal as an administrator
2. Navigate to **Azure Active Directory** > **Enterprise applications**
3. Click the **+ New Application**

4. Select **Non-gallery application**

5. Enter Application name, for example MetaDefender IT Access
6. Under the **Getting Started** section, select **2. Set up Single sign on**

7. Click Edit icon on **Basic SAML Configuration**. Enter <https://gears.opswat.com> as a placeholder for all parameters. Click **Save**.

8. Click Edit icon on **User Attributes & Claims**: configure **Unique User Identifier (Name ID)** format as EmailFormat and its value as a user's email by clicking on that claim and choose its format as email address and source attribute as user.mail or user.localprinciplename

9. On **SAML Signing Certificate** section, you can now download the IdP configuration xml file by downloading Federation Metadata XML (for example, azure.xml). You can use this file to import to MetaDefender IT Access.

10. (Optional) Get additional information

    1. Download Azure’s certificate
    2. Get Azure Login URL
    3. Get Azure AD Identifier

**Configure Microsoft Azure on** **MetaDefender IT Access:**

1. Log into the MetaDefender IT Access console with an admin permission
2. Navigate to User management > SSO
3. On Console Authentication tab, enable "**Enable Single Sign On**" checkbox
4. Enter an **IdP Name**, for example: Azure
5. Click **Choose File** to import the identity provider metadata you got earlier in step #9 . Select the file you saved in step #9, Azure.xml. If the file is valid then IdP certificate, Issuer, and IdP SSO URL will pop up. Click SAVE
6. (Optional) Use this step if you can not import the metadata file

   1. **IdP Certificate**: Upload the certificate downloaded in Step 10.a
   2. **Issuer:** Use the value got in Step 10.c
   3. **IdP SSO URL**: Use the value got in Step 10.b
7. After you save your changes successfully, MetaDefender IT Access generates a MetaDefender IT Access Login URL. Copy this URL to import to Microsoft Azure

**Update MetaDefender IT Access app on Microsoft Azure**

1. Switch to Azure Portal
2. Navigate to the application you created earlier, MetaDefender IT Access, click Edit icon on **Basic SAML Configuration**. Replace value of Reply URL (Assertion Consumer Service URL) and Relay State with the MetaDefender IT Access Login URL you copied in step 7 then click Save.

**Log in to the MD IT Access Console from Microsoft Azure**

Log in to the Azure portal using this link: <https://myapps.microsoft.com>. Click on the MetaDefender IT-OT Access application, which the admin previously configured, to access the MD IT-OT Access Console.

**DONE.**

If You couldn't import the identity provider information from the IdP metadata file, you can get information from the Set up instruction page of the app and copy IdP certificate, Issuer, and IdP SSO URL to the MetaDefender IT Access console.
