<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/advanced-deployment/configuring-adfs-as-saml-identity-provider -->

# Configuring ADFS as SAML Identity Provider

View as Markdown Ask ChatGPT about this page Ask Claude about this page

This section provides instructions for administrator to configure ADFS as SAML Identity Provider for authenticating to Kiosk UI and Kiosk Web Management Console.

## [I. Configure ADFS server](/docs/mdkiosk/v4.8.6/advanced-deployment/configuring-adfs-as-saml-identity-provider#i-configure-adfs-server)

- On Windows Server 2019/2022, enable role “Active Directory Federation Services”
- Ensure service “Active Directory Federation Services” - “adfssrv” - is running.
- Create a certificate (self-signed is acceptable) for the ADFS server.

## [II. Configure ADFS as SAML Identity Provider for Kiosk](/docs/mdkiosk/v4.8.6/advanced-deployment/configuring-adfs-as-saml-identity-provider#ii-configure-adfs-as-saml-identity-provider-for-kiosk)

### [**Pre-conditions**](/docs/mdkiosk/v4.8.6/advanced-deployment/configuring-adfs-as-saml-identity-provider#pre-conditions)

- Make sure Kiosk system can access ADFS via domain name, e.g. `https://adfs.local`
- Enable HTTPS on Mangement Console. See [Enable HTTPS](https://docs.opswat.com/mdkiosk/operating/configuring-the-web-server#enabling-https) for more detail.
- Get metadata URL from the ADFS server

### [**Step 1: Get the** *Login URL*](/docs/mdkiosk/v4.8.6/advanced-deployment/configuring-adfs-as-saml-identity-provider#step-1-get-the-login-url)

**Login URL** will be used as **Relying Party Trust Identifier** on ADFS Management

#### [**Login URL for Kiosk UI:**](/docs/mdkiosk/v4.8.6/advanced-deployment/configuring-adfs-as-saml-identity-provider#login-url-for-kiosk-ui)

1. On Kiosk WebMC, navigate to the **Workflows** tab, click on **Select Default Login Method**
2. Select **Single Sign-On**, and select **Protocol Type**, in this case using **SAML 2.0,** then enter **Name**
3. Enter the metadata URL into the Kiosk console according to the format: `https://<ADFS server_name>/FederationMetadata/2007-06/FederationMetadata.xml`
4. **Identifier** will be automated generated → Check if the status is `Connected`and then click on **Apply**

Info

Kiosk UI **Login URL** format:

<http/https>://**localhost**:<port>/metadefender_rest/**uissologin**/saml/<identifier>

Please modify the elements enclosed in <> to match your Kiosk's configuration. It must be **localhost** for Kiosk UI login.

#### [**Login URL for** **Kiosk Console:**](/docs/mdkiosk/v4.8.6/advanced-deployment/configuring-adfs-as-saml-identity-provider#login-url-for-kiosk-console)

Select **SAML (SSO)** in the menu to create a **User Directory** that integrates with a SAML 2.0 SSO Identity Provider (IdP). Switch the toggle button to **ON** to enable this User Directory. As soon as it is submitted, any other User Directories configured with SAML (SSO) will be automatically disabled. Switching to **OFF** only creates the User Directory and will not change any currently enabled User Directories.

Click **CONTINUE** to go to the **Configure Service Provider** page. This will set up the login URL the Identity Provider uses to redirect after a successful login. Fill in **Host or IP** to generate the **Login URL**.

Info

Kiosk console **Login URL** format:

<http/https>://localhost:<port>/metadefender_rest/**ssologin**/saml/<identifier>

### [**Step 2: On ADFS server, open “ADFS Management“.**](/docs/mdkiosk/v4.8.6/advanced-deployment/configuring-adfs-as-saml-identity-provider#step-2-on-adfs-server-open-adfs-management)

### [**Step 3: Add Relying Party Trust**](/docs/mdkiosk/v4.8.6/advanced-deployment/configuring-adfs-as-saml-identity-provider#step-3-add-relying-party-trust)

1. Navigate to **Tools** → ADFS Management, select **Relying Party Trust,** and then click on **Add Relying Party Trust**.
2. Select **Claims aware** from the **Relying Party Trust Wizard** and click on **Start** button.

3. Enter **Display name** and then click on **Next** twice
4. Perform the following two steps

   1. Check on **Enable support for the SAML 2.0 Web SSO protocol** option and then enter the **Relying party SAML 2.0 service URL**.
   2. Enter the **Login URL** from **Step 1** as **Relying party trust identifier** and click on **Add**

5. Click on **Next** 3 times and then **Close**

### [**Step 4: Define the ADFS claim rules**](/docs/mdkiosk/v4.8.6/advanced-deployment/configuring-adfs-as-saml-identity-provider#step-4-define-the-adfs-claim-rules)

1. Go to the **Edit Claim Issuance Transform Rules** tab and click **Add Rules** to launch the **Add Transform Claim Rule Wizard**.
2. In the **Choose Rule Type** panel, choose **Send LDAP Attribute as Claims** and click **Next**.
3. Type the **Claim rule name** in the respective field
4. From the **Attribute store** drop-down list, choose **Active Directory**. In the **Mapping of LDAP attributes to outgoing claim types** section, choose the following values from the respective

   1. **For Kiosk UI:** [Require] LDAP Attribute: **SAM-Account-Name**, Outgoing Claim Type: **Name ID**
   2. **For Web Console:** [Require] LDAP Attribute: **User-Principal-Name**, Outgoing Claim Type: **Name ID**
5. Click on **Finish**

### [**Notes**](/docs/mdkiosk/v4.8.6/advanced-deployment/configuring-adfs-as-saml-identity-provider#notes)

- Make sure the Binding method is POST (not Artifact)

- Any updates in Login URL must be updated on both **Identifiers** and **Endpoints** tabs → **Apply**

## [III. Configure many Kiosks - using as many Relying Party Trusts on ADFS](/docs/mdkiosk/v4.8.6/advanced-deployment/configuring-adfs-as-saml-identity-provider#iii-configure-many-kiosks---using-as-many-relying-party-trusts-on-adfs)

1. Configure each Kiosk as a seperate Relying Party Trust, using [II. Configure ADFS as SAML Identity Provider for Kiosk](https://docs.opswat.com/mdkiosk/advanced-deployment/configuring-adfs-as-saml-identity-provider#ii-configure-adfs-as-saml-identity-provider-for-kiosk)
2. Each Kiosk must have a different Identifier.

## [IV. Configure many Kiosks - using one Relying Party Trust on ADFS](/docs/mdkiosk/v4.8.6/advanced-deployment/configuring-adfs-as-saml-identity-provider#iv-configure-many-kiosks---using-one-relying-party-trust-on-adfs)

1. Not support to config directly from Kiosk, will need OCM for this.
2. Add all Kiosks to one OCM set of Kiosks.
3. Config from OCM using [II. Configure ADFS as SAML Identity Provider for Kiosk](https://docs.opswat.com/mdkiosk/advanced-deployment/configuring-adfs-as-saml-identity-provider#ii-configure-adfs-as-saml-identity-provider-for-kiosk)
4. Make sure all Kiosk have the same port number and SSL is enabled.
