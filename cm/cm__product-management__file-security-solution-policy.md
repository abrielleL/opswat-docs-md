<!-- source: https://www.opswat.com/docs/cm/product-management/file-security-solution-policy -->

# File Security Solution Policy

This document explains how to manage policies for products under File Security Solution.

## **Supported Products**

The File Security Solution Policy applies to the following products:

- MetaDefender Core
- MetaDefender ICAP Server

## Available Actions

1. Log into the My OPSWAT Central Management console.
2. Go to **File Security > Policies,** select the product whose policies you want to view

The following actions are available for all supported products:

| **Available actions** | **What it does** |
| ---- | ---- |
| **Import Policy from Instance** | Import a policy into My OPSWAT Central Management from the configuration of an enrolled instance |
| **Delete** | Permanently removes a policy |
| **Assign Policy to a Group** | Applies a policy to instances in the selected group |
| **Enable "Automatically Sync Group Policy for New Instances"** | Automatically applies the group’s assigned policy to instances added or reassigned to the group and keeps them synchronized with subsequent policy changes |

Please Note My OPSWAT Central Management does not support creating File Security policies or editing their configurations.

## Import Policy from Instance

Import a policy when an enrolled instance has a tested configuration you want to reuse on other instances.

1. On the **File Security > Policies** page, select** Import Policy from Instance**.

![](https://uploads.developerhub.io/prod/97qW/u5yzc718ppv6by1hvxnhvoyg39gckoet9mpnigwons9y3cge2v9pziywf3e6hvua.png)

2. In the popup dialog:
   1. Search for specific instance or select a group, then select the instance from that group
   2. Enter PIN (optional)

![](https://uploads.developerhub.io/prod/97qW/w3fr0mlkt6v0uce0b2h8c3k1tittc70em2yqkhggpqsi5k3vwy1rk2pwl28ngq5k.png)

3. Click Next to start the import
4. A confirmation message appears when the import completes. Select **View Policy** to open the policy details page.

![](https://uploads.developerhub.io/prod/97qW/j2uz1ptrakrprjxw3y99jrq6xrx6spslcsfv57mq19h91f4r0d6ru0kn49aimsp9.png)

![](https://uploads.developerhub.io/prod/97qW/rzsp0d9xbdtg9eo4dskg47ildlfzn03i331va8uedzve3w9cijz98ljgzzrqvrms.png)

## Delete a Policy

1. On the **File Security > Policies** page, locate the policy you want to remove
2. Select **Delete** icon

![](https://uploads.developerhub.io/prod/97qW/890vok8up8xbqnt3ssv7oc3vkt8bqp8f839b8jar5gf7vx2qbbw6h1ikv5e8jow1.png)

3. Confirm the deletion. If prompted, enter your PIN.

## Assign Policy to a Group

1. Go to **Inventory > Groups**
2. Select the group you want to apply the policy to, and open **Settings** tab

![](https://uploads.developerhub.io/prod/97qW/kit6yrv86lccq6bbuvy12hecgzbmeyvkrvehc8wjzjtn5gka857dhoz7nm9rc6u6.png)

3. Under Assign Policy, select the policy

![](https://uploads.developerhub.io/prod/97qW/5s4trzpwhl8eb8518dpfwyh1k4evl412yza1f16emn9ba1tg6s256az7cys4bnub.png)

4. Click **Save **to confirm

Please Note My OPSWAT Central Management will re-assess device status for devices in the group with the new policy, except changes for Threat Detection.

## Automatically Sync Group Policy for New Instances

1. Go to **Inventory > Groups**
2. Select the group you want to apply the policy to, and open **Settings** tab

![](https://uploads.developerhub.io/prod/97qW/kit6yrv86lccq6bbuvy12hecgzbmeyvkrvehc8wjzjtn5gka857dhoz7nm9rc6u6.png)

3. Enable "Automatically sync group policy for new instances"
   1. Whenever a new instance being added or re-assigned into this group, the group’s assigned policy configuration is automatically applied to that instance
   2. Any subsequent edits made to this group's assigned policy will automatically push down to that instance

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
