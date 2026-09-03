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
