<!-- source: https://www.opswat.com/docs/mdss/4.4.2/integrations/how-to-enable-autodiscovery-azure-blob -->

# How to Enable Autodiscovery

## [This guide provides step-by-step instructions for enabling Autodiscovery for Amazon S3 storage in MetaDefender Storage Security.](/docs/mdss/4.4.2/integrations/how-to-enable-autodiscovery-azure-blob#this-guide-provides-step-by-step-instructions-for-enabling-autodiscovery-for-amazon-s3-storage-in-metadefender-storage-security)

Autodiscovery automatically detects and adds S3 buckets as storage units, saving time and reducing configuration errors.

## [Prerequisites](/docs/mdss/4.4.2/integrations/how-to-enable-autodiscovery-azure-blob#prerequisites)

Before enabling Autodiscovery, ensure you have:

1. Valid AWS access key ID and secret access key with sufficient permissions
2. Permissions as stated in [Add An Amazon S3 Storage](/docs/mdss/4.4.2/integrations/add-an-amazon-s3-storage)

#### [Method 1: Enable Autodiscovery During Storage Unit Addition](/docs/mdss/4.4.2/integrations/how-to-enable-autodiscovery-azure-blob#method-1-enable-autodiscovery-during-storage-unit-addition)

- Navigate to **Storage Units** page
- Click **Add Storage Unit** button
- Select **Amazon S3** Storage Type
- Select **Storage Discovery** and click **Continue**
- Fill out the form with valid Amazon S3 credentials and click **Continue**

REGION-SPECIFIC ENDPOINTS

Only the storages from the selected region endpoint will be discovered in the next steps.

ACCOUNT ALREADY EXISTS

If an account with the same credentials already exists, it will just use the existing account; this means at the final step, you will see the original account name (which might differ than the one you provided at this step).

- In the next step, select your integration method. You have two choices: Autodiscovery and Manual Selection.

  - **Autodiscovery** for convenience, this option automatically adds all the buckets MDSS finds
  - **Manual Selection** for precise control, this option lets users choose specific buckets from the discovered list to integrate.

To learn more about each integration type, please consult the [Autodiscovery](/docs/mdss/4.4.2/operations/autodiscovery) documentation.

NO BUCKETS FOUND FOR THE SPECIFIC REGION

If there were no buckets found for the specific region, you will be presented with a third option - **Add Individually** - which will reveal the credentials form to manually add the storage by using the bucket name.

- If selecting **Autodiscovery** option:

  - Click **Continue** and an informative message will be displayed that the autodiscovery process has started in the background. You can safely close the modal and the storages will be added in background to the Storage Units page

- If selecting **Manual Selection** option:

  - Click **Continue**
  - Select the buckets you want to add from the discovered list
  - Click **Continue**

ERROR ADDING A STORAGE THAT WAS SELECTED DURING MANUAL SELECTION

In case there was an error while trying to add your storage, you will see the error message in the Storage card while hovering over the (i) icon.

#### [Method 2: Enable Autodiscovery for an Existing Account](/docs/mdss/4.4.2/integrations/how-to-enable-autodiscovery-azure-blob#method-2-enable-autodiscovery-for-an-existing-account)

- Navigate to **Storage Units** page
- Identify a storage that's using the account you want to start autodiscovery for
- Click on the 3-dots button from the storage's card and select **Manage Storage Unit**
- From the top toggle, select **Change account info**
- Turn on autodiscovery by toggling the **Enable storage autodiscovery** switch
