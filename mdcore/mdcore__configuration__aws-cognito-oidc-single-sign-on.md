<!-- source: https://www.opswat.com/docs/mdcore/configuration/aws-cognito-oidc-single-sign-on -->

# Configure OIDC SSO

### [Create OIDC directory in MetaDefender Core](/docs/mdcore/configuration/aws-cognito-oidc-single-sign-on#create-oidc-directory-in-metadefender-core)

1. Sign in to MetaDefender Core.
2. In the dashboard, click on `User Management` in the left sidebar.
3. In `User Management` page, select `Directories` tab and click `Add Directory` in the top right corner.

4. In `Add Directory` page, select OIDC as `Directory type`, and enter a name for the new directory, such as MDCore-OIDC.
5. Enter `Host or IP` where MetaDefender Core is hosted, for this example use [http://localhost:8008](http://localhost:8008/).
6. Copy the string generated under `Login URL` and store it as *reply_uri*.

### [Create Amazon Cognito user pool](/docs/mdcore/configuration/aws-cognito-oidc-single-sign-on#create-amazon-cognito-user-pool)

1. Access <https://aws.amazon.com/cognito/v2/home> and sign in with your account.
2. On the main page, click `Create user pool`.

3. In `Step 1 - Configure sign-in experience`, select `Cognito user pool` for `Provider types`.

4. Tick `User name`, `Email`, and `Allow users to sign in with a preferred user name`, then click `Next`.

5. In `Step 2 - Configure security requirements`, select `No MFA` for `MFA enforcement`, leave all others as default , and click `Next`.

6. In `Step 3 - Configure sign-up experience`, navigate to `Required attributes` and add additional attributes: given_name, middle_name , and family_name. Click `Next`.

7. In `Step 4 - Configure message delivery`, choose `Send email with Cognito` and click `Next`.

8. In `Step 5 - Integrate your app`, enter the user pool name and tick `Use the Cognito Hosted UI`.

9. Enter your domain to `Cognito domain`.

10. Under `Initial app client` section, select `Public client` for `App type`, enter `App client name`, and select `Generate a client secret` for `Client secret`.

11. Under `Allowed callback URLs` section, fill in `URL` box with the value of *reply_uri*.

12. Expand `Advanced app client settings`, then stick to ALLOW_ADMIN_USER_PASSWORD_AUTH and ALLOW_USER_PASSWORD_AUTH for `Authentication flows`.

13. Navigate to `OpenID Connect scopes` and add `Profile` scope.

14. Click `Next` in the final review page and click `Create user pool`.

### [Create Amazon Cognito user](/docs/mdcore/configuration/aws-cognito-oidc-single-sign-on#create-amazon-cognito-user)

1. In Amazon Cognito, click `User Pools` in the left sidebar and select the user pool that has been created.
2. In `Users` tab, click `Create User`.

3. Enter the user name, and optional email address; stick to `Set a password`, and enter your temporary password. Click `Create User` to complete.

### [Download and modify ODIC metadata](/docs/mdcore/configuration/aws-cognito-oidc-single-sign-on#download-and-modify-odic-metadata)

1. Start your favorite web browser and enter a URL in the following format: `https://cognito-idp.{region_where user_pool_is_created}.amazonaws.com/{user_pool_id}/.well-known/openid-configuration`, where `user_pool_id` can be found in `User pool overview`.

2. Save the responded content to a file on disk.
3. Open the file in your favorite editor.
4. Add the following content to the beginning of the file, right after the first open brace.

JsonCopy"claims_supported": ["middle_name", "given_name", "family_name"],

5. Save the file.

Info

`claims_supported` includes items that are selected for `Required Attributes` at step 6 of [Create Amazon Cognito user pool](/docs/mdcore/configuration/aws-cognito-oidc-single-sign-on#create-amazon-cognito-user-pool) stage.

### [Complete the configurations](/docs/mdcore/configuration/aws-cognito-oidc-single-sign-on#complete-the-configurations)

1. In Amazon Cognito, click on `User Pools` in the left sidebar and select the user pool that has been created.
2. In `App Integration` tab, navigate to `App Client list` and select the app client that has been created.

3. Copy `Client ID` and `Client Secret`.

4. Switch to MetaDefender Core, under `Service Provider`, paste `Client ID` and `Client Secret` from the previous step into their respective fields.

5. In `Identity Provider`, click `Submit JSON` button and upload the file that was modified in the previous stage. Wait a moment for MetaDefender Core to set Amazon Cognito as its IdP.

6. Enter `User identified by` with ${given_name} and select the appropriate role.

7. Click `Add` to complete.
8. In `User Management`, toggle the new directory. A dialog box will appear to confirm the action. Once `Enable` is clicked, all sessions will be expired immediately.

### [Test the integration](/docs/mdcore/configuration/aws-cognito-oidc-single-sign-on#test-the-integration)

1. On the home screen of MetaDefender Core, click `Login`; the user is redirected to Amazon Cognito page.

2. Change the password, enter other required fields, and click `Send`.

3. If everything goes well, MetaDefender Core dashboard is displayed with the user identity in the top right corner.

4. Otherwise, access backup login page at `<mdcore-host>#/public/backuplogin` for trouble shooting.
