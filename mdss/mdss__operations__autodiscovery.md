<!-- source: https://www.opswat.com/docs/mdss/operations/autodiscovery -->

# Autodiscovery

Autodiscovery is a powerful feature in MetaDefender Storage Security designed to **simplify and accelerate the integration of your cloud storage**.

It automatically detects and adds storage units from supported cloud storage services, eliminating the need to manually configure each one.

This significantly streamlines the process of onboarding multiple storage units, saving valuable administrative time and reducing the potential for configuration errors.

## Supported Storage Types

> **Info**
>
> Currently, Autodiscovery functionality is available for the following storage types:
>
> - **Amazon S3** — [How to Enable Autodiscovery](https://www.opswat.com/docs/mdss/integrations/how-to-enable-autodiscovery-amazon-s3)
> - **S3 Compatible**, **Wasabi**, **Oracle S3-Compatible**, **Cubbit** and **Scality RING** — these follow the same flow as Amazon S3; see the Amazon S3 guide above
> - **Azure Blob** — [How to Enable Autodiscovery](https://www.opswat.com/docs/mdss/integrations/how-to-enable-autodiscovery-azure-blob)
> - **Google Cloud** — [How to Enable Autodiscovery](https://www.opswat.com/docs/mdss/integrations/how-to-enable-autodiscovery-google-cloud)
> - **SharePoint Online** — [How to Enable Autodiscovery](https://www.opswat.com/docs/mdss/integrations/how-to-enable-autodiscovery-sharepoint-online)

*Note: MetaDefender Storage Security is continuously evolving. Support for additional cloud storage services may be introduced in future releases. Please refer to the latest release notes for the most up-to-date information.*

## How Autodiscovery Works

The Autodiscovery process involves several key stages:

1. #### Prerequisites
   - Before initiating autodiscovery, ensure the credentials you provide for your cloud storage service have the necessary permissions to list all available storage units. For example, an AWS IAM user or role needs the `s3:ListAllMyBuckets` permission for Amazon S3 and S3-compatible storages, and a Google Cloud service account needs the `storage.buckets.list` permission on the project (for example through a custom role or Storage Admin). The exact permissions for each storage type are listed on its "Add a … Storage" page. Without these permissions, MetaDefender Storage Security cannot detect your storage units.
   - Familiarize yourself with how accounts and groups are managed within MetaDefender Storage Security. This will help you understand how autodiscovered storage units are organized post-discovery. For comprehensive details, please review the [Accounts & Groups](https://www.opswat.com/docs/mdss/operations/accounts-and-groups) documentation below.
2. #### Initiating Storage Discovery
   - You provide valid credentials for a supported cloud storage service through the MDSS interface.
3. #### Scanning and Detection
   - MDSS uses the provided credentials to securely connect to your cloud storage account
   - It then scans the account to detect all available storage units (e.g. S3 buckets associated with the AWS account, Azure Blob containers in the storage account, or SharePoint Online sites in the tenant).
4. #### Automated Integration & Configuration
   - Successfully detected storage units are automatically added to MetaDefender Storage Security.
   - These autodiscovered storage units will typically be associated with a specific account and group within MetaDefender Storage Security, often based on the context of the autodiscovery setup.

> **LIMITATION**
>
> **All units discovered in a single operation will share the same initial account and group configuration.**

The Autodiscovery feature works by:

- **Storage Discovery**: When provided with valid credentials for a supported cloud storage service, the system scans the associated account to detect all available storage units (such as S3 buckets).

![](https://uploads.developerhub.io/prod/k8zL/cys112i2pj8hi2bo4ccxs8oxh32ue37ddvzjip1p9bhxa7pea4ja1h99p2fd1qdt.png)

- **Automated Addition**: Depending on the chosen method, the system can either:
  - Automatically add all discovered storage units
  - Present a list of discovered storage units for manual selection
  - Allow individual adding of storage units
- **Periodic Synchronization**: For accounts with Autodiscovery enabled, the system periodically checks for new storage units and automatically adds them to MetaDefender Storage Security.

### Using Autodiscovery

#### Method 1: When Adding an Account

1. From the left side menu, navigate to **Inventory**, click **Add New** > **Account**, choose one of the supported storage types listed above and click **Next**
2. Fill out the form with valid account credentials
3. Turn on the **Autodiscovery** switch and select the **Destination Group** where the discovered storage units will be added
4. Click **Next**. The **Summary** step shows Autodiscovery as **Enabled** together with the destination group, and the discovered storage units are added to that group. Click **View in inventory** or **Finish**

To add only specific storage units, leave **Autodiscovery** disabled, click **Add unit** on the **Summary** step, and choose:

1. **Single unit** to add one storage unit with full configuration control
2. **Multiple units** to select which of the discovered storage units to add

![](https://uploads.developerhub.io/prod/k8zL/9uj9rdd1nk74kkhees4djm4luajmmtmd2odt4ze3nv5471cy1k8itdljpzy8mtxw.png)

![](https://uploads.developerhub.io/prod/k8zL/uufrh8gh7lcwj6o0tq3gzbvgpc7tzw3re3ztgu6eubjim7wslsm157rnnsc4yl4q.png)

#### Method 2: Enabling Autodiscovery for an Existing Account

1. Navigate to **Inventory** > **Accounts** and open the account (or select **Account Settings** from the account's three-dot menu)
2. Open the **Settings** tab
3. Turn the **Autodiscovery** switch on or off and select the **Destination Group**
4. Input the secret key or credentials file and complete the process by clicking **Update**

![](https://uploads.developerhub.io/prod/k8zL/hue1gm5aeduobl0bp0ttr8w9nhxthv8om5exhtp0ovxlluojjjejebx90yopwwjx.png)

### Common Issues

1. **No storage units discovered**
   1. Verify the credentials have sufficient permissions
   2. Check that the selected region is correct
   3. Confirm that the account contains storage units of the supported type
2. **Autodiscovery not working periodically**
   1. Verify the account's Autodiscovery setting is enabled
   2. Check system logs (e.g., Audit page) for any authentication or connection errors
3. **Storages not appearing in Inventory**
   1. If the storage units were added with **Add unit** > **Multiple units**, the Summary step lists the storage units that weren't added successfully, including the error why each wasn't added.

> **LIMITATIONS**
>
> When storage units are autodiscovered, they will all be set up in the system sharing the same account and group details provided during the autodiscovery configuration.
>
> For autodiscovery to successfully identify your storage units, the credentials used must possess the necessary permissions to list all accessible storage units.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
