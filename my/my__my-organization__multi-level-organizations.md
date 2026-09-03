<!-- source: https://www.opswat.com/docs/my/my-organization/multi-level-organizations -->

# For Organization with Sub-organizations

> **Who can use this feature?**
>
> - **User type:** [Organization user](https://www.opswat.com/docs/my/get-started/user-types-in-my-opswat-portal#organization-user)
> - **Role:**
>   - View Only/Full Access on [User Management - Sub Organizations](https://www.opswat.com/docs/my/my-organization/multi-level-organizations#sub-organization-custom-roles)
>   - View Only/Full Access on [Role Management - Sub Organizations](https://www.opswat.com/docs/my/my-organization/multi-level-organizations#sub-organization-custom-roles)

If your organization operates with sub-organizations, the My OPSWAT Portal allows you to manage users and roles across all levels efficiently.

> **Please note**
>
> By default, organizations are set to **Single Organization mode**. To enable sub-organization management, contact OPSWAT Support or your Customer Success Manager.

## User Management in Multi-level Organizations

To oversee users across your organization and its sub-organizations, the following conditions must be met:

- **Sub-Organization Management Enabled:** Your organization must have the "Manage Sub-organizations" setting enabled. Submit a support ticket or contact your Customer Success Manager to request this.
- **User Management Permission:** You have **View Only** or **Full Access** on the **User Management** role object. (See [Roles](https://www.opswat.com/docs/my/my-organization/single-organization#custom-roles) for details).
- **Sub-Organization User Permission:** You must have **View Only** or **Full Access** permission on the **User Management - Sub Organizations** role object. Request your organization's Admin to grant this permission if necessary. (Refer to [Sub-organization Roles](https://www.opswat.com/docs/my/my-organization/multi-level-organizations#sub-organization-custom-roles) for details)

![](https://uploads.developerhub.io/prod/JYvy/k78t1hc51w0at7trrefjr7y9bxn80efgqad1jxpr95f2i8fqysqu224h7gzl3xrv.png)

Access the **Users** tab via **My Organization > Users** to:

- **Filter users by**
  - Organization (by selecting the organization in the dropdown list)
  - Status (Active or Pending or Inactive)
  - Roles (User, Admin, Super Admin and custom roles of all selected organizations)
- **Search all users** by **Role Name** or **Email**
- **Invite new users to** the current organization and assign them roles. See [Invite Users to Your Organization](https://www.opswat.com/docs/my/my-organization/single-organization#invite-users-to-your-organization)
- **Accept user's request** to join organization. See [Accept User Request to Join Organization](https://www.opswat.com/docs/my/my-organization/single-organization#accept-user-request-to-join-organization)
- **Remove Users** from the current organization as needed.
- **Export** visible data in the **Users** tab directly to an Excel file.
- **Create sub-organizations**. When a sub-organization is created, the creator is automatically assigned the **Super Admin** role for that sub-organization.
- **Join sub-organizations:** Admins can add themselves to sub-organizations without any users by navigating to the three-dot menu > **Join Organization** > **Confirm**. By default, they are assigned as the Super Admin of that sub-organization and cannot leave if they are the sole Super Admin.

![](https://uploads.developerhub.io/prod/JYvy/73k5ivwktipsdewxfy56sqnlwz0as4xoo62dam5pw73qkbka4b5ubrpysbzbfyb2.png)

> **Please note**
>
> To manage users (invite or remove) in sub-organizations, authorized users must switch to the respective sub-organization.

### Set a user as Inactive

Instead of removing a member, you can set them to Inactive to turn off their access while keeping their account on record for audit purposes.

You can only deactivate users in your **main organization**. Users that belong to a sub-organization are view-only in the combined Users list and cannot be deactivated from here.

1. Go to **My Organization** and select **Users**.
2. Find the user in your main organization in the list.
3. Select the action button (three dots) on the user's row, then select **Deactivate**.
4. Review the confirmation dialog and select **Confirm**.

![](https://uploads.developerhub.io/prod/JYvy/s762mp9i23itmf1whjufp8dz4dx1jy9h02bcfcy911x5to1aa6jyiurg1tm0kp9j.png)

**What happens when a user is set to Inactive:**

- The user's status changes to Inactive in your organization only.
- Their role is preserved, so you do not need to reassign it if you reactivate them later.
- The user's active session for the organization ends immediately.
- The organization is removed from the user's account, so it no longer appears in their organization switcher on next sign-in.
- The user receives a notification in their bell and an email letting them know their access has changed.

To restore access, select the action button on the same user's row, choose **Activate**, and confirm. The user's previous role and access are restored.

Use the **Status** filter on the Users tab to review active or inactive members.

> **Info**
>
> Setting a user's status requires **Full Access** on User Management. The Deactivate/Activate action is available for users in your **main organization** that you're landing only and is hidden for the organization's Super Admin, for your own account, and where you lack permission.

## Role Management in Multi-level Organization

To oversee roles across your organization and its sub-organizations, the following conditions must be met:

- **Sub-Organization Management Enabled:** Your organization must have the "Manage Sub-organizations" setting enabled. Submit a support ticket or contact your Customer Success Manager to request this.
- **Role Management Permission:** You have **View Only** or **Full Access** on the **Role Management** role object. (See [Roles](https://www.opswat.com/docs/my/my-organization/single-organization#custom-roles) for details).
- **Sub-Organization Role Permission:** You must have **View Only** permission on the **User Management - Sub Organizations** role object. Request your organization's Admin to grant this permission if necessary. (Refer to [Sub-organization Roles](https://www.opswat.com/docs/my/my-organization/multi-level-organizations#sub-organization-custom-roles) for details)

![](https://uploads.developerhub.io/prod/JYvy/1upt7dh6z3th35rfd2knrukb1s99pvkwj104iq3xmobz8k9cgkovd1nvz1rlf1jf.png)

Access the **Roles** tab via **My Organization > Roles** to:

- **Filter Roles** by
  - Organization (by selecting the organization in the dropdown list)
  - Status (Active or Pending)
  - Roles (User, Admin, Super Admin and custom roles of all selected organizations)
- **Search**: Quickly search for roles by **Name** or **Description**.
- **User List by Role**: Click on the "**Number of Users**" associated with a role to directly navigate to the **Users list**, with filters applied to the selected **Organization** and **Role**
- **Add new custom roles** to the current organization. To add roles to sub-organizations, authorized users must switch to the respective sub-organization.

### Built-in Roles

In multi-level organizations, built-in roles retain all permissions from the [Single Organization](https://www.opswat.com/docs/my/my-organization/single-organization#predefined-roles) setup, with **additional capabilities to manage sub-organizations**.

Please see the table below for a detailed permission breakdown.

|  | Super Admin | Admin | User |
| ---- | ---- | ---- | ---- |
| Number of users | 1 | Multiple | Multiple |
| Super Admin ownership | Can transfer to another Admin | None | None |
| **Role Object** | **Permissions** |  |  |
| Critical Alerts | Full Access | Full Access | View Only |
| Event History | View Only | View Only | View Only |
| License Management | Full Access | Full Access | View Only |
| Organization General Information | Full Access | Full Access | View Only |
| Role Management | Full Access | Full Access | View Only |
| Security Management | Full Access | Full Access | View Only |
| Support Service - Organization Cases | Full Access | Full Access | View Only |
| Support Service - Partner Cases | Full Access | Full Access | View Only |
| User Management | Full Access | Full Access | View Only |
| **Sub-Organization Permissions** |  |  |  |
| License Management - Sub Organizations | Full Access | Full Access | None |
| Role Management - Sub Organizations | View Only | View Only | None |
| User Management - Sub Organizations | Full Access | Full Access | None |

### Sub-organization Custom Roles

My OPSWAT Portal allows you and other authorized users to manage roles for sub-organizations similarly to manage roles for a single organization, please check [Single Organization Custom Roles](https://www.opswat.com/docs/my/my-organization/single-organization#custom-roles)

With **Sub-Organization Management Enabled**, additional role configurations become available.

| Role objects | None | View Only | Full Access |
| ---- | ---- | ---- | ---- |
| **License Management - Sub Organization** *Prerequisite:* *Full Access or View Only permission on the* ***License Management*** *role object.* | View licenses, but they are not categorized by sub-organization. All licenses appear in a single list without indication of which belong to sub-organizations. | View licenses categorized by sub-organization, including functions like **Active License** and **See Full License History** | Includes **View Only** permissions and adds the ability to **Download Active Deployment Report** and **View Organization's MetaDefender Cloud License** |
| **Role Management - Sub Organizations** *Prerequisite:* *Full Access or View Only permission on the* ***Role Management*** *role object.* | No access to sub-organization's role data. | View the list of roles in the sub-organizations; cannot make changes. | -  |
| **User Management - Sub Organizations** *Prerequisite:* *Full Access or View Only permission on the* ***User Management*** *role object.* | No access to users of sub-organizations. | View, search, and filter users of sub-organizations. Export user list to excel file. | Includes **View Only** permissions and adds the ability to **create new sub-organizations** for the current organization. |
