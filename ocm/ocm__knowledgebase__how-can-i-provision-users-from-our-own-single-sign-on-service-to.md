<!-- source: https://www.opswat.com/docs/ocm/knowledgebase/how-can-i-provision-users-from-our-own-single-sign-on-service-to -->

# How can I provision users from our own single sign-on service to OPSWAT Central Management?

This article applies to all OPSWAT Central Management V7.5.0+ releases deployed on Windows or Linux systems.

OPSWAT Central Management includes the option to integrate with your third-party **single sign-on service** (**SSO**). This enables the seamless provisioning of new manager-users to your account.

When a user logs into the OPSWAT Central Management Console via your SSO service, OPSWAT Central Management will provision that user as a read-only user on your account, but this role and its associated limitations can be updated as you see fit.

Pro Tip:

OPSWAT Central Management utilizes the secure and widely adopted industry standard **Security Assertion Markup Language 2.0** (**SAML 2.0**), allowing users to seamlessly integrate with any popular identity provider that also supports SAML 2.0.

To begin the integration process, navigate to your identity provider’s (IdP’s) website and follow their instructions for configuring an SSO application. In this case, the SSO application is being configured for OPSWAT Central Management.

## [To integrate OPSWAT Central Management with your own SSO service](/docs/ocm/knowledgebase/how-can-i-provision-users-from-our-own-single-sign-on-service-to#to-integrate-opswat-central-management-with-your-own-sso-service)

1. Log into the **OPSWAT Central Management Console** with administrator permissions.
2. Navigate to **Settings>Integrations>Single Sign-On**, then select the **Enable Single Sign On** checkbox.

3. For your own reference purposes, enter an **IdP Name** in the field provided.
4. Click the **Choose File** button to upload the IdP X.509 certificate *.pem* file, downloaded/received from your IdP.
5. Enter the **Issuer** information that you received from your IdP in the relevant field.
6. Enter the **Idp SSO URL** that you received from your IdP in the relevant field.
7. Enter the **IdP Logout URL** and **Error URL**, if any, that you received from your IdP in the relevant field.
8. Click the **Save** button to implement your changes.
9. Following this implementation, OPSWAT Central Management will issue an **OPSWAT Central Management Login URL** that you must copy and use to update the Postback SSO URL (also known as the Assertion Consumer Service URL) of the SSO application for OPSWAT Central Management that you configured via your IdP.

Pro Tip:

The information required for step 4 though step 8 above can be imported from the IdP metadata file that you received earlier from your IdP, if such a file was made available.

Support:

If you have followed the instructions above but have been unable to **Provision Users From Your Own Single Sign-On Service To OPSWAT Central Management**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
