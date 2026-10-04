<!-- source: https://www.opswat.com/docs/supply-chain/configuration/single-sign-on -->

# Single Sign-On

MetaDefender Software Supply Chain can authenticate users through your identity provider with OpenID Connect or SAML 2.0. Users sign in with their corporate account, and MetaDefender grants them the Administrator or Read-only role based on the group the identity provider sends.

Local accounts keep working after you enable SSO. The login page shows **Sign In with SSO** next to the local login form.

## Before you start

- **HTTPS is required.** Identity providers reject redirect URIs that use plain HTTP, except `http://localhost`, and the MetaDefender session cookie is only sent over HTTPS. Enable HTTPS first. See [Configuring HTTPS](https://www.opswat.com/docs/supply-chain/configuration/configuring-https).
- **Open MetaDefender at the address your users will use.** MetaDefender takes the redirect URI from the browser address you are on when you save the SSO settings. Save from `https://mdssc.example.com`, and the redirect URI becomes `https://mdssc.example.com/callback`.
- **You need the Administrator role** to change SSO settings. Administrators who signed in through SSO can view the page but cannot save it.
- **Decide the two groups.** Create or choose two groups, or application roles, in your identity provider: one for administrators and one for read-only users. Group names are matched exactly and are case-sensitive.

## Register MetaDefender with the identity provider

The steps below are for Microsoft Entra ID. Okta, Auth0, ADFS and PingFederate need the same four items: a redirect URI, a client ID and secret (OpenID Connect) or a signing certificate (SAML), and group or role claims in the token.

1. In the Entra admin center, create an **App registration** for MetaDefender.
2. Under **Authentication**, add a **Web** platform with the redirect URI `https://<your-mdssc-address>/callback`. For SAML, use `https://<your-mdssc-address>/callback/saml`.
3. Under **Authentication**, enable **ID tokens** in the implicit grant and hybrid flows section. MetaDefender requests `code id_token`.
4. Under **Certificates & secrets**, create a client secret. Copy the value now. Entra shows it only once.
5. Under **App roles**, create two roles. The role **value** is what MetaDefender matches, for example `MDSSC-Admins` and `MDSSC-ReadOnly`.
6. In **Enterprise applications**, open the application and assign users or groups to the two roles.

Note the **Application (client) ID** and the **Directory (tenant) ID**. You need both in the next section.

## Configure SSO in MetaDefender

1. Sign in as an Administrator and go to **Settings** > **SSO Configuration**.
2. Turn on **Enable Single Sign-On**.
3. Select the **SSO Type**: **OpenID Connect** or **SAML 2.0**.
4. Select the **Identity Provider**: **Microsoft Entra ID**, **Okta**, **Auth0**, **ADFS** or **PingFederate**.
5. Fill in the fields for your SSO type.
6. Under **Role Mapping**, enter the two group names.
7. Click **Save**.

The **Save** button stays disabled until you change a value.

### Fields for OpenID Connect

| Field | Value |
| ---- | ---- |
| Authority URL | The issuer URL of your tenant. For Entra: `https://login.microsoftonline.com/<tenant-id>/v2.0` |
| Client ID | The Application (client) ID of the app registration |
| Client Secret | The client secret value |

### Fields for SAML 2.0

| Field | Value |
| ---- | ---- |
| Authority URL | The base URL of the identity provider, for example `https://adfs.example.com/adfs` |
| Identity Provider Issuer | The entity ID the identity provider puts in its assertions |
| Identity Provider Login URL | The single sign-on service URL |
| Identity Provider Logout URL | The single logout service URL |
| Identity Provider Certificate | The identity provider's signing certificate, as a `.cer`, `.crt` or `.pem` file |

### Role Mapping

| Field | Value |
| ---- | ---- |
| Administrator group | The group or application role whose members get the Administrator role |
| Read-only group | The group or application role whose members get the Read-only role |

Enter the group name only, for example `MDSSC-Admins`. The two names must differ. If you leave a field empty, MetaDefender uses `SsoAdministrator` for administrators and `SsoReadOnlyAdministrator` for read-only users, so you can also name your identity provider groups that way and leave both fields empty.

Matching is case-sensitive. `mdssc-admins` does not match `MDSSC-Admins`.

For **ADFS** and **PingFederate**, the identity provider sends LDAP distinguished names such as `CN=MDSSC-Admins,OU=Groups,DC=example,DC=com`. Enter the group name only, `MDSSC-Admins`. MetaDefender finds it inside the distinguished name.

## Secrets and certificates

MetaDefender stores the client secret and the SAML certificate encrypted and never shows them again. The fields show **Stored** when a value exists.

## How users sign in

1. The user clicks **Sign In with SSO** on the login page.
2. The browser goes to the identity provider. The user signs in there, including any multi-factor authentication.
3. The identity provider returns the user to MetaDefender. MetaDefender creates the user account on first sign-in and grants the role mapped from the user's group.

The role is resolved at every sign-in. When you move a user to the other group in the identity provider, the change applies the next time the user signs in.

If the identity provider does not send a group that matches one of the two entries, the sign-in fails and MetaDefender does not create the account. Add the user to one of the two groups in the identity provider and sign in again.

Users created through SSO appear on the **Users** page like local users. See [User management](https://www.opswat.com/docs/supply-chain/configuration/user-management).

## Troubleshooting

| Symptom | Cause | Fix |
| ---- | ---- | ---- |
| **Sign In with SSO** is not on the login page | SSO is disabled | Turn on **Enable Single Sign-On** and save |
| Entra shows error **AADSTS50011**, redirect URI mismatch | The redirect URI registered in Entra differs from `https://<address>/callback`, where `<address>` is the one you saved the SSO settings from | Register the exact URI, or open MetaDefender at the registered address and save the SSO settings again |
| After signing in at the identity provider, MetaDefender shows **Tenant Configuration service error** | The sign-in took longer than 15 minutes, for example during multi-factor registration, or the browser blocked the sign-in cookies | Start the sign-in again. Complete multi-factor registration before signing in to MetaDefender |
| The user signs in but every action says the role does not allow it | The user's group matched the **Read-only group** | Move the user to the administrator group in the identity provider and sign in again |
| The user signs in at the identity provider, but MetaDefender rejects the sign-in and no account appears on the **Users** page | The user is in neither group, or the group name differs in case from the **Role Mapping** entry | Compare the group name in the identity provider with the **Role Mapping** fields, character by character. Add the user to the group and sign in again |
| Save fails with **Use a different group for each role** | Both Role Mapping fields hold the same name | Enter two different group names |
| Save fails with **Enter a valid http or https URL** | The Authority URL or an identity provider URL is malformed | Enter the full URL including the scheme |

---

[All pages in this documentation](https://www.opswat.com/docs/supply-chain/llms.txt)
