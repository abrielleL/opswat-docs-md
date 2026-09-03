<!-- source: https://www.opswat.com/docs/cm/knowledge-base/why-can-one-user-in-the-org-see-inventory-devices-while-another- -->

# Why can one user in the org see inventory devices while another cannot in My OPSWAT Central Management?

## **Issue**

A user in the same organization is unable to see devices listed in the **Devices Inventory** within My OPSWAT Central Management, while another user can.

## **Cause**

Access to the devices inventory is tied to console user permissions. If a user has not been invited as a **console user** to the account, they will not be able to view devices.

## **Resolution**

To ensure all relevant users can view devices in the inventory, the user that manages the account must invite them as console users.

### Step 1: Invite a Console User

1. Log in to **My OPSWAT Central Management**.
2. Navigate to: **User Management > Users > Console Users**.
3. Click **Invite Console User**.

![](https://uploads.developerhub.io/prod/97qW/ann14d6e7zk1rbdofflrjym6tq74hq6xhlefuvjec8h1y82mh8xzwl6hyuir6s07.png)

4. In the invitation popup:
   - Select the appropriate **user role**.
   - Enter the **email address** of the person to be invited.
5. Enter your **PIN** to confirm the action.
6. Click **Invite**.
7. The invited user will receive an **email invitation**.

### Step 2: Accept the Invitation

Each invited user must accept the invitation to gain access:

1. Log in to **My OPSWAT Central Management**. 2. Navigate to: **OCM > Username (top right corner) > Manage Account**. 3. Click **Accept** next to the invitation. 4. Click **Switch** to access the organization’s OCM console. - Optionally, click **Make default** to automatically enter this console on future logins.

![](https://uploads.developerhub.io/prod/97qW/u7wfn97t2ew80aq9kd3zuid2e4hzs0exucv2bu3313bx53luglt2jeia7xxlo59v.png)

Once completed, the user will have access to the same devices in the inventory as other console users in the organization.

> **Support:**
>
> If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
