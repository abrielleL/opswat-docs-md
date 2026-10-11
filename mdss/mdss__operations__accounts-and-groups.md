<!-- source: https://www.opswat.com/docs/mdss/operations/accounts-and-groups -->

# Inventory

The **Inventory** page is where you view and manage all the storage resources that MetaDefender Storage Security (MDSS) protects. From here you can see every storage unit registered for scanning, the groups they are organized into, and the accounts used to connect to your storage providers.

**Access:** Select **Inventory** in the left navigation menu.

### **Tabs**

The page is organized into three tabs:

- **Units** — Individual storage locations registered for scanning (for example, an Amazon S3 bucket or an NFS share).
- **Groups** — Logical collections of units, used to apply shared settings and workflows.
- **Accounts** — The connections and credentials MDSS uses to reach each storage provider.

## Units

Individual storage locations registered for scanning (for example, an Amazon S3 bucket or an NFS share).

To add a new storage unit, please follow the [Integrations](https://www.opswat.com/docs/mdss/integrations/storage-units) page.

## Accounts

### What are Accounts?

Accounts in MetaDefender Storage Security allow you to:

- Store and manage access credentials for storage services in one centralized location (credentials are encrypted and stored securely in the database)
- Associate multiple storage units with a single account for simplified management
- Enable automatic discovery of new storage units for supported services (see [Autodiscovery](https://www.opswat.com/docs/mdss/operations/autodiscovery))
- Organize storage resources within groups for better administration

> **Security Note**
>
> Role-based access control governs all account operations - Administrator, SSO Administrator, and Tenant Administrator roles have full permissions to create, modify, and delete accounts, while Read-Only Administrator and SSO Read-Only Administrator roles cannot perform these actions.

### Creating a New Account

![](https://uploads.developerhub.io/prod/k8zL/cjdo852kyonv7o0pxfqsy14yva4grzx7sufd4adllw4qg3xfpubi0ba280ax384m.png)

To create an account:

1. From the left side menu, navigate to **Inventory** and click **Add New** > **Account**
2. Select the service you want to integrate and click **Next**
3. Fill out the required account's credentials and click **Next**
4. On the **Summary** step, click **Add unit** to add a storage unit to the new account

> **Note**
>
> There are no limits on the number of accounts that can be created.

### Managing Existing Accounts

1. Navigate to **Inventory** and open the **Accounts** tab
2. Locate the account you want to manage
3. Click the **three-dot menu** next to the account name

#### Available Account Actions

![](https://uploads.developerhub.io/prod/k8zL/mb7oehilw1stiumlrygyb8huqdygpakbci42xe9zgrc2h4mqcoajrvj3q51tp1h4.png)

- **Create Job -** Starts instant scans for all storage units under the account. These scans can be monitored through the ongoing scans interface. If individual scans fail, they are handled independently without affecting other scans in the batch.
- **Account Settings** - Opens the account's **Settings** tab to modify account credentials
- **Add unit** - Add a new storage unit in this account
- **Delete Account** - Removes the account

#### Account Settings

![](https://uploads.developerhub.io/prod/k8zL/xqvwpsmoqlffp19uab29fc5nufqfzzlkesd0khtmdjptwronjosxsvp6dnuvi7al.png)

1. From the account's three-dot menu, select **"Account Settings"**
2. The **Settings** tab opens pre-populated with current account details
3. You'll be required to input credentials or credentials file to validate changes
4. Click **"Update"** to update the account

#### Delete Account

1. From the account's three-dot menu, select **"Delete Account"**
2. **Accounts with storage units:** The confirmation message shows the count of associated storage units, which are deleted together with the account
3. **Empty accounts:** Can be deleted after explicit confirmation
4. Confirm the deletion when prompted

> **IMPORTANT**
>
> When accounts are deleted, all associated reports and historical scan data are permanently removed and cannot be exported - there are currently no data export capabilities for this purpose.

## Groups

### What are Groups?

Groups in MetaDefender Storage Security provide an organizational structure for managing storage units and accounts. They enable logical grouping of related storage resources, simplifying administration and enhancing visibility across the system.

Key Features include ways to:

- Organize storage units and accounts in logical collections
- Perform actions on multiple storage units at once
- Clear visual separation of resources in the user interface

> **IMPORTANT**
>
> MDSS groups operate as a single-level organization system without nesting capabilities, and storage units cannot belong to multiple groups simultaneously. All storage units are mandatory to be assigned to a group.

## Default Group

The system includes a default group. This ensures that all storage units and accounts always have a group assignment, even if a custom group is deleted.

- Storage units or accounts can be moved to the default group if their assigned group is deleted
- The default group has a predefined ID and name but can have its description modified

## Creating and Managing Groups

### Creating a New Group

![](https://uploads.developerhub.io/prod/k8zL/n7lh5355lhml0sroqodvvhfl87gmg47l2i73pn4qz0k7n4m3ib4wlu6ryo3nyfmj.png)

Groups can be created from the Inventory page

- Click **Add New** > **Group**
- Enter a **Group Name** (required field)
- Optionally **select existing storage units** in the **Units** field to include in the group
- Click **"Add group"** to finalize

> **Note**
>
> During storage unit creation, the first available group is pre-selected by default. There are no limits on the number of groups that can be created.

### Managing Existing Groups

![](https://uploads.developerhub.io/prod/k8zL/dm5c58k3b70i2jla6w5lwulsrves7pd2zyt6fwfjigqjc7eblzxk7caxqvlsmwrw.png)

1. Navigate to **Inventory** and open the **Groups** tab
2. Locate the group you want to manage
3. Click the **three-dot menu** next to the group name

> **Security Note**
>
> Role-based access control governs all group operations - Administrator, SSO Administrator, and Tenant Administrator roles have full permissions to create, modify, and delete groups, while Read-Only Administrator and SSO Read-Only Administrator roles cannot perform these actions.

#### **Available Group Actions**

**Scan All Group Items**

![](https://uploads.developerhub.io/prod/k8zL/68f9hrfvte5oixqfk2n7birkcyz2empnqdnoz1ytpgabrlutvrpqg0u5isz4s5we.png)

- Starts instant scans for all storage units under the group. These scans can be monitored through the ongoing scans interface. If individual scans fail, they are handled independently without affecting other scans in the batch.

#### **Group Status Information**

**Storage Count Badge**

- Shows the total number of storage units in each group with format: "X storage units"

**Status Badges**

Visual indicators showing:

- **Error Count** - Badge showing storage units with errors
- **Testing/Untested Count** - Badge showing storage units being tested or untested
- **Success State** - No badges when all storage units are operational

**Moving Storage Units Between Groups**

1. From any storage unit's management options(three-dots), select **"Move to Group"**
2. Choose the destination group from the dropdown
3. Confirm the move to complete the transfer

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
