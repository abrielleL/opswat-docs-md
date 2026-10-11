<!-- source: https://www.opswat.com/docs/mdss/integrations/add-an-azure-files-storage -->

# Add an Azure Files Storage

> **Warning**
>
> **Limitation :** Due to an Azure Files restriction, uploading 0-byte files is not supported. If a remediation action attempts to upload an empty file, the operation will fail.

In order to integrate Azure Files with MetaDefender Storage Security please follow these steps:

1. From the left side menu, navigate to **Inventory**, click **Add New** > **Account**, choose **Azure Files** and click **Next**

![](https://uploads.developerhub.io/prod/k8zL/cj36swf8cziy1o2re9y2pvead4ha12em10s96fw2mxfaucohoz8joe0uz4ve9wxf.png)

2. In **Account Name**, enter a name that identifies this [account](https://www.opswat.com/docs/mdss/operations/accounts-and-groups) in MetaDefender Storage Security. It is not the Azure storage account name.
3. In **Storage Account**, enter the name of your Azure storage account.
4. Enter your **Account Key**. Scroll to the end of this page for more details.
5. Click **Next** and finish the process.
6. Add a new unit for the previously created account (**Inventory** > **Add New** > **Unit**).

![](https://uploads.developerhub.io/prod/k8zL/e6kbi7oynuj1xivhcelcmwp76dwpm43v8izhb78o0yukw6ntwlr3bhzibx2s0cmi.png)

7. Give your unit an unique name
8. Assign your unit to a Group
9. Enter the **name of the share** you wish to process with MetaDefender Storage Security.
10. Click **Next** in order to finish the process.

### Where can I find the Account Key?

To find the Account Key, please follow these steps:

[https://learn.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
