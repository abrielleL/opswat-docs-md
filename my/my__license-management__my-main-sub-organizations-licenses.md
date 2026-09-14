<!-- source: https://www.opswat.com/docs/my/license-management/my-main-sub-organizations-licenses -->

# Organization and its sub-organizations' Licenses

> **Who can use this feature?**
>
> - User type: [Organization user](https://www.opswat.com/docs/my/get-started/user-types-in-my-opswat-portal#organization-user)
> - Role: View Only/Full Access on  [License Management - Sub Organization](https://www.opswat.com/docs/my/my-organization/multi-level-organizations#sub-organization-custom-roles)

This section outlines how to view and manage licenses for both your main organization and its sub-organizations within My OPSWAT Portal.

To view licenses for your organization and its sub-organizations, the following conditions must be met:

- **Sub-Organization Management Enabled:** Your organization must have the "Manage Sub-organizations" setting enabled. [Submit a support ticket](https://my.opswat.com/portal/support) or contact your Customer Success Manager to request this.
- **License Management Permission:** You have **View Only** or **Full Access** on the **License Management** role object. (See [Roles](https://www.opswat.com/docs/my/my-organization/single-organization#custom-roles) for details).
- **Sub-Organization License Permission:** You must have **View Only or Full Access** permission on the **License Management - Sub Organizations** role object. Request your organization's Admin to grant this permission if necessary. (Refer to [Sub-organization Roles](https://www.opswat.com/docs/my/my-organization/multi-level-organizations#sub-organization-custom-roles) for details)

### Viewing Licenses

If you have the required permissions, you can view and manage licenses for both your main organization and its sub-organizations in a single, unified view.

#### Statistical charts

At the top of the **Organization Licenses** tab, interactive charts provide a summary of all licenses across your selected organizations (main and sub-orgs).

![](https://uploads.developerhub.io/prod/JYvy/9gfuclf17v00tbmutes4oehltn3szng6jfq9ixjt1m4cx4z9rbu4tgdu3owuobi2.png)

- Use the **Select Organization(s)** filter (combo box) to select which organizations to include in the charts and license list.
- The charts update dynamically based on your selection.
- Hover over chart sections for details, or click to filter the license list below.

#### Detailed Lists of Product Licenses

Below the charts, you’ll find a detailed list of licenses for the selected organizations:

**1. Cloud Services:**

![](https://uploads.developerhub.io/prod/JYvy/chv1ojhn2bs758yserqmj7th303j8k3g2idwbuz6xqrzr94z64lk67fij6xhi4up.png)

This section shows personal and organization cloud licenses

- **Personal Cloud Licenses:** Shows the user's own MetaDefender Cloud and My OPSWAT Central Management (SaaS) license information
- **Organization cloud licenses**:
  - **For MetaDefender Cloud:** My OPSWAT Portal displays the main organization’s license information, including the **user's API Key** and **license details.** For sub-organizations, only license details are displayed.
  - **For My OPSWAT Central Management (SaaS):** Since the license is personal, the Portal shows the user's license information for the current organization only.

**2. On-Premises Product Licenses:** Each license entry includes:

| Field | Description |
| ---- | ---- |
| Product | Name of the OPSWAT product. |
| License Key | License keys associated with the OPSWAT Product. |
| Status | Active, Expiring or Expired. |
| Start Date (UTC) | The date when the license becomes effective. |
| Expiration Date (UTC) | The expiration date of the license. Please note License start and expiration dates are shown in **UTC (UTC+0)** for consistency across all environments and time zones. This may look different from other features of My OPSWAT Portal that use your local time zone. |
| NewEntitlement | Maximum licensed instances. - **Regular license:** You purchase a fixed number of product instances, and each instance is activated individually against the OPSWAT Activation Server. Hover to see   - **Max Instances**: number of product instances the license covers   - **Deployed instances: **how many of those instances are currently activated - **Volume license:** A licensing model managed through OLMS (On-Premises License Management Server). Product instances connect to OLMS locally to obtain a license; when an instance stops, its license is automatically released and can be reused by another instance. Hover to see   - **Max Instances**: maximum concurrent instances that can hold a license   - **Max Offline Time**: maximum minutes an instance can continue using its license while disconnected from OLMS |
| Type | Evaluation/Purchased - **Evaluated Licenses:** Temporary licenses used for evaluating a product. - **Purchased Licenses**: Licenses for on-premises products that have been purchased by the user account. |
| Note | Custom remarks for each license key. |

> **For Product Licenses:**
>
> The Portal prioritizes displaying the licenses of sub-organizations. Licenses assigned to both main and sub‑organizations appear **only** under the sub‑organization to avoid duplication.

### Actions

Depending on your permission level on the **License Management - Sub-organization** role object, you have access to different actions:

| Permission | Description |
| ---- | ---- |
| **None** | - **Activate License:** Activate a license for the selected product. Please refer to [Activate License](https://www.opswat.com/docs/my/license-management/activate-license) for details. - View **personal** MetaDefender Cloud licenses - View **personal** MetaDefender IT Access License |
| **View Only** | - **Pin:** Move the license to the top of the section for better visibility and quick access. - **See full License History:** View the full license history *(expired ones are hidden by default).* - **Download Product Installer:** Open the installer download dialog. - **Filter** by Product name, license status and license type. - **Search** by License key and Product name |
| **Full Access** | - View **organization's** MetaDefender Cloud licenses - **Manage Active Deployment Report:** see every active deployment associated with a license key and, and deactivate Core deployments. Further reading at [Manage Active Deployments](https://www.opswat.com/docs/my/license-management/manage-active-deployments) |

## License Expiration Notifications

My OPSWAT Portal provides function called [Critical Alerts Users](https://www.opswat.com/docs/my/my-organization/critical-alert-users) allowing individuals on this list receive to receive automatic alerts for upcoming license expirations—**60 and 30 days in advance**, enabling better planning and prioritization.

![](https://uploads.developerhub.io/prod/JYvy/riz1y7t6ey8rpp47dxtmtoto1rj9bqil7eeqlhfi7vow31gj12q54xdhezlmiebj.png)

**Settings:**

- **For organization admins:** Add add any email address to the list, even if it is not a registered user in My OPSWAT Portal  by navigating to ***My Organization > License >*** [***Critical Alerts Users***](https://my.opswat.com/my-organization/critical-alert-users) ***> Add Users***

### Licenses across your organization hierarchy

If your organization has sub-organizations, this reminder can cover the whole hierarchy in one email. Which version you receive depends on your permissions:

- **Without** View Only or Full Access on the **License Management - Sub Organizations** role object, you receive the reminder for your current organization only. This is also the version sent to any address on the Critical Alerts Users list that does not belong to a My OPSWAT account. (See [Sub-organization Custom Roles](https://www.opswat.com/docs/my/my-organization/multi-level-organizations#sub-organization-custom-roles) for details.)
- **With** View Only or Full Access on **License Management - Sub Organizations**, you receive one reminder covering your main organization and each of its sub-organizations. The licenses are grouped under **Main Organization**, then one group per **Sub-Organization**.

Both versions are sent from noreply@opswat.com, with the subject *[My OPSWAT Portal Notification] - Renewal needed within 30 days* or *[My OPSWAT Portal Notification] - Renewal needed within 60 days*. They cover purchased licenses expiring within 60 or 30 days, and are sent once a day only when there are expiring licenses to report.

A license held by both a main organization and a sub-organization is listed once, under the sub-organization.

![](https://uploads.developerhub.io/prod/JYvy/7yjquib1vu9f1vm7k98woq6fmdy8dnc3jxsp08my9ntd11uh378g35r6uzf2j4m9.png)
