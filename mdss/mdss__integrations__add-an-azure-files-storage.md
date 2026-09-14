<!-- source: https://www.opswat.com/docs/mdss/integrations/add-an-azure-files-storage -->

# Add an Azure Files Storage

**Limitation :** Due to an Azure Files restriction, uploading 0-byte files is not supported. If a remediation action attempts to upload an empty file, the operation will fail.

In order to integrate Azure Files with MetaDefender Storage Security please follow these steps:

1. From the left side menu, navigate to **Inventory** , click on **Add account** and choose **Azure Files**

2. Give your [account](/docs/mdss/operations/accounts-and-groups) a name so you can easily identify it later

2. Enter the **Account Name**.
3. Enter your Azure **Storage Account**
4. Enter your **Account Key**. Scroll to the end of this page for more details.
5. Click next and finish the process
6. Add a new unit for the previously created account

7. Give your unit an unique name
8. Assign your unit to a Group
9. Enter the **name of the share** you wish to process with MetaDefender Storage Security.
10. Click **Next** in order to finish the process.

### [Where can I find the Access Key?](https://docs.opswat.com/mdss/3.1.2/integrations/add-an-alibaba-cloud-storage#where-can-i-find-the-endpoint-url)

To find the Account Key, please follow these steps:

<https://learn.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal>
