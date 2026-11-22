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

![](https://uploads.developerhub.io/prod/JYvy/04osq0zm4zk06sx3qpzwo4ah3c5nh9mx5pmaxqlu3ayymkyarrmienm2o2ls0wbz.png)

| Field | Description |
| ---- | ---- |
| Product Name | Name of the OPSWAT product. |
| License Key | License keys associated with the OPSWAT Product. |
| Status | Active, Expiring or Expired. |
| Start Date (UTC) | The date when the license becomes effective. |
| Expiration Date (UTC) | The expiration date of the license. Please note License start and expiration dates are shown in **UTC (UTC+0)** for consistency across all environments and time zones. This may look different from other features of My OPSWAT Portal that use your local time zone. |
| NewEntitlement | Maximum licensed instances. - **Regular license:** You purchase a fixed number of product instances, and each instance is activated individually against the OPSWAT Activation Server. Hover to see   - **Max Instances**: number of product instances the license covers   - **Deployed instances:** how many of those instances are currently activated   - For OPSWAT Central Management (CM7), My OPSWAT On-premises (CM8), My OPSWAT Central Management (CM10), MetaDefender Kiosk Linux, and MetaDefender Endpoint licenses, hovering will additionally show the **Max devices** value. - **Volume license:** A licensing model managed through OLMS (On-Premises License Management Server). Product instances connect to OLMS locally to obtain a license; when an instance stops, its license is automatically released and can be reused by another instance. Hover to see   - **Max Instances**: maximum concurrent instances that can hold a license   - **Max Offline Time**: maximum minutes an instance can continue using its license while disconnected from OLMS |
| Type | Evaluation/Purchased - **Evaluated Licenses:** Temporary licenses used for evaluating a product. - **Purchased Licenses**: Licenses for on-premises products that have been purchased by the user account. |
| NewOwner | The users assigned as owners of the license key. Their full names are shown; hover to see their email addresses. If there are more than two owners, the first two are shown followed by **+N more**, and hovering shows the full list. Shows `-` when no owner is assigned. |
| NewPO Number | Your organization's own reference for the license key, for example for internal tracking, renewals or finance. It is not OPSWAT's order number. Shows `-` when empty. |
| Note | Custom remarks for each license key. |

> **View licenses across main and sub‑organizations**
>
> If your organization uses a hierarchy (main organization + sub‑organizations), please refer to [Organization and its sub-organizations' Licenses](https://www.opswat.com/docs/my/license-management/my-main-sub-organizations-licenses)

### Actions

Depending on your permission level on the **License Management** role object, you have access to different actions:

| Permission | Description |
| ---- | ---- |
| **None** | - **Activate License:** Activate a license for the selected product. Please refer to [Activate License](https://www.opswat.com/docs/my/license-management/activate-license) for details. - View **personal** MetaDefender Cloud licenses - View personal MetaDefender IT Access License |
| **View Only** | - **Pin:** Move the license to the top of the section for better visibility and quick access. - **See full License History:** View the full license history *(expired ones are hidden by default).* - **Download Product Installer:** Open the installer download dialog. - **Filter** by Product name, license status, license type, **Owner** (including **No owner**) and **Deployment Owner**. You can select several owners in each owner filter. A license matches the **Deployment Owner** filter when any of its deployments has a selected owner. - **Search** by License key, Product name, Note, PO Number and deployment description. A license matches a description when any of its deployments, whatever its status, has a matching description. Search matches part of the text, is not case-sensitive, and works together with the selected filters. |
| **Full Access** | - View organization's MetaDefender Cloud licenses - **Edit:** Edit the key owners, note and PO Number of the license. This action replaces **Edit note**. See [Edit a license](https://www.opswat.com/docs/my/license-management/my-organization-license#edit-a-license). - **Manage Active Deployment Report:** see every active deployment associated with a license key and, and deactivate Core deployments. Further reading at [Manage Active Deployments](https://www.opswat.com/docs/my/license-management/manage-active-deployments) - **Edit deployment:** In **Manage Active Deployments**, edit the description and deployment owners of an active deployment. See [Edit a deployment](https://www.opswat.com/docs/my/license-management/manage-active-deployments#edit-a-deployment). |

> **Info**
>
> If you're not belong to any organization, you’ll only see the cloud-based product licenses specifically associated with your personal user account.

### Edit a license

As a user with **Full Access** on the **License Management** role object, you can record who owns a license key, add a note, and add your own PO Number. For licenses of a sub-organization, you need **Full Access** on **License Management - Sub Organizations** (see [Organization and its sub-organizations' Licenses](https://www.opswat.com/docs/my/license-management/my-main-sub-organizations-licenses)).

1. In the **On-Premises Product Licenses** list, click the **three-dot icon** next to the license key.
2. Select **Edit**.
3. In the **Edit License** dialog, update any of the following fields:
   - **Key Owners:** select one or more active users of the organization that owns the license key. You can search by name or email, and there is no limit on the number of owners.
   - **Note:** your remarks for the license key.
   - **PO Number:** optional free text, up to 50 characters, for your own reference such as internal tracking, renewals or finance. It is not OPSWAT's order number and is never filled in automatically.
4. Click **Save**. The button stays disabled until you change a value.

![](https://uploads.developerhub.io/prod/JYvy/2ts4jiy3eb9mjrq49r1kay3xawdrbqnohvsb5elca0sgep0hespn8n7u3bdpeely.png)

You can edit active, expiring and expired licenses. The **Owner** and **PO Number** of a license key are also shown in **See full License History**.

> **Info**
>
> Key owners are for your records. They do not change anyone's permissions, and License Management still shows every license to users with access. Their only effect is on which license keys are suggested to a user when they [submit a support case](https://www.opswat.com/docs/my/support-services/submit-a-case), together with the [Unassigned license keys visible](https://www.opswat.com/docs/my/my-organization/security#unassigned-license-keys-visible) setting.

When a user is removed from your organization or set to Inactive, they are removed from the owners of every license key of the organization. Every edit is recorded in [Event History](https://www.opswat.com/docs/my/my-organization/event-history).

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

---

[All pages in this documentation](https://www.opswat.com/docs/my/llms.txt)
