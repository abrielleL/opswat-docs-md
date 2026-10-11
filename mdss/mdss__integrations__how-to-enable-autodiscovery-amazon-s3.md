<!-- source: https://www.opswat.com/docs/mdss/integrations/how-to-enable-autodiscovery-amazon-s3 -->

# How to Enable Autodiscovery

This guide provides step-by-step instructions for enabling Autodiscovery for Amazon S3 storage in MetaDefender Storage Security.

Autodiscovery automatically detects and adds S3 buckets as storage units, saving time and reducing configuration errors.

> **S3-COMPATIBLE STORAGES**
>
> The same steps apply to the **S3 Compatible**, **Wasabi**, **Oracle S3-Compatible**, **Cubbit** and **Scality RING** storage types. Select that provider instead of Amazon S3 in Method 1, and provide the endpoint and credentials described on its "Add a … Storage" page.

## Prerequisites

Before enabling Autodiscovery, ensure you have:

1. Valid AWS access key ID and secret access key with sufficient permissions
2. Permissions as stated in [Add An Amazon S3 Storage](https://www.opswat.com/docs/mdss/integrations/add-an-amazon-s3-storage)

#### Method 1: Enable Autodiscovery When Adding an Account

- Navigate to **Inventory** › **Accounts** and click **Add account**
- Select the **Amazon S3** provider
- Fill out the form with valid Amazon S3 credentials
- Turn on the **Autodiscovery** switch and select the **Destination Group** where the discovered buckets will be added

> **REGION-SPECIFIC ENDPOINTS**
>
> Only the storages from the selected region endpoint will be discovered.

![](https://uploads.developerhub.io/prod/k8zL/lgcrja1d58grm0o9swxxvf5qd3w4hcpe5nxj54z96e5t6lp0qgnhzg99mwpehbuf.png)

- Continue to the **Summary** step. Autodiscovery starts in the background and the discovered buckets are added as storage units to the destination group. Click **View in inventory** to open the account, or **Finish**

![](https://uploads.developerhub.io/prod/k8zL/6fdo616at7f2yb6jmgeap4btt2mgymojm14mkboul92gmvz6a85tpn3fx1gk9792.png)

To learn more, please consult the [Autodiscovery](https://www.opswat.com/docs/mdss/operations/autodiscovery) documentation.

> **ADDING SPECIFIC BUCKETS ONLY**
>
> To add only specific buckets, leave **Autodiscovery** disabled, click **Add unit** on the **Summary** step, and choose **Single unit** or **Multiple units**.

#### Method 2: Enable Autodiscovery for an Existing Account

- Navigate to **Inventory** › **Accounts** and open the account you want to start autodiscovery for
- Open the **Settings** tab
- Turn on the **Autodiscovery** switch and select the **Destination Group**
- Enter the **Secret Access Key**
- Click **Update**

![](https://uploads.developerhub.io/prod/k8zL/ksgvwjq2kf0azeram0twi15eyoaxqfi3yn1870vfio198eoy030zquude10ow7uz.png)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
