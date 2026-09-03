<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/configuration-idp-mfa -->

# Configuration

## Setup

1. In My OPSWAT Central Management, navigate to **User Management > SSO > IdP MFA**, and **Enable IdP MFA**
2. Copy the **Entity ID**, **Single Sign-On URL**, and download the **IdP Certificate**. Then navigate to your Service Provider’s Administrator account.
3. Create a new Identity Provider that will be used for Multi-Factor Authentication with My OPSWAT Central Management's metadata.
4. Enable your newly created Multi-Factor Authentication for logins and/or application sign-ons.
5. The MFA will now prompt for logins and application sign-ons. To validate the configuration is properly setup:
   1. Test with a compliant device and the user login should flow seamlessly through My OPSWAT Central Management's authentication and back to your login flow.
   2. Test with a non-compliant device and the user should not return back to login, and redirect to a remediation page. The remediation page gives details on how to return your devices back to a compliant state.
