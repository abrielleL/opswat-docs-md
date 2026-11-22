<!-- source: https://www.opswat.com/docs/my/license-management/manage-active-deployments -->

# Manage Active Deployments

> **Who can use this feature?**
>
> - **User type:** [Organization user](https://www.opswat.com/docs/my/get-started/user-types-in-my-opswat-portal#organization-user)
> - **Role:** Full access on [License Management](https://www.opswat.com/docs/my/my-organization/single-organization#role-objects-and-permissions)

**Manage Active Deployments** allows users to see every active deployment associated with a license key and, for supported products, to self-service deactivate deployments without the need to submit support ticket.

![](https://uploads.developerhub.io/prod/JYvy/7o2r46gn01qo9nl9wxokcg4qune090tpn1fw5zedwai9j6dl9xkwi003rtobn4cv.png)

To view active deployments of a license key:

1. Select **License Management** in the left navigation.
2. Locate a specific license key (not applicable to expired licenses)
3. Click the **three-dot icon** next to the license key
4. Select **Manage Active** **Deployments**.

![](https://uploads.developerhub.io/prod/JYvy/v99gck60zuku4dpycsk9u8olal3gnyycczazchnodv0qro4edaonm814wwrep593.png)

You can

- View all active Deployment IDs associated with the license key.
- Search the list to find a specific Deployment ID.
- Export selected deployment IDs to excel file *(not applicable for* *Expired* *licenses)*
- Select one or multiple Deployment IDs and deactivate them (see below).
- **Edit** the description and deployment owners of an active deployment (see [Edit a deployment](https://www.opswat.com/docs/my/license-management/manage-active-deployments#edit-a-deployment)).
- Search the list by deployment **Description**.

The list also shows each deployment's **Description** and **Deployment Owner**, and the **PO Number** of the license key. The PO Number is view only here; you set it when you [edit the license](https://www.opswat.com/docs/my/license-management/my-organization-license#edit-a-license).

> **NOTE**
> **'Manage Active Deployments'** is not available for Volume licenses.

## Deactivate Deployments

> **NOTE**
>
> Self-service deactivation is currently supported for **MetaDefender Core** licenses only

**To deactivate deployments, follow the below steps**

![](https://uploads.developerhub.io/prod/JYvy/u2yfkr2xmqoum7z8u4z6t3kpxr6thvd9ywk8lqht3w7mrl8i23s6xod580aopaqg.png)

1. Open **Manage Active Deployments** for a MetaDefender Core license key.
2. Select the checkbox next to each Deployment ID you want to deactivate. You can select one or multiple.
3. Click **Remove** to confirm the deactivation.

![](https://uploads.developerhub.io/prod/JYvy/lvlx4ci8lq3srpauf8jo41anoo2lx7kjwyidrgw289kg4o177b8mkc52pkbe580r.png)

The selected deployments are deactivated, and the freed slots become available for reuse. Every activate and deactivate action is recorded in the organization event log. (My Organization > [Event History](https://www.opswat.com/docs/my/my-organization/event-history))

## Edit a deployment

![](https://uploads.developerhub.io/prod/JYvy/gqxhx7gkbvg3fe6rome3p0diqfjq7kkplr7zldhf79t4wzy8gwl1vrs51khmu30x.png)

As a user with **Full Access** on the **License Management** role object (or on **License Management - Sub Organizations** for licenses of a sub-organization), you can edit the description and the owners of an active deployment.

1. Open **Manage Active Deployments** for the license key.
2. Find the deployment and click **Edit** on its row.
3. In the **Edit Deployment** dialog, update any of the following fields:
   - **Description:** optional. The same rules apply as for the description you enter when you [activate a license](https://www.opswat.com/docs/my/license-management/activate-license).
   - **Deployment Owner:** optional. Select one or more active users of the organization that owns the license who have access to License Management in that organization. You can search by name or email, and there is no limit on the number of owners.
4. Click **Save**. The button stays disabled until you change a value.

> **NOTE**
>
> Only active deployments can be edited. For removed and failed deployments, the **Edit** action is disabled.

Deployment owners are for your records and give no extra permissions. Owners are cleared automatically when:

- the owner is removed from the organization or set to Inactive.
- the deployment's status becomes Removed.

If an owner later loses access to License Management, they stay an owner, but they are no longer offered when you pick new owners. Every edit is recorded in [Event History](https://www.opswat.com/docs/my/my-organization/event-history).

---

[All pages in this documentation](https://www.opswat.com/docs/my/llms.txt)
