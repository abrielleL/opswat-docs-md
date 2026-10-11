<!-- source: https://www.opswat.com/docs/mdss/integrations/how-to-enable-autodiscovery-azure-blob -->

# How to Enable Autodiscovery

This guide provides step-by-step instructions for enabling Autodiscovery for Azure Blob storage in MetaDefender Storage Security.

Autodiscovery automatically detects and adds Azure Blob containers as storage units, saving time and reducing configuration errors.

## Prerequisites

Before enabling Autodiscovery, ensure you have:

1. Valid Azure Blob credentials with sufficient permissions
2. Permissions as stated in [Add an Azure Blob storage](https://www.opswat.com/docs/mdss/integrations/add-an-azure-blob-storage)

#### Method 1: Enable Autodiscovery When Adding an Account

- Navigate to **Inventory** › **Accounts** and click **Add account**
- Select the **Azure Blob** provider
- Fill out the form with valid Azure Blob credentials
- Turn on the **Autodiscovery** switch and select the **Destination Group** where the discovered containers will be added

![](https://uploads.developerhub.io/prod/k8zL/thpbsbosjbsm0v9cn06j6ouszcndptf2v2zna4khig6j3136k9huxvgdqn3snh5t.png)

- Continue to the **Summary** step. Autodiscovery starts in the background and the discovered containers are added as storage units to the destination group. Click **View in inventory** to open the account, or **Finish**

![](https://uploads.developerhub.io/prod/k8zL/gwpy5aq31kpsawupa8ymtx1l1404qwlzmk0h15zlrnbzs8ggjcnfx395axq18xh0.png)

To learn more, please consult the [Autodiscovery](https://www.opswat.com/docs/mdss/operations/autodiscovery) documentation.

> **ADDING SPECIFIC CONTAINERS ONLY**
>
> To add only specific containers, leave **Autodiscovery** disabled, click **Add unit** on the **Summary** step, and choose **Single unit** or **Multiple units**.

#### Method 2: Enable Autodiscovery for an Existing Account

- Navigate to **Inventory** › **Accounts** and open the account you want to start autodiscovery for
- Open the **Settings** tab
- Turn on the **Autodiscovery** switch and select the **Destination Group**
- Enter the **Client Secret**
- Click **Update**

![](https://uploads.developerhub.io/prod/k8zL/kmf7969zyxoj0dzvljh5i4saio6gwhcq1d39bbj1meu62qv5qu635bwc3mxpptvh.png)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
