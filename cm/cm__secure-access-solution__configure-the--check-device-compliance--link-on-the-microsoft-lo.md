<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/configure-the--check-device-compliance--link-on-the-microsoft-lo -->

# Configure the "Check Device Compliance" link on the Microsoft Login Page

End users may inquire why they are unable to authenticate into their applications using their Microsoft account and what actions are required to regain access. In such cases, organization administrators may need to configure the "Check Device Compliance" link on the Microsoft login page to redirect users to the My OPSWAT Central Management remediation page.

![](https://uploads.developerhub.io/prod/97qW/tgkt2a9bdfbrf2ewasng4zx6vhna0r7hnx9gddkjufsiegqst2fgi82vro0qgyue.png)

## Prerequisites

To utilize this feature, you need to enable cross-domain API integration in **Settings** > **Integrations** > **Endpoint Identity**

![](https://uploads.developerhub.io/prod/97qW/f4oeppem2l38xgedqq0gi6p3qotvjm3q7xu3g471ed2ifdtz5s8x1txm0ogc8akm.png)

1. To obtain your My OPSWAT Central Management Remediation URL sign in to the My OPSWAT Central Management console and go to **Secure Access > Access Methods > Microsoft Entra ID**

![](https://uploads.developerhub.io/prod/97qW/nl8knoukp1h1apsr76cpv702h7ut9f2hp54a5fxnumawro7a86b62ayhtm471saw.png)

2. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com/) as an [Organizational Branding Administrator](https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/permissions-reference#organizational-branding-administrator).
3. Navigate to **Identity > User experiences > Company branding**

![](https://uploads.developerhub.io/prod/97qW/l5gtuqwcxu66tq6x5hwdn0o7aat8q6h2xrgfla9iv9ecqq6u22ne7b367gyvt470.png)

4. On the **Sign-in** form tab, Navigate to the **Sign-in page** **text** section and input as follows

`In case you can not log in, you can [**Check your device Compliance**](Remediation URL) and log in again in a few minutes.`

![](https://uploads.developerhub.io/prod/97qW/v4n6i5mieiqtvxlihghlvn4cicaw0mt6s3hvf7emahutuuvta6lrcftm29f2xdkf.png)

5. Click **Review** to review your changes and when you are done, select the **Save** button

> **Notice**
>
> The My OPSWAT Central Management Remediation URL will be changed after revoking the registration code from **Settings > Global > Account**. If you are utilizing this feature and are planning to revoke your registration code, remember to obtain the new Remediation URL and make updates on your Entra Company Branding accordingly afterward.

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
