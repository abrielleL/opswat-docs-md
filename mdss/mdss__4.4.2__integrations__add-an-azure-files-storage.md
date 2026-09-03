<!-- source: https://www.opswat.com/docs/mdss/4.4.2/integrations/add-an-azure-files-storage -->

# Add an Azure Files Storage

**Limitation :** Due to an Azure Files restriction, uploading 0-byte files is not supported. If a remediation action attempts to upload an empty file, the operation will fail.

In order to integrate Azure Files with MetaDefender Storage Security please follow these steps:

1. From the left side menu, navigate to **Storage units**, click on **Add storage unit** and choose **Azure Files**

2. Give your [account](/docs/mdss/4.4.2/operations/accounts-and-groups) a name so you can easily identify it later
3. Give your storage a name so you can easily identify it later
4. Enter the **Account Name**.
5. Enter your **Account Key**. Scroll to the end of this page for more details.
6. Enter the **name of the share** you wish to process with MetaDefender Storage Security.
7. Click **Continue** in order to finish the process.

### [Where can I find the Access Key?](https://docs.opswat.com/mdss/3.1.2/integrations/add-an-alibaba-cloud-storage#where-can-i-find-the-endpoint-url)

To find the Account Key, please follow these steps:

<https://learn.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal>
