<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/configuration/onelogin-oidc-single-sign-on -->

# Configure OIDC SSO

### [Create OneLogin application](/docs/mdcore/v5.21.0/configuration/onelogin-oidc-single-sign-on#create-onelogin-application)

1. Access [OneLogin](https://www.onelogin.com/) and sign in.
2. On the navigation bar, click `Administration` to access administrator mode, then click on `Applications` to add a new application for integration.

3. Click `Add App` to add a new application.

4. Enter "OpenId Connect" in the search box and select `OpenId Connect (OIDC)` in the results panel.

5. In the new page, fill in `Display Name` with MDCore-OIDC, for example, and click `Save`.

### [Create OIDC directory in MetaDefender Core](/docs/mdcore/v5.21.0/configuration/onelogin-oidc-single-sign-on#create-oidc-directory-in-metadefender-core)

1. Sign in to MetaDefender Core.
2. In the dashboard, click on `User Management` in the left sidebar.
3. On `User Management` page, select `Directories` tab and click `Add Directory` in the top right corner.

4. In `Add Directory` page, select OIDC as `Directory type`, and enter a name for the new directory, such as MDCore-OIDC.
5. Enter `Host or IP` where MetaDefender Core is hosted, for this example use <https://127.0.0.1:8008>.
6. Copy the string generated under `Login URL`.

### [Complete configuration in OneLogin](/docs/mdcore/v5.21.0/configuration/onelogin-oidc-single-sign-on#complete-configuration-in-onelogin)

1. Back to `Applications` screen in OneLogin.
2. Choose `Configuration` in the left side bar and paste value of `Login URL` from MetaDefender Core into `Redirect URI's` field.

3. In `SSO` of the left side bar, under `Enable OpenID Connect` section, copy `Client ID`, `Client Secret`, and `Issuer URL`.

4. Click `Save` to complete.

### [Complete configuration in MetaDefender Core](/docs/mdcore/v5.21.0/configuration/onelogin-oidc-single-sign-on#complete-configuration-in-metadefender-core)

1. Switch back to MetaDefender Core. Under `Identity Provider`, click `Fetch URL`, paste value of `Issuer URL` from OneLogin into the box below, click `OK`, and wait a moment for MetaDefender Core to check and set OneLogin as its IdP.

2. Under `Service Provider`, paste the values of `Client ID` and `Client Secret` from OneLogin into the boxes labeled `Client ID` and `Client secret`, respectively.

3. Fill in `User Identified By` with ${given_name}.
4. Select `Default role` option, choose the appropriate role under `User Role`, and click `Add` to complete.

5. In `User Management` page, toggle the new directory, MDCORE-OIDC in this example. A dialog box will appear to confirm the action. Once `Enable` is clicked, all sessions will expire immediately.

### [Test the integration](/docs/mdcore/v5.21.0/configuration/onelogin-oidc-single-sign-on#test-the-integration)

1. On the home screen of MetaDefender Core, click `Login`; the user is redirected to OneLogin page.

2. Sign in using the account registered with OneLogin.
3. If everything goes well, MetaDefender Core dashboard is displayed with the user identity in the top right corner.

4. Otherwise, access backup login page at `<mdcore-host>#/public/backuplogin` for trouble shooting.
