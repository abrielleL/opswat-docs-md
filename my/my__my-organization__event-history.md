<!-- source: https://www.opswat.com/docs/my/my-organization/event-history -->

# Event History

> **Who can use this feature?**
>
> - **User type:** [Organization User](https://www.opswat.com/docs/my/get-started/user-types-in-my-opswat-portal#organization-user)
> - **Role:** View only on [Event History](https://www.opswat.com/docs/my/my-organization/single-organization#role-objects-and-permissions)

As an organization admin or a user with **View only access** on **Event History** role object, you can access all events that happened within your organization by navigating to ***My Organization > Event History***

![](https://uploads.developerhub.io/prod/JYvy/abcj219h783dbptxxax2creetqf085xeg8x2tmvya83jzme9cjlmvbpbk3cye0ck.png)

The following events are available.

- **Invite**: A new user has been invited to the organization. The **Impacted** column shows the invited user's email address.
- **Change:** Settings have been changed. The details of the change are displayed in the **Old Value** and **New Value** columns.
- **Remove:** A user has been removed from the organization. The **Impacted** column shows the removed user's email address.
- **Sign In:** A user has just logged into My OPSWAT.
- **Sign Out:** A use has just logged out of My OPSWAT

The following changes are also recorded:

- **Default Support Case Watchers:** turning default watchers on or off, adding a default watcher, and removing a default watcher, including the option selected for the contact's open cases. See [Default Support Case Watchers](https://www.opswat.com/docs/my/my-organization/notifications).
- **Unassigned license keys visible:** changing the setting in ***My Organization > Settings***. See [Unassigned license keys visible](https://www.opswat.com/docs/my/my-organization/security#unassigned-license-keys-visible).
- **License edits:** changes to the key owners, note or PO Number of a license key. See [Edit a license](https://www.opswat.com/docs/my/license-management/my-organization-license#edit-a-license).
- **Deployment edits:** changes to the description or deployment owners of a deployment. See [Edit a deployment](https://www.opswat.com/docs/my/license-management/manage-active-deployments#edit-a-deployment).

When owners are cleared automatically, for example because a user is removed from the organization, the change is recorded as made by the system. Edits to a license of a sub-organization are recorded in the Event History of the sub-organization that owns the license.

---

[All pages in this documentation](https://www.opswat.com/docs/my/llms.txt)
