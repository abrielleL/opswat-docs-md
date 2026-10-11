<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/why-am-i-receiving--ldap-is-unsupported--when-trying-to-configur -->

# Why am I receiving "LDAP is unsupported" when trying to configure an AD server on a Kiosk instance managed by Central Management v8?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

When managing a MetaDefender Kiosk instance using Central Management (OCM) v8 on-premises, you may encounter one of the following two scenarios when configuring an AD server:

1. **Error During Kiosk AD Configuration from OCM**

When configuring the Kiosk AD from within OCM, an error message stating **“LDAP is unsupported”** appears. This occurs even though the same AD settings work when configured directly on a standalone (non-managed) Kiosk instance.

2. **Empty Users and Groups After adding the Kiosk to OCM** If the AD was already configured on a Kiosk instance and that instance is later imported into OCM, the AD user and group lists may be empty. Attempts to revalidate the settings from the OCM side will result in the same **“LDAP is unsupported”** error.

---

**Root Cause** This issue occurs due to the format of the AD bind credentials or the need for anonymous bind support on the AD server.

---

**Resolution**

To successfully bind the Kiosk to Active Directory via OCM:

### [Option 1: Use Fully Qualified Bind Username](/docs/mdkiosk/v4.8.6/knowledge-base/why-am-i-receiving--ldap-is-unsupported--when-trying-to-configur#option-1-use-fully-qualified-bind-username)

Ensure the bind username includes the domain, using either of the following formats:

- `domain\username`
- `username@domain.test`

### [Option 2: Enable Anonymous Bind on Active Directory](/docs/mdkiosk/v4.8.6/knowledge-base/why-am-i-receiving--ldap-is-unsupported--when-trying-to-configur#option-2-enable-anonymous-bind-on-active-directory)

If using a non-domain-qualified username, you must enable anonymous bind on the AD server:

#### [Step 1: Modify the dSHeuristics Attribute](/docs/mdkiosk/v4.8.6/knowledge-base/why-am-i-receiving--ldap-is-unsupported--when-trying-to-configur#step-1-modify-the-dsheuristics--attribute)

1. Open **ADSI Edit** on the Active Directory server (`Start Menu > Search > ADSI Edit`).
2. Right-click **ADSI Edit** and select **Connect To...**
3. In “Select a well-known naming context,” choose **Configuration**.
4. Navigate to: `DC=<your domain>` > `CN=Configuration` > `CN=Services` > `CN=Windows NT` > `CN=Directory Service`
5. Open **Properties** of "Directory Service."
6. Set the `dSHeuristics` attribute to `0000002`. If it already has a value, modify only the **seventh digit** to `"2"`.

#### [Step 2: Grant Read Permissions to Anonymous Logon](/docs/mdkiosk/v4.8.6/knowledge-base/why-am-i-receiving--ldap-is-unsupported--when-trying-to-configur#step-2-grant-read-permissions-to-anonymous-logon)

1. Open **Active Directory Users and Computers**.
2. Right-click the domain or relevant OU and select **Properties > Security**.
3. Add **ANONYMOUS LOGON** and grant **Read** permissions as needed.

#### [Step 3: Verify Access](/docs/mdkiosk/v4.8.6/knowledge-base/why-am-i-receiving--ldap-is-unsupported--when-trying-to-configur#step-3-verify-access)

After completing these changes, confirm that anonymous users can access the intended directory parts without authentication and that the users and groups are available when configuring the Kiosk AD from Central Management v8

---

**Security Considerations** Enabling anonymous bind introduces potential security risks. Ensure:

- Access is limited to only the necessary directory objects and attributes.
- All changes align with organizational security policies and compliance standards.

---

**Applies To**

- MetaDefender Kiosk
- Central Management (OCM) v8
- Microsoft Active Directory

---

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
