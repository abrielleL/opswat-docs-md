<!-- source: https://www.opswat.com/docs/cm/user-management/with-azure -->

# Provision console users via Microsoft EntraID

My OPSWAT Central Management offers an integration with a 3rd-party Single Sign-on Service (SSO). This enables an account to provision new users to manage your account. When a user logs into the My OPSWAT Central Management console through your own SSO service, My OPSWAT Central Management will provision that user as a read-only user on your account. You can update the user's role later.

My OPSWAT Central Management uses the secure and widely adopted industry standard Security Assertion Markup Language 2.0 (SAML 2.0), so that you can integrate easily with any large identity provider that supports SAML 2.0.

**To get started, log into Microsoft EntraID Portal and create an application for** **My OPSWAT Central Management** **. Details can be found **[**here**](https://docs.microsoft.com/en-us/azure/active-directory/manage-apps/configure-single-sign-on-non-gallery-applications)**.**

1. Log into Azure Portal as an administrator
2. Navigate to **Azure Active Directory** > **Enterprise applications**
3. Click the **+ New Application**

![](https://uploads.developerhub.io/prod/97qW/yo24b96gnlq5ex9zg9onf8e5yashyi71pf7uib6vvcqylr1suq0cf2m4g2mwdruq.png)

4. Select **Non-gallery application**

![](https://uploads.developerhub.io/prod/97qW/gvzp7ihaeemyfswzwfvn11vavnd3v0p6piffpto71k6363xe74i917ziaeqqr38a.png)

5. Enter  Application name, for example My OPSWAT Central Management
6. Under the **Getting Started** section, select **2. Set up Single sign on**

![](https://uploads.developerhub.io/prod/97qW/5eltxo8dk3nz38ipupzyktgv3fb28q1bptxnxog5wz7g5h3rlv024uorxtepkrkv.jpg)

7. Click Edit icon on **Basic SAML Configuration**. Enter [https://gears.opswat.com](https://gears.opswat.com) as a placeholder for all parameters. Click **Save**.

![](https://uploads.developerhub.io/prod/97qW/uqt4jc6rswmi1zfd9pzzigkckxlmctrp0p6xw25blo7jlgvuta7svgwy5cm90unx.png)

8. Click Edit icon on **User Attributes & Claims**: configure **Unique User Identifier (Name ID)** format as EmailFormat and its value as a user's email by clicking on that claim and choose its format as email address and source attribute as user.mail or user.localprinciplename

![](https://uploads.developerhub.io/prod/97qW/te5rg8qxt9icc8eca4h877p6324nemyc4k7qvit540l3yct6kcx3pfmikc3hupp9.png)

![](https://uploads.developerhub.io/prod/97qW/j69tuhm1yl9su5ur5djar81uu2hzou6kgnznklh78x0e55lkidj9qnszqaiyvipp.png)

9. On **SAML Signing Certificate** section, you can now download the IdP configuration xml file by downloading Federation Metadata XML (for example, azure.xml). You can use this file to import to My OPSWAT Central Management.

![](https://uploads.developerhub.io/prod/97qW/7cm7u63etbdjyzkbn62uou1c0cmcfeguuwju3tl7360qgj1yccm0m0ld5wkjgr5p.jpg)

10. (Optional) Get additional information
    1. Download Azure’s certificate
    2. Get Azure Login URL
    3. Get Azure AD Identifier

![](https://uploads.developerhub.io/prod/97qW/sqmv15hrie3i9shhxfd5dclpokii5emx45s76ep20d00a4q3pbrqgcbcevjw1o68.png)

**Configure Microsoft Azure on** **My OPSWAT Central Management :**

1. Log into the My OPSWAT Central Management console with an admin permission
2. Navigate to User management > SSO
3. On Console Authentication tab, enable "**Enable Single Sign On**" checkbox
4. Enter an **IdP Name**, for example: Azure
5. Click **Choose File** to import the identity provider metadata you got earlier in step #9 . Select the file you saved in step #9, Azure.xml. If the file is valid then IdP certificate, Issuer, and IdP SSO URL will pop up. Click SAVE
6. (Optional) Use this step if you can not import the metadata file
   1. **IdP Certificate**: Upload the certificate downloaded in Step 10.a
   2. **Issuer:** Use the value got in Step 10.c
   3. **IdP SSO URL**: Use the value got in Step 10.b
7. After you save your changes successfully, My OPSWAT Central Management generates a *My OPSWAT Central Management Login URL* and *My OPSWAT Central Management Entity ID*. Copy those values to import to Microsoft Azure

![](https://uploads.developerhub.io/prod/97qW/tbamtbg9cbzrnx1syzq9femzpcsrffubdwcmjlhah50hp7tkinmj7zb6bulzmw43.png)

**Update** **My OPSWAT Central Management** **app on Microsoft Azure**

1. Switch to Azure Portal
2. Navigate to the application you created earlier, My OPSWAT Central Management, click Edit icon on **Basic SAML Configuration**.
3. Replace the value of **Identifier (Entity ID)** with the **My OPSWAT Central Management Entity ID** you copied in step 7 of "Configure Microsoft Azure on My OPSWAT Central Management"
4. Replace value of Reply URL (Assertion Consumer Service URL) and Relay State with the My OPSWAT Central Management Login URL you copied in step 7 then click Save.

![](https://uploads.developerhub.io/prod/97qW/731by5ouuz98e37i90c6zz35xl2rbgt1sm0qi0gbd21lmfaph2gmiti8dweac7iz.png)

**Log in to the** **My OPSWAT Central Management** **Console from Microsoft Azure**

Log in to the Azure portal using this link: [https://myapps.microsoft.com](https://myapps.microsoft.com). Click on the My OPSWAT Central Management application, which the admin previously configured, to access the My OPSWAT Central Management Console.

If you couldn't import the identity provider information from the IdP metadata file, you can get information from the Set up instruction page of the app and copy IdP certificate, Issuer, and IdP SSO URL to the My OPSWAT Central Management console.

### IDP Mappings

IdP Mapping allows you to synchronize user groups from your external Identity Provider (IdP) to specific roles within **My** **OPSWAT Central Management**. This ensures users are automatically assigned the correct permissions upon their SSO login.

Azure handles group claims differently than Okta, often using unique identifiers rather than names.

#### Step A: Attributes & Claims

1. In Azure Portal, go to **Enterprise Applications** > **My** **OPSWAT Central Management** **App** > **Single sign-on**.
2. Edit **Attributes & Claims**:
   - **firstName**: `user.givenname`
   - **lastName**: `user.surname`
3. Click **Add a group claim**:
   - Select **Security groups** (or your preferred group type).
   - **Source attribute**: Select **Group ID** (Note: This sends the Azure Object ID).
   - **Customize the name of the group claim**: Set to `groups`.

![](https://uploads.developerhub.io/prod/97qW/cgoyj2v6o7qc8kma64th6za7se2ht9e8iqyki68rw2h28iqa4n0w7q1pdpryqn9z.png)

#### Step B: **My** **OPSWAT Central Management** Configuration

1. In **My** **OPSWAT Central Management** **> User Management > SSO**, ensure the **Group Attributes** field is set to `groups`.
2. Navigate to **User Management > IdP Mappings** > **Add IdP Mapping**.
3. **Name on IdP**: Paste the **Azure Object ID** (e.g., `a1b2c3d4-e5f6...`).

> **Note:** Unless you specifically configured Azure to send "cloud-only" group names, My OPSWAT Central Management requires the Object ID here to match successfully.

4. **Role**: Select the corresponding My OPSWAT Central Management role.

![](https://uploads.developerhub.io/prod/97qW/jsit9ntnsokdp63db34faeosrd5fufeiyk59bw4hqparryengz56op2e86g0fjow.png)
