<!-- source: https://www.opswat.com/docs/my/faqs/can-we-enable-sso--for-cloud-email-security -->

# Can we enable Single Sign-On (SSO) for Cloud Email Security (CES)?

> **Check Your Version:**
>
> This article is applied to all versions of OPSWAT Cloud Email Security.

### Overview

Cloud Email Security (CES) supports Single Sign-On (SSO) login, but by default, this feature is not enabled for new users or organizations. If SSO has not been set up for your CES account, new users will not be able to access CES using their identity provider (IdP) credentials.

### SSO Behavior (When Enabled)

When SSO is enabled for your organization, the login flow works as follows:

1. A user navigates to CES and enters their email address.
2. The system redirects the user to [https://id.opswat.com/login](https://id.opswat.com/login).
3. If SSO is enabled, the user is automatically redirected to their configured Identity Provider (e.g., Microsoft Entra or Okta) for authentication.
4. Upon successful authentication, the user is redirected back to CES and granted access.

This process is consistent with how SSO is handled in My OPSWAT Portal.

### How to Enable SSO for CES

To enable SSO for your Cloud Email Security account:

- Contact OPSWAT Support or your OPSWAT account representative.
- OPSWAT will configure SSO settings for your CES instance.
- Currently, Microsoft Entra (Azure AD) and Okta are supported as IdPs for SSO integration.

Once set up, all eligible users in your domain will be able to log in to CES via SSO.

> **Support**
>
> If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
