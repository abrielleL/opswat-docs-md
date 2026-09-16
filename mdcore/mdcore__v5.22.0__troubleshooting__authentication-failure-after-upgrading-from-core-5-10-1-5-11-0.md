<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/troubleshooting/authentication-failure-after-upgrading-from-core-5-10-1-5-11-0 -->

# Authentication Failure After Upgrading From Core 5.10.1/5.11.0

## [Issue Description](/docs/mdcore/v5.22.0/troubleshooting/authentication-failure-after-upgrading-from-core-5-10-1-5-11-0#issue-description)

After upgrading from MetaDefender Core 5.10.1/5.11.0 to more recent versions, users may experience authentication failures when attempting to log in using SSO or AD/LDAP credentials.

This issue occurs due to an encryption key incompatibility that may have affected your previous upgrade to 5.10.1/5.11.0. If the initial upgrade was completed with incompatible encryption keys, subsequent upgrade will encounter this authentication problem.

## [Resolution Path](/docs/mdcore/v5.22.0/troubleshooting/authentication-failure-after-upgrading-from-core-5-10-1-5-11-0#resolution-path)

Please follow these steps to resolve the authentication issue:

**- Upgrade to MetaDefender Core 5.14.0** or newer version if you haven't already done so.

- **Log in using a LOCAL administrator account**.

- Reconfigure your identity provider settings
- **OIDC directories**:

  - Re-enter your Client ID
  - Re-enter your Client Secret
  - Verify and update the Login URL

- With **SAML** directory: Customer has to re-enter

  - **Private Key** - If option Enable Assertion Decryption is in used.
  - **Login URL.**

With **AD/LDAP** directory: Customer has to re-enter **Bind password**

Once reconfigured, your SSO and AD/LDAP authentication should function properly again.

If you encounter any difficulties during this process, please contact OPSWAT Technical Support for assistance.
