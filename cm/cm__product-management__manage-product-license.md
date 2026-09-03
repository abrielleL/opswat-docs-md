<!-- source: https://www.opswat.com/docs/cm/product-management/manage-product-license -->

# Manage Product License

This section explains how to add or remove license keys.

## Add License

My OPSWAT Central Management supports two methods to add license key depending on your environment:

### **Online License**

Use this method if your environment has an active internet connection.

![](https://uploads.developerhub.io/prod/97qW/nezidi55z0frferh5ie6gxi3a20e7b3i1ueyf07sw3b7wakmdw00z8xni87bfha0.png)

- Navigate to the **License** page and locate your targeted product section, then click **Add License**.
- In the popup dialog, enter your unique license key and select the device group.
- Click **Active**
  - Any enrolled instance without a license will automatically retrieve available license from My OPSWAT Central Management. No manual step is required.
  - Instances using standalone licenses will automatically switch to the license managed by My OPSWAT Central Management once that standalone license expires, provided a valid key has been added.
- Verify the license status updates to **Active**.

> **MetaDefender Endpoint Upgrade Request**
>
> Unlicensed installations of My OPSWAT Central Management include a free tier that supports a limited number of MetaDefender Endpoint instances. Click **Upgrade Request** to contact OPSWAT and increase your license capacity.

![Send Upgrade Request for MetaDefender Endpoint](https://uploads.developerhub.io/prod/97qW/q6x7p0c4rb9dr9htcp7ahx1oovu5s2xczivae0fdxg8s9enqn11mpkr795846b0a.png)

### **Offline License**

If your environment connects to the internet, follow the steps for [Online License](https://www.opswat.com/docs/cm/product-management/manage-product-license#online-license).

Use the method below if your environment does not have internet access.

**For MetaDefender Endpoint and MetaDefender Kiosk L-Series**

- Navigate to the **License** page
  - **MetaDefender Endpoint**: Click **Update**
  - **MetaDefender Kiosk L-Series**: Click **Add License**
- Select the **Offline** activation tab.
- Log in to [My OPSWAT Portal](https://my.opswat.com/) and download your product activation file using the provided Deployment ID. Refer to the [Activate License](https://www.opswat.com/docs/my/license-management/activate-license) documentation for detailed retrieval instructions
- Upload the downloaded activation file and click **Active.**

![](https://uploads.developerhub.io/prod/97qW/fqz705zo3kbpgdxrfw3a5yuxzjbjbcgymclvkbj1p4cx3c58mfrtri9jhym601qs.png)

**For other supported products**

- Navigate to the **License** page and click **Add License**, then select the **Offline** activation tab.
- Log in to [My OPSWAT Portal](https://my.opswat.com/) and download your product activation file using the Product Deployment ID. Refer to the [Activate License](https://www.opswat.com/docs/my/license-management/activate-license) documentation for detailed retrieval instructions.
- Upload the downloaded activation file and click **Active**.

![](https://uploads.developerhub.io/prod/97qW/ppbmb6n8nq6l5zc1gxtuto9o0mn1lahko85nrpdb1mq9ri4qelvtbx5mcil8qiyx.png)

## Remove License

To remove a license key:

- Open the **License** page and find the specific product section you want to modify.
- Click **Remove.**

![](https://uploads.developerhub.io/prod/97qW/5heoz4c4qa462s5f5dazskwg1il26n5v7eaf00hzha313bv0g7wu2sc1tni07gwj.png)

My OPSWAT Central Management processes the removal action differently depending on the product type:

- **Online License**
  - **MetaDefender Endpoint**: License removal is not supported.
  - **MetaDefender Kiosk L-Series**: Removing an online key deactivates the license instantly and unregisters the instance Deployment ID from the activation server.
  - **Other Products:** Removing an online key stops My OPSWAT Central Management from from managing or granting the license.
- **Offline License**
  - **MetaDefender Endpoint**: License removal is not supported.
  - **Others Products:** Removing an offline key stops My OPSWAT Central Management from from managing or granting the license.

## License Expiration

Admins can monitor license expiration status within the **License** page.

![](https://uploads.developerhub.io/prod/97qW/rvdmkgsj0lw5q3yh81u2vrifxmwu3c44xvbki7n2nv77ms9vjn7bbt4ucaixp91c.png)

When a license expires, its status changes to **Expired**.

- The instance remains in **Expired** state until a valid license is added.
- If a valid license is added, instances automatically pick up the new license and return to **Active** status.
- Instances using standalone licenses will automatically switch to the license managed by My OPSWAT Central Management once that standalone license expires, provided a valid key has been added.

Refer to [Allocate Group License](https://www.opswat.com/docs/cm/product-management/allocate-group-license) for instructions on assigning licenses to specific groups.
