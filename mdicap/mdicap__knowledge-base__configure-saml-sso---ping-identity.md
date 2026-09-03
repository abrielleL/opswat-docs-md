<!-- source: https://www.opswat.com/docs/mdicap/knowledge-base/configure-saml-sso---ping-identity -->

# Configure SAML SSO - Ping Identity

## [**Create SAML directory in MetaDefender ICAP**](/docs/mdicap/knowledge-base/configure-saml-sso---ping-identity#create-saml-directory-in-metadefender-icap)

1. Sign in to MetaDefender ICAP.
2. In the dashboard, click on `User Management` in the left sidebar.
3. On `User Management` page, select `Directories` tab and click `Add Directory` in the top right corner.
4. In `Add Directory` page, select `SAML` as `Directory type`, and enter a name for the new directory, such as MDICAP-SAML.
5. In `Service Provider` section, enable `Use custom entity ID` option and enter the ID, such as MDICAP-PINGONE-SAML, then store it in *entity_id*.
6. Enter `Host or IP` where MD ICAP is hosted, for this example use <https://127.0.0.1:8048>
7. Copy the string generated under `Login URL` and store it as *reply_uri*.

## [**Create and configure SAML application in PingOne**](/docs/mdicap/knowledge-base/configure-saml-sso---ping-identity#create-and-configure-saml-application-in-pingone)

1. In the PingOne Overview page, navigate to `Applications`on the sidebar.

2. Click the plus button to add a new application.

3. Enter the application name, MDICAP-SAML as an example, choose `SAML Application` for `Application Type`, and click `Configure`.

4. Select `Manually Enter` for SAML Configuration, fill in `ACS URLs` with *reply_uri*, `Entity ID` with *entity_id*, and click `Save`.

5. Select `Overview`tab, navigate to `IDP Metadata URL`, copy the link below, and store it in *metadata_url*.

6. Select `Attribute Mappings` tab and click Edit button.

7. On `Edit Attribute Mappings` page, click `Add` to create a new mapping.

In this step, we create a mapping from the key name used by MetaDefender ICAP to the one exported by PingOne. For example, we set `given_name` mapped to `Given Name` from PingOne. Later, `given_name` is utilized by MetaDefender ICAP to identify the logged-in user..

8. Enter the attribute name, `given_name` in this example, select the item `Given Name` in `PingOne Mappings`, enable `Required` option, and click `Save` to complete.

9. Enable the new application in PingOne.

### [**Complete configuration in MetaDefender ICAP**](/docs/mdicap/knowledge-base/configure-saml-sso---ping-identity#complete-configuration-in-metadefender-icap)

1. Switch back to MetaDefender ICAP. Under `Identity Provider`, click `Fetch URL`, paste the value of *metadata_url* into the box below, click `OK`, and wait a moment for MetaDefender ICAP to check and set PingOne as its IdP.
2. Under `Service Provider`, fill in ${given_name} in the box labeled `User identified by`.

3. Select `Default role` option, choose the appropriate role to assign to users under `User Role`, and click `Add` to complete the settings in MetaDefender ICAP.

4. On `User Management` page, toggle the new directory, MDICAP-SAML in this example. A dialog box will appear to confirm the action. Once `Enable` is clicked , all sessions will expire immediately.

## [**Test the integration**](/docs/mdicap/knowledge-base/configure-saml-sso---ping-identity#test-the-integration)

1. On the home screen of MetaDefender ICAP, click `Login`; the user is redirected to PingIdentity login page.

2. Select the Directory to Login

3. Sign in using the account registered with PingIdentity.
4. If everything goes well, MetaDefender ICAP dashboard is displayed with the user identity in the top right corner
5. Otherwise, access backup login page at `<mdicap-host>#/public/backuplogin` for troubleshooting.

## [**Test IdP-initiated login**](/docs/mdicap/knowledge-base/configure-saml-sso---ping-identity#test-idp-initiated-login)

1. Sign in to PingOne management page.
2. In the left sidebar, click on `Applications`, then `Applications`.
3. Select the SSO directory from which IdP-initiated login is enabled, such as MDICAP-SAML in this example.

4. In the right sidebar, click on `Overview`tab. Copy the URL under `Initiate Single Sign-On URL`.

5. Paste the URL into your browser and try to sign in.
6. If everything goes well, MetaDefender ICAP dashboard is displayed with the user identity in the top right corner.
