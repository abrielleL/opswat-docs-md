<!-- source: https://www.opswat.com/docs/my/partner-guide/partner-role-management -->

# Roles & Permissions

> **Who can use this feature?**
>
> - **User type:** [Organization user](https://www.opswat.com/docs/my/get-started/user-types-in-my-opswat-portal#organization-user)
> - **Organization type:** Partner organization
> - **Role**: View Only/Full Access on [Role Management](https://www.opswat.com/docs/my/my-organization/single-organization#role-objects-and-permissions)

Besides the role objects available to customer organizations, partner organizations include additional built-in roles and extra role objects.

For the full list of role objects and permissions available to all organizations, see the [Roles](https://www.opswat.com/docs/my/my-organization/single-organization#custom-roles) page.

### Built-in Roles

Partner organizations include **3 standard built-in roles**, plus **2 additional roles**

**Super Admin**

- Holds the highest level of permissions, with **full control** over all organizational functions.
- Each organization can have only **one (1)** Super Admin, automatically assigned to the first Admin added.
- Super Admins can transfer their role to another Admin.

**Admin:** Has full control over all organizational functions, except assigning MDF Admin role to other users.

**User:** Have view-only permission to all data of the organization

**MDF Admin:** Has full control over all organizational function, except user management

**Partner user:** Have view-only permission to all data of the organization, plus ability to submit a deal and manage partner resources.

The table below provides detailed permission breakdown.

|  | **Super Admin** | **Admin** | **User** | **MDF Admin*** | **Partner User** |
| ---- | ---- | ---- | ---- | ---- | ---- |
| Number of users | 1 | Multiple | Multiple | Multiple | Multiple |
| Super Admin ownership | Can transfer to another Admin | None | None | None | None |
| **Role Object** | **Permissions** |  |  |  |  |
| Critical Alerts | Full Access | Full Access | View Only | Full Access | View Only |
| Event History | View Only | View Only | View Only | View Only | View Only |
| License Management | Full Access | Full Access | View Only | Full Access | View Only |
| License Management - Sub Organizations | Full Access | Full Access | None | Full Access | None |
| Hardware Orders - Organization Hardware | View Only | View Only | View Only | View Only | View Only |
| Hardware Orders - Customer Hardware  | View Only | View Only | View Only | View Only | View Only |
| License Management - Customer Organizations | Full Access | Full Access | None | Full Access | View Only |
| Organization General Information | Full Access | Full Access | View Only | Full Access | View Only |
| Role Management | Full Access | Full Access | View Only | View Only | View Only |
| Role Management - Sub Organizations | View Only | View Only | None | View Only | None |
| Security Management | Full Access | Full Access | View Only | Full Access | View Only |
| Support Service - Organization Cases | Full Access | Full Access | View Only | Full Access | View Only |
| Support Service - Customer Cases | Full Access | Full Access | View Only | Full Access | View Only |
| Support Service - RMA Cases | Full Access | Full Access | View Only | Full Access | View Only |
| User Management | Full Access | Full Access | View Only | View Only | View Only |
| User Management - Sub Organizations | Full Access | Full Access | None | View Only | None |
|  | **Super Admin** | **Admin** | **User** | **MDF Admin** | **Partner User** |
| **Channel Partner Portal Role Object** |  |  |  |  |  |
| Channel Partner Portal - Deal Management | Full Access | Full Access | View Only | Full Access | Full Access |
| Channel Partner Portal - MDF ** | Full Access | Full Access | View Only | Full Access | View Only |
| Channel Partner Portal - Organization Playbook | Full Access | Full Access | View Only | Full Access | Full Access |

> **PLEASE NOTE**
>
> (*) Only Super Admin can assign the MDF Admin role
>
> (**) MDF Admin role and Channel Partner Portal - MDF role object is only visible only to OPSWAT Preferred Partners enrolled in the MDF Program. To request enrollment, please contact your dedicated Channel Manager.

### Custom Roles

If you have **Full Access** to **Role Management**, you can **create, modify, or delete roles** tailored to your organization's needs

#### Create a Custom Role

1. Login to My OPSWAT Portal
2. Navigate to **My Organization > Roles**
3. Click on the **"Add Role"** button to create a new user role.
4. Give the new role a **Name** and a **Description** (optional).
5. Adjust the **None, View Only or Full Access** permissions as desired for each role object.

![](https://uploads.developerhub.io/prod/JYvy/cjvmbkp9tx9kxddn0s94ff3ri5ox4ew1jv034i7wvaegujxqp64waf7numy8t1n5.png)

> **PLEASE NOTE**
>
> Default permission for **Channel Partner Portal Role Objects** will be NONE for custom role and cannot be edited, except for Channel Partner Portal - Organization Playbook

#### Role Objects & Permissions

In addition to the [standard role objects](https://www.opswat.com/docs/my/my-organization/single-organization#role-objects-and-permissions), partner organizations have access to the following:

| Role Objects | None | View Only | Full Access |
| ---- | ---- | ---- | ---- |
| **Channel Partner Portal - My Deal Management** *Applies to Partner Portal > Deal Registration tab* | No access |  | Access the page and **Register New Deal** |
| **Channel Partner Portal - Organization Deal Management** *Applies to Partner Portal > Deal Registration tab* | No access | View all deal registrations submitted by your organization |  |
| **Channel Partner Portal - MDF** *Applies to Partner Portal > Marketing Development Funds tab* Please note* This role* *object is only visible only to OPSWAT Preferred Partners enrolled in the MDF Program. To request enrollment, please contact your dedicated Channel Manager.* | No access | Access the page and view all MDF submitted by your organization | Includes View Only permissions and adds the ability to **Request New Fund**. |
| **Channel Partner Portal - Organization Playbook** *Applies to Partner Portal > Resources > Playbooks tab* |  | View playbooks shared by your organization | Create, edit, and delete organization playbooks |
| **License Management - Customer Organizations** *Applies to License Management > Customer Licenses and Customer contracts tab* | No access | View licenses of the customer's organization, including functions like **Active License,** **See Full License History**, **View Organization's MetaDefender Cloud License, See Customer Note and Partner Note.** | Includes View Only permissions and adds the ability to **Download Active Deployment Report, Edit Partner Note.** |
| **License Management - Customer Organizations** *Applies to Hardware Orders > Customer Hardware* | No access | View your customers' hardware inventory and orders. |  |
| **Support Service - Customer Cases** *Applies to Partner Organization has at least one linked customer with a Preferred Partner relationship* | No access | View cases submitted on behalf of customers by other users within the organization | Log cases on behalf on assigned customers |
| **Support Service - RMA Cases** *Applies to Partner Organization has Hardware Orders module* | No access | View RMA cases | Log RMA cases on behalf of customers |
