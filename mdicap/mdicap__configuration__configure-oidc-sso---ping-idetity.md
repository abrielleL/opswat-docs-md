<!-- source: https://www.opswat.com/docs/mdicap/configuration/configure-oidc-sso---ping-idetity -->

# Configure OIDC SSO - Ping Idetity

This article applies to all MetaDefender ICAP releases deployed on Windows and Linux systems.

## [Create OIDC directory on MD ICAP](/docs/mdicap/configuration/configure-oidc-sso---ping-idetity#create-oidc-directory-on-md-icap)

1. Sign in to MetaDefender ICAP.
2. In the dashboard, click on `User Management` in the left sidebar.
3. On `User Management` page, select `Directories` tab and click `Add Directory` in the top right

4. In `Add Directory` page, choose `OIDC` in `Directory Type`, fill `Name` for the new directory, MDICAP-OIDC for example
5. Fill `Host or IP` where MD ICAP is hosting, [***https://127.0.0.1:8048***](https://127.0.0.1:8008/) for this example
6. Copy string generated under Login URL and store to redirect_uri

## [Create and configure OIDC application on PingOne](/docs/mdicap/configuration/configure-oidc-sso---ping-idetity#create-and-configure-oidc-application-on-pingone)

1. In the PingOne Overview page, navigate `Applications`on sidebar

2. Click the plus button to add a new application.

3. Enter the application name, MDICAP-OIDC as an example, choose `OIDC Web App` for `Application Type`, and click `Save`.

4. Select `Configuration` tab, hit Edit button

5. In `Edit Configuration` page, navigate to `Redirect URIs` and paste [***redirect_uri***](https://opswat.atlassian.net/wiki/spaces/VN/pages/2567472127/PingOne+OIDC#redirect_uri) to the box below, then hit `Save`

6. In `Overview` tab, navigate to `OIDC Discovery Endpoint`, copy the link below and store to *metadata_url*

7. Select `Configuration` tab, expand `General` section, navigate to `Client ID` and `Client Secret`, copy and store them in *client_id* and *client_secret.*

__

8. Select `Attribute Mappings` tab and hit Edit button

9. In `Edit Attribute Mappings` page, hit `Add` to add new mapping

In this step, we make a mapping from the key name used by MD ICAP and the name exported by PingOne. For example, we set `given_name` mapped to `Given Name` exported by PingOne. Later on, `given_name` is used by MD ICAP to identify the login user

10. Fill attribute name, given_name in this example, select item Given Name in PingOne Mappings and hit Save to complete

11. Enable the new application on PingOne

## [Complete configuration on MD ICAP](/docs/mdicap/configuration/configure-oidc-sso---ping-idetity#complete-configuration-on-md-icap)

1. Switch back to MD ICAP, under `Identity Provider`, hit `Fetch URL`, paste [***metadata_url***](https://opswat.atlassian.net/wiki/spaces/VN/pages/2567472127/PingOne+OIDC#metadata_url) to the box under, and then hit `OK`, which requests MD ICAP to check and set PingOne as its IDP if succeed

2. Under `Service Provider`, paste [***client_id***](https://opswat.atlassian.net/wiki/spaces/VN/pages/2567472127/PingOne+OIDC#client_id) and [***client_secret***](https://opswat.atlassian.net/wiki/spaces/VN/pages/2567472127/PingOne+OIDC#client_secret) to boxes under `Client ID` and `Client secret` respectively
3. Fill ${given_name} in the box under `User identified by`
4. Select `Default role` option, choose the role to assign to login user under `User Role` and hit `Add` to complete setting on MD ICAP.

Note: When we successfully fetch, Scope default will be selected is OPENID

5. In `User Management` page, toggle the new directory, MDICAP-OIDC in this example. A dialog box is shown to confirm the action.

## [Test the integration](/docs/mdicap/configuration/configure-oidc-sso---ping-idetity#test-the-integration)

1. In Home screen on MD ICAP, the user is redirected to login page having “Sign-In with SSO” option

2. Select `Sign-In with SSO` and Select Directory to Login `MDICAP-OIDC` in this example

Result Sign on using IDP authentication

3. Login by the account registered to PingIdentity
4. If everything goes right, MD ICAP dashboard is shown with user identity set at the top right corner

5. Otherwise, access back login page at `<mdicap-host>#/public/login` and sign in using the local administrator account for troubleshooting purposes.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
