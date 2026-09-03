<!-- source: https://www.opswat.com/docs/my/license-management/my-organization-license -->

# Organization Licenses

> **Who can use this feature?**
>
> - **User type:** Both [Personal](https://www.opswat.com/docs/my/get-started/user-types-in-my-opswat-portal#personal-user) or [Organization](https://www.opswat.com/docs/my/get-started/user-types-in-my-opswat-portal#organization-user) users
> - **Role:** View only or Full access on [License Management](https://www.opswat.com/docs/my/my-organization/single-organization#role-objects-and-permissions)

Your **Organization Licenses** tab shows all product licenses associated with your current organization.

## Access the Organization Licenses tab

1. Sign in to My OPSWAT Portal
2. Select **License Management** in the left navigation.
3. Click the **Organization Licenses** tab.

---

### No Organization or Licenses

If you’re not in any organization or your organization has no licenses, you’ll see the below message:

![](https://uploads.developerhub.io/prod/JYvy/8ymorfa28jg7ncyliezz884ru5mk7a13xuyzpbeqqe3jcu1erwyfc0rcaiftryd0.png)

### Valid Organization and Licenses

When you belong to an organization that holds licenses and have either **View Only** or **Full Access permission** on **License Management**  (See [Roles](https://www.opswat.com/docs/my/my-organization/single-organization#custom-roles) for details), you’ll see a detailed list of your organization’s licenses.

#### Statistical charts

At the top of the **Organization Licenses** tab, you’ll see **interactive charts** that provides a visual summary of your organization’s licenses. This chart captures key figures of your license data.

![](https://uploads.developerhub.io/prod/JYvy/cdfv6divbdg0jf5hfqnnaj3h8m0e1twg0z84001kqk73s0fgbxl4l4trzflk4oy9.png)

- Hover over pie chart for details
- Click dashboard numbers or pie sections to filter data
- Page scrolls automatically to filtered results in the Details section

#### Detailed Lists of Product Licenses

Below the overview chart, you’ll find a detailed list of your organization’s licenses and personal cloud licenses

**1. Cloud Services:** You can view the limitations associated with your licenses when interacting with the cloud services, such as the number of specific API requests per day.

![](https://uploads.developerhub.io/prod/JYvy/fwr9dtefjlzrwfo4f7xg44pkpfk1pka1szemvwl90p7p8syidrkxziljxh8joumh.png)

**2. On-Premises Product Licenses**: Each license entry includes:

| Field | Description |
| ---- | ---- |
| Product | Name of the OPSWAT product. |
| License Key | License keys associated with the OPSWAT Product. |
| Status | Active, Expiring or Expired. |
| Start Date (UTC) | The date when the license becomes effective. |
| Expiration Date (UTC) | The expiration date of the license. Please note License start and expiration dates are shown in **UTC (UTC+0)** for consistency across all environments and time zones. This may look different from other features of My OPSWAT Portal that use your local time zone. |
| Deployed / Purchased | Number of deployed instances versus purchased limit. |
| Type | Evaluation/Purchased - **Evaluated Licenses:** Temporary licenses used for evaluating a product. - **Purchased Licenses**: Licenses for on-premises products that have been purchased by the user account. |
| Note | Custom remarks for each license key. |

> **View licenses across main and sub‑organizations**
>
> If your organization uses a hierarchy (main organization + sub‑organizations), please refer to [Organization and its sub-organizations' Licenses](https://www.opswat.com/docs/my/license-management/my-main-sub-organizations-licenses)

### Actions

Depending on your permission level on the **License Management** role object, you have access to different actions:

| Permission | Description |
| ---- | ---- |
| **None** | - **Activate License:** Activate a license for the selected product. Please refer to [Activate License](https://www.opswat.com/docs/my/license-management/activate-license) for details. - View **personal** MetaDefender Cloud licenses - View personal MetaDefender IT Access License |
| **View Only** | - **Pin:** Move the license to the top of the section for better visibility and quick access. - **See full License History:** View the full license history *(expired ones are hidden by default).* - **Download Product Installer:** Open the installer download dialog. - **Filter** by Product name, license status and license type. - **Search** by License key and Product name |
| **Full Access** | - View organization's MetaDefender Cloud licenses - **Edit note:** Edit the note attached to the license. - **Manage Active Deployment Report:** see every active deployment associated with a license key and, and deactivate Core deployments. Further reading at [Manage Active Deployments](https://www.opswat.com/docs/my/license-management/manage-active-deployments) |

> **Info**
>
> If you're not belong to any organization, you’ll only see the cloud-based product licenses specifically associated with your personal user account.

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

For organizations with sub-organizations, refer to additional details at [Organization and its sub-organizations' Licenses](https://www.opswat.com/docs/my/license-management/my-main-sub-organizations-licenses)
