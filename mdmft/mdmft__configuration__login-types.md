<!-- source: https://www.opswat.com/docs/mdmft/configuration/login-types -->

# Login Types

Summarize Page    Connect to Cursor Connect to VS Code

Managed File Transfer allows restriction of login types based on IP addresses or ranges.

Available login types include:

- Local Users
- External Users
- Guests
- Active Directory Users
- Single Sign-on Users
- Radius
- Integrated Windows Authentication

You can customize the login screen for different IP addresses by adding or removing login types. Customize your login screen by mixing and matching rules.

### [Integrated Windows Authentication](/docs/mdmft/configuration/login-types#integrated-windows-authentication)

Integrated Windows Authentication (IWA) allows users to sign in automatically using their Active Directory (AD) credentials without entering a username or password. IWA relies on the underlying Windows authentication mechanisms, either Kerberos or NTLM, to securely verify the user’s identity.

IWA requires the following conditions:

- An Active Directory domain must be configured.
- The user’s computer must be joined to the same Active Directory domain.
- The user must be logged in to the computer with an Active Directory account.

When these conditions are met, the browser or client application can use the user’s existing Windows session to request authentication. Kerberos is the preferred protocol when available, as it provides stronger security and better performance. NTLM is used as a fallback when Kerberos cannot be applied.

Warning

When using Firefox, Integrated Windows Authentication is not enabled by default. Firefox does not automatically provide Windows credentials to the browser. As a result, users are prompted to manually enter their Active Directory username and password unless Firefox has been explicitly configured to allow IWA.

Info

To enable Integrated Windows Authentication (IWA) in Firefox, administrators must configure the browser to trust the MetaDefender Managed File Transfer™ instance.

Steps**:**

1. Open Firefox.
2. In the address bar, enter `about:config` and select **Accept the Risk and Continue**.
3. In the search bar, locate the following settings:

   - `network.automatic-ntlm-auth.trusted-uris`
   - `network.negotiate-auth.trusted-uris` (required for Kerberos authentication)
4. Add the URL of your MFT instance to these fields.
5. Restart Firefox and verify login.
### [Enforcing Guest Authentication](/docs/mdmft/configuration/login-types#enforcing-guest-authentication)

### [Enforcing Active Directory Authentication](/docs/mdmft/configuration/login-types#enforcing-active-directory-authentication)

Select only the *Active Directory* login type for the selected network rule to restrict login for active directory users with specific IP addresses only.

### [Enforcing Single Sign-On Authentication](/docs/mdmft/configuration/login-types#enforcing-single-sign-on-authentication)

Select the "Single Sign-On" login type for the selected network rule to allow SSO only for specific IP addresses.

### [Enforcing Radius Authentication](/docs/mdmft/configuration/login-types#enforcing-radius-authentication)

Select only the "Radius" login type for the selected network rule to allow radius authentication only for specific IP addresses.
