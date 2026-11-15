<!-- source: https://www.opswat.com/docs/cm/product-management/file-security-solution-policy -->

# File Security Solution Policy

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

This document explains how to manage policies for products under File Security Solution.

## [**Supported Products**](/docs/cm/product-management/file-security-solution-policy#supported-products)

The File Security solution includes the following products:

- MetaDefender Core
- MetaDefender ICAP Server
- MetaDefender Storage Security (MDSS)
- MetaDefender Managed File Transfer (MFT)

## [View File Security Policies](/docs/cm/product-management/file-security-solution-policy#view-file-security-policies)

1. Log into the My OPSWAT Central Management console.
2. Go to **File Security > Policies,** select the product whose policies you want to view

From this page, you can:

| **Action** | **What it does** |
| --- | --- |
| **Import Policy from Instance** | Creates a new policy in My OPSWAT Central Management from the configuration of an enrolled instance |
| **Delete** | Permanently removes a policy |

### [Import Policy from Instance](/docs/cm/product-management/file-security-solution-policy#import-policy-from-instance)

Use this option when an instance already has a tested configuration you want to reuse across other instances.

1. On the **File Security > Policies** page, select **Import Policy from Instance**.

2. In the popup dialog:

   1. Search for specific instance or select a group, then select the instance from that group
   2. Enter PIN (optional)

3. Click Next to start the import
4. A confirmation message appears when the import completes. Select **View Policy** to open the policy details page.

### [Delete a policy](/docs/cm/product-management/file-security-solution-policy#delete-a-policy)

1. On the **File Security > Policies** page, locate the policy you want to remove
2. Select **Delete** icon

3. Confirm the deletion. If prompted, enter your PIN.

## [Apply Policy to a Group](/docs/cm/product-management/file-security-solution-policy#apply-policy-to-a-group)

1. Go to **Inventory > Groups**
2. Select the group you want to apply the policy to, and open **Settings** tab

3. Under Assign Policy, select the policy

4. Click **Save** to confirm

Please Note My OPSWAT Central Management will re-assess device status for devices in the group with the new policy, except changes for Threat Detection.
