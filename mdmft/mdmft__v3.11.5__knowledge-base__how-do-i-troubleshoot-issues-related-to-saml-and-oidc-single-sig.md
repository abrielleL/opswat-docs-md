<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/knowledge-base/how-do-i-troubleshoot-issues-related-to-saml-and-oidc-single-sig -->

# How do I troubleshoot issues related to SAML and OIDC Single Sign-On configuration in MetaDefender Managed File Transfer?

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

When configuring SAML or OIDC-based Single Sign-On (SSO) for MetaDefender Managed File Transfer (MFT), some issues are not covered by the existing Active Directory and LDAP troubleshooting guidance. This article focuses on common SSO-specific problems related to attribute mapping, identity uniqueness, and provider-specific configuration behavior.

Use this article when SSO is already configured but users experience login failures, missing profile data, duplicate identity conflicts, or provider-specific OIDC redirect issues, and updating the product is not an option yet. Most of the following scenarios and issues have been added to product [updates.no](http://updates.no)

## **Unable to log in when the SAML subject identifier is longer than 50 characters**

### **Issue**

A first-time SAML login may fail if the identity provider sends a subject identifier value that exceeds 50 characters. This often occurs when the assertion uses a long value such as a full UPN or another verbose unique identifier.

### **Solution**

1. Review the SAML assertion sent by your identity provider and identify the value used as the subject identifier or `NameID`.
2. Confirm whether that value exceeds 50 characters.
3. Update the identity provider configuration to use a shorter unique identifier where possible.
4. Prefer a stable, unique value that remains consistent across logins and stays within the character limit.
5. If failed login attempts already created incomplete or conflicting user records, remove the affected entries before testing again.

Examples of shorter identifiers may include a shorter username format rather than a full principal name, provided the value remains unique in your environment.

If the identifier is changed after users have already logged in successfully, MFT may interpret the new value as a different user identity.

## **Unable to sync the user email address from Okta through SAML SSO**

### **Issue**

Users can authenticate successfully with Okta, but their email address is not populated in MFT. This can affect notifications, approval workflows, and any process that depends on the email field.

### **Solution**

1. Open the Okta application used for MFT SSO.
2. Review the SAML attribute statements configured for the application.
3. Ensure an email attribute is explicitly sent in the assertion.
4. Use a value that maps to the user's actual email address in Okta.
5. Have the affected user sign out and sign back in after saving the updated configuration.

Commonly, the attribute name is configured as `email` and mapped to the user email value maintained in Okta.

If you are already updating SAML attributes, it can also be helpful to review whether other user profile fields such as first name and last name should be populated for consistency.

## **Unable to complete Microsoft Entra ID OIDC login in Kiosk mode**

### **Issue**

OIDC authentication with Microsoft Entra ID may fail or loop during Kiosk login if the redirect URI or token claims do not align with the Kiosk endpoint being used.

### **Solution**

1. Verify the application registration in Microsoft Entra ID matches the exact Kiosk endpoint used by end users.
2. Confirm the redirect URI includes the correct protocol, host name, port, and path for the Kiosk deployment.
3. Review token configuration and ensure the required identity claims are included for MFT to identify the user correctly.
4. Verify the configured client ID, issuer URL, and scopes in MFT match the Entra ID application settings.
5. If Kiosk is published behind a reverse proxy or load balancer, confirm forwarded host and protocol headers preserve the external URL seen by the identity provider.

A mismatch between the registered redirect URI and the externally accessed Kiosk URL is a common cause of repeated redirects or failed sign-in attempts.

Even small differences in the redirect URI, such as the host name, trailing path, or HTTPS usage, can cause OIDC authentication to fail.

## **Best practices**

- Use a unique and stable identifier for SSO users.
- Keep attribute mapping consistent across identity provider changes.
- Validate email-related attributes if MFT workflows depend on notifications or approvals.
- For OIDC integrations, always validate the effective external URL presented to end users.

## **When to collect additional troubleshooting data**

If the issue persists after reviewing the configuration, collect relevant logs, screenshots of the identity provider settings, and details of the exact user experience during login. Include the assertion or token claims where possible, while following your organization's security handling requirements.

**Support:**

If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support) and share the gathered information about the issue.
