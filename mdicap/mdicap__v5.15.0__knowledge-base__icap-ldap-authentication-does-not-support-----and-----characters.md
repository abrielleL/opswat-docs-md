<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/knowledge-base/icap-ldap-authentication-does-not-support-----and-----characters -->

# ICAP LDAP Authentication Does Not Support "<" and ">" characters in the password.

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**Check Your Version:**

This article applies to All version of Metadefender ICAP up to V5.13.0

**Issue:**

If an LDAP user's password includes the `<` or `>` characters, the application blocks those characters to prevent XSS (Cross-Site Scripting) attacks. This affects BIND user credentials and surfaces as an error during **Test Connection** testing.

**Solution:**

ICAP Server V5.14.0, expected at the end of June 2026, will resolve this issue and add full support for `<` and `>` in LDAP authentication passwords.

In the meantime, LDAP authentication users must avoid using `<` or `>` as special characters in their passwords.

**Support:**

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
