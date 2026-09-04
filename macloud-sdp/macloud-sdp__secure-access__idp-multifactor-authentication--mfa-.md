<!-- source: https://www.opswat.com/docs/macloud-sdp/secure-access/idp-multifactor-authentication--mfa- -->

# IdP Multifactor Authentication (MFA)

## [How it works](/docs/macloud-sdp/secure-access/idp-multifactor-authentication--mfa-#how-it-works)

IdP MFA is a device compliance access control solution that leverages the Multi-Factor Authentication flow in Service Provided applications. Communication with your Service Provider is done with SAML, which returns a successful response for compliant devices that have the MetaDefender Endpoint installed.

The Endpoint Client Device is in constant communication with MetaDefender IT-OT Access, sending device information to help determine its compliance status.

Users attempt to initiate a login from their Service Provider’s dashboard, or launch an application managed by their Service Provider.

1. The Service Provider will send a Multi-Factor verification request to MetaDefender IT-OT Access
2. MetaDefender IT-OT Access will determine if the device is either compliant or not compliant

   1. If compliant, the user will return to the Service Provider with a successful authentication
   2. If not compliant, the user will be redirected to a remediation page specifying details on exactly why their device is not compliant.
3. After a successful authentication, the user will be able to navigate to their Service Provider’s dashboard and access their applications.

## [Setup](/docs/macloud-sdp/secure-access/idp-multifactor-authentication--mfa-#setup)

1. In MetaDefender IT-OT Access, navigate to **User Management > SSO > IdP MFA**, and **Enable IdP MFA**
2. Copy the **Entity ID**, **Single Sign-On URL**, and download the **IdP Certificate**. Then navigate to your Service Provider’s Administrator account.
3. Create a new Identity Provider that will be used for Multi-Factor Authentication with MetaDefender IT-OT Access' metadata.
4. Enable your newly created Multi-Factor Authentication for logins and/or application sign-ons.
5. The MFA will now prompt for logins and application sign-ons. To validate the configuration is properly setup:

   1. Test with a compliant device and the user login should flow seamlessly through MetaDefender IT-OT Access' authentication and back to your login flow.
   2. Test with a non-compliant device and the user should not return back to login, and redirect to a remediation page. The remediation page gives details on how to return your devices back to a compliant state.
