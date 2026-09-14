<!-- source: https://www.opswat.com/docs/mdss/integrations/how-to-enable-autodiscoveryyn1740 -->

# How to Enable Autodiscovery

## [This guide provides step-by-step instructions for enabling Autodiscovery for SharePoint Online in MetaDefender Storage Security.](/docs/mdss/integrations/how-to-enable-autodiscoveryyn1740#this-guide-provides-step-by-step-instructions-for-enabling-autodiscovery-for-sharepoint-online-in-metadefender-storage-security)

Autodiscovery automatically detects and adds SharePoint Online sites as storage units, saving time and reducing configuration errors.

## [Prerequisites](/docs/mdss/integrations/how-to-enable-autodiscoveryyn1740#prerequisites)

Before enabling Autodiscovery, ensure you have:

1. Valid SharePoint Online credentials with sufficient permissions
2. Permissions as stated in [Add a SharePoint Online Storage](/docs/mdss/integrations/add-a-sharepoint-storage)

#### [Method 1: Enable Autodiscovery During Storage Unit Addition](/docs/mdss/integrations/how-to-enable-autodiscoveryyn1740#method-1-enable-autodiscovery-during-storage-unit-addition)

- Navigate to **Storage Units** page
- Click **Add Storage Unit** button
- Select **SharePoint Online** Storage Type
- Select **Storage Discovery** and click **Continue**

- Fill out the form with valid SharePoint Online credentials and click **Continue**

- In the next step, select your integration method. You have two choices: Autodiscovery and Manual Selection.

  - **Autodiscovery** for convenience, this option automatically adds all the sites MDSS finds
  - **Manual Selection** for precise control, this option lets users choose specific sites from the discovered list to integrate.

To learn more about each integration type, please consult the [Autodiscovery](/docs/mdss/operations/autodiscovery) documentation.

NO SITES FOUND

If there were no sites found, you will be presented with a third option - **Add Individually** - which will reveal the credentials form to manually add the storage by using the site name.

- If selecting **Autodiscovery** option:

  - Click **Continue** and an informative message will be displayed that the autodiscovery process has started in the background. You can safely close the modal and the storages will be added in background to the Storage Units page

- If selecting **Manual Selection** option:

  - Click **Continue**
  - Select the sites you want to add from the discovered list
  - Click **Continue**

ERROR ADDING A STORAGE THAT WAS SELECTED DURING MANUAL SELECTION

In case there was an error while trying to add your storage, you will see the error message in the Storage card while hovering over the (i) icon.

#### [Method 2: Enable Autodiscovery for an Existing Account](/docs/mdss/integrations/how-to-enable-autodiscoveryyn1740#method-2-enable-autodiscovery-for-an-existing-account)

- Navigate to **Storage Units** page
- Identify a storage that's using the account you want to start autodiscovery for
- Click on the 3-dots button from the storage's card and select **Manage Storage Unit**
- From the top toggle, select **Change account info**
- Turn on autodiscovery by toggling the **Enable storage auto** **discovery** switch
