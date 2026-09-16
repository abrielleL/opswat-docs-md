<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/configuration/entra-saml-single-sign-on -->

# Configure SAML SSO

Microsoft Entra ID requires MetaDefender Core to enable HTTPS for connections. Please follow these [steps](/docs/mdcore/v5.22.0/configuration/enabling-https) to first enable HTTPS on MetaDefender Core.

### [Register a new application in Azure](/docs/mdcore/v5.22.0/configuration/entra-saml-single-sign-on#register-a-new-application-in-azure)

1. Access [Azure portal](https://portal.azure.com/) and sign in.
2. On the homepage, select `Microsoft Entra ID` under `Azure services`.

3. Select `Enterprise applications` in the left sidebar.

4. On `All applications` page, click `New application`.

5. On `Browse Azure AD Gallery` page, search for "Microsoft Entra SAML Toolkit" and click on `Microsoft Entra SAML Toolkit` in the result panel.

6. Fill in `Name` field with MDCore-SAML**,** for example, and click `Create` in the right sidebar.

7. Navigate to `Single sign-on` on the left sidebar and click `SAML`.

8. Go to `SAML Certificates` section, click the copy button at the far right of `App Federation Metadata Url` and store as *metadata_uri.*

9. Navigate to `Users and groups` in the left sidebar, click `Add user/group`.

10. On `Add Assignment` screen, click `Non Selected` and add users who are allowed to log in to the app, then click `Select` in the right panel.

11. Finally, click `Assign` to complete.

### [Create SAML directory in MetaDefender Core](/docs/mdcore/v5.22.0/configuration/entra-saml-single-sign-on#create-saml-directory-in-metadefender-core)

1. Sign in to MetaDefender Core management console.
2. On the dashboard, click `User Management` in the left sidebar.
3. In `User Management` page, select `Directories` tab and click on `Add directory` in the top right corner.

4. In `Add Directory` page, choose SAML in `Directory type`, enter a name for the new directory, such as MDCore-SAML and click `Fetch URL`.

5. Paste the URI stored in *metadata_uri* into the box under `Fetch URL`, then click `OK` and wait a moment for MetaDefender Core to set Microsoft Entra ID as its IDP.

6. In `Service Provider` section, fill in `Host or IP` with the address where MetaDefender Core is hosted, for example <https://127.0.0.1:8008>.
7. Copy the `Login URL` and store in *reply_uri* for the later steps.

### [Complete configuration in Entra ID](/docs/mdcore/v5.22.0/configuration/entra-saml-single-sign-on#complete-configuration-in-entra-id)

1. Switch back to Microsoft Entra ID, on `SAML-based Sign-on` page, navigate to `Basic SAML Configuration` and click `Edit` in the top right corner.

2. Navigate to `Identifier (Entity ID)` in the right sidebar, click `Add identifier`, then enter a unique ID to identify MDCore, such as MDCore-SAML. Store the identifier to *identifier.*
3. Navigate to `Reply URL(Assertion Consumer Service URL)`, click `Add reply URL` and fill in the URI with the value stored in *reply_uri* and click `Save`.

4. Navigate to `Attributes & Claims`, then click `Edit`.

5. In `Attributes & Claims` page, go to `Additional claims`, and click on any item under `Claim name` to change its name.

6. Change value of `Name` field, leave `Namespace` empty and click `Save` to complete. In this instruction, the claim name is changed to given_name, which will be used later to identify the logged-in user on MetaDefender Core.

Info

If the names of attributes and claims provided by Microsoft Entra ID are sufficient, the customers are recommended for direct use in identifying the logged-in user in MetaDefender Core.

### [Complete configuration in MetaDefender Core](/docs/mdcore/v5.22.0/configuration/entra-saml-single-sign-on#complete-configuration-in-metadefender-core)

1. Switch back to MetaDefender Core screen. Under `Service Provider`, go to `Use custom entity ID` and fill in it with value stored in *identifier*, MDCore-SAML in this example.
2. Fill in `User identified by` with ${given_name}.

Info

If the namespace is not removed from the claim name in step 6 of the previous section, the full claim name including the namespace must be used here to build user identity.

For example, if the claim of <http://schemas.xmlsoap.org/ws/2005/05/identitity/clams/given_name> is added to Microsoft Entra ID, then ${<http://schemas.xmlsoap.org/ws/2005/05/identitity/clams/given_name>} should be used by MetaDefender Core to build user identity.

3. Select appropriate role for the user under `User Role`.
4. Click `Add` to complete the settings.

5. In `User Management` screen of MetaDefender Core, toggle the new directory named MDCORE-SAML. A dialog box appears to confirm the action. Once `Enable` is clicked, all sessions are expired immediately.

### [Test the integration](/docs/mdcore/v5.22.0/configuration/entra-saml-single-sign-on#test-the-integration)

1. At the home screen of MetaDefender Core, click `Login`; the user is redirected to Microsoft Entra ID sign-in page.

2. Sign in using the account registered with Microsoft Entra ID.
3. If everything goes correctly, MetaDefender Core dashboard is displayed with user's identity shown in the top right corner.
4. Otherwise, access backup login page at `<mdcore-host>#/public/backuplogin` for trouble shooting.

### [Setup pseudo IdP-initiated SSO](/docs/mdcore/v5.22.0/configuration/entra-saml-single-sign-on#setup-pseudo-idp-initiated-sso)

Info

Microsoft Entra ID does not support IdP-initiated SSO in the same way as other Identity Providers. It actually accesses the login page of its SP and does initiate Single Sign-in from there; so basically, it is SP-initiated.

1. Sign in to Azure management page.
2. Navigate to `Azure services` section, click on `Microsoft Entra ID`.

3. In the left sidebar, click on `Enterprise applications`.

4. Select `Azure AD SAML Toolkit` from the list of enterprise applications.

5. Choose `Single sign-on` in the left sidebar, go to `Basic SAML Configuration` section, and click `Edit` at the top right of the section.

6. In `Basic SAML Configuration` right sidebar, enter Core login URL in the field under `Sign on URL`.

7. Click `Save` to complete.

### [Test IdP-initiated SSO](/docs/mdcore/v5.22.0/configuration/entra-saml-single-sign-on#test-idp-initiated-sso)

1. Sign in to Azure management page.
2. Navigate to `Azure services` section, and select `Microsoft Entra ID`.
3. In the left sidebar, click on `Enterprise applications`.
4. Choose `Azure AD SAML Toolkit` from the list of enterprise applications.
5. Go to `Properties` tab.

6. Copy the URL next to `User access URL`.
7. Paste the copied URL into your browser and sign in.

8. If everything goes well, MetaDefender Core dashboard will appear with the user identity displayed in the top right corner.

9. Otherwise, access backup login page at `<mdcore-host>#/public/backuplogin` for trouble shooting.
