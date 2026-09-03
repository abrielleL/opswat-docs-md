<!-- source: https://www.opswat.com/docs/mdemail/6.4.1/knowledge-base/how-to-integrate-with-entra-id-for-sso-authentication-over-saml- -->

# How to integrate with Entra ID for SSO Authentication over SAML?

**Step 1:**

Create a new **Enterprise Application** on **Microsoft Azure**

**Step 2:**

Assign the users/groups as needed, so that they can authenticate once the integration is completed, and proceed with the **Single Sign On** setup, selecting **SAML** as method

**Step 3:**

Go to **MetaDefender Email Gateway Security** (**EGS**) **Web UI** > **User Management** > **User Directories** and create a new **SAML User Directory**, configuring everything as follows:

**__ __**

****On the EGS****:

- `User Directory Type`: **SAML**
- `User Directory name`: Enter a custom name
- `IDP Issuer URL`: Upload the `Federation Metadata XML` from **Azure**

  - Please note that the **Azure Federation Metadata XML** automatically updates whenever you modify any settings that influence the SAML configuration.
- `Use custom Entity ID`: Enable and enter a custom value
- `Public URL` and `Login callback URL`: Leave unchanged
- `User identified by`: Use the support claims from Azure
- `SSO user role mapping`: Configure the user mapping as needed

****On the Entra ID****:

**Basic SAML Configuration:**

- `Identifier (Entity ID)`: The value configured on EGS
- `Reply URL (Assertion Consumer Service URL)`: EGS Login Callback URL
- `Sign on URL`: EGS Public URL

**Step 4:**

Save the changes and enable the newly created User Directory on the EGS:

Once completed, the option to authenticate with SSO will appear on the Login Page:

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
