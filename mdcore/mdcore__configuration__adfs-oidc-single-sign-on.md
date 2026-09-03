<!-- source: https://www.opswat.com/docs/mdcore/configuration/adfs-oidc-single-sign-on -->

# Configure OIDC SSO

ADFS requires MetaDefender Core to enable HTTPS for connections. Please follow these [steps](/docs/mdcore/configuration/enabling-https) to first enable HTTPS on MetaDefender Core.

### [Set up OIDC in ADFS](/docs/mdcore/configuration/adfs-oidc-single-sign-on#set-up-oidc-in-adfs)

1. In the top right corner of `Server Manager`, click on `Tools` and select `AD FS Management` from the drop-down menu.

2. In `AD FS` window, right click on `Application Groups` and select `Add Application Group` from the drop-down menu.

3. On `Welcome` page, provide a descriptive name for your application , e.g. MDCORE_OIDC, select `Server application accessing a web API` under `Template`, and click `Next`.

4. On `Server application` page, copy the string under `Client Identifier` for later use, set a placeholder <https://myplaceholder> for `Redirect URI`, then click `Add` and `Next`.

5. On `Configure Application Credentials` page, check `Generate a shared secre`t, click `Copy to clipboard`, then save the secret string for later use and click `Next`.

6. On `Configure Web API` page, enter the string of `Client Identifier` from step 4 into the box under `Identifier`, click `Add` , and `Next`.

7. On `Choose Access Control Policy` page, select `Permit everyone` and click `Next`.

8. On `Configure Application Permissions` page, select the scopes `allatclaims`, `email`, `openid`, and `profile` under `Permitted scopes`, and then click `Next`.

9. Click `Next` on the following page and `Close` to finish.

10. Back in `AD FS` window, right click on the item MDCORE_OIDC and select `Properties`.

11. Select `MDCORE_OIDC - Web API` and click `Edit`.

12. Go to `Issuance Transform Rules` tab and click `Add Rule`.

13. Select `Send LDAP Attributes as Claims` for `Claim rule template` and click `Next`.

14. Enter a name for `Claim rule`, e.g. display_name, select `Active Directory` for `Attribute Store`. Under `LDAP Attribute` column, select `Display-Name` from the drop-down list, enter given_name for the `Outgoing Claim Type` column, and click `Finish`.

15. Click `Apply` on the next page and `OK` to close the wizard.

### [Create OIDC directory in MetaDefender Core](/docs/mdcore/configuration/adfs-oidc-single-sign-on#create-oidc-directory-in-metadefender-core)

1. Sign in to MetaDefender Core.
2. On the dashboard, click `User Management` in the sidebar.
3. In `User Management` page, select `Directories` tab and click `Add Directory` in the top right corner.

4. In `Add Directory` page, choose OIDC as `Directory type`.
5. Enter the name of the new directory, such as ADFS_OIDC.
6. In `Service Provider` section, paste the values of `Client ID` and `Client Secret` copied from ADFS, respectively.
7. In `Service Provider` section, fill in `Host or IP` with the host or IP address where MetaDefender Core is hosted; for this example, it is <https://localhost:8008>.
8. Copy `Login URL`.

### [Complete configuration in ADFS](/docs/mdcore/configuration/adfs-oidc-single-sign-on#complete-configuration-in-adfs)

1. Back to `AD FS`, right click on item MDCORE_OIDC and select `Properties`, then choose `MDCORE OIDC - Server application` and click `Edit`.

2. Remove the placeholder <https://myplaceholder> by selecting it and clicking `Remove`.

3. Paste the `Login URL` from MetaDefender Core into `Redirect URI`, click `Add`, then `Apply` and `OK`.

4. Click `OK` to complete the setup.

### [Complete configuration in MetaDefender Core](/docs/mdcore/configuration/adfs-oidc-single-sign-on#complete-configuration-in-metadefender-core)

1. Access `AD FS Management` tool from `Server Manager`, expand `AD FS` --> `Service` --> `Endpoints` on the left panel. In `Endpoints` panel, navigate to `OpenID Connect` section and copy the URL path of type `OpenID Connect Discovery`.

2. Build the full URL to the metadata endpoint by appending the path from step 1 to the qualified domain name of ADFS

HtmlCopyhttps://<adfs_fully_qualified_domain_name>/<metadata_endpoint_path>

- For example:

HtmlCopyhttps://win-tst/adfs/.well-known/openid-configuration

3. Switch back to MetaDefender Core. Under `Identity Provider` section, click `Fetch URL` and paste the link above into the box under `Fetch URL`. Click `OK` and wait a moment for MetaDefender Core to set ADFS as its IDP.
4. In `Service Provider` section, fill in the user identity under `User identified by` with the configured values of `Outgoing Claim Type`, e.g. ${given_name} in this instruction.
5. Select the correct role for the user under `User Role`.
6. Disable `Load additional profiles from the user endpoint` option since AD FS 2016 and newer have not yet supported the `/userinfo` endpoint.
7. Click `Add` to complete the settings.

8. On `User Management` screen, toggle ADFS_OIDC directory. A dialog box appears to confirm the action. Once `Enable` is clicked, all sessions are expired immediately, and ADFS is used to authenticate the user.

### [Test the integration](/docs/mdcore/configuration/adfs-oidc-single-sign-on#test-the-integration)

1. Click `Login` from the home screen of MetaDefender Core; the user is redirected to the ADFS page.

2. Sign in with the account created in the system domain.
3. If everything goes right, the MetaDefender Core dashboard is displayed with the user identity set in the top right corner.

4. Otherwise, access backup login page at `<mdcore-host>#/public/backuplogin` for trouble shooting.
