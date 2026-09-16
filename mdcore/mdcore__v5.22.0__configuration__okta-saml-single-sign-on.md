<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/configuration/okta-saml-single-sign-on -->

# Configure SAML SSO

Since 5.15.0, MetaDefender Core has stopped supporting weak digest algorithms SHA1 and MD5. Customers who integrate MD Core with Okta SAML 2.0 are advised to update their Digest Algorithm option to a stronger algorithm if the option is configured in the current settings.

Please follow these steps to update your digest algorithm in Okta:

1. Sign to Okta console with your account.
2. In dashboard, expand `Applications` in the left sidebar and click `Applications`.
3. In your SSO integration, select `General` tab.
4. Navigate to `SAML Settings` and click `Edit`.
5. On `Edit SAML Integration` page, select `Configure SAML` tab.
6. Expand Advanced Settings, navigate to `Digest Algorithm` and select SHA256 or higher.

From MetaDefender Core,

1. Sign in to MetaDefender Core with your account.
2. Select your SSO directory and click `Edit`.
3. Under `Identity Provider` , click `Fetch URL`.
4. Fill the metadata URL with SAML metadata link from Okta.
5. Click `Save Changes`.
### [Create Okta application](/docs/mdcore/v5.22.0/configuration/okta-saml-single-sign-on#create-okta-application)

1. Access <https://www.okta.com/login/> and sign in.
2. In sidebar of dashboard, hit `Applications` to drop sub items down, then select `Applications`.
3. Click `Create App Integration`.

4. In `Sign-in method`, choose `SAML 2.0` and click `Next`.

5. Fill `App name`, MDCore-SAML for example and click `Next`.

### [Create SAML directory in MetaDefender Core](/docs/mdcore/v5.22.0/configuration/okta-saml-single-sign-on#create-saml-directory-in-metadefender-core)

1. Sign in to MetaDefender Core management console.
2. Under `Dashboard`, hit `User Management` in the left sidebar.
3. Under `User Management`, choose `Directories` tab and click `Add directory` in the top right.

4. In `Add Directory` page, select SAML for `Directory Type`.
5. Fill `Name` of the new directory, MDCore-SAML for example.
6. Under `Service Provider`, fill in `Host or IP` where MetaDefender Core is being hosted, [*http://localhost:8008*](https://127.0.0.1:8008/) for this example.

### [Configure Okta](/docs/mdcore/v5.22.0/configuration/okta-saml-single-sign-on#configure-okta)

1. Switch to `Applications` screen in Okta home page.
2. Paste the `Login URL` from MetaDefender Core into `Single sign on URL` and set ID for `Audience URI`, metadefender_core-saml for example.

3. Scroll down, navigate to `Attribute Statements` and set mapping from Okta key name to the one set at `User identified by` in MetaDefender Core, then hit `Next`.

4. Choose your answer at `Feedback` screen and click `Finish`.
5. On the next screen, navigate to `SAML Signing Certificates`, choose the row that has value of column `Status` is "Active" then drop `Actions` down and click `View IdP metadata`.

6. Copy SAML Metadata link.

7. Switch to `Applications` screen in Okta, navigate to `Assignments` tab, and assign users for the application.

### [Complete configuration in MetaDefender Core](/docs/mdcore/v5.22.0/configuration/okta-saml-single-sign-on#complete-configuration-in-metadefender-core)

1. Switch to MetaDefender Core screen, under `Identity Provider`, click on `Fetch URL`.
2. Paste "SAML Metadata link" from Okta to the box under `Fetch URL` and click `OK` to ensure MetaDefender Core can set Okta as its IdP.

3. Under `Service Provider`, fill in user identity under `User identified by` with ${first_name}_${last_name} for example.
4. Select the appropriate role for the user under `User Role`.
5. Click `Add` to complete the settings.

6. In `User Management` screen, toggle the new directory, MDCORE-SAML in this example. A dialog box is shown to confirm the action. Once `Enable` is hit, all existing sessions will be expired immediately and Okta will be used to authenticate users going forward.

### [Test the integration](/docs/mdcore/v5.22.0/configuration/okta-saml-single-sign-on#test-the-integration)

1. Browse MetaDefender Core, hit `Login`, user is redirected to Okta's sign-in page.

2. Sign in by the account registered in Okta.
3. If everything goes right, MetaDefender Core dashboard is shown with user identity set at the top right corner.

4. For troubleshooting, browse `<mdcore-host>#/public/backuplogin`.

### [Test IdP-initiated SSO](/docs/mdcore/v5.22.0/configuration/okta-saml-single-sign-on#test-idp-initiated-sso)

1. Sign in to Okta management page.
2. Navigate to `Applications`/ `Applications` on the sidebar.
3. Select the active SAML application.

4. In `Sign On` tab, find and hit `View SAML setup instructions` button.

5. In the new page, copy the URL under `Identity Provider Single Sign-On URL` section.

6. Paste the copied URL to a web browser and sign in.

3. If everything goes right, MetaDefender Core dashboard is shown with user identity set at the top right corner.

4. For troubleshooting, browse `<mdcore-host>#/public/backuplogin`.
