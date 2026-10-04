<!-- source: https://www.opswat.com/docs/supply-chain/configuration/sso-entra-id-configuration -->

# SSO Entra ID Configuration

Use Microsoft Entra ID as an OpenID Connect identity provider for MetaDefender Software Supply Chain. Users sign in with their corporate account, and MetaDefender grants them the Administrator or Read-only role based on the application role Entra ID sends.

For general SSO behavior, SAML configuration, and additional troubleshooting, see [Single Sign-On](https://www.opswat.com/docs/supply-chain/configuration/single-sign-on).

## Before you start

- **HTTPS is required.** Entra ID rejects redirect URIs that use plain HTTP, except `http://localhost`, and the MetaDefender session cookie is only sent over HTTPS. Enable HTTPS first. See [Configuring HTTPS](https://www.opswat.com/docs/supply-chain/configuration/configuring-https).
- **Open MetaDefender at the address your users will use.** MetaDefender takes the redirect URI from the browser address you are on when you save the SSO settings. Save from `https://mdssc.example.com`, and the redirect URI becomes `https://mdssc.example.com/callback`. Do not save from `localhost` or an IP address unless that is the address users sign in from.
- **You need the Administrator role** to change SSO settings. Administrators who signed in through SSO can view the page but cannot save it.
- **Decide the two application roles.** Create one role for administrators and one for read-only users. Role values are matched exactly and are case-sensitive.

## Register MetaDefender in Entra ID

1. In the Entra admin center, create an **App registration** for MetaDefender.
2. Under **Authentication**, add a **Web** platform with the redirect URI `https://<your-mdssc-address>/callback`.
3. Under **Authentication**, enable **ID tokens** in the implicit grant and hybrid flows section. MetaDefender requests `code id_token`.
4. Under **Certificates & secrets**, create a client secret. Copy the value now. Entra shows it only once.
5. Under **App roles**, create two roles. The role **value** is what MetaDefender matches, for example `MDSSC-Admins` and `MDSSC-ReadOnly`.
6. In **Enterprise applications**, open the application and assign users or groups to the two roles.

Note the **Application (client) ID** and the **Directory (tenant) ID**. You need both when you configure MetaDefender.

## Configure SSO in MetaDefender

1. Sign in as an Administrator and go to **Settings** > **SSO Configuration**.
2. Turn on **Enable Single Sign-On**.
3. Set **SSO Type** to **OpenID Connect**.
4. Set **Identity Provider** to **Microsoft Entra ID**.
5. Enter the OpenID Connect settings:

   | Field | Value |
   | ---- | ---- |
   | Authority URL | `https://login.microsoftonline.com/<tenant-id>/v2.0`, replacing `<tenant-id>` with the Directory (tenant) ID |
   | Client ID | The Application (client) ID of the app registration |
   | Client Secret | The client secret value |
6. Under **Role Mapping**, enter the two application role values:

   | Field | Value |
   | ---- | ---- |
   | Administrator group | The application role whose members get the Administrator role |
   | Read-only group | The application role whose members get the Read-only role |
7. Click **Save**.

The **Save** button stays disabled until you change a value.

Enter the role value only, for example `MDSSC-Admins`. The two values must differ, and matching is case-sensitive. `mdssc-admins` does not match `MDSSC-Admins`.

If you leave a field empty, MetaDefender uses `SsoAdministrator` for administrators and `SsoReadOnlyAdministrator` for read-only users. You can use those values for the Entra ID application roles and leave both fields empty.

## Client secret storage

MetaDefender stores the client secret encrypted and never shows it again. The field shows **Stored** when a value exists.

To save any later change on the SSO Configuration page, enter the **Client Secret** again. A save with an empty secret is rejected.

## Assign users and groups

In the Entra admin center, open the MetaDefender enterprise application and assign each user or group to either the administrator or read-only application role.

MetaDefender resolves the role at every sign-in. When you assign a user to the other role in Entra ID, the change applies the next time the user signs in.

If Entra ID does not send an application role that matches one of the two Role Mapping entries, sign-in fails and MetaDefender does not create the account. Assign the user to one of the two application roles and sign in again.

Users created through SSO appear on the **Users** page like local users. See [User management](https://www.opswat.com/docs/supply-chain/configuration/user-management).

## Troubleshooting

| Symptom | Cause | Fix |
| ---- | ---- | ---- |
| **Sign In with SSO** is not on the login page | SSO is disabled | Turn on **Enable Single Sign-On** and save |
| Entra shows error **AADSTS50011**, redirect URI mismatch | The redirect URI registered in Entra differs from `https://<address>/callback`, where `<address>` is the one you saved the SSO settings from | Register the exact URI, or open MetaDefender at the registered address and save the SSO settings again |
| After signing in at Entra ID, MetaDefender shows **Tenant Configuration service error** | The sign-in took longer than 15 minutes, for example during multi-factor registration, or the browser blocked the sign-in cookies | Start the sign-in again. Complete multi-factor registration before signing in to MetaDefender |
| The user signs in but every action says the role does not allow it | The user's application role matched the **Read-only group** | Assign the user to the administrator application role in Entra ID and sign in again |
| The user signs in at Entra ID, but MetaDefender rejects the sign-in and no account appears on the **Users** page | The user has neither application role, or the role value differs in case from the **Role Mapping** entry | Compare the role value in Entra ID with the **Role Mapping** fields, character by character. Assign the user to the role and sign in again |
| Save fails with **Use a different group for each role** | Both Role Mapping fields hold the same value | Enter two different application role values |
| Save fails with **Enter a valid http or https URL** | The Authority URL is malformed | Enter the full URL including the scheme |

---

[All pages in this documentation](https://www.opswat.com/docs/supply-chain/llms.txt)
