<!-- source: https://www.opswat.com/docs/mdss/4.4.2/integrations/how-to-enable-autodiscovery -->

# How to Enable Autodiscovery

This guide provides step-by-step instructions for enabling Autodiscovery for Azure Blob storage in MetaDefender Storage Security.

Autodiscovery automatically detects and adds Azure Blob containers as storage units, saving time and reducing configuration errors.

## [Prerequisites](https://www.opswat.com/docs/mdss/integrations/how-to-enable-autodiscoveryyn1#prerequisites)

Before enabling Autodiscovery, ensure you have:

1. Valid Azure Blob credentials with sufficient permissions
2. Permissions as stated in [Add an Azure Blob storage](https://www.opswat.com/docs/mdss/integrations/add-an-azure-blob-storage)

#### [Method 1: Enable Autodiscovery During Storage Unit Addition](/docs/mdss/4.4.2/integrations/how-to-enable-autodiscovery#method-1-enable-autodiscovery-during-storage-unit-addition)

- Navigate to **Storage Units** page
- Click **Add Storage Unit** button
- Select **Azure Blob** Storage Type
- Select **Storage Discovery** and click **Continue**

- Fill out the form with valid Azure Blob credentials and click **Continue**

- In the next step, select your integration method. You have two choices: Autodiscovery and Manual Selection.

  - **Autodiscovery** for convenience, this option automatically adds all the containers that MDSS finds
  - **Manual Selection** for precise control, this option lets users choose specific containers from the discovered list to integrate.

To learn more about each integration type, please consult the [Autodiscovery](/docs/mdss/4.4.2/metadefender-storage-security/4.3.0/operations/autodiscovery) documentation.

NO CONTAINERS FOUND

If there were no containers found, you will be presented with a third option - **Add Individually** - which will reveal the credentials form to manually add the storage by using the site name.

- If selecting the **Autodiscovery** option:

  - Click **Continue,** and an informative message will be displayed that the autodiscovery process has started in the background. You can safely close the modal, and the storage units will be added in the background to the Storage Units page

- If selecting **Manual Selection** option:

  - Click **Continue**
  - Select the containers you want to add from the discovered list
  - Click **Continue**

ERROR ADDING A STORAGE THAT WAS SELECTED DURING MANUAL SELECTION

In case there was an error while trying to add your storage, you will see the error message in the Storage card while hovering over the (i) icon.

#### [Method 2: Enable Autodiscovery for an Existing Account](/docs/mdss/4.4.2/integrations/how-to-enable-autodiscovery#method-2-enable-autodiscovery-for-an-existing-account)

- Navigate to the **Storage Units** page
- Identify a storage that's using the account you want to start autodiscovery for
- Click on the 3-dots button from the storage card and select **Manage Storage Unit**
- From the top toggle, select **Change account info**
- Turn on autodiscovery by toggling the **Enable storage auto** **discovery** switch
