<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/configuration/adfs-saml-single-sign-on -->

# Configure SAML SSO

ADFS requires MetaDefender Core to enable HTTPS for connections. Please follow these [steps](/docs/mdcore/v5.22.0/configuration/enabling-https) to first enable HTTPS on MetaDefender Core.

### [Add Relying Party Trust for ADFS](/docs/mdcore/v5.22.0/configuration/adfs-saml-single-sign-on#add-relying-party-trust-for-adfs)

1. In the top right corner of `Server Manager`, click `Tools` and select `AD FS Management` from the drop-down list.

2. In `AD FS` window, right click on `Relying Party Trusts` and select `Add Relying Party Trust` from the drop-down menu.

3. In `Add Relying Party Trust Wizard,` select `Claims aware` on the `Welcome` page and click `Start`.
4. On `Select Data Source` page, choose `Enter data about the relying party manually` and click `Next`.
5. On `Specify Display Name` page, provide a descriptive name for your relying party, e.g. MDCORE_SAML, and click `Next`.

6. Click `Next` on `Configure Certificate` page.
7. On `Configure URL` page, check the box for `Enable support for the SAML 2.0 WebSSO protocol` and set a placeholder, using <https://myplaceholder> as an example, for `Relying party SAML 2.0 SSO service URL`.

8. On `Configure Identifiers` page, set MDCORE_SAML as `Relying party trust identifier`, then click `Add` and `Next`.

9. On `Choose Access Control Policy` page, select `Permit everyone` and click `Next`.
10. Click `Next` on `Ready to Add Trust` page to save your information.
11. If everything goes well, `Finish` page will be displayed for you to click `Close`.

### [Configure claims Issuance Policy for ADFS](/docs/mdcore/v5.22.0/configuration/adfs-saml-single-sign-on#configure-claims-issuance-policy-for-adfs)

1. In `Relying Party Trusts` table of `AD FS` window, navigate to the item MDCORE_SAML that was added in the previous step, right-click on it, and select `Edit Claim Issuance Policy...` from the drop-down menu.

2. Click `Add Rule`.
3. Select `Send LDAP Attributes as Claims` for `Claim rule template`, and click `Next`.

4. Enter a name for `Claim rule name`, for instance, display_name. Select `Active Directory` for `Attribute Store`. Under `LDAP Attribute` column, choose `Display-Name` from the drop-down list, type given_name for the `Outgoing Claim Type` column, and click `Finish`.

5. Click `Add Rule` once more. At `Choose Rule Type` option, select `Transform an Incoming Claim` for `Claim rule template` and click `Next`.

6. Enter name_id for the `Claim rule name` and given_name from step 4 for `Incoming claim type`. Select `Name ID` for `Outgoing claim type` and `Transient Identifier` for `Outgoing Name ID format` from the respective drop-down lists. Finally, check `Pass through all claim values` and click `Finish`.

7. Click `Apply` on the next page and `OK` to close the wizard.

### [Create a SAML directory in MetaDefender Core](/docs/mdcore/v5.22.0/configuration/adfs-saml-single-sign-on#create-a-saml-directory-in-metadefender-core)

1. Sign in to MetaDefender Core.
2. On the dashboard, click `User Management` in the left sidebar.
3. On `User Management` page, select `Directories` tab and click `Add Directory` in the top right corner .

4. On `Add Directory` page, choose SAML as `Directory type`.
5. Enter the name of the new directory, such as ADFS_SAML.
6. In `Service Provider` section, check `Use custom entity ID` and type MDCORE_SAML in `Custom entity ID` text box.

7. In `Service Provider` section, fill in `Host or IP` filed with the address where MetaDefender Core is hosted, using <https://localhost:8008> as an example.
8. Copy `Login URL`.

### [Modify Replying Party Trust on ADFS](/docs/mdcore/v5.22.0/configuration/adfs-saml-single-sign-on#modify-replying-party-trust-on-adfs)

1. Access `AD FS Management` tool from `Server Manager`, select `Relying Party Trusts`, right click on the item MDCORE_SAML, and choose `Properties`.

2. Navigate to `Endpoints` tab, select <https://myplaceholder>, and click `Edit`.

3. Select `POST` from the drop-down list for `Binding`. Check `Set the trusted URL as default`, then paste the `Login URL` from MetaDefender Core into `Trusted URL` and click `OK`.

4. Click `Apply` and `OK` to complete the Relying Party Trust modification.

### [Complete configuration in MetaDefender Core](/docs/mdcore/v5.22.0/configuration/adfs-saml-single-sign-on#complete-configuration-in-metadefender-core)

1. Access `AD FS Management` tool from `Server Manager`, expand `AD FS` --> `Service` --> `Endpoints`. In `Endpoints` panel, navigate to `Metadata` section and copy the URL path of type `Federation Metadata`.

2. Build the complete URL to the metadata endpoint by appending the path from step 1 to the qualified domain name of ADFS.

HtmlCopyhttps://<adfs_fully_qualified_domain_name>/<metadata_endpoint_path>

- For example:

HtmlCopyhttps://win-tst/FederationMetadata/2007-06/FederationMetadata.xml

3. Switch back to MetaDefender Core. Under the section `Identity Provider`, click `Fetch URL` and paste the link above into the box under `Fetch URL`, then click `OK` to ensure MetaDefender Core can set ADFS as its IDP.
4. Under the section `Service Provider`, fill in the user identity under `User identified by` with the configured values of `Outgoing Claim Type`, e.g. ${given_name}.
5. Select the appropriate role for the user under `User Role`.
6. Click `Add` to complete the settings.

7. On `User Management` screen, toggle the new directory `ADFS_SAML` in this example. A dialog box appears to confirm the action. Once `Enable` is clicked, all sessions are immediately expired, and ADFS is used to authenticate the user.

### [Test the integration](/docs/mdcore/v5.22.0/configuration/adfs-saml-single-sign-on#test-the-integration)

1. Click `Login` from the home screen of MetaDefender Core; the user is redirected to ADFS page.

2. Sign in with the account created in the system domain.
3. If everything goes right, the MetaDefender Core dashboard is displayed with the user identity set in the top right corner.

4. Otherwise, access backup login page at `<mdcore-host>#/public/backuplogin` for trouble shooting.
