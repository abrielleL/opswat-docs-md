<!-- source: https://www.opswat.com/docs/my/my-organization/security -->

# Settings

> **Who can use this feature?**
>
> - **User type:** [Organization user](https://www.opswat.com/docs/my/get-started/user-types-in-my-opswat-portal#organization-user)
> - **Role:** Full Access on [Settings Management](https://www.opswat.com/docs/my/my-organization/single-organization#role-objects-and-permissions)

As an organization admin, or a user with **Full Access on Settings Management** role object, you can manage your organization's settings by navigating to ***My Organization > Settings***. This tab was previously named **Security**.

![](https://uploads.developerhub.io/prod/JYvy/263pw112vye03djp16hh9pfc6pzqizcnha7h8v0op47cg2j4p2g5kltlkbz792vz.png)

### Multi-Factor Authentication

> **Info**
>
> Beginning **June 17, 2026**, Multi-Factor Authentication (MFA) will be mandatory for all users, except for those who authenticate using their organization's own Identity Provider (IdP). Therefore, organization-level MFA settings will no longer be available.

### Data Retention

By default, [Event History](https://www.opswat.com/docs/my/my-organization/event-history) is stored for **30 days** for new organizations. As a user with permission, you can adjust this retention period to any value between **1 and 365 days**.

When an event is recorded, its expiration is calculated as: **Event Timestamp + Retention Period (in days)**

> **Info**
>
> Changes to the retention value apply only to events logged after the setting is updated. Existing event records will expire based on the retention period active at the time they were recorded.

### AI Assistance

This setting allows you to manage whether your organization uses AI assistance in the Portal. By default, AI assistance is **enabled** for all organizations.

As a user with permission, you can disable if your organization has restrictions on using AI-powered services.

> **Info**
>
> This setting can be changed at the main organization level. Sub-organizations inherit the setting from their parent. If you're landing at a sub-organization, the setting is disabled with message:
>
> "*This setting is inherited from parent organization <main organization name>. Only an administrator of <main organization name> can change this setting*.”

> **Info**
>
> If the setting is disabled with the below message, contact our support team for assistance.
>
> *"You can’t change this setting because your organization configuration is incomplete. Please contact* [*our support team*](https://my.opswat.com/portal/support) *to complete the setup so you can manage this setting yourself."*

When AI Assistance is disabled, the following changes will apply to Support features within the Portal:

![](https://uploads.developerhub.io/prod/JYvy/jfii5idx7d85p7cvyti2ajrbl6m44z08shq569dv4wq2f9oj3aclzi3rx0e7vq23.png)

- The **Search** bar on Support page is hidden.
- The **Submit a Case** button appears directly.
- The **Chatbot** in the right corner remains visible and connects directly with human support.
- The “Suggest Knowledge Base” step is removed from [case submission](https://www.opswat.com/docs/my/support-services/submit-a-case).

> **Please note**
>
> If an administrator updates the AI Assistance setting, changes only apply on the user's next login.

### Unassigned license keys visible

This setting decides whether license keys with no owner are also suggested to users of your organization when they [submit a support case](https://www.opswat.com/docs/my/support-services/submit-a-case). By default, the setting is **on**, so keys with no owner are suggested along with the keys a user owns.

The helper text in the portal reads: *"When on, license keys with no owner are also suggested when users submit a support case. When off, users are only suggested the keys they own."*

![](https://uploads.developerhub.io/prod/JYvy/eozoy952h3co4m48wgawfcs2y45ofnh05tpy8vlsu911xu7tlyudfos6k0d1fct1.png)

Turn the setting off if your organization assigns key owners and you want users to be suggested only the license keys they own. You assign key owners in License Management, see [Edit a license](https://www.opswat.com/docs/my/license-management/my-organization-license#edit-a-license).

This setting does not change what License Management shows. Each organization has its own setting, and a sub-organization sets its value in its own ***My Organization > Settings*** tab. Changes are recorded in [Event History](https://www.opswat.com/docs/my/my-organization/event-history).

---

[All pages in this documentation](https://www.opswat.com/docs/my/llms.txt)
