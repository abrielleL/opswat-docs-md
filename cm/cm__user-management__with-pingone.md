<!-- source: https://www.opswat.com/docs/cm/user-management/with-pingone -->

# Provision console users via PingOne

My OPSWAT Central Management offers an integration with a 3rd-party Single Sign-on Service (SSO). This enables an account to provision new users to manage your account. When a user logs into the My OPSWAT Central Management console through your own SSO service, My OPSWAT Central Management will provision that user as a read-only user on your account. You can update the user's role later.

My OPSWAT Central Management uses the secure and widely adopted industry standard Security Assertion Markup Language 2.0 (SAML 2.0), so that you can integrate easily with any large identity provider that supports SAML 2.0.

**To get started, log into PingOne and create an application for** **My OPSWAT Central Management.**

1. Log into PingOne as an administrator
2. Navigate to **Applications**
3. Click  **Add Application** **>** **New SAML Application**
4. Fill in required information and click Continue to Next Step

![](https://uploads.developerhub.io/prod/97qW/f2n3kxo3j628edht1e3ga40rx877r0twbezhbqb4kxq39g00bjvcj7273us30b1m.png)

5. Provide SAML details as below:
   1. Protocol version: select SAML v2.0
   2. Assertion Consumer Service (ACS) & Entity ID: your My OPSWAT Central Management, for example: if your account is connecting to US tenant, it should be [https://gears.opswat.com](https://gears.opswat.com/)

![](https://uploads.developerhub.io/prod/97qW/lg00gvj82ij4e7fsx1r2o0wcg9umk1hpbpfplwdw7tjqkoo4ech5plfoe8h9qe1x.png)

6. Click **Continue to Next Step**
7. **Click** **Save and Exit . You can continue to next steps if you would like to grant access to users and groups or you can do this later.**
8. Expand the app again and download the metadata to import it to My OPSWAT Central Management later, named it *saml2metadata PingOne,xml*

**Configure PingOne on** **My OPSWAT Central Management**

9. Log into the My OPSWAT Central Management console with an admin permission. Navigate to User management > SSO
10. On Control tab, enable "**Enable Single Sign On**" checkbox
11. Click **Choose File** to import the identity provider metadata you got earlier in step #8, saml2_metadata_PingOne,xml. If the file is valid then IdP certificate, Issuer, and IdP SSO URL will be popped up.
12. Enter an IdP Name, for example: PingOne

![](https://uploads.developerhub.io/prod/97qW/g4lndg3n975bgsuccqw71kf5x1qei7sy5h7afre4sds676e1u7cfukz2vo1peklu.jpg)

13. Click the **Save** button and enter your PIN to confirm the action.
14. After you save your changes successfully, My OPSWAT Central Management generates a login URL. Copy this URL.

![](https://uploads.developerhub.io/prod/97qW/i5oseaz94qf4r8sv6mab4nsugb1c2jmuj0ekouydt754c20fbkqzhx8unqqxgkxu.jpg)

**Go back to PingOne to update ACS URL for the** **My OPSWAT Central Management** **app**

15. Switch to PingOne Admin
16. Navigate to Applications, then select the application My OPSWAT Central Management application you created earlier.
17. Click Edit and Continue to Next Step
18. Replace the ACS URL with the URL the My OPSWAT Central Management generated in step #14

![](https://uploads.developerhub.io/prod/97qW/mlwuimu9kbnatxrvu1rmfqry7q9co3sn16ekrwbydbsr28ori9ic04rxybwnkage.png)

19. Click Continue to Next Step until the end and click Finish.

**DONE.** Now you need to assign people/groups who can access this application on PingOne.

If You couldn't import the identity provider information from the IdP metadata file, you can copy IdP certificate, Issuer, and IdP SSO URL to the My OPSWAT Central Management console

### IDP Mappings

IdP Mapping allows you to synchronize user groups from your external Identity Provider (IdP) to specific roles within **My** **OPSWAT Central Management**. This ensures users are automatically assigned the correct permissions upon their SSO login.

To enable group syncing, Okta must be configured to include group memberships in the SAML assertion.

#### Step A: Attribute & Group Statements

1. Log in to your **PingOne Admin Console**.
2. Navigate to **Connections > Applications** and select your **My OPSWAT Central Management SAML Application**.
3. Go to the **Attribute Mappings** tab and click the **Edit** (pencil) icon.
4. Ensure the following core identity attributes are mapped:
   - **firstName** — Maps to `User > First Name`
   - **lastName** — Maps to `User > Last Name`
   - **email** — Maps to `User > Email`
5. **Add Group Attribute:** To send group data, click **Add Attribute**.
   - **Attribute:** `groups`
   - **Mapping:** Select **Group Names**.
   - **Requirement:** Ensure this attribute is included in the SAML assertion.

#### Step B: My OPSWAT Central Management Configuration

1. Go to **My OPSWAT Central Management > User Management > SSO**.
2. In the **Group Attributes** field, enter: `groups` (this must be an exact string match to the attribute name defined in PingOne).
3. Navigate to **User Management > IdP Mappings** > **Add IdP Mapping**.
4. **Name on IdP**: Enter the **exact Group Name** from PingOne (e.g., `IT_Admins`).
5. **Role**: Select the corresponding My OPSWAT Central Management  role (e.g., `Security-Admin`).
