<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/configuration/pingfederate-saml-single-sign-on -->

# Configure SAML SSO

### [Set up PingFederate](/docs/mdcore/v5.22.0/configuration/pingfederate-saml-single-sign-on#set-up-pingfederate)

#### [Configurate PingFederate](/docs/mdcore/v5.22.0/configuration/pingfederate-saml-single-sign-on#configurate-pingfederate)

1. Sign in to PingFederate console at `https://service-ip:service-port`, where `service-ip` and `service-port` refer to the IP address and port of the machine hosting PingFederate server.
2. In homepage, navigate to `SYSTEM` tab and select `Server` from the left sidebar.
3. Select `Protocol Settings`, enter `Base URL`, `SAML 2.0 ENTITY ID,` and `SAML 1.X ISSUER/AUDIENCE`, then click `Save` to complete.

#### [Set up simple Password Credential Validators](/docs/mdcore/v5.22.0/configuration/pingfederate-saml-single-sign-on#set-up-simple-password-credential-validators)

1. In homepage, navigate to `SYSTEM` tab and click on `Password Credential Validators`.

2. Click `Create New Instance`.
3. Enter `INSTANCE NAME` and `INSTANCE ID`, select `Simple Username Password Credential Validator` for `TYPE`, and click `Next`.

4. In `Create Credential Validator Instance` page, click `Add a new row to 'Users'.`

5. Enter `Username`, `Password`, and `Confirm Password`, then click `Update` and `Next`.

6. Review all selected options in `Summary` tab, and click `Save`.

#### [Set up a simple IdP Adapter](/docs/mdcore/v5.22.0/configuration/pingfederate-saml-single-sign-on#set-up-a-simple-idp-adapter)

1. In homepage, navigate to `AUTHENTICATION` tab and click on `IdP Adapters`.

2. Click `Create New Instance`.
3. Enter `INSTANCE NAME`, `INSTANCE ID,` and select `HTML Form IdP Adapter` for `TYPE` . Click `Next`.

4. Click `Add a new row to 'Credential Validators'`.

5. Select the Password Credential Validator created in the previous stage, that is "Simple MDCore PCV", then click `Update` and `Next`.

6. Click `Next` on `Extended Contract` tab.
7. In `Adapter Attributes` tab, toggle `username` attribute under `Pseudonym` column, and click `Next`.

8. Click `Next` on `Adapter Contract Mapping` tab.
9. Review all selected options in `Summary` tab and click `Save` to complete.

#### [Set up Signing, Decryption Keys and Certificates](/docs/mdcore/v5.22.0/configuration/pingfederate-saml-single-sign-on#set-up-signing-decryption-keys-and-certificates)

1. In homepage, navigate to `SECURITY` tab and select `Signing & Decryption Keys & Certificates`.

2. Click `Create New`.
3. Enter `COMMON NAME`, `ORGANIZATION`, and `COUNTRY`, along with any other necessary information, then click `Next`.

4. Review all selected options in `Summary` tab and click `Save` to complete.

#### [Set up Service Provider connections](/docs/mdcore/v5.22.0/configuration/pingfederate-saml-single-sign-on#set-up-service-provider-connections)

1. In homepage, go to `APPLICATIONS` tab and choose `SP Connections`.

2. Select `Create Connection`.
3. Select `DO NOT USE A TEMPLATE FOR THIS CONNECTION` and then click `Next`.
4. In `Connection Type` phase, toggle `BROWSER SSO PROFILES` and choose `SAML 2.0` for `PROTOCOL`. Press `Next`.

5. In `Connection Options` phrase, select `BROWSER SSO` and then click `Next`.

6. In `Import Metadata` phase, select `NONE` for `METADATA` subtab and press `Next`.

7. In `General Info` section, enter `PARTNER'S ENTITY ID (CONNECTION ID)` and `CONNECTION NAME`, then click `Next`.

Info

`PARTNER'S ENTITY ID`, 'md_core' in this case, will later be used to configure `Custom entity ID` in MetaDefender Core.

8. In `Browser SSO` phrase, select `Configure Browser SSO`.

9. In `SAML Profiles` phrase, check `SP-INITIATED SSO` under `Single Sign-On (SSO) Profiles` column. Press `Next` once you are finished.

10. Select `Next` in `Assertion Lifetime` phase.
11. In `Assertion Creation` phase, select `Configure Assertion Creation`.

12. In `Identity Mapping` phrase, choose `STANDARD` and press `Next`.

13. In `Attribute Contract` phase, navigate to `Extend the Contract`, complete the contract needed by MetaDefender Core, using 'username' as a sample. Select the basic format for `Attribute Name Format`, then click `Add` followed by `Next`.

14. In `Authentication Source Mapping` phase, select `Map New Adapter Instance`.

15. In `Adapter Instance` phase, choose the appropriate IdP Adapter for `ADAPTER INSTANCE` and then click `Next`.

