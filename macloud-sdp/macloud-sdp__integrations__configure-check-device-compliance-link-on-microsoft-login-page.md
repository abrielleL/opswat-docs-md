<!-- source: https://www.opswat.com/docs/macloud-sdp/integrations/configure-check-device-compliance-link-on-microsoft-login-page -->

# Configure the "Check Device Compliance" link on the Microsoft login page

End users may inquire why they are unable to authenticate into their applications using their Microsoft account and what actions are required to regain access. In such cases, organization administrators may need to configure the "Check Device Compliance" link on the Microsoft login page to redirect users to the MetaDefender IT Access remediation page.

## [Prerequisites](/docs/macloud-sdp/integrations/configure-check-device-compliance-link-on-microsoft-login-page#prerequisites)

To utilize this feature, you need to enable cross-domain API integration in **Settings** > **Integrations** > **Endpoint Identity**

1. To obtain your MetaDefender IT Access Remediation URL sign in to the MetaDefender IT Access console and go to **Secure Access > Access Methods > Microsoft Entra ID**

2. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/) as an [Organizational Branding Administrator](https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/permissions-reference#organizational-branding-administrator).
3. Navigate to **Identity > User experiences > Company branding**

4. On the **Sign-in** form tab, Navigate to the **Sign-in page** **text** section and input as follows

`In case you can not log in, you can [**Check your device Compliance**](Remediation URL) and log in again in a few minutes.`

5. Click **Review** to review your changes and when you are done, select the **Save** button

Notice

The MetaDefender IT Access Remediation URL will be changed after revoking the registration code from **Settings > Global > Account**. If you are utilizing this feature and are planning to revoke your registration code, remember to obtain the new Remediation URL and make updates on your Entra Company Branding accordingly afterward.
