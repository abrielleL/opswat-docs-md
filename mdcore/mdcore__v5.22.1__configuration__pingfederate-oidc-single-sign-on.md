<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/configuration/pingfederate-oidc-single-sign-on -->

# Configure OIDC SSO

View as Markdown Ask ChatGPT about this page Ask Claude about this page
### [Set up PingFederate](/docs/mdcore/v5.22.1/configuration/pingfederate-oidc-single-sign-on#set-up-pingfederate)

#### [Configurate PingFederate](/docs/mdcore/v5.22.1/configuration/pingfederate-oidc-single-sign-on#configurate-pingfederate)

1. Sign in to PingFederate console at `https://service-ip:service-port`, where `service-ip` and `service-port` refer to the IP address and port of the machine hosting PingFederate server.
2. In homepage, navigate to `SYSTEM` tab and select `Server` from the left sidebar.
3. Select `Protocol Settings`, enter `Base URL`, `SAML 2.0 ENTITY ID,` and `SAML 1.X ISSUER/AUDIENCE`, then click `Save` to complete.

#### [Set up simple Password Credential Validators](/docs/mdcore/v5.22.1/configuration/pingfederate-oidc-single-sign-on#set-up-simple-password-credential-validators)

1. In homepage, navigate to `SYSTEM` tab and click on `Password Credential Validators`.

2. Click `Create New Instance`.
3. Enter `INSTANCE NAME` and `INSTANCE ID`, select `Simple Username Password Credential Validator` for `TYPE`, and click `Next`.

4. In `Create Credential Validator Instance` page, click `Add a new row to 'Users'.`

5. Enter `Username`, `Password`, and `Confirm Password`, then click `Update` and `Next`.

6. Review all selected options in `Summary` tab, and click `Save`.

#### [Set up a simple IdP Adapter](/docs/mdcore/v5.22.1/configuration/pingfederate-oidc-single-sign-on#set-up-a-simple-idp-adapter)

1. In homepage, navigate to `AUTHENTICATION` tab and click on `IdP Adapters`.

2. Click `Create New Instance`.
3. Enter `INSTANCE NAME`, `INSTANCE ID,` and select `HTML Form IdP Adapter` for `TYPE` . Click `Next`.

4. Click `Add a new row to 'Credential Validators'`.

5. Select the Password Credential Validator created in the previous stage, that is "Simple MDCore PCV", then click `Update` and `Next`.

6. Click `Next` on `Extended Contract` tab.
7. In `Adapter Attributes` tab, toggle `username` attribute under `Pseudonym` column, and click `Next`.

8. Click `Next` on `Adapter Contract Mapping` tab.
9. Review all selected options in `Summary` tab and click `Save` to complete.

#### [Set up Signing, Decryption Keys and Certificates](/docs/mdcore/v5.22.1/configuration/pingfederate-oidc-single-sign-on#set-up-signing-decryption-keys-and-certificates)

1. In homepage, navigate to `SECURITY` tab and select `Signing & Decryption Keys & Certificates`.

2. Click `Create New`.
3. Enter `COMMON NAME`, `ORGANIZATION`, and `COUNTRY`, along with any other necessary information, then click `Next`.

4. Review all selected options in `Summary` tab and click `Save` to complete.

#### [Set up Authentication Policies](/docs/mdcore/v5.22.1/configuration/pingfederate-oidc-single-sign-on#set-up-authentication-policies)

1. In homepage, navigate to `AUTHENTICATION` tab, and click `Policies`.

2. Click `Add Policy` in the next page.
3. Enter `NAME`, select the IdP Adapter from the previous stage for `POLICY`. Click `Done` for `FAIL` and `SUCCESS` options. Once finished, click `Done`.

4. Ensure the new policy is enabled, then click `Save` to complete.

#### [Set up Policy Contracts](/docs/mdcore/v5.22.1/configuration/pingfederate-oidc-single-sign-on#set-up-policy-contracts)

1. In homepage, navigate to `AUTHENTICATION` tab. Select `Policies` icon on the left sidebar, then click `Policy Contracts`.

2. Press `Create New Contract` on the next page.
3. In `Contract Info` step, enter `CONTRACT NAME` and click `Next`.