16. In `Mapping Method` phase, select `USE ONLY THE ADAPTER CONTRACT VALUES IN THE SAML ASSERTION`, then press `Next`.

17. In `Attribute Contract Fulfillment` phase, choose 'Adapter' for `Source` column and 'username' for `Value` column, then click `Next`.

18. Press `Next` on `Issuance Criteria` phrase.
19. Examine all chosen options in `Summary`, then select `Done` and `Next`.
20. Return to `Assertion Creation` phrase, examine all chosen options in `Summary`, and then click `Done` and `Next`.
21. In `Protocol Settings` phase, select `Configure Protocol Settings`.

22. Check the box under `Default` column, enter **0** in `Index` column, select POST for `Binding`, and input the address of the machine hosting MetaDefender Core in `Endpoint URL` column, then click `Add` and `Next`.

23. In `Acceptable SAML Bindings` phase, select only 'POST' and 'REDIRECT' choices, then click `Next`.

24. Press `Next` on the phrases for `Signature Policy` and `Encryption Policy`.
25. Examine all chosen options in `Summary` and click `Done`.
26. Select `Next` on `Browser SSO`.
27. Examine all chosen options in `Summary`, then select `Done` and `Next`.
28. In `Credentials` phase, select `Configure Credentials`.

29. In `Digital Signature Settings` phase, go to `SIGNING CERTIFICATE`, choose the signing signature configured in the earlier step, activate the option `INCLUDE THE CERTIFICATE IN THE SIGNATURE <KEYINFO> ELEMENT`, and then click `Next`.

30. Examine all chosen options in `Summary` phrase, then press `Done`.
31. Return to `Credentials` tab and select `Next`.
32. Examine all chosen options in `Activation & Summary` phrase, verify that the connection is active, and then click `Save` to finish.

#### [Export Identity Provider metadata](/docs/mdcore/v5.22.0/configuration/pingfederate-saml-single-sign-on#export-identity-provider-metadata)

1. Go to `APPLICATIONS` and click on `SP Connections` on the left sidebar.
2. Go to the connection established in the prior step, click `Select Action` link located in `Action` column, and choose `Export Metadata`.

3. Choose the prior signing certificate, then press `Next`.

4. Examine all chosen options in `Summary` and select `Export`.

5. Save the exported file as 'metadata.xml', and then press `Done`.

Info

The 'metadata.xml' file will be used in the upcoming phase to set up `Identity Provider` in MetaDefender Core.

#### [Configure SAML in MetaDefender Core](/docs/mdcore/v5.22.0/configuration/pingfederate-saml-single-sign-on#configure-saml-in-metadefender-core)

1. Sign in to MetaDefender Core.
2. In the dashboard, click on `User Management` in the left sidebar.
3. On `User Management` page, select `Directories` tab and click `Add Directory` in the top right corner.

4. In `Add Directory` page, select OIDC as `Directory type`, and enter a name for the new directory, such as MDCORE-SAML.
5. Click `Submit JSON` and upload the 'metadata.xml' file exported in the earlier stage.

6. Navigate to `Service Provider`, toggle `Use custom entity ID` and fill in `Custom entity ID` with the partner's entity ID configured in PingFederate. That is 'md_core' for this case.
7. Enter value or `Host or IP`, click `Copy` and save it in *redirect_url*.

Info

*redirect_url* will serve to establish the value for `Endpoint URL` in the final configuration phase in PingFederate.

8. Establish `User Identified by` using ${username}.
9. Choose `Default role` and select the appropriate role for the logged-in user.
10. Press `Add` when finished.

11. In `User Management` page, toggle the new directory, MDCORE-SAML, in this instance. A confirmation dialog box will pop up to verify the action. After clicking `Enable`, all sessions will end instantly.

### [Complete configuration in PingFederate](/docs/mdcore/v5.22.0/configuration/pingfederate-saml-single-sign-on#complete-configuration-in-pingfederate)

1. Access the PingFederate management console.
2. Go to `APPLICATION` and choose `SP Connections` from the left sidebar.
3. In `Signature Policy`, set `Always Sign Assertion` to 'true'.

4. Go to `Assertion Consumer Service URL` and select the link next to `Endpoint`.

5. Click `Edit`.

6. Modify the URL located below `Endpoint URL` to the value found in *redirect_url*, then click `Update` and `Save`.

### [Test the integration](/docs/mdcore/v5.22.0/configuration/pingfederate-saml-single-sign-on#test-the-integration)

1. On the home screen of MetaDefender Core, click `Login`; the user is redirected to PingFederate Sign-on page.

2. Sign in using the account registered with PingFederate.
3. If everything goes well, MetaDefender Core dashboard is displayed with the user identity in the top right corner.

4. Otherwise, access backup login page at `<mdcore-host>#/public/backuplogin` for trouble shooting.
