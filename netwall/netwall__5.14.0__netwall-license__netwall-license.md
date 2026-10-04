<!-- source: https://www.opswat.com/docs/netwall/5.14.0/netwall-license/netwall-license -->

# License Activation

Before activating a license, users must be registered on my.opswat.com. Registration is free.

OPSWAT MetaDefender Security Gateway needs to be licensed to be fully operational. In this section we will show how to get a valid license file and how to apply it to your MetaDefender Security Gateway system.

### [Activating the Security Gateway](/docs/netwall/5.14.0/netwall-license/netwall-license#activating-the-security-gateway)

Info

A license is only required on the Security Gateway BLUE side. There is no need to apply the license in the RED side.

First thing is to check the **Deployment ID**. This ID can be found in **Configuration -> License**. Deployment ID needs to be copied as we will need it to get a valid license file.

Then browse to [my.opswat.com](https://my.opswat.com) and login with your user/password. Once correctly logged in, click on License Activation and fill in the following fields:

- **Package:** Select MetaDefender NetWall from the dropdown.
- **Activation Key:** Insert the Activation Key that your OPSWAT sales representative has provided you with.
- **Deployment ID:** Paste the Deployment ID you've copied in the previous step
- **Optional description:** In this optional field, a description for the license key can be included.

Once filled in click on **Request Unlock Key** button and then click on **Download Unlock Key** to get the license file.

Once you have the Unlock Key file, we need to come back to MetaDefender Security Gateway UI to activate the key. Go to **Configuration -> License** and click on **Activate**.

Click on **Select File** and browse to the Activation Key we have stored in the previous step. Then click on **Activate**. Once Active, you will be able to see new information in the fields Product ID, Product Name and Expiration.

### [Deactivating Security Gateway](/docs/netwall/5.14.0/netwall-license/netwall-license#deactivating-security-gateway)

Deactivation needs to be done in two steps:

1. The MetaDefender Security Gateway needs to be deactivated from the GUI interface
2. The deployment needs to be deactivated from the Activation Key (**This is done by OPSWAT Support Team**)

Info

If you need to fully deactivate the MetaDefender Security Gateway please contact OPSWAT Support Team to help assist in deactivating MetaDefender Security Gateway.
