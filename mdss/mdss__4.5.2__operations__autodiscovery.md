<!-- source: https://www.opswat.com/docs/mdss/4.5.2/operations/autodiscovery -->

# Autodiscovery

Autodiscovery is a powerful feature in MetaDefender Storage Security designed to **simplify and accelerate the integration of your cloud storage**.

It automatically detects and adds storage units from supported cloud storage services, eliminating the need to manually configure each one.

This significantly streamlines the process of onboarding multiple storage units, saving valuable administrative time and reducing the potential for configuration errors.

## Supported Storage Types

> **Info**
>
> Currently, Autodiscovery functionality is available for the following cloud storage service:
>
> - **Amazon S3**
> - **Google Cloud**
> - **SharePoint Cloud**

*Note: MetaDefender Storage Security is continuously evolving. Support for additional cloud storage services may be introduced in future releases. Please refer to the latest release notes for the most up-to-date information.*

## How Autodiscovery Works

The Autodiscovery process involves several key stages:

1. #### Prerequisites
   - Before initiating autodiscovery, ensure the credentials you provide for your cloud storage service (for example AWS IAM user or role for Amazon S3) have the necessary permissions to list all available storage units (`s3:ListAllMyBuckets` permission for S3). Without these permissions, MetaDefender Storage Security cannot detect your storage units.
   - Familiarize yourself with how accounts and groups are managed within MetaDefender Storage Security. This will help you understand how autodiscovered storage units are organized post-discovery. For comprehensive details, please review the [Accounts & Groups](https://www.opswat.com/docs/mdss/operations/accounts-and-groups) documentation below.
2. #### Initiating Storage Discovery
   - You provide valid credentials for a supported cloud storage service through the MDSS interface.
3. #### Scanning and Detection
   - MDSS uses the provided credentials to securely connect to your cloud storage account
   - It then scans the account to detect all available storage units (e.g. S3 buckets associated with the AWS account).
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

#### Method 1: During Storage Unit Addition

1. From the Storage Units page, click "Add Storage Unit"
2. Select a supported storage type (Amazon S3, Google Cloud)
3. You'll be presented with two options:
   1. Add one storage unit with full configuration control
   2. Use Autodiscovery to add multiple storage units
4. If you select "Storage Discovery", you'll need to:
   1. Provide account credentials
   2. Select a region (if applicable)
   3. The system will then discover available storage units
5. After discovery completes, you'll have two options:
   1. Automatically add all discovered storage units (Autodiscovery)
   2. Select which specific units to add (Manual Selection)
6. Complete the process by clicking "Continue" and confirming your choices

![](https://uploads.developerhub.io/prod/k8zL/9uj9rdd1nk74kkhees4djm4luajmmtmd2odt4ze3nv5471cy1k8itdljpzy8mtxw.png)

![](https://uploads.developerhub.io/prod/k8zL/uufrh8gh7lcwj6o0tq3gzbvgpc7tzw3re3ztgu6eubjim7wslsm157rnnsc4yl4q.png)

#### Method 2: Enabling Autodiscovery for an Existing Account

1. From the Storage Units page, click on the 3-dots menu of a supported storage type card (e.g., Amazon S3) and select "Manage Storage Unit"
2. You'll be presented with two options:
   1. Update just the storage information (not the credentials of the account)
   2. Update the account's credentials
3. If you select "Change Account Info", you'll be able to toggle the Autodiscovery on or off
4. Input the secret key and complete the process by clicking "Save changes"

![](https://uploads.developerhub.io/prod/k8zL/hue1gm5aeduobl0bp0ttr8w9nhxthv8om5exhtp0ovxlluojjjejebx90yopwwjx.png)

### Common Issues

1. **No storage units discovered**
   1. Verify the credentials have sufficient permissions
   2. Check that the selected region is correct
   3. Confirm that the account contains storage units of the supported type
2. **Autodiscovery not working periodically**
   1. Verify the account's Autodiscovery setting is enabled
   2. Check system logs (e.g., Audit page) for any authentication or connection errors
3. **Storages not appearing in Storage Units page**
   1. If the used option was "Storage Discovery" + "Manual Selection", in the Summary view of adding the storage unit, a list of the storages that weren't added successfully will be visible, including the error why it wasn't added.

> **LIMITATIONS**
>
> When storage units are autodiscovered, they will all be set up in the system sharing the same account and group details provided during the autodiscovery configuration.
>
> For autodiscovery to successfully identify your storage units, the credentials used must possess the necessary permissions to list all accessible buckets.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
