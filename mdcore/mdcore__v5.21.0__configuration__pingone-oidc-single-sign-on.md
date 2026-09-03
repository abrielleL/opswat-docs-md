<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/configuration/pingone-oidc-single-sign-on -->

# Configure OIDC SSO

### [Create OIDC directory in MDCore](/docs/mdcore/v5.21.0/configuration/pingone-oidc-single-sign-on#create-oidc-directory-in-mdcore)

1. Login to MDCore
2. At dashboard, hit `User Management` in sidebar
3. Under `User Management` page, choose `Directories` tab and hit `Add directory` on the top right

4. In `Add Directory` page, choose `OIDC` in `Directory Type`, fill `Name` for the new directory, MDCore-OIDC for example
5. Fill `Host or IP` where MDCore is hosting, [***https://127.0.0.1:8008***](https://127.0.0.1:8008/) for this example
6. Copy string generated under `Login URL` and store to *redirect_uri*

__

### [Create and configure OIDC application on PingOne](/docs/mdcore/v5.21.0/configuration/pingone-oidc-single-sign-on#create-and-configure-oidc-application-on-pingone)

1. In the PingOne Overview page, navigate `Applications`on sidebar

2. Hit on plus button to add new application

3. Fill application name, MDCore-OIDC for an example, choose `OIDC Web App` for Application Type and hit `Save`

4. Select `Configuration` tab, hit Edit button

5. In `Edit Configuration` page, navigate to `Redirect URIs` and paste [***redirect_uri***](https://opswat.atlassian.net/wiki/spaces/VN/pages/2567472127/PingOne+OIDC#redirect_uri) to the box below, then hit `Save`

6. In `Overview` tab, navigate to `OIDC Discovery Endpoint`, copy the link below and store to *metadata_url*

7. Select Configuration tab, expand General section, navigate to Client ID and Client Secret, copy and store them in client_id and client_secret.

8. Select Attribute Mappings tab and hit Edit button

9. In Edit Attribute Mappings page, hit Add to add new mapping

Info

In this step, we make a mapping from the key name used by MDCore and the name exported by PingOne. For example, we set `given_name` mapped to `Given Name` exported by PingOne. Later on, `given_name` is used by MDCore to identify the login user

10. Fill attribute name, `given_name` in this example, select item `Given Name` in PingOne Mappings and hit `Save` to complete

11. Enable the new application on PingOne

## [Complete configuration on MDCore](/docs/mdcore/v5.21.0/configuration/pingone-oidc-single-sign-on#complete-configuration-on-mdcore)

1. Switch back to MDCore, under Identity Provider, hit Fetch URL, paste metadata_url to the box under, and then hit OK, which requests MDCore to check and set PingOne as its IDP if succeed

2. Under `Service Provider`, paste [***client_id***](https://opswat.atlassian.net/wiki/spaces/VN/pages/2567472127/PingOne+OIDC#client_id) and [***client_secret***](https://opswat.atlassian.net/wiki/spaces/VN/pages/2567472127/PingOne+OIDC#client_secret) to boxes under `Client ID` and `Client secret` respectively
3. Fill ${given_name} in the box under `User identified by`
4. Select `Default role` option, choose the role to assign to login user under `User Role` and hit `Add` to complete setting on MDCore

5. In `User Management` page, toggle the new directory, MDCORE-OIDC in this example. A dialog box is shown to confirm the action. Once `Enable` is hit, all sessions are expired immediately

### [Test the integration](/docs/mdcore/v5.21.0/configuration/pingone-oidc-single-sign-on#test-the-integration)

1. In Home screen on MDCore, hit `Login`, the user is redirected to login page from PingIdentity

2. Login by the account registered to PingIdentity
3. If everything goes right, MDCore dashboard is shown with user identity set at the top right corner

4. Otherwise, access back login page at `<mdcore-host>#/public/backuplogin` for trouble shooting.
