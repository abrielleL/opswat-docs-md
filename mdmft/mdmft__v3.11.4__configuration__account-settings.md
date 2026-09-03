<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/configuration/account-settings -->

# Account Settings

Summarize Page    Connect to Cursor Connect to VS Code

When adding a new user directory, the first step is to configure the "User Directory Account Settings."

Required Fields:

| Setting | Description |
| --- | --- |
| Server Address | Address of the user directory server from where the users will be synchronized. |
| Port | The port used to connect to the user directory *default port for LDAP is 389; for LDAPS, 636.* |
| Authentication Protocol | **Unsecure**: Use basic authentication (simple bind).  **Less unsecure**: Request secure authentication. Note: AD DS uses Kerberos and possibly NTLM.  **Secure communication**: Uses cryptographic signatures to ensure that the senders of messages are identified and content remains intact during transit.  Note: AD DS requires Certificate Server for Secure Sockets Layer (SSL)/TLS encryption. |
| Username | Username of a user in the user directory with read permissions. |
| Password | Password for the specified user. |
| User Directory Type | **Active Directory**: Integrate with active directory.  **LDAP Directory**: Integrate with any custom user directory that supports LDAP protocol.  Note: Integration with LDAP directory requires additional fields. |

---

Click "Continue" to [Synchronization and Login Configuration](/docs/mdmft/v3.11.4/configuration/synchronization-and-login-configuration) after filling out the required information.

### [Required Directory Account Permissions](/docs/mdmft/v3.11.4/configuration/account-settings#required-directory-account-permissions)

The user used for integration must be able to **read** all information from the active directory in order to populate MetaDefender Managed File Transfer™ with the desired groups and users.

The account must be able to **read** the following objects:

- **Users**
- **Groups**
- **Organizational Units (OUs)** (to enumerate structure)
- **Group Memberships**

These permissions are typically covered by **default read access** for **“Authenticated Users”** or **“Domain Users”** in AD, meaning: Most products can use a **standard domain user account** (non-admin) for integration.

However, if permissions were restricted in your AD (e.g., via custom ACLs), ensure the following **explicit read rights** exist:

| Object | Permissions Needed | Applies To |
| --- | --- | --- |
| User objects | Read all user properties | This object and all descendant objects |
| Group objects | Read all group properties | This object and all descendant objects |
| Organizational Units | List contents, read all properties | This object and all descendant objects |

### [LDAP Directory Configuration](/docs/mdmft/v3.11.4/configuration/account-settings#ldap-directory-configuration)

If **LDAP Directory** is selected, additional configuration fields are required in "Account Configuration" to connect and synchronize an LDAP directory.

Info

If the administrator user for LDAP connection is not a part of the base DN, specify the full distinguished name in the "Username" field.

(eg. cn=Administrator,cn=Users,dc=example,dc=com)

Configuring an LDAP user directory:

| Attribute | Description |
| --- | --- |
| Base DN | The DN from where all users can be reached (e.g. dc=CompanyName,dc=com) |
| User Object Class | The name of the object class (objectClass) for user objects. (e.g. posixAccount or person) |
| Object Unique Identifier Attribute | The name of the LDAP attribute that uniquely identifies an entry (e.g. entryUUID or objectGUID) |
| User Email Attribute | The name of the LDAP attribute containing user emails (e.g. mail or email) |
| User Display Name Attribute | The name of the LDAP attribute for the display name of users. (e.g. cn, uid or sAMAccountName) |
| Group Object Class | The name of the object class (objectClass) that is for group objects (e.g. posixGroup or group) |
| Organizational Unit Object Class | The name of the object class (objectClass) for organizational unit objects (e.g. organizationalUnit or ou) |

Warning

Only LDAP attributes should be provided in this configuration step. Aliases are not recognized.

---

Click "Continue" to [Synchronization and Login Configuration](/docs/mdmft/v3.11.4/configuration/synchronization-and-login-configuration) after filling out the required information.
