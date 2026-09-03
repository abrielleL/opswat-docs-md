<!-- source: https://www.opswat.com/docs/supply-chain/integrations/add-an-azure-devops-service -->

# Add An Azure DevOps Service

In order to integrate **Azure DevOps** with MetaDefender Software Supply Chain, please follow these steps:

1. From the left side menu, navigate to **Inventory** and choose **Azure DevOps**.
2. Give your connection a name so you can easily identify it later.

![](https://uploads.developerhub.io/prod/jdK6/dzd8ywl4lhu8e8iw4fbzqgppiuazs2wnqgv2ym8if8hcofyxzxiduj573pi8gcce.png)

3. Enter your **Azure DevOps Organization** name. Scroll to the end of this page for more details.
4. Enter your **Azure DevOps Access Token**. Scroll to the end of this page for more details.
5. Select **Add Connection** in order to finish the process.

### Where can I find the Organization name?

In order to find the Organization name, the following options are available:

1. From the **Azure DevOps URL:**
   - When you access Azure DevOps, the URL format is `https://dev.azure.com/[OrganizationName]`.
   - The Organization name is the part after `dev.azure.com/`.
2. From **Azure DevOps Home Page:**
   - Log in to your Azure DevOps account.
   - Organization name is displayed in the top-left corner.
3. From your Administrator:
   - If you are unsure, contact your Azure DevOps administrator or project lead.

### Where can I find the Access Token?

1. Log in to your **Azure DevOps** account.
2. Click on **User settings** icon (top-right corner, next to profile picture).
3. Select **Personal access tokens**.
4. Click the **+ New Token** button.
5. Enter a **name** so you can easily identify it later and an **expiration date.**
6. Under **Scopes** select **Custom defined** option.
7. For **Code** category**,** select the mandatory scopes:
   - **Read & Write**: Read is required to access repositories and Write is required if you want to enable soft-delete remediation actions.
8. Click on **Create.**
9. Store the token somewhere safe because you will not be able to view it again.
