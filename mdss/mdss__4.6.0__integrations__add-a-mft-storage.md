<!-- source: https://www.opswat.com/docs/mdss/4.6.0/integrations/add-a-mft-storage -->

# Add an OPSWAT MFT Storage

This guide outlines the necessary steps to integrate an OPSWAT Managed File Transfer (MFT) storage solution with your OPSWAT MetaDefender Storage Security (MDSS) instance.

> **LIMITATION**
>
> The MFT integration does not currently support the "Shared Space" feature within Custom Groups. Consequently, while files in a Custom Group's Shared Space will be discovered during a scan using the "All users" storage option, any attempts to apply remediation actions to these files will fail.

### 1. Prerequisites

Before you begin adding an MFT storage unit in MDSS, make sure you have the following:

- an **MFT Service URL** - this is the base web address used to access your OPSWAT MFT provider
- an **API Key** required for MDSS to authenticate and interact with your MFT service
- You will need **administrator privileges** for both your MFT dashboard and your MDSS web page.

![](https://uploads.developerhub.io/prod/k8zL/z0qtaggi369w0kbhx8bow3ysq13p6pi0sgh4998xspbjb014bn2erbr583boymed.png)

## 2. Obtaining the Service URL

The MFT Service URL is the primary address for your MFT provider.

- Determine the complete base URL where your MFT service is hosted.
- Make sure the URL includes the correct protocol, either `http://` or `https://`.
  - Example: `https://mft.yourcompany.com` or `http://mft.internal.net`

## 3. Generating Your MFT API Key

An API key is essential for secure communication between MDSS and your MFT service.

- Log in to your MFT dashboard with administrator credentials and navigate to the **Settings** page.
- Within the Settings menu, find and select the **Security** section. This is often located in a side navigation panel.
- Within the Security section, select the **API Keys** tab.

![](https://uploads.developerhub.io/prod/k8zL/n94um6ugqgq7xy5vtwkv4bq2a145sx8woz436ywgu6azafbgykj0vgzuud1lnfo5.png)

- Click on the **Add API key** button (or a similarly named option like "Generate New Key").
- Set an appropriate expiration date for the API key to enhance security. Consider your organization's security policies.
- Once generated, the API key will be displayed. **Immediately and securely copy and store this key.** For security reasons, treat this key like a password.

![](https://uploads.developerhub.io/prod/k8zL/6imzah4m47q26s01zgt10heso5bo6cj480ynlk9wiojccsug4r8zypn7de6z4pce.png)

## 4. Configuring MFT File Upload Settings

To ensure MDSS can successfully upload files, a specific MFT setting needs to be enabled. This allows MDSS to upload files on behalf of users, even if those users are part of a group and the group membership isn't explicitly specified during the upload.

- As an administrator, navigate to the **Settings** page on your MFT dashboard
- Under the **Global Settings** section, locate and select the **Files** tab
- Make sure that the option labeled **"Allow Users to Upload Files Without Specifying Group Membership"** is **checked (enabled)**
- If you've made any modifications to this setting, ensure you save them

![](https://uploads.developerhub.io/prod/k8zL/1lrba1c4t6kbhaxaeefoaxr3mf6spf3mlag3kofpdfywmvc86534xg15uapwqm30.png)

### 5. Adding the MFT Storage Unit in MDSS

With the MFT Service URL and API key obtained, and the necessary MFT setting configured, you can now add the MFT storage to MDSS. (**Note**: The latest supported version of MFT Storage is **3.9.4**)

- Log in to your MDSS web interface.
- From the left side menu, navigate to **Inventory**, click **Add New** > **Account**, choose **OPSWAT MFT** and click **Next**
- Fill in the account fields:
  - **Account name** - a name so you can easily identify the account later.
  - **Service URL** - enter the URL obtained in Step 2.
  - **API Key** - enter the API key generated and saved in Step 3.
- Click **Next** to create the account.
- On the **Summary** step, click **Add unit** (or navigate to **Inventory**, click **Add New** > **Unit**, choose the MFT account and click **Next**)
- Fill in the unit fields:
  - **Unit name** - a name so you can easily identify the unit later.
  - **Group** - the group the unit is assigned to.
  - **Process files from** - choose **All users** or **Current user**.
- Click **Next** to finish. It is highly recommended to test the integration by uploading or scanning a file to ensure the MFT storage is working correctly with MDSS.

> **IMPORTANT**
>
> MDSS will not discover or process files that OPSWAT MFT has already blocked and made unavailable for download.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
