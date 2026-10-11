<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/configuration/keycloak-saml-single-sign-on -->

# Configure SAML SSO

View as Markdown Ask ChatGPT about this page Ask Claude about this page
### [Create a realm in Keycloak](/docs/mdcore/v5.22.1/configuration/keycloak-saml-single-sign-on#create-a-realm-in-keycloak)

1. Sign in to Administrator Console, drop the list in the top left corner, and click `Create realm`.

Info

Keycloak initially includes a single realm `master` which is used for managing Keycloak only and not for any applications.

2. Enter `Realm name` e.g. myrealm and click `Create`.

3. Select `Users` in the left sidebar and click `Add user`.

4. Enter values for `Username`, `Email`, `First name` and `Last name`; then click `Create`.

5. Under `User details`, select `Credentials` tab and click `Set password` to create a password for the user created in the previous step.

6. Enter the password and toggle `Temporary` to Off, then click `Save`.

### [Create SAML directory in MetaDefender Core](/docs/mdcore/v5.22.1/configuration/keycloak-saml-single-sign-on#create-saml-directory-in-metadefender-core)

1. Sign in to MetaDefender Core management console.
2. Under `Dashboard`, click `User Management` in the left sidebar.
3. Under `User Management`, select `Directories` tab and hit `Add directory` in the top right.

4. On `Add Directory` page, select SAML in `Directory type`.
5. Fill `Name` of the new directory, such as KEYCLOAK_SAML.
6. Under `Service Provider`, fill in `Host or IP` where MetaDefender Core is being hosted, using <http://localhost:8008> as an example.
7. Copy the value of `Login URL`.

### [Create Keycloak application](/docs/mdcore/v5.22.1/configuration/keycloak-saml-single-sign-on#create-keycloak-application)

1. On screen `myrealm`, select `Clients` in the sidebar and click `Create client`.

2. Choose **SAML** for `Client type` and enter **MDCORE** for `Client ID` then click `Next` and `Save`.

3. Under `General Settings`, find the `Valid Redirect URIs` field, then paste the **Login URL** from MetaDefender Core into the corresponding input box.

4. Find `Signature and Encryption` section, enable `Sign assertions` and click `Save`.

5. Go to `Advance` tab and paste the value of **Login URL** from MetaDefender Core to `Assertion Consumer Service Redirect Binding URL` and click `Save`.

6. In `Keys`tab, toggle `Client signature required` to Off.

7. In `Client scopes` tab, select `MDCORE-dedicated`.

8. Under `Dedicated scopes`, navigate to `Mappers` tab and click `Add predefines mapper`.

9. Check `X500 givenName` and `X500 surname`, then click `Add`.

10. Back to `Mappers` tabs, click on `X500 givenName`.

11. Enter first_name to `SAML Attribute Name` and click `Save`.

12. Click `X500 surname` in `Mappers` tab.

13. Enter last_name for `SAML Attribute Name` and click `Save`.

14. Select `Realm settings` in the sidebar, navigate to `General` tab, click `SAML 2.0 Identity Provider Metadata` and copy the metadata link.

### [Complete configuration in MetaDefender Core](/docs/mdcore/v5.22.1/configuration/keycloak-saml-single-sign-on#complete-configuration-in-metadefender-core)

1. Switch to MetaDefender Core screen, under `Identity Provider`, click `Fetch URL`.
2. Paste the metadata link from Keycloak to the box under `Fetch URL` and click `OK` to ensure MetaDefender Core can set Keycloak as its IdP.

3. Under `Service Provider` section, enable `Use Custom Entity ID` and enter MDCORE in `Custom Entity ID` field.

Info

The ID set for `Use Custom Entity ID` must match `Client ID` created by Keycloak.

4. Fill in the user identity under `Use Identified by` with ${first_name}_${last_name}, for example.
5. Select the appropriate role for the user under `User Role`.
6. Click `Add` to complete the settings.

7. On `User Management` screen, toggle the new directory, *KEYCLOAK-SAML* in this example. A dialog box will appear to confirm the action. Once `Enable` is clicked, all existing sessions will expire immediately.

### [Test the integration](/docs/mdcore/v5.22.1/configuration/keycloak-saml-single-sign-on#test-the-integration)

1. Click `Login` from the home screen of MetaDefender Core; the user is redirected to Keycloak page.

2. Sign in with the account registered in Keycloak.

3. If everything goes well, MetaDefender Core dashboard will be displayed with user identity set in the top right corner.

4. Otherwise, access backup login page at `<mdcore-host>#/public/backuplogin` for trouble shooting.
