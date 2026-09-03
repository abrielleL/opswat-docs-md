<!-- source: https://www.opswat.com/docs/mdss/4.4.2/integrations/add-a-sharepoint-storage -->

# Add a SharePoint Online Storage

In order to integrate Microsoft SharePoint service with MetaDefender for Secure Storage you will be required to create an application registration, assign the necessary permissions and then generate a secret key. Please follow these steps:

Info

Please note this page is **applicable only for SharePoint Online** and not applicable for SharePoint On Premise. For a guide to integrating a Sharepoint On-Premise deployment, consult this page: [Add a SharePoint On-Premise Storage](/docs/mdss/4.4.2/integrations/add-a-sharepoint-on-premise-storage).

Info

When the upload process takes more than a few seconds, SharePoint creates a temporary file having the same name as your uploading file and the size of 0 bytes. By default, we will discover that file and show it into the list of discovered files. Once the upload is complete, we will discover the original uploaded file and process it accordingly. To skip the discovery of the temporary empty file created, please follow these instructions: [How to handle empty objects in Discovery?](/docs/mdss/4.4.2/where-to-get-help/how-to-handle-empty-objects-in-discovery)

1. From the left side menu, navigate to **Storage units**, click on **Add storage unit** and choose **SharePoint**

2. Give your [account](/docs/mdss/4.4.2/operations/accounts-and-groups) a name so you can easily identify it later
3. Give your storage a name so you can easily identify it later.
4. Check **Enable for Azure Government (GCC High/DoD)** only if your organization uses Microsoft 365 GCC High or DoD environments. Leave unchecked for commercial or standard GCC environments.
5. Enter your **Tenant ID**. Scroll to the end of this page for more details.
6. Enter your **Client ID.** Scroll to the end of this page for more details.
7. Enter your **Client Secret.** Scroll to the end of this page for more details.
8. Enter the **URL of a site** you wish to process files and folders.
9. Enter the **name of a Document Library** from the Site URL if you wish to process files and folders from a specific Document Library. This is optional. In case is not provided, we will process the files and folders from all the **Public Document Libraries** (we do not scan the private ones) that belong to the Site provided at step 6.
10. Enter the **name of a Folder** if you wish to process files and folders only from a specific folder, inside a specific Document Library. To be able to add a folder location, you need to provide a Document Library (step 7). Once a Document Library is provided, a new box with Folder location will appear on the form.

9. Select **Continue** in order to finish the process. If the data you entered is valid, a new SharePoint storage will be created. If is not valid, a specific error message will inform you.

### [How to create a SharePoint application](https://docs.opswat.com/mdss/integrations/add-an-onedrive-storage#how-to-create-a-onedrive-application)

In order to process our SharePoint files and folders with MetaDefender for Secure Storage you will be required to add a new app registration in your Microsoft Entra ID Azure Portal

1. Log in to [Azure Portal](https://portal.azure.com/) and from the left navigation menu choose **Microsoft Entra ID**

2. Make a copy of the **Tenant ID** from the overview page
3. From the left side menu choose **App registrations**
4. Click **New registration**
5. Give your app a name so you can easily identify it

6. There is no need to modify the other properties. When ready, please click **Register**
7. From the **Overview** page of your newly created application, make a copy of **Application (client) ID **

8. You now need to specify which permissions should the application have. To do this, please navigate to **API permissions** from the left-side menu
9. Click **Add a permission **

10. Select **Microsoft Graph** from the right-side menu

11. Select **Application permissions **

12. In order for MetaDefender Storage Security to correctly work please add the following permissions:

    1. Files.ReadWrite.All
    2. Sites.Read.All
13. When ready, click **Add permissions**
14. We need to grant admin consent for the added permissions

15. Now that the required permissions are in place, you are ready for the final step. Please navigate to **Certificates & secrets** from the left-side menu
16. Click **New client secret** and make sure that it **will not expire** as long as MetaDefender Storage Security is using it
17. Click **Add** and then you will need to make a copy of the generated **secret key** because it will not be available later

18. Now that you have the **Tenant ID,** the **Client ID** and the **Client Secret Key** you can go back in **MetaDefender Storage Security** and finish the SharePoint integration. Congratulations!

---