4. In `Contract Attributes` step, navigate to `Extend the Contract`, fill in claims that will be returned to MetaDefender Core, click`Add` to add the claim, and then `Next`.

5. Review all selected options in `Summary` tab, then click `Save` to complete.

#### [Set up Policy Sessions](/docs/mdcore/v5.22.1/configuration/pingfederate-oidc-single-sign-on#set-up-policy-sessions)

1. In homepage, navigate to `AUTHENTICATION` tab and click `Sessions`.

2. In `Sessions` menu, find `OVERRIDES` subtab.
3. Select "MD Core Adapter" for Authentication Source, tick `Enable Sessions`, and click `Add` to include the authentication source.

4. Click `Save` to complete.

#### [Set up Policy Contract Grant Mapping](/docs/mdcore/v5.22.1/configuration/pingfederate-oidc-single-sign-on#set-up-policy-contract-grant-mapping)

1. In homepage, navigate to `AUTHENTICATION` and click `Policy Contract Grant Mapping`.

2. Select the Policy contract in previous stage, then click `Add Mapping`.

3. In `Attribute Sources & User Lookup` step, click `Next`.
4. In `Contract Fulfillment` step, select the appropriate mapping for `Source` and `Value` columns, then click `Next`.

5. Click `Next` in `Issuance Criteria` step.
6. Review all selected options in `Summary` tab, then click `Save` to complete.

#### [Set up IdP Adapter Grant Mapping](/docs/mdcore/v5.22.1/configuration/pingfederate-oidc-single-sign-on#set-up-idp-adapter-grant-mapping)

1. In homepage, navigate to `AUTHENTICATION`, select `OAUTH` in the left side bar, and click `IdP Adapter Grant Mapping`.
2. Under `SOURCE ADAPTER INSTANCE`, select the IdP Adapter that was set up in the previous stage and click `Add Mapping`.

3. Click `Next` in `Attribute Sources & User Lookup` step.
4. In `IdP Adapter Mapping` step, select the appropriate mapping for `Source`, `Value`, and click `Next`.

5. Click `Next` in `Issuance Criteria` step.
6. Review all selected options in `Summary` tab, then click `Save` to complete.

#### [Set up Resource Owner Credentials Grant Mapping](/docs/mdcore/v5.22.1/configuration/pingfederate-oidc-single-sign-on#set-up-resource-owner-credentials-grant-mapping)

1. In homepage, navigate to `AUTHENTICATION`, select `OAUTH` in the left side bar, and click `Resource Owner Credentials Grant Mapping`.
2. Under `SOURCE PASSWORD VALIDATOR INSTANCE`, select the Password Credential Validator that was set up in the previous stage, which is "Simple MDCore PCV", and click `Add Mapping`.

3. Click `Next` in `Attribute Sources & User Lookup` step.
4. In `Contract Fulfillment` step, choose the appropriate mapping for `Source` and `Value`, and then click `Next`.

5. Click `Next` in `Issuance Criteria` step.
6. Review all selected options in `Summary` tab, then click `Save` to complete.

#### [Set up Access Token Management](/docs/mdcore/v5.22.1/configuration/pingfederate-oidc-single-sign-on#set-up-access-token-management)

1. In homepage, navigate to `APPLICATIONS`, and click `Access Token Management`.

2. Click `Create New Instance`.
3. Enter `INSTANCE NAME,` `INSTANCE ID`, and select `JSON Web Tokens` for `TYPE`. Click `Next` to continue.

4. In `Instance Configuration` step, click `Add a new row to 'Symmetric Keys'` under `Symmetric Keys`.

5. Enter `Key ID`, `Key`, and select the correct `Encoding`. Click `Update`.

6. Back to `Instance Configuration` step, click `Add a new row to 'Certificates'` under `Certificates`.

7. Enter `Key ID` and choose `Certificate` from the previous stage. Then click `Update`.

8. Back in `Instance Configuration` step, navigate to `JWS ALGORITHM` and select the appropriate algorithm. Proceed to `ACTIVE SYMMETRIC KEY ID` and `ACTIVE SIGNING CERTIFICATE KEY ID`, then select the key and certificate that were set up in steps 4 and 5 of this stage. Click `Next` when finished.

9. In `Session Validation` step, check all options and click `Next`.

