<!-- source: https://www.opswat.com/docs/mdcore/configuration/onelogin-saml-single-sign-on -->

# Configure SAML SSO

### [Create OneLogin application](/docs/mdcore/configuration/onelogin-saml-single-sign-on#create-onelogin-application)

1. Access [OneLogin](https://www.onelogin.com/) and sign in.
2. On the navigation bar, click `Administration` to access administrator mode, then click on `Applications` to add a new application for integration.

3. Click `Add App` to add a new application.

4. Enter "SAML" in the search box and select `SAML Custom Connector (Advanced)` version SAML2.0 in the results panel.

5. In the new page, fill in `Display Name` with MDCore-SAML, for example, and click `Save`.

### [Create SAML directory in MetaDefender Core](/docs/mdcore/configuration/onelogin-saml-single-sign-on#create-saml-directory-in-metadefender-core)

1. Sign in to MetaDefender Core.
2. In the dashboard, click on `User Management` in the left sidebar.
3. On `User Management` page, select `Directories` tab and click `Add Directory` in the top right corner.

4. In `Add Directory` page, select SAML as `Directory type`, and enter a name for the new directory, such as MDCore-SAML.
5. In `Service Provider` section, enter `Host or IP` where MetaDefender Core is hosted, for this example use <https://127.0.0.1:8008>.
6. Copy the string generated under `Login URL` and store it as *reply_uri*.

### [Complete configuration in OneLogin](/docs/mdcore/configuration/onelogin-saml-single-sign-on#complete-configuration-in-onelogin)

1. In `Applications` screen on OneLogin, select `Configuration` tab.
2. In `Application Details` section, fill in `Recipient` and `ACS (Consumer) URL*` with the `Login URL` copied from MetaDefender Core. Fill in `ACS (Consumer) URL Validator*` with a regular expression version of `Login URL`.

3. Expand `SAML Initiator` section, select `Service Provider`, enter the `Login URL` copied from MetaDefender Core and click `Save`.

4. Select `Parameters` tab and click the plus button to add more fields that will be used to identify the signed-in users in MetaDefender Core.

5. Fill in `Field name` with first_name and click `Save`.

6. Expand `Value` section, choose an appropriate attribute, First Name is an example. Then toggle `Include in SAML assertion` and click `Save`.

7. Click `Save` in the top right corner.
8. Drop `More Actions` down and click on `SAML Metadata` to copy *metadata_url*.

### [Complete configuration in MetaDefender Core](/docs/mdcore/configuration/onelogin-saml-single-sign-on#complete-configuration-in-metadefender-core)

1. Switch back to MetaDefender Core. Under `Identity Provider`, click `Fetch URL`, paste the value of *metadata_url* into the box below, click `OK`, and wait a moment for MetaDefender Core to check and set OneLogin as its IdP.

2. Under `Service Provider`, fill in ${first_name} in the box labeled `User identified by`.
3. Select `Default role` option, choose the appropriate role to assign to users under `User Role`, and click `Add` to complete the settings in MetaDefender Core.

4. On `User Management` page, toggle the new directory, MDCORE-SAML in this example. A dialog box will appear to confirm the action. Once `Enable` is clicked , all sessions will expire immediately.

### [Test the integration](/docs/mdcore/configuration/onelogin-saml-single-sign-on#test-the-integration)

1. On the home screen of MetaDefender Core, click `Login`; the user is redirected to OneLogin page.

2. Sign in using the account registered with OneLogin.
3. If everything goes well, MetaDefender Core dashboard is displayed with the user identity in the top right corner.

4. Otherwise, access backup login page at `<mdcore-host>#/public/backuplogin` for trouble shooting.

### [Test IdP-initiated login](/docs/mdcore/configuration/onelogin-saml-single-sign-on#test-idp-initiated-login)

1. Sign in to OneLogin management page.
2. From the portal menu, navigate to MDCore-SAML and click on the icon.

3. If everything goes well, the user is redirected to MetaDefender Core dashboard with the user identity in the top right corner.

4. Otherwise, access backup login page at <mdcore-host>#/public/backuplogin for trouble shooting.
