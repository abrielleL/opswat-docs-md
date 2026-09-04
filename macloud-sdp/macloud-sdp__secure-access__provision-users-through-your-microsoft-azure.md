<!-- source: https://www.opswat.com/docs/macloud-sdp/secure-access/provision-users-through-your-microsoft-azure -->

# Provision users through your Microsoft Azure

## [Step 1. Create SDP app on Microsoft Azure](/docs/macloud-sdp/secure-access/provision-users-through-your-microsoft-azure#step-1-create-sdp-app-on-microsoft-azure)

1. Log into Azure Portal as Administrator
2. Navigate to **Enterprise applications >** **All applications**. Then click on **New application**

3. Click on **Create your on application** and input a name. Then click **Create**

4. Enter some placeholder value for fields in Basic SAML Configuration, then click save. You will need to to update these fields in later steps.

5. Add group claim for SAML Response

   1. Click *Edit* on section *User Attributes & Claims*

2. Click on "Add a group claim", choose "All groups" options(or you can choose what group you want to include in the SAML response) then click **Save**

3. Get the Group Claim name

6. Download Azure metadata for the SDP app. This data will be used to upload to MetaDefender IT-OT Access to enable single sign on for your users. Select Single sign-on on the left navigation, scroll down to SAML Signing Certificate section and and click on "Federation Metadata XML" to download IDP metadata file

7. (Optional) Get additional information

   1. Download Azure’s certificate

2. Get Azure Login URL

3. Get Azure AD Identifier

8. Assign your users/groups you want to allow log into SDP on MetaDefender IT-OT Access to this application

## [Step 2. Configure SSO SDP on MetaDefender IT-OT Access](/docs/macloud-sdp/secure-access/provision-users-through-your-microsoft-azure#step-2-configure-sso-sdp-on-metadefender-it-ot-access)

1. Log into the [MetaDefender IT-OT Access console](https://gears.opswat.com/console)
2. Navigate to User Management > SSO > SDP and check “Enable Single Sign On”

3. Next to “Import configuration from XML Metadata file”, click “Choose File” and upload the “metadata” file you just downloaded in Step 1.6. This should automatically fill in the “Current Certificate”, “Issuer”, and “IdP SSO URL” fields Leave the Logout URL and Error URL fields blank
4. (Optional) Use this step if you can not import the metadata file

   1. **IdP Certificate**: Upload the certificate downloaded in Step 1.7.a
   2. **Issuer:** Use the value got from Step 1.7.c
   3. **IdP SSO URL**: Use the value got from Step 1.7.b
5. At the bottom, click “Add Group Attribute” and enter the value from Step 1.5.c

6. Scroll to the top of the page, click “Save” and enter your PIN
7. At the bottom of the page you will see a new value called “MetaDefender IT-OT Access Login URL”

8. Copy new value called “MetaDefender IT-OT Access Entity ID“

## [Step 3. Update Applications settings on Identity Provider](/docs/macloud-sdp/secure-access/provision-users-through-your-microsoft-azure#step-3-update-applications-settings-on-identity-provider)

1. Log into Azure Portal as administrator
2. Click **Azure Active Directory**.
3. Navigate to **Enterprise applications >** **All applications**.
4. Select the SDP application
5. Select Single sign-on.
6. Click the edit icon (pencil icon) on Basic SAML Configuration section
7. Replace Identifier with value got from step 2.8. Replace Reply URL with the MetaDefender IT-OT Access URL which you got from Step 2.7
8. Click **Save**

## [Step 4. Configure IDP Groups on MetaDefender IT-OT Access](/docs/macloud-sdp/secure-access/provision-users-through-your-microsoft-azure#step-4-configure-idp-groups-on-metadefender-it-ot-access)

1. Navigate to the MetaDefender IT-OT Access console at metaaccess.com, then go to User Management > IdP Groups, and click “Add”
2. Fill in a group name from your Azure, enter your PIN and choose Add. Your new group will show up in the “IdP Groups” section.

3. When you are ready to assign your new groups to protected applications, go to Secure Access > Protected Apps, click the “Assign” link next to your desired application(s)
4. On the “Assign End Users/IdP Groups to Protected Applications” Move groups “Available Users/Groups” to “Selected Users/Groups” to assign access, then enter your PIN again and choose Enter
