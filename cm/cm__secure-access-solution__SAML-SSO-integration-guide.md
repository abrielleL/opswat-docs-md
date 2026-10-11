<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/SAML-SSO-integration-guide -->

# SAML SSO Integration Guide

**What is SAML?**

Security Assertion Markup Language (SAML) is an XML-based standard for web browser single sign-on (SSO) that eliminates the need for application specific passwords. SAML uses single-use, expiring, digital "tokens" to exchange authentication and authorization data between an identity provider and cloud application service provider that have an established trust relationship.

## How does SAML SSO work with Cloud Access Control?

![](https://uploads.developerhub.io/prod/97qW/2t8i8u9q1dnjgzrty4tar4yhmb1h348933r0qjur5p326psu6hmhhzkxe5rfnjax.png)

SAML single sign-on works by transferring the user's identity from one place (the identity provider) to another (the service provider). This is done through an exchange of digitally signed XML documents. Consider the following scenario: A user is logged into a system, which acts as an identity provider. The user would like to log into a remote application such as Salesforce or Dropbox (i.e. the service provider) but before the user is granted access, the user's device needs to pass a security check as defined by the organization's security policy. The following happens:

1. The user clicks on the link to the application, either on the corporate intranet, a bookmark or similar and the application loads.
2. The application identifies the user origin (either by application subdomain, user IP address or similar) and redirects the user back to the identity provider, asking for authentication. This is the authentication request.
3. The user either has a session with the identity provider already, or establishes one by logging into the identity provider.
4. The identity provider builds the authentication response in the form of an XML document containing the user's username or email address, signs it using a certificate and posts this information to My OPSWAT Central Management.
5. My OPSWAT Central Management performs the security or posture check on the device and takes a decision on whether to grant or deny access; if it decides to grant access, it passes a SAML response from IdP to SP. Otherwise, it logs the user out
6. The service provider retrieves the security check and authentication response and determines whether to grant access or deny it

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
