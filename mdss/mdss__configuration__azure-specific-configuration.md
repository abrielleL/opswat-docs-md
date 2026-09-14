<!-- source: https://www.opswat.com/docs/mdss/configuration/azure-specific-configuration -->

# Azure AD Specific Configuration

To set up Azure AD SSO for MDSS, follow these steps:

1. In the Microsoft Azure portal, navigate to **App registrations** and click on **New registration**

2. In the **Register an application** window, enter a name for your application, select your preferred configuration for **Supported account types** (recommended is Single tenant), and configure the **Redirect URI**. The redirect URI should be composed of the address where MDSS is deployed, along with the **/callback** suffix added to the path.

3. Afterwards, navigate to the **Overview** tab. There, to successfully configure the SSO Configuration in MDSS afterwards, store the **Application (Client) ID** and the **Direcory (Tenant) ID** somewhere safe on your computer. Then, click on the **Endpoints** button.

4. There, the authority URL is located in the right-hand side menu and is the following: **"https: //login.microsoftonline.com/<YOUR-TENANT-ID >/v2.0"**

5. Navigate to the **Certificates & secrets** tab and click on **New client secret**

6. Give a description to your client secret, configure the expiration to your liking, and add it

7. Copy your secret value and store it somewhere safe on your computer (you will only be able to copy it at this stage)

8. Navigate to **App Roles** and click on **Create app role**

9. Give your role a Display name, configure the **Allowed member types** to be set to **Both (Users/Groups + Applications)**. Then, for the value, give one of the two values to determine the role that this user will have within MDSS:

- **SsoAdministrator** - equivalent to the administrator role in MDSS
- **SsoReadOnlyAdministrator** - equivalent to the read-only admin role in MDSS

10. Navigate to the **API permissions** and click on **Add a permission**. Then, select the **My APIs** tab and find your app

11. Click on your app and select the app role you have configured.

12. Next, click on **Grant admin consent**

13. Go to the **Authentication** tab. Here, click **Add a platform** and select the **Web** option. Then, click on the checkbox for **ID tokens** and also for **Supported account types**, select whatever you prefer (recommended is Single tenant).

14. Now, leave the **Azure Portal** and navigate to the **Microsoft Entra admin center**. Here, find the **Enterprise applications** window under the **Applications** tab on the left. Search for your configured app.

15. Navigate to the **Users and groups** tab and select **Add user/group**

16. Find your user and assign the configured App Role to it.

17. Lastly, navigate to **App registrations**, find your app and click on the **Token configuration**. There, click on **Add optional claim**, select **ID**, and add the **email** claim.
