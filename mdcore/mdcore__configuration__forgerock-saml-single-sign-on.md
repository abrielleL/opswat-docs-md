<!-- source: https://www.opswat.com/docs/mdcore/configuration/forgerock-saml-single-sign-on -->

# Configure SAML SSO

The integration is demonstrated using ForgeRock version 7.2.0.

#### [Configure Identity Provider in ForgeRock](/docs/mdcore/configuration/forgerock-saml-single-sign-on#configure-identity-provider-in-forgerock)

1. Access ForgeRock console.
2. On `Realms` page, select `Top Level Realm` located in the upper left corner.
3. Go to `Applications` in the sidebar, expand `Federation`, choose `Circles of Trust`, and press `Add Circle of Trust`.

4. Input the name, 'my_circle_of_trust' for instance, then select `Create` and `Save Changes`.

5. Select `Entity Providers` from `Federation` in the side bar, select `Add Entity Provider`, and pick `Hosted`.

6. Input 'mdcore' for `Entity ID`, 'mdcoreidp' for `Identity Provider Meta Alias`, 'mdcoresp' for `Service Provider Meta Alias`, and 'my_circle_of_trust' for `Circles of Trust`, then click `Create`.

Info

The value of `Entity ID`, 'mdcore' in this case, will later be used to configure `Custom entity ID` in MetaDefender Core.

#### [Create SAML directory in MetaDefender Core](/docs/mdcore/configuration/forgerock-saml-single-sign-on#create-saml-directory-in-metadefender-core)

1. Access MetaDefender Core console.
2. On the dashboard, select `User Management` from the sidebar.
3. On `User Management` page, choose `Directories` tab and then click on `Add Directory` in the upper right corner.
4. On `Add Directory` page, select `SAML` for directory type.
5. Input the name of the new folder, such as 'FORGEROCK_SAML'.
6. In `Service Provider` area, toggle `Use Custom Entity ID` option and type 'mdcore' in `Custom entity ID` box.
7. Fill in `Host or IP` with the address of the machine where MetaDefender Core is located, using '<http://localhost:8008'> as an example.
8. Click the copy button beside `Login URL`.

Info

The copied login URL will be used subsequently in `Location` setting of ForgeRock.

Warning

The setup in MetaDefender Core is incomplete, please refrain from clicking outside of `Add Directory` screen.

#### [Configure Service Provider in ForgeRock](/docs/mdcore/configuration/forgerock-saml-single-sign-on#configure-service-provider-in-forgerock)

1. In the ForgeRock console, switch to `SP` for the entity provider 'mdcore'.

2. Click on `Services` tab.

3. Go to `Assertion Consumer Service` area, choose HTTP-POST binding entry, and tap the edit icon located in the top right.

4. Input login URL from MetaDefender Core into `Location`, toggle `isDefault` switch in the upper left, and press `Update`.

5. Remove HTTP-Artifact and PAOS bindings, then press `Save Changes`.

6. Select `Assertion Processing` tab, navigate to `Attribute Map`, enter 'given_name' and 'givenName' as `Key` and `Value`, accordingly.

7. Press `Add` and `Save Changes`.

#### [Complete configuration in MetaDefender Core](/docs/mdcore/configuration/forgerock-saml-single-sign-on#complete-configuration-in-metadefender-core)

1. Go back to MetaDfender Core, in `Add Directory` page, navigate to `Identity Provider` section and click on `Fetch URL`.
2. Enter the SAML Metadata URL from ForgeRock into the field beneath `Fetch URL`, click `OK` and wait a moment for MetaDefender Core to assign ForgeRock as its IDP.

Info

The structure of the metadata URL is as outlined below:

`http://<forgerock`*server>:<port>/openam/saml2/jsp/exportmetadata.jsp?entityid=<entity*`id>`

In which, `forgerock_server` and `port` correspond to the host and port of the machine hosting ForgeRock server; `entity_id` refers to the value of `Entity ID` configured in ForgeRock. In this guide, ForgeRock is located at 'myforgerock.com:8080' and the `Entity ID` is 'mdcore'; thus, the metadata URL becomes

`http://myforgerock.com:8080/openam/saml2/jsp/exportmetadata.jsp?entityid=mdcore`

3. Populate `User identified by` field with '${given_name}', as set up in ForgeRock during the earlier step.
4. Choose the appropriate role for the user in `User Role` and click `Add` to finish the process.

5. On `User Management` screen, switch on the new directory, 'FORGEROCK_SAML' in this case.

6. A confirmation dialog box will pop up to verify the action. Upon clicking `Enable`, all sessions will be terminated instantly, and ForgeRock will be utilized for user authentication.

#### [Test the integration](/docs/mdcore/configuration/forgerock-saml-single-sign-on#test-the-integration)

1. On the home screen of MetaDefender Core, click `Login`; the user is redirected to ForgeRock Sign-in page.

2. Sign in with your ForgeRock account.
3. If all proceeds smoothly, MetaDefender Core dashboard will appear with the user's identity in the upper right corner.

4. Otherwise, visit backup login page at `<mdcore-host>#/public/backuplogin` for trouble shooting.
