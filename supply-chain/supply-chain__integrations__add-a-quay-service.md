<!-- source: https://www.opswat.com/docs/supply-chain/integrations/add-a-quay-service -->

# Add A Quay Service

In order to integrate Quay with MetaDefender Software Supply Chain, please follow these steps:

1. From the left side menu, navigate to **Inventory** and choose **Quay**
2. Give your connection a name so you can easily identify it later.

![](https://uploads.developerhub.io/prod/jdK6/x46g1lm8n338hlkayrmp38r24lhf4lm2nil5weu1sm05sot7knhuvuzjllib194s.png)

3. Enter your **Registry URL**. Scroll to the end of this page for more details.
4. Enter your **Application Token**. It is used to list your repositories through the Quay API. Scroll to the end of this page for more details.
5. Enter your **Robot Token**. It is used to log in to the registry and pull images for scanning. Scroll to the end of this page for more details.
6. Select **Add Connection** in order to finish the process.

> **Info**
>
> Both tokens are required. The Application Token alone cannot pull images, and the Robot Token alone cannot list repositories.

### Where can I find the Quay Registry URL?

To get your Registry URL, please follow these steps:

1. Log in to your Quay Domain and head to **Account Settings**.
2. The Registry URL is found at the top or within the account details.

> **Info**
>
> If the input is left empty, [https://quay.io](https://quay.io) will be used as default.

### How to generate the Application Token?

To generate the Application Token, please follow these steps:

1. Log in to your Quay domain.
2. Navigate to the desired organization you want to generate the application token for.
3. From the left-hand menu, find and click on the **Applications** tab.
4. Click the **Create New Application**.
5. Fill out the required information for your application, ensuring it is correctly set up for your organization's needs.
6. Click on the application's name to access its details.
7. In the left-hand menu of the application page, click on **Generate Token**
8. There are two options for the access token:
   - Check **View all visible repositories** option if you want the token to have access to all repositories within the organization.
   - Select the repositories you want to use for the integration.
9. Click on the **Generate Access Token** button to generate the token for your application.
10. You may be prompted to authorize the application. If applicable, click on **Authorize Application** to confirm the token generation.
11. Once the token is generate and authorized, it will be displayed on the screen.

> **Info**
>
> Ensure you keep the access token secure as it grants access to your organization's resources.

### How to generate the Robot Token?

To generate the Robot Token, please follow these steps:

1. Log in to your Quay domain.
2. Navigate to the desired organization you want to generate the robot token for.
3. In the left-hand menu, find and click on **Robot Accounts**.
4. Click on **Create Robot Account**.
5. Give it a name to easily identify it.
6. Select the desired repositories by checking the appropriate boxes.
7. Click **Add Permissions** to confirm the repository access.
8. Click on the newly created robot account to access its details.
9. Look for **Docker Configuration** within the robot account settings.
10. Click on **View (your-organization-robot-name).json**.
11. Locate the **auth** field in the JSON configuration.
12. Copy the value of **auth** without the quotation marks - this is your robot token.

---

[All pages in this documentation](https://www.opswat.com/docs/supply-chain/llms.txt)
