<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/configuration/okta-oidc-single-sign-on -->

# Configure OIDC SSO

View as Markdown Ask ChatGPT about this page Ask Claude about this page Warning

After the integration is successfully set up, any modifications on Okta application could lead to the regeneration of the client secret, causing Okta to reject requests from MetaDefender Core due to a mismatch in the client secret. In this instance, the customer should copy the new secret from Okta and update `Client secret` field within `Service Provider` of MetaDefender Core with the new one.

### [Create Okta application](/docs/mdcore/v5.22.1/configuration/okta-oidc-single-sign-on#create-okta-application)

1. Access <https://www.okta.com/login/> and sign in.
2. In the sidebar of dashboard, hit `Applications` to drop sub items down, then select `Applications`.
3. Click `Create App Integration`.

4. In `Sign-in method`, select `OIDC - OpenID Connect`. In `Application type` choose `Web Application` and click `Next`.

5. Fill `App name`, MDCore-OIDC for example and click `Next`.

### [Create OIDC directory in MetaDefender Core](/docs/mdcore/v5.22.1/configuration/okta-oidc-single-sign-on#create-oidc-directory-in-metadefender-core)

1. Sign in to MetaDefender Core management console.
2. Under `Dashboard`, hit `User Management` in the sidebar.
3. Under `User Management`, select `Directories` tab and click `Add directory` in the top right.

4. In `Add Directory` page, choose OIDC for `Directory Type`.
5. Fill `Name` of the new directory, MDCore-OIDC for example.
6. Under `Service Provider`, fill in `Host or IP` where MetaDefender Core is being hosted, [*http://localhost:8008*](https://127.0.0.1:8008/) for this example.

### [Complete configuration in Okta](/docs/mdcore/v5.22.1/configuration/okta-oidc-single-sign-on#complete-configuration-in-okta)

1. Switch to `Applications` screen in Okta home page.
2. Paste the `Login URL` from MetaDefender Core into `Sign-in redirect URIs` and grant permission for everyone to access our application in `Assignments` then click `Save`.

3. In `General` tab, copy `Client ID` and `Client Secret`.

### [Complete configuration in MetaDefender Core](/docs/mdcore/v5.22.1/configuration/okta-oidc-single-sign-on#complete-configuration-in-metadefender-core)

1. Switch to MetaDefender Core screen, under `Identity Provider`, click on `Fetch URL`.
2. OIDC link will be built by appending */.well-known/openid-configuration* to your Okta domain url (Referred [Okta document](https://developer.okta.com/docs/reference/api/oidc/#well-known-openid-configuration)). For example `dev-115662.okta.com/.well-known/openid-configuration`.
3. Paste OIDC configuration link above to the box under `Fetch URL` and hit `OK` to ensure MetaDefender Core can set Okta as its IdP.

4. Under `Service Provider`, paste the value of `Client ID` and `Client secret` that you copied from Okta respectively.

4. Under `Service Provider`, fill in `User identified by` with ${given_name}_${family_name} for example.
5. Select appropriate role for the user under `User Role`.
6. Click `Add` to complete the settings.

7. On `User Management` screen, toggle the new directory, MDCORE-OIDC in this example. A dialog box is shown to confirm the action. Once `Enable` is hit, all existing sessions will be expired immediately and Okta will be used to authenticate users going forward.

### [Test the integration](/docs/mdcore/v5.22.1/configuration/okta-oidc-single-sign-on#test-the-integration)

1. Browse MetaDefender Core, hit `Login`, user is redirected to Okta's sign-in page.

2. Sign in by the account registered in Okta.
3. If everything goes right, MetaDefender Core dashboard is shown with user identity set at the top right corner.

4. For troubleshooting, browse `<mdcore-host>#/public/backuplogin`.
