<!-- source: https://www.opswat.com/docs/mdss/4.5.2/integrations/how-to-enable-autodiscovery-azure-blob -->

# How to Enable Autodiscovery

## This guide provides step-by-step instructions for enabling Autodiscovery for Amazon S3 storage in MetaDefender Storage Security.

Autodiscovery automatically detects and adds S3 buckets as storage units, saving time and reducing configuration errors.

## Prerequisites

Before enabling Autodiscovery, ensure you have:

1. Valid AWS access key ID and secret access key with sufficient permissions
2. Permissions as stated in [Add An Amazon S3 Storage](https://www.opswat.com/docs/mdss/integrations/add-an-amazon-s3-storage)

#### Method 1: Enable Autodiscovery During Storage Unit Addition

![](https://uploads.developerhub.io/prod/k8zL/zzgwqu9g1hmhsmm34hf8dq78v64zv31aem2g82povwzm7t2yl19x2c5yhdoadu8q.png)

![](https://uploads.developerhub.io/prod/k8zL/w9918a1e9q3p7vzsg1gzjoqxm4xtp6ktcaiv7g7374dyf9un4e1d7qmxtcda334x.png)

![](https://uploads.developerhub.io/prod/k8zL/tgkvsuds8545avlpyr9brj67u1bl7agv0t5y4tg9vii2t6fffy8x7qwkl94e2nzw.png)

- Navigate to **Storage Units** page
- Click **Add Storage Unit** button
- Select **Amazon S3** Storage Type
- Select **Storage Discovery** and click **Continue**
- Fill out the form with valid Amazon S3 credentials and click **Continue**

> **REGION-SPECIFIC ENDPOINTS**
>
> Only the storages from the selected region endpoint will be discovered in the next steps.

> **ACCOUNT ALREADY EXISTS**
>
> If an account with the same credentials already exists, it will just use the existing account; this means at the final step, you will see the original account name (which might differ than the one you provided at this step).
>
> ![](https://uploads.developerhub.io/prod/k8zL/osu91s9d3lt3berz57g7tq2ou3pfy4qt9rx39qxv085a17wvd5kcyvkd3qgety8w.png)

- In the next step, select your integration method. You have two choices: Autodiscovery and Manual Selection.
  - **Autodiscovery** for convenience, this option automatically adds all the buckets MDSS finds
  - **Manual Selection** for precise control, this option lets users choose specific buckets from the discovered list to integrate.

To learn more about each integration type, please consult the [Autodiscovery](https://www.opswat.com/docs/mdss/operations/autodiscovery) documentation.

> **NO BUCKETS FOUND FOR THE SPECIFIC REGION**
>
> If there were no buckets found for the specific region, you will be presented with a third option - **Add Individually** - which will reveal the credentials form to manually add the storage by using the bucket name.

- If selecting **Autodiscovery** option:
  - Click **Continue** and an informative message will be displayed that the autodiscovery process has started in the background. You can safely close the modal and the storages will be added in background to the Storage Units page

![](https://uploads.developerhub.io/prod/k8zL/3ehlyl1ez5ady4577uf9j4wxpy3eflkiq51lavbciceu281hoa6apag5fth7n5it.png)

![](https://uploads.developerhub.io/prod/k8zL/2nledlkp8twpth08xqpbmkyzm07ohdhn8r1jm3qblucakohnavxmbr5mqb3bm3sd.png)

- If selecting **Manual Selection** option:
  - Click **Continue**
  - Select the buckets you want to add from the discovered list
  - Click **Continue**

![](https://uploads.developerhub.io/prod/k8zL/9ggmwm73f0i7u6hqsgk53fzbaxa8rvkpjzrh0qf3wi66p75s61gu7x9f841sg3iv.png)

![](https://uploads.developerhub.io/prod/k8zL/k40ubsq88gjzfvnox0b7a47jo20rhykmhhlfy1cu06n4edcfp1hyjwtcdmcxjc0s.png)

![](https://uploads.developerhub.io/prod/k8zL/wzqxy2mth19y9bws7m4y964fvisxzevqr7pjslhhybghuws1rsnlut8tc64cfbjv.png)

> **ERROR ADDING A STORAGE THAT WAS SELECTED DURING MANUAL SELECTION**
>
> In case there was an error while trying to add your storage, you will see the error message in the Storage card while hovering over the (i) icon.

#### Method 2: Enable Autodiscovery for an Existing Account

- Navigate to **Storage Units** page
- Identify a storage that's using the account you want to start autodiscovery for
- Click on the 3-dots button from the storage's card and select **Manage Storage Unit**
- From the top toggle, select **Change account info**
- Turn on autodiscovery by toggling the **Enable storage autodiscovery** switch

![](https://uploads.developerhub.io/prod/k8zL/xs7zn1sj9jf3rv9w7s49hmlc22e90qm05tndavp8n19wwco47enaxj95g5q76ke4.png)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
