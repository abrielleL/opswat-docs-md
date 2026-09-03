<!-- source: https://www.opswat.com/docs/mdss/4.4.2/integrations/add-an-azure-blob-storage -->

# Add an Azure Blob Storage

In order to integrate Azure Blob with MetaDefender Storage Security you will be required to create an application registration, assign the necessary permissions and roles, and then generate a secret key. Please follow these steps:

1. From the left side menu, navigate to **Storage units**, click on **Add storage unit** and choose **Azure Blob**

2. Give your [account](/docs/mdss/4.4.2/operations/accounts-and-groups) a name so you can easily identify it later
3. Give your storage a name so you can easily identify it later.
4. Select **Government Cloud type** if the storage belongs to Azure US Government Cloud.
5. Enter the **Storage Account** name.
6. Enter your **Tenant ID**. Scroll to the end of this page for more details.
7. Enter your **Client ID.** Scroll to the end of this page for more details.
8. Enter your **Client Secret.** Scroll to the end of this page for more details.
9. Enter the **name of a container** to process objects from a particular container.
10. Select **Continue** in order to finish the process.

### [How to create an Azure Blob application?](/docs/mdss/4.4.2/integrations/add-an-azure-blob-storage#how-to-create-an-azure-blob-application)

In order to process your Azure Blob objects with MetaDefender Storage Security you will be required to add a new app registration in your Microsoft Entra ID Azure Portal.

1. Log in to [Azure Portal](https://portal.azure.com/) and from the left navigation menu choose **Microsoft Entra ID**

2. Make a copy of the **Tenant ID** from the overview page

3. From the left side menu, choose **App registrations**
4. Click **New registration**
5. Give your app a name so you can easily identify it

6. There is no need to modify the other properties. When ready, please click **Register**
7. From the **Overview** page of your newly created application, make a copy of **Application (client) ID**
8. Navigate to **Certificates & Secrets** from the left-side menu
9. Click **New client secret** and choose Expires in 24 months

10. Click Add and then you will need to make a copy of the generated secret key because it will not be available later
11. Navigate to your **Storage Account** and select the **Access Control (IAM)** menu
12. Select the **Role assignments** tab, then select the **Add role assignment** option from the **Add** dropdown.

13. Assign the following roles to the **Client Application** you previously registered:

    1. Storage Blob Data Contributor
    2. Reader
14. Navigate back to your **Storage Account** and from **Security + networking** menu, select **Networking**

15. Navigate to **Public access** tab (the first and default one)

16. Click Manage on the Public network access section

17. Enable **Public network access**

18. From the **Public network access scope**, you have two options:

    1. Enable from all networks: this is less restrictive and will allow any applications to try to establish a successful connection to your storage account.
    2. Enable from selected networks: this will restrict access only to specific IPv4 addresses. If you enable this option, please add the IP address of the machine where MetaDefender Storage Security instance is running. If is running on Kubernetes, please add the IP addresses of the following pods: storagesservice-azureblob, discoveryazureblobservice, remediationsservice-azureblob, scanningservice. If you are moving file from Azure Blob to another type of storage unit, please add its remediationsservice-{storageType} pod to this list.

19. Now that you have the **Tenant ID**, **Client ID** and the **Client Secret Key**, you can go back in **MetaDefender Storage Security** and finish the Azure Blob integration. Congratulations!

For additional configuration of how MetaDefender Storage Security handles blobs please check [custom configuration](/docs/mdss/4.4.2/configuration/custom-configuration).