10. In `Access Token Attribute Contract` step, navigate to `Extend the Contract` and add the same claims that have already been set up in the stages: `Policy Contract Grant Mapping`, `IdP Adapter Grant Mapping`, and `Resource Owner Credentials Grant Mapping`. Click `Next`.

11. Click `Next` in `Resource URI`s and `Access Control` steps.
12. Review all selected options in `Summary` tab, then click `Save` to complete.

#### [Set up Access Token Mappings](/docs/mdcore/v5.22.1/configuration/pingfederate-oidc-single-sign-on#set-up-access-token-mappings)

1. In homepage, navigate to `APPLICATIONS` and click on `Access Token Mappings`.

2. In `Access Token Mappings` page, select the Authentication Policy Contract from the previous step to map to `ACCESS TOKEN MANAGER`. Click `Add Mapping`.

3. Click `Next` in `Attribute Sources & User Lookup` step.
4. In `Contract Fulfillment` step, select the appropriate `Source` and `Value`, then click `Next`.

5. Click `Next` in `Issuance Criteria` step.
6. Review all selected options in `Summary` tab, then click `Save`.
7. Return to `Access Token Mappings` page and repeat the steps 2 to 6 for Validator and IdP Adapter.

#### [Set up Scope Management](/docs/mdcore/v5.22.1/configuration/pingfederate-oidc-single-sign-on#set-up-scope-management)

1. In homepage, navigate to `SYSTEM` and click `OAuth Scopes`.

2. Under `Scope Management`, at `Common Scopes` tab, click `Add Common Scope`.

3. Due to MetaDefender Core requires **profile** scope, fill the scope name and click `Save`.

4. Repeat the above step to add `username` scope.

5. Click `Save` to complete.

#### [Setup Authorization Server Settings](/docs/mdcore/v5.22.1/configuration/pingfederate-oidc-single-sign-on#setup-authorization-server-settings)

1. In homepage, navigate to `SYSTEM` and click `Authorization Server Settings`.

2. Navigate to `OAuth Administrative Web Services Settings` and select the password credential validator that was set up in previous stage for `PASSWORD CREDENTIAL VALIDATOR`.
3. Navigate to `Persistent Grant Management API`.
4. Select the access token manager and scope that were set up in the previous stage for `ACCESS TOKEN MANAGER` and `REQUIRED SCOPE`, respectively.

5. Click `Save` to complete.

#### [Set up OpenID Connect Policy Management](/docs/mdcore/v5.22.1/configuration/pingfederate-oidc-single-sign-on#set-up-openid-connect-policy-management)

1. In homepage, navigate to `APPLICATIONS` and click `OpenID Connect Policy Management`.

2. Click `Add Policy` in the next page.
3. In `Manage Policy` step, enter `POLICY ID`, `NAME` and select the manager that was set up in previous stage for `ACCESS TOKEN MANAGER`. Click `Next` on done.

Info

Store the value assigned to `POLICY ID` as *policy_id*. It will be used later on fetching metadata in MetaDefender Core.

5. In `Attribute Contract` step, navigate to `Extend the Contract`, add the scopes requested by MetaDefender Core (i.e. username), and click `Next`.

Info

PingFederate, by default, lists all extended contracts. Within the scope of the instructions, only `profile` contract is required, all the remaining ones must be deleted.

6. In `Attribute Scopes` step, match the scope with its attributes and click `Next`.

7. Click `Next` in `Attribute Sources & User Lookup` step.
8. In `Contract Fulfillment` step, select the appropriate `Source` and `Value`, and click `Next`.

9. Click `Next` in `Issuance Criteria` step.
10. Review all selected options in `Summary` tab, then click `Save`.

#### [Add OAuth client](/docs/mdcore/v5.22.1/configuration/pingfederate-oidc-single-sign-on#add-oauth-client)

1. In homepage, navigate to `APPLICATIONS` and click `OAuth Clients`.

2. Click `Add Client` in the next page.
3. Enter `CLIENT ID`and store to *client_id*.
4. Enter `NAME`.
5. Choose `CLIENT SECRET` for `CLIENT AUTHENTICATION`.
6. Navigate to `CLIENT SECRET`, check `CHANGE SECRET` box, click `Generate Secret`, and store the generated string as *client_secret*.

Info

