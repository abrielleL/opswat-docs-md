<!-- source: https://www.opswat.com/docs/supply-chain/integrations/add-a-github-service -->

# Add A GitHub Service

In order to integrate GitHub with MetaDefender Software Supply Chain, please follow these steps:

1. From the left side menu, navigate to **Inventory** and choose GitHub
2. There are two ways to connect

![](https://uploads.developerhub.io/prod/jdK6/0ne6k50qducdua2bnhphl6ayhfw29hlsifmufaxw6pf6evo8lrikk2dx7zwyaq9u.png)

- **Using a GitHub App**

![](https://uploads.developerhub.io/prod/jdK6/46gyexlyie6g5l6usxw776ocjrxu5spx1tadrm8laivgz1utte09vvrj90x84c5l.png)

- **Using a GitHub Personal Access Token**

![](https://uploads.developerhub.io/prod/jdK6/dxhgk1rxj89ytkrcs8imblzrhd0r5tsqarrqookimguz28eo3mwee04kbp4xyigv.png)

3. Give your connection a name so you can easily identify it later.
4. Enter your **Access Token**. Scroll to the end of this page for more details.
5. Enter your **App ID**. Scroll to the end of this page for more details.
6. Enter your **Installation ID**. Scroll down to the end of this page for more details.
7. Enter your **Private Key**. Scroll down to the end of this page for more details.
8. Select **Add Connection** in order to finish the process.

### Where can I find the Access Token?

To generate an Access Token, please follow these steps:

1. Log in to [GitHub](https://github.com/) and go to **Settings**.
2. Navigate to **Developer Settings** and from the left menu, select **Personal access tokens**, and then **Tokens (classic)**.
3. Click on **Generate new token (classic).**
4. Give it a **Note** so you can easily identify it later.
5. Set the **Expiration** to **No expiration**.
6. The scopes required by MetaDefender Software Supply Chain are:
   - repo
     - `repo:status`
     - `repo_deployment`
     - `public_repo`
     - `repo:invite`
     - `security_events`

> **Info**
>
> By configuring an expiration date for temporary access (e.g., 30 days), the integration with MetaDefender Software Supply Chain will be operational exclusively for the specified duration. Once this period elapses, you will have to create a new token and update the connection.

### Permissions for copy remediation

Copy remediation pushes the scanned repository to a destination repository. The destination connection needs write access to that repository:

- **Personal Access Token (classic):** the `repo` scope above gives write access.
- **GitHub App:** grant **Contents: Read and write**. For **Create Pull Request**, also grant **Pull requests: Read and write**.

The destination repository must already exist. MDSSC does not create it.

With **Push Directly**, MDSSC pushes to the branch that has the same name as the scanned branch. A branch protection rule on that branch can stop the copy. To avoid this, use **Create Pull Request**.

### Registering a new GitHub App

1. Log in to [GitHub](https://github.com/) and go to **Settings**.
2. Navigate to **Developer Settings** from the left menu and click on **New GitHub App**.
3. Fill in the required information for your app and configure the permissions your app requires for accessing repositories and performing actions.
4. Once you have filled in all the details, click on the **Create GitHub App** button.
5. Generate and download a **private key** for your app. This key will be used for authentication.
6. On the app settings page, scroll down to the **Install App** section.
7. Click on the **Install** button next to the repository where you want to install your app.
8. Review the access permissions and click **Install** again to confirm.
9. The **GitHub App ID**, **GitHub App Installation ID**, and the contents of the **Private Key** are required in order to see the connection.
10. Navigate to Settings -> Developer settings and click on your GitHub App. Copy the App ID from here and provide it in the input field.
11. Navigate to **Install App**, click on the configure icon and in the URL you will find the **Installation ID** (e.g. [https://github.com/settings/installations/**{InstallationID}](https://github.com/settings/installations/**%7BInstallationID%7D)**).
12. Copy the contents of your previously downloaded **Private Key** (including the headers) and paste them in the input field.

---

[All pages in this documentation](https://www.opswat.com/docs/supply-chain/llms.txt)
