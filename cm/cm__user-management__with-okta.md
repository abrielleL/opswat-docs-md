<!-- source: https://www.opswat.com/docs/cm/user-management/with-okta -->

# Provision console users via Okta

My OPSWAT Central Management offers an integration with a 3rd-party Single Sign-on Service (SSO). This enables an account to provision new users to manage your account. When a user logs into the My OPSWAT Central Management console through your own SSO service, My OPSWAT Central Management will provision that user as a read-only user on your account. You can update the user's role later.

My OPSWAT Central Management uses the secure and widely adopted industry standard Security Assertion Markup Language 2.0 (SAML 2.0), so that you can integrate easily with any large identity provider that supports SAML 2.0.

#### Prerequisites

The 3rd-party Single Sign-on Service (SSO) feature is available for paid Customers. If you are using a free account and would like to use this feature, please click the "Upgrade Request" button under **Console Management > Settings > Global > Account** tab.

#### Supported features

- IdP-initiated SSO
- SP-initiated SSO
- Just-In-Time provisioning

#### Configuration steps

1. Log into Okta as an administrator
2. Navigate to **Applications** and click on "Browsers App Catalog" button
3. Search OPSWAT and select My OPSWAT Central Management application

![](https://uploads.developerhub.io/prod/97qW/aj9662i2so1d5ivcgf3fn60y5styl2i0o49pgg7wqfk9vp8f5ffeh2om6y3ledbr.png)

4. Click the **Add Integration** button

![](https://uploads.developerhub.io/prod/97qW/xaghd9xz1etwbdb9g87qskmto51zfod41myaklv7jhs28jiev0uh0hkzwkho97fa.png)

5. Enter the Application Label, for example **My OPSWAT Central Management** and click the **Done** button

![](https://uploads.developerhub.io/prod/97qW/yw6sm9lkz966ad4xxoj25hv07bbcr6cgrv4jkg2tvw4men4wi5tlvz6fjjqcz47v.png)

6. Navigate to **Sign On** tab.
7. Open the **Metadata URL** on another tab and save the content as **idpmetadata.xml**

![](https://uploads.developerhub.io/prod/97qW/4wdc3rvnk1lpu5sz0770m4c6ln38wxbgpz0pin13hao2r2g14qzdlvxcnqhooqhr.png)

8. Login My OPSWAT Central Management Console
9. Navigate to **User Management** **> SSO >** **Console Authentication**
10. Check **Enable Single Sign On**
11. Upload idpmetadata.xml from step 7 and click the **SAVE** button

![](https://uploads.developerhub.io/prod/97qW/c8srlmxmud89kjph4grkl7z3roxbifzf19qntceow6btjucg0oe43um030zmjjv2.png)

12. Scroll down to the My OPSWAT Central Management Login URL and copy the URL

![](https://uploads.developerhub.io/prod/97qW/x0xpvqh046f9myps49t1out1vwjm4bagbxtot77axrbc2bv5fyttcxp0y2akzl23.png)

13. Switch to Okta Admin
14. Click the **Edit** button
15. Scroll down to the Advanced Sign-on Settings and paste the My OPSWAT Central Management Login URL

![](https://uploads.developerhub.io/prod/97qW/8g1r1z0tvbopytec6ubijz549tjp682lrtwgue4ng5cmdt56rntugbzx9qw5vi6z.png)

16. Click the **Save** button
17. **DONE.** Now you need to assign people/groups who can access this application on Okta.

If You couldn't import the identity provider information from the IdP metadata file, you can get information from the Set up instruction page of the app and copy IdP certificate, Issuer, and IdP SSO URL to the My OPSWAT Central Management console

### IDP Mappings

IdP Mapping allows you to synchronize user groups from your external Identity Provider (IdP) to specific roles within **My** **OPSWAT Central Management** . This ensures users are automatically assigned the correct permissions upon their SSO login.

To enable group syncing, Okta must be configured to include group memberships in the SAML assertion.

#### Step A: Attribute & Group Statements

1. Navigate to your **My OPSWAT Central Management** **Application** in Okta > **General** > **SAML Settings** > **Edit**.
2. In **Attribute Statements**, ensure these core fields are mapped:
   - **Name:** `firstName` | **Value:** `user.firstName`
   - **Name:** `lastName` | **Value:** `user.lastName`
3. In **Group Attribute Statements**, add:
   - **Name:** `groups`
   - **Name format:** `Basic`
   - **Filter:** `Matches regex` | **Value:** `.*` (This sends all groups the user belongs to).

![](https://uploads.developerhub.io/prod/97qW/y8eiafavgug3eu0uewc36q2z8g944lgz81blo3zu8veqti8br8n0x102oe1panqa.png)

#### Step B: OCM Configuration

1. Go to **My OPSWAT Central Management > User Management > SSO**.
2. In the **Group Attributes** field, enter: `groups` (This must match the "Name" defined in Okta).
3. Navigate to **User Management > IdP Mappings** > **Add IdP Mapping**.
4. **Name on IdP**: Enter the **exact Group Name** from Okta (e.g., `IT_Admins`).
5. **Role**: Select the corresponding OCM role (e.g., `Security-Admin`).

![](https://uploads.developerhub.io/prod/97qW/jsit9ntnsokdp63db34faeosrd5fufeiyk59bw4hqparryengz56op2e86g0fjow.png)

#### SP-initiated SSO

Contact [OPSWAT Support](https://www.opswat.com/support/contact-support) to enable SP-initiated SSO for your domain users