*client_id* and *client_secret* will be used later on setting up MetaDefender Core.

7. Navigate to `REDIRECT URIS`, fill in a temporary Redirection URI, and click `Add`.

Warning

A temporary redirection URI is used at this step to complete configuration in PingFederate. We will return to update this setting with the correct URI from MetaDefender Core later.

8. Navigate to `ALLOWED GRANT TYPES`, and tick `Authorization Code`.
9. Navigate to `DEFAULT ACCESS TOKEN MANAGER`, and select Access Token Manager that was set up previously.

10. Navigate to `OPENID CONNECT`, under `Policy`, select OpenID connect policy that was set up previously.

11. Click `Save` to complete.

### [Set up MetaDefender Core](/docs/mdcore/v5.22.1/configuration/pingfederate-oidc-single-sign-on#set-up-metadefender-core)

#### [Install PingFederate certificate](/docs/mdcore/v5.22.1/configuration/pingfederate-oidc-single-sign-on#install-pingfederate-certificate)

1. In homepage, go to `SECURITY` and click `SSL Server Certificates`.

2. Click `Create New` to generate a new certificate.

3. Complete the information for the new certificate, click `Next` and `Save`.

Info

`COMMON NAME` must refer to the domain or IP address hosting PingFederate.

4. Activate the new certificate.

Warning

Activating the certificate will end all current sessions, and users will need to sign in again into PingFederate using the domain or IP specified in the certificate.

5. Select the certificate and select `Export`.

6. Retain the default settings and click `Next`.
7. Click `Export` to download the certificate.

8. Install the certificate on the server running MetaDefender Core.
9. Restart MetaDefender Core for the changes to take effect.

#### [Configure OIDC in MetaDefender Core](/docs/mdcore/v5.22.1/configuration/pingfederate-oidc-single-sign-on#configure-oidc-in-metadefender-core)

1. Sign in to MetaDefender Core.
2. In the dashboard, click on `User Management` in the left sidebar.
3. On `User Management` page, select `Directories` tab and click `Add Directory` in the top right corner.

4. In `Add Directory` page, select OIDC as `Directory type`, and enter a name for the new directory, such as MDCore-OIDC.
5. Click `Fetch URL`.

6. Enter PingFederate metadata URL and click `OK`.

Info

PingFederate metadata URL is in format of `<host>:<port>/.well-known/openid-configuration?policy_id=<policy_id>` , in which:

- `host` and `port` are the host/IP and port of the machine hosting PingFederate. The default port is 9031.
- `policy_id` is *policy_id* that is set to `POLICY_ID` in the stage of **Setup OpenID Connect Policy Management**.

7. Under `Service Provider`, paste *client_id* and *client_secret* to boxes under `Client ID` and `Client secret` respectively.
8. Fill in `Host or IP` with the host or IP where MetaDefender Core is hosted, such as <http://127.0.0.1:8008> for this example.

9. Copy `Login URL` and store it as *login_url*.

Info

*login_url* is used to update Redirection URI setting in PingFederate in the next stage.

10. Fill in `User Identified by` with **${username}**.
11. Select the default role and choose the appropriate role for the login user.
12. Click `Add` to complete.
13. In `User Management` page, toggle the new directory, MDCORE-OIDC in this example. A dialog box will appear to confirm the action. Once `Enable` is clicked, all sessions will expire immediately.

### [Complete configuration in PingFederate](/docs/mdcore/v5.22.1/configuration/pingfederate-oidc-single-sign-on#complete-configuration-in-pingfederate)

1. Back to PingFederate, in `OAuth`, navigate to `Clients` in the sidebar.
2. In `APPLICATIONS` tab, navigate to `Redirection URIs`, click `Edit`, modify the URI with *login_url* copied from MetaDefender Core.
3. Click `Update` and `Save`.

### [Test the integration](/docs/mdcore/v5.22.1/configuration/pingfederate-oidc-single-sign-on#test-the-integration)

1. On the home screen of MetaDefender Core, click `Login`; the user is redirected to PingFederate Sign-on page.

2. Sign in using the account registered with PingFederate.
3. If everything goes well, MetaDefender Core dashboard is displayed with the user identity in the top right corner.

4. Otherwise, access backup login page at `<mdcore-host>#/public/backuplogin` for trouble shooting.
