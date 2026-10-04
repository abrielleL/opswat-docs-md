<!-- source: https://www.opswat.com/docs/cm/product-management/password-storage -->

# Password Storage

Password Storage is a feature in My OPSWAT Central Management that lets you manage MetaDefender Core archive passwords centrally, across your entire Core fleet, instead of maintaining them on each Core instance individually.

> **Feature Availability**
>
> This feature supports MetaDefender Core version 5.23.0 or later.

To access the feature, navigate to **File Security > Password Storage**.

- [Creating a Password Storage](https://www.opswat.com/docs/cm/product-management/password-storage#creating-a-password-storage)
- [Adding a Password to Storage](https://www.opswat.com/docs/cm/product-management/password-storage#adding-a-password-to-storage)
- [Assigning a Storage to Policies](https://www.opswat.com/docs/cm/product-management/password-storage#assigning-a-storage-to-policies)

## Before You Begin

Keep the following in mind before creating password storages:

|  |  |
| ---- | ---- |
| **Supported products** | Password Storage currently only applies to **MetaDefender Core version 5.23.0 or later** |
| **Permissions** | Your user role must include the **Password Storage** permission. Users with write permission have full control. Users without it can view and search, but cannot create, edit, delete, or assign storages. See [Role Management](https://www.opswat.com/docs/cm/user-management/role-management) for configuration details |
| **Assign to policy** | A password storage takes effect only after it is **assigned to a Core policy**. Creating a storage and adding passwords to it has no effect on any instance until you assign it. See [Assigning a Storage to Policies](https://www.opswat.com/docs/cm/product-management/password-storage#assigning-a-storage-to-policies) |
| **Passwords cannot be retrieved** | Once you save a password,** you cannot view it again**, not even as an administrator. You can only replace it with a new value or delete it. Keep your own record of any password you may need to reference elsewhere |
| **Storage capacity** | Each password storage holds **up to 10 passwords** |
| **Password length** | **Up to 64 characters** for standard Latin characters; fewer if the password contains accented or non-Latin characters |
| **Audit log** | Every create, edit, delete, assign, and unassign action is logged with the user and timestamp, giving you a full trail for compliance or troubleshooting. |

## **Main Screens**

| Navigation | Details |
| ---- | ---- |
| File Security > Password Storage | This page lists all password storages in your account. Each row displays: 1. Storage name & description  2. Number of passwords it holds 3. Number of policies it is assigned to 4. Date and time of created 5. Last modified date and time ![](https://uploads.developerhub.io/prod/97qW/lqx9hx2iqq8iwqirlqb4gqmtsusvgr90df7vl0kwdsuyimkz93chtu9fdp9jbh41.png) |
| Select a storage from the list to open its detail page | The page shows two sections:  - **Summary**: total passwords used out of the 10-password limit, date added, and last updated - **Assigned Policies**: every policy the storage is currently assigned to ![](https://uploads.developerhub.io/prod/97qW/2h50cxzpzohugpw5tu14imx6l1uy8u8353m9x580h7p8tav37iz1o6v2km9euzc6.png) |

## Creating a Password Storage

1. On the Password Storage page, select **Add Password Storage**
2. In the dialog that appears, fill in the following fields:
   1. Enter a **Name** and **Description**
   2. Type password value. Click Add Password to add one or more passwords
3. Click** Add **to save

![](https://uploads.developerhub.io/prod/97qW/jmnovjeco0j85admrnuv9ue8e87mjop9abv4hv354yg2h53d6tbvwt0h821hlayi.png)

After creation, the storage is unassigned. Assign it to one or more policies to make the passwords available to Core instances. See [Assigning a Storage to Policies.](https://www.opswat.com/docs/cm/product-management/password-storage#assigning-a-storage-to-policies)

## Managing Passwords

Open a storage to manage the passwords it holds. Each password entry shows when it was added and when it was last changed. The password value itself is never displayed after it is saved.

### **Adding a Password to Storage**

1. Open a storage
2. Select **Add password**
3. Type the password value. Select **Add Password **to add one or more passwords
4. Click** Add **to save

![](https://uploads.developerhub.io/prod/97qW/jnr20l8gf6j4rt67rzccvcqoe7v38z30zgah6btucoi889r3ml23r3pwhsfx9vak.png)

### Delete a Password Storage

On the Password Storage page, click the icon on the row of the storage you want to delete. Click **Delete** to confirm, or **Cancel** to go back.

![](https://uploads.developerhub.io/prod/97qW/yz55krankcef4hav7glug61btzb7qx6czhx82l1qanflcyiufzklbub2uftpu7jx.png)

## Assigning a Storage to Policies

Password storages take effect through **MetaDefender Core policies**. A storage can be assigned to multiple policies, and a policy can hold multiple storages at the same time.

> **How synchronization works**
>
> Once a storage is assigned to a policy, every Core instance under that policy receives updates whenever passwords are added, changed, or removed. Offline instances pick up changes the next time they reconnect.

### **Assign a storage to a policy**

1. On the storage detail page, click **Assign to Policy**
2. In the dialog that appears, search by name or browse the list of Policies
3. Select one or more policies using the checkboxes
4. Click **Assign**

Note  Assignments are additive, assigning a new storage to a policy never removes an existing one.

![](https://uploads.developerhub.io/prod/97qW/zmwigtz8h1972dx8narzgyr2rr8sz7bry7ac85da1g8d2svjr7of1s5rzhowyw3a.png)

### **Remove an assignment**

- Click the delete icon on the policy row you want to unassign
- Use the **Select Action** dropdown to perform a bulk action on selected rows

Note Removing an assignment clears that storage from all Core instances under the policy. Other assignments are unaffected.

![](https://uploads.developerhub.io/prod/97qW/p6pbveic5edtas1uf0hpxngm9m9hhwoprueur3um1jut6balu431s6h308jle56z.png)

### **Verify Password Storage has been assigned to Policies**

- Navigate to File Security > Policies.
- Select the policy that password storage has been assigned to
- Open Password Storage tab to verify

## Using a Password Storage in a Workflow Rule

When configuring a MetaDefender Core policy's Archive workflow rule, the password picker lists only the storages assigned to that policy. If it is empty or missing the storage you expect, go to the Password Storage page and assign it to the policy first.

## Troubleshooting

| Issues | Causes | Solutions |
| ---- | ---- | ---- |
| Policy sync fails with "Significant Issues" across MetaDefender Core instances | The policy references an archive password created locally on a single Core instance rather than in My OPSWAT Central Management. Other Core instances do not recognize the password reference and reject the workflow configuration. | **Option 1 (Recommended):** Add the password to **My OPSWAT Central Management**, assign it to the policy, and select it in the Archive workflow rule so it syncs fleet-wide.  **Option 2:** Open the policy's **Archive workflow rule** and **unselect/remove** the local password. |

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
