<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/configuration/entra-oidc-single-sign-on -->

# Configure OIDC SSO

### [Register a new application in Azure](/docs/mdcore/v5.22.0/configuration/entra-oidc-single-sign-on#register-a-new-application-in-azure)

1. Access [Azure portal](https://portal.azure.com/) and sign in.
2. On the home page, select `Microsoft Entra ID` under `Azure services`.

3. Select `App registrations` under `Manage` section on the left sidebar, then click on `New registration` on the top menu bar.

4. In `Register an application` page, fill in the name for the new application, using MDCore-OIDC as an example, and click `Register` to complete.

5. Select `Token configuration` in the left sidebar, hit `Add optional claim`, choose `ID` on the right sidebar, enable essential claims (given_name in this example) and click `Add` at the bottom.

6. Click `Add` on the popup to finish.

Info

Enabled claims will be used later by MetaDefender Core to identify logged-in user.

### [Create OIDC directory in MetaDefender Core](/docs/mdcore/v5.22.0/configuration/entra-oidc-single-sign-on#create-oidc-directory-in-metadefender-core)

1. Sign in to MetaDefender Core.
2. At the dashboard, click `User Management` in the left sidebar.
3. In `User Management` page, choose `Directories` tab and click `Add directory` on the top right corner.

4. In `Add Directory` page, choose OIDC in `Directory type`.
5. Fill in the name the new directory, such as MDCore-OIDC.
6. In `Service Provider` section, fill in `Host or IP` with the host or IP address where MetaDefender Core is hosted; for this example, it is [https://127.0.0.1:8008](https://localhost:8008).
7. Copy the `Login URL` and store it somewhere for later use.

### [Complete configuration in Entra ID](/docs/mdcore/v5.22.0/configuration/entra-oidc-single-sign-on#complete-configuration-in-entra-id)

1. Back to Microsoft Entra ID, on `MDCore-OIDC` page, select `Overview` section in the left sidebar and click on `Add a Redirect URI` link to switch to `Authentication` page.

2. In `Authentication` page, click `Add a platform` and choose `Web` option in the right sidebar.

3. Fill in `Redirect URIs` field with the `Login URL` copied from MDCore, enable `Access tokens` option and click `Configure`.

4. Select `Overview` in the left sidebar again, copy the string next to `Application (client) ID` and store as *client_id.*

5. Click `Endpoints` in the top bar, copy the URI under `OpenID Connect metadata document` in the right sidebar and store it as *metadata_uri.*

6. Select `Certificates & secrets` in the left sidebar, go to `Client secrets (0)` tab, click `New client secret`, fill in the secret description and set expiration and, then click `Add` to complete.

7. A new client secret is created under `Client secret (1)` tab; copy the string under `Value` column and store it as *client_secret.*

Info

Entra ID will hide the client secret completely when page `Certificate & secrets` is left. Administrator is recommended to store the client secret in a safe place, otherwise they have to create a new one.

### [Complete configuration in MetaDefender Core](/docs/mdcore/v5.22.0/configuration/entra-oidc-single-sign-on#complete-configuration-in-metadefender-core)

1. Switch back to MetaDefender Core. Under `Identity Provider` section, click `Fetch URL` and paste [*metadata_uri*](https://opswat.atlassian.net/wiki/spaces/VN/pages/2567537666/Entra+OIDC#metadata_uri) gathered in **Configure Azure** stage into the box under `Fetch URL`. Click `OK` and wait a moment for MetaDefender Core to set Microsoft Entra ID as its IDP.

2. Under `Service Provider` section, paste [*client_id*](https://opswat.atlassian.net/wiki/spaces/VN/pages/2567537666/Entra+OIDC#client_id) and [*client_secret*](https://opswat.atlassian.net/wiki/spaces/VN/pages/2567537666/Entra+OIDC#client_secret) gathered in **Configure Azure** stage to `Client ID` and `Client secret` respectively.

3. Fill user identity under `User identified by`, ${given_name} is used in this example.
4. Select `Default role` option and select correct role for the user under `User Role`
5. Click `Add` to complete the settings.

6. In `User Management` screen of MetaDefender Core, toggle MDCORE-OIDC directory. A dialog box appears to confirm the action. Once `Enable` is clicked, all sessions expire immediately.

### [Test the integration](/docs/mdcore/v5.22.0/configuration/entra-oidc-single-sign-on#test-the-integration)

1. At the home screen of MetaDefender Core, click `Login`; the user is redirected to Microsoft Entra ID sign-in page.

2. Sign in using the account registered with Microsoft Entra ID.
3. If everything goes correctly, MetaDefender Core dashboard is displayed with user's identity shown in the top right corner.

4. Otherwise, access backup login page at `<mdcore-host>#/public/backuplogin` for trouble shooting.
