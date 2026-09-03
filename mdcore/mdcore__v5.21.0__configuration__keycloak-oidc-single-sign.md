<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/configuration/keycloak-oidc-single-sign -->

# Configure OIDC SSO

### [Create a realm in Keycloak](/docs/mdcore/v5.21.0/configuration/keycloak-oidc-single-sign#create-a-realm-in-keycloak)

1. Sign in to Administrator Console, drop the list in the top left corner, and click `Create realm`.

Info

Keycloak initially includes a single realm `master` which is used for managing Keycloak only and not for any applications.

2. Enter `Realm name` e.g. myrealm and click `Create`.

3. Select `Users` in the left sidebar and click `Create new user`.

4. Enter values for `Username`, `Email`, `First name` and `Last name`; then click `Create`.

5. Under `User details`, select `Credentials` tab and click `Set password` to create a password for the user created in the previous step.

6. Enter the password and toggle `Temporary` to Off, then click `Save`.

### [Create OIDC directory in MetaDefender Core](/docs/mdcore/v5.21.0/configuration/keycloak-oidc-single-sign#create-oidc-directory-in-metadefender-core)

1. Sign in to MetaDefender Core management console.
2. Under `Dashboard`, click `User Management` in the left sidebar.
3. Under `User Management`, select `Directories` tab and hit `Add directory` in the top right.

4. On `Add Directory` page, select OIDC in `Directory type`.
5. Fill `Name` of the new directory, such as KEYCLOAK_OIDC.
6. Under `Service Provider`, fill in `Host or IP` where MetaDefender Core is being hosted, using <http://metadefendercore.com:8008> as an example.
7. Click `Add`.
8. Copy the value of `Login URLs` and store to *login_url.*

### [Create Keycloak application](/docs/mdcore/v5.21.0/configuration/keycloak-oidc-single-sign#create-keycloak-application)

1. On screen `myrealm`, select `Clients` in the sidebar and click `Create client`.

2. Choose `OpenID Connect` for `Client type` and enter `Client ID` (MD_CORE_OIDC for example) and store to *client_id*, then hit `Next`.

3. Turn on `Client authentication` then click `Next`.

4. Paste the *login_url* into `Valid redirect URIs` and click `Save`.

5. Go to tab `Credentials` and copy the `Client Secret` and store to *client_secret.*

6. At tab `Client scopes`, select `MD_CORE_OIDC-dedicated`.

7. Under `Dedicated scopes`, navigate to `Mappers` tab and click `Add predefines mapper`.

8. Search for `given name`, then press `Add`.

9. Select `Realm settings` in sidebar, navigate to tab `General`, click `OpenID Endpoint Configuration` and store OIDC metadata link to *metadata_url*.

### [Complete configuration in MetaDefender Core](/docs/mdcore/v5.21.0/configuration/keycloak-oidc-single-sign#complete-configuration-in-metadefender-core)

1. Switch to MetaDefender Core screen, under `Identity Provider`, click `Fetch URL`.
2. Paste the *metadata_url* from Keycloak to the box under `Fetch URL` and click `OK` to ensure MetaDefender Core can set Keycloak as its IdP.
3. Under section `Service Provider`, paste the *client_id* and *client_secret* to boxes under `Client ID` and `Client Secret` respectively.
4. Fill user identity under `User identified` by with `${given_name}`.

5. Select the appropriate role for the user under `User Role`.
6. Click `Add` to complete the settings.
7. On `User Management` screen, toggle the new directory, *KEYCLOAK-OIDC* in this example. A dialog box will appear to confirm the action. Once `Enable` is clicked, all existing sessions will expire immediately.

### [Test the integration](/docs/mdcore/v5.21.0/configuration/keycloak-oidc-single-sign#test-the-integration)

1. Click `Login` from the home screen of MetaDefender Core; the user is redirected to Keycloak page.
2. Sign in with the account registered in Keycloak.

3. If everything goes well, MetaDefender Core dashboard will be displayed with user identity set in the top right corner.

4. Otherwise, access backup login page at `<mdcore-host>#/public/backuplogin` for trouble shooting.
