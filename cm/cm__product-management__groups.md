<!-- source: https://www.opswat.com/docs/cm/product-management/groups -->

# Groups

The Inventory>Groups feature in My OPSWAT Central Management enables organizations to categorize and manage assets efficiently by providing structured oversight of endpoints, product instances, users, applications, and network devices, ensuring optimized security enforcement and policy. It enhances **visibility, security enforcement, and operational efficiency** and also allow IT and security teams to automate policies, enforce compliance, and respond to threats in a scalable and proactive manner.

My OPSWAT Central Management auto-creates a default group for each product when your account is set up.

The groups page gives you an overview about all product groups within your account includes product type, what policy assigned to that group, how many devices/instances in that group and the last update.  You can also perform some actions such as

- Create a new group
- Delete a group. Please note that you could not delete a default group of each product.

> **Info**
>
> Please note that each group can only contain one type of product. You could not assign devices/instances from multiple products to one group.

## Create a new group

- Navigate to Inventory --> Groups
- Click "Create New Group".
- Select what product you would like to create a group
- Follow the create group wizard to fill required information or enable settings you desired for each product type such as
  - Name: this must be a unique name
  - Policy: select a policy of the product you would like to assign to the new group
  - Assign devices/instances to the group. This can be done later.
- Click Create to create a new group

## Update a group

1. Navigate to Inventory --> Groups
2. Click on a group you want to update.
3. You can view devices/instances assigned to this group.
4. Via the **Actions** drop-down menu, you can make changes to selected devices in the group. If you want to assign more devices to this group, click on **Add Devices To Group.**
5. You can choose to assign a new policy or update other settings in Settings tab

## Delete a group

- Navigate to Inventory --> Groups
- Click the trash bin icon on the right side of a group you would like to delete
- Click Delete to confirm your action

Please note that

- if there are any devices/instances belong to the deleted group, they will be moved to the default group of that product
- endpoints belong to the deleted group will be re-assessed with a policy assigned to the default endpoint group.
