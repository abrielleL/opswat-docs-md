<!-- source: https://www.opswat.com/docs/macloud-sdp/secure-access/pingone-setup-guide -->

# PingOne IdP MFA Setup Guide

## [How does it work?](/docs/macloud-sdp/secure-access/pingone-setup-guide#how-does-it-work)

In this setup guide, the authentication process will have 3 steps:

- Step 1: User enters the account credential
- Step 2: User enters the authentication code from the Authenticator App
- Step 3: Run a device posture check on the user's device

Administrators also can customize the Secure Access rules.

Notes: The IdP MFA method will apply to all applications on IT Access Secure Access Rules. To apply IdP MFA for specific applications, you must assign applications from Ping Console. More detail is in step "15. Assign Policy to Selected Applications"

## [Setup guide](/docs/macloud-sdp/secure-access/pingone-setup-guide#setup-guide)

1. In MetaDefender IT-OT Access, navigate to Secure Access > Access Methods > IdP MFA, and Enable IdP MFA

2. Then download **IdP Metadata (XML)** file
3. In PingIdentity, go to “Integrations > External Idps“, then click on Add Provider
4. Select **SAML**, and filling information
5. Choose Signing Certificate and check on "Sign Authn Request"
6. Import Metadata downloaded in Step 2, and select "HTTP POST" as SSO Binding
7. Click on **Save & Finish**
8. Enabled the new IDP
9. From the new created IDP, click on the pencil icon, then click on IDP Configuration tab and click to download the metadata
10. Upload the Ping Metadata in MetaDefender IT-OT Access and **Save**
11. In PingIdentity, go to Authentication > Authentication, click on **Add Policy** button and fill information
12. Add Login as first step then click on **Add step** for next step
13. (Optional) Select Multi-factor Authentication as second step and click on **Add step**
14. Select **External Identity Provider** then select the new IDP for **External Identity Provider** then check on the box **Pass user context to provider**
15. Assign Policy to Selected Applications.

Navigate to Applications. Add the policy to selected applications

16. Test the integration
