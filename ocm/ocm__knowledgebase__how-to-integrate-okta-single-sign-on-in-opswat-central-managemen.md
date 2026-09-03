<!-- source: https://www.opswat.com/docs/ocm/knowledgebase/how-to-integrate-okta-single-sign-on-in-opswat-central-managemen -->

# How to integrate Okta Single sign-on in OPSWAT Central Management?

Integrating **Okta Single Sign-On (SSO)** with **OPSWAT Central Management** allows users to authenticate using Okta, improving security and simplifying access control. Here is how to do it:

## [Configure Okta as the Identity Provider (IdP)](/docs/ocm/knowledgebase/how-to-integrate-okta-single-sign-on-in-opswat-central-managemen#configure-okta-as-the-identity-provider-idp)

1. Log in to Okta Admin Console

   1. Navigate to **Applications** > **Create App Integration**.
   2. Choose **SAML 2.0** as the sign-in method.
   3. Click **Next** to configure the integration.

2. Set Up SAML Configuration

   1. In the **General Settings**, enter an **App name** (e.g., "OPSWAT Central Management").
   2. In **SAML Settings**, configure:

- **Single sign-on URL**: This is the **ACS (Assertion Consumer Service) URL** from OPSWAT Central Management. You should be able to get this URL by logging to Central Management --> Settings --> Integrations --> Single sign-on --> Enable Single Sign on and the URL should be at the bottom of the page:

- **Audience URI (SP Entity ID)**: Use the **Entity ID** provided by OPSWAT. You can put the URL of OPSWAT Central Management.
- **Name ID Format**: Choose **EmailAddress**.
- **Application username**: Set to **Email**.

3. After creating the application, go to settings of the application then go to Sign on and do the following to get the files to configure OPSWAT Central Management later

   1. Download from the IdP the xml file in the Metadata URL
   2. Download from the IdP the certificate in the Signing Certificate section

4. Go to Assignments tab then assign the people or groups that can access to [the OPSWAT Central Management.](the OPSWAT Central Management.)

## [Configure](https://www.opswat.com/docs/ocm/v7.36.0/knowledgebase/how-to-integrate-okta-single-sign-on-in-opswat-central-managemen#configure) OPSWAT Central Management as the Service Provider (SP)

1. Login to OPSWAT Central Management as an admin
2. Navigate to Settings --> Integrations --> Single sign-on and check Enable Single Sign On
3. Upload the XML and the certificate downloaded above.
4. Modify the Logout URL to be your Okta organization URL

After finishing the configuration, you can now login to OPSWAT Central Management from the Okta Dashboard.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/portal/support).
