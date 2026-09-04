<!-- source: https://www.opswat.com/docs/macloud-sdp/secure-access/okta-idp-mfa-setup-guidegyz -->

# Okta Identity Engine - IdP MFA Setup Guide

## [Setup Steps](/docs/macloud-sdp/secure-access/okta-idp-mfa-setup-guidegyz#setup-steps)

1. In MetaDefender IT-OT Access, navigate to Secure Access > Access Methods > IdP MFA, and Enable IdP MFA

2. Copy the Entity ID, Single Sign-On Url, and download the IdP Certificate. Then navigate to your Okta Administrator account.
3. In Okta Admin, go to “Security > Identity Providers“ to setup OPWAT’s Compliance-Based IdP MFA

4. Add Identity Provider, select “SAML 2.0 IdP“ and click "Next" button

5. Fill in the information with the provided metadata from MetaDefender IT-OT Access

6. Keep the default configurations in the Advanced Settings
7. Download the SAML metadata of the new IdP

 _

8. **Upload** the Okta Metadata in MetaDefender IT-OT Access and **Save**

9. In Okta, navigate to Security > Authenticators > Setup and click "Add authenticator"

9. In the Security > Authenticators, select Enrollment tab and add a new MetaDefender IT-OT Access policy

- It's recommended to assign **none-admin** group in this policy before testing all the configuration and flow.
- Need to require "MetaDefender IT-OT Access (IdP)" and "Password" and disable other authenticators
- Keep the default rule

10. Configure your Global Session Policy.

- It's recommended to assign to a **none-admin group** before testing the flow and policy
- It's recommended to require MFA at every sign in

11. Test your integration
