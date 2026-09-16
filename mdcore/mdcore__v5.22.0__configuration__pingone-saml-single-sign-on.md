<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/configuration/pingone-saml-single-sign-on -->

# Configure SAML SSO

## [Create SAML directory on MDCore](/docs/mdcore/v5.22.0/configuration/pingone-saml-single-sign-on#create-saml-directory-on-mdcore)

1. Login to MDCore
2. At dashboard, hit `User Management` in sidebar
3. Under `User Management` page, choose `Directories` tab and hit `Add directory` on the top right

4. In `Add Directory` page, choose `SAML` in `Directory Type`, fill `Name` for the new directory, MDCore-SAML for example
5. Under `Service Provider` section, enable option `Use custom entity ID` and fill out the ID, MDCORE-PINGONE-SAML for example, then store it in *entity_id*
6. Fill `Host or IP` where MDCore is hosting, [*https://127.0.0.1:8008*](https://127.0.0.1:8008/) for this example
7. Copy string generated under `Login URL` and store to *reply_uri*

### [Create and configure SAML application in PingOne](/docs/mdcore/v5.22.0/configuration/pingone-saml-single-sign-on#create-and-configure-saml-application-in-pingone)

1. In the PingOne Overview page, navigate `Applications`on sidebar

2. Hit on plus button to add new application

3. Fill application name, MDCore-SAML for an example, choose `SAML Application` for Application Type and hit `Configure`

4. Select `Manually Enter` for SAML Configuration, fill `ACS URLs` with *reply_uri*, and `Entity ID` with *entity_id*, and hit `Save`

5. Select `Overview` tab, navigate to `IDP Metadata URL`, copy the link below and store to *metadata_url*

__

6. Select `Attribute Mappings` tab and click Edit button.

7. In `Edit Attribute Mappings` page, hit `Add` to add new mapping

Info

In this step, we make a mapping from the key name used by MDCore and the name exported by PingOne. For example, we set `given_name` mapped to `Given Name` exported by PingOne. Later on, `given_name` is used by MDCore to identify the login user

8. Fill attribute name, `given_name` in this example, select item `Given Name` in PingOne Mappings, enable `Required` option and hit `Save` to complete

9. Enable the new application on PingOne

## [Complete configuration on MDCore](/docs/mdcore/v5.22.0/configuration/pingone-saml-single-sign-on#complete-configuration-on-mdcore)

1. Switch back to MDCore, under `Identity Provider`, hit `Fetch URL`, paste *metadata_url* to the box under, and then hit `OK`, which requests MDCore to check and set PingOne as its IDP if succeed

2. Under `Service Provider`, fill ${given_name} in the box under `User identified by`

3. Select `Default role` option, choose the role to assign to login user under `User Role` and hit `Add` to complete setting on MDCore

4. In `User Management` page, toggle the new directory, MDCORE-SAML in this example. A dialog box is shown to confirm the action. Once `Enable` is hit, all sessions are expired immediately

### [Test the integration](/docs/mdcore/v5.22.0/configuration/pingone-saml-single-sign-on#test-the-integration)

1. In home screen on MDCore, hit `Login`, the user is redirected to login page from PingIdentity

2. Login by the account registered to PingIdentity
3. If everything goes right, MDCore dashboard is shown with user identity set at the top right corner

4. Otherwise, access back login page at `<mdcore-host>#/public/backuplogin` for trouble shooting.

### [Test IdP-initiated login](/docs/mdcore/v5.22.0/configuration/pingone-saml-single-sign-on#test-idp-initiated-login)

1. Login to PingOne management page.
2. On the left sidebar, hit `Applications`, then `Applications`.
3. Select the SSO directory from which IdP-initiated login is enabled. MDCore-SAML in this example.

4. On the right sidebar, hit tab `Overview`. Copy the URL under `Initiate Single Sign-On URL`.

5. Paste the URL into your browser and try to sign in.

6. If everything goes right, MDCore dashboard is shown with user identity set at the top right corner

7. Otherwise, access back login page at `<mdcore-host>#/public/backuplogin` for troubleshooting.
