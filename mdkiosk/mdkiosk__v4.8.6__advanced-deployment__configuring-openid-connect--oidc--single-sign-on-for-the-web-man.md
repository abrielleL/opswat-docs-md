<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/advanced-deployment/configuring-openid-connect--oidc--single-sign-on-for-the-web-man -->

# Configuring OpenID Connect (OIDC) Single Sign-On for the Web Management Console

View as Markdown Ask ChatGPT about this page Ask Claude about this page

MetaDefender Kiosk's Web Management Console (WebMC) can authenticate administrators and other console users against an external identity provider using single sign-on. Starting in Kiosk 4.8.3, you can configure this with **OpenID Connect (OIDC)** in addition to SAML and Microsoft Entra ID — so you can connect WebMC to any OIDC-compliant identity provider, including Active Directory Federation Services (ADFS), Okta, and ManageEngine, using its published discovery information instead of a SAML metadata exchange.

## [Prerequisites](/docs/mdkiosk/v4.8.6/advanced-deployment/configuring-openid-connect--oidc--single-sign-on-for-the-web-man#prerequisites)

- Kiosk 4.8.3 or later.
- Administrator access to the Web Management Console.
- An OIDC application registered with your identity provider, giving you a **discovery (well-known) URL**, a **Client ID**, and a **Client Secret**.
- A reachable hostname or IP address for your Kiosk server. Loopback addresses (`localhost`, `127.0.0.1`) cannot be used here.
- A decision on how signed-in users should get their Kiosk role: everyone gets the same **default role**, or each user/email is mapped to a specific role individually.

## [Configuring an OIDC user directory](/docs/mdkiosk/v4.8.6/advanced-deployment/configuring-openid-connect--oidc--single-sign-on-for-the-web-man#configuring-an-oidc-user-directory)

1. Sign in to the Web Management Console as an administrator.
2. Navigate to **User Management > User Directories**.
3. Click **Add new directory**.
4. Under **Type of directory**, select **Single Sign-on**.
5. In **Choose Protocol Type**, select **OIDC**. The form updates to show the OIDC fields.
6. Enter a **Directory name** and turn the **Status** toggle on if you want this directory active as soon as it's saved.
7. Fill in:

   - **Host or IP** — the address your identity provider will redirect back to after login.
   - **Authority Well-known URL** — your identity provider's OIDC discovery URL.
   - **Client ID** and **Client Secret** — from your identity provider's application registration.
8. Click **Test connection**. Once it reports a successful connection, click **Continue**.
9. On the role assignment step, choose **Default role** to give every user signing in through this directory the same role, or **Role Mapping** to assign roles individually — add at least one user's email and pick a role for them.
10. Click **Continue**, review the summary, and click **Submit**.

Note

Only one single sign-on directory (SAML, Microsoft Entra ID, or OIDC) can be active at a time. Enabling a new OIDC directory automatically disables any SAML or Entra ID directory that was previously enabled, and vice versa.

Note

Once a directory is created, its type can't be changed. To switch an existing SAML directory to OIDC (or the reverse), create a new directory with the desired protocol and delete the old one.

Once enabled, a **Sign-In with SSO** button appears on the WebMC login page. Selecting it takes users to your identity provider to sign in, then returns them to WebMC already authenticated.

## [Example: Moving from SAML to OIDC](/docs/mdkiosk/v4.8.6/advanced-deployment/configuring-openid-connect--oidc--single-sign-on-for-the-web-man#example-moving-from-saml-to-oidc)

Suppose your organization currently signs in to WebMC through a SAML directory, but your identity provider team wants to standardize on OIDC instead:

1. Create a new directory, choosing **Single Sign-on** as the type and **OIDC** as the protocol.
2. Fill in the OIDC fields using your identity provider's discovery URL and application credentials, test the connection, and set up role assignment the same way your SAML directory was configured.
3. Turn the new OIDC directory's status on. Your existing SAML directory is automatically disabled at that point — no separate step is needed to turn it off.
4. Confirm the **Sign-In with SSO** button on the login page now authenticates through your identity provider's OIDC flow.

Your OIDC directory configuration, including your Client Secret, is included whenever you back up or restore your Kiosk configuration, and survives an in-place upgrade — you won't need to re-enter these details afterward.
