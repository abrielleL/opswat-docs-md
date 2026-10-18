<!-- source: https://www.opswat.com/docs/mdss/4.6.0/integrations/add-an-onedrive-storage -->

# Add an OneDrive Storage

In order to integrate Microsoft OneDrive service with MetaDefender Storage Security you will be required to create an application registration, assign the necessary permissions and then generate a secret key. Please follow these steps:

> **Info**
>
> When the upload process takes more than a few seconds, OneDrive creates a temporary file having the same name as your uploading file and the size of 0 bytes. By default, we will discover that file and show it into the list of discovered files. Once the upload is complete, we will discover the original uploaded file and process it accordingly. To skip the discovery of the temporary empty file created, please follow these instructions: [How to handle empty objects in Discovery?](https://www.opswat.com/docs/mdss/where-to-get-help/how-to-handle-empty-objects-in-discovery)

1. From the left side menu, navigate to **Inventory**, click **Add New** > **Account**, choose **OneDrive** and click **Next**

![](https://uploads.developerhub.io/prod/k8zL/t8fo6j2li51gtrg4o4xmo695kwsaaksxty0ubshsvfbb6ipppeg4p8pvj3o025x6.png)

2. Give your [account](https://www.opswat.com/docs/mdss/operations/accounts-and-groups) a name so you can easily identify it later
3. Enter your **Tenant ID**. Scroll to the end of this page for more details.
4. Enter your **Client ID.** Scroll to the end of this page for more details.
5. Enter your **Client Secret.** Scroll to the end of this page for more details.
6. Once the account is added, proceed with adding the unit

![](https://uploads.developerhub.io/prod/k8zL/oe4jesk9ch9wg3mro5oejc286m9promt74tffaidu7l9qyxvvvjt0qfjnwevs94y.png)

6. Enter an unique name for your unit
7. Assign the unit to a Group
8. Optionally, enter the name of a OneDrive Group that you want to protect
9. Optionally, enter the **UPN** of a user from the selected group if you wish to only process files from that specific user.
10. Optionally, enter the **name of a folder** from the user's files if you wish to only process files from that folder. This field will appear only if there is a value inputted in the **User** field.
11. Select **Continue** in order to finish the process.

### How to create a OneDrive application

In order to process your OneDrive files and folders with MetaDefender Storage Security you will be required to add a new app registration in your Microsoft Entra ID Azure Portal.

1. Log in to [Azure Portal](https://portal.azure.com/) and from the left navigation menu choose **Microsoft Entra ID**

![](https://uploads.developerhub.io/prod/k8zL/7awdgppmhieg3242alrbai4ghzg6ghm873i9444yby0oy6ud9jgi8tx92sgwxwlg.png)

2. Make a copy of the **Tenant ID** from the overview page

![](https://uploads.developerhub.io/prod/k8zL/xbv39a5akoq8z4o5pl1zj7s3blx7hra1c03l99s1rqj82fgzolgwd54moqd0yb0q.png)

3. From the left side menu, choose **App registrations**
4. Click **New registration**
5. Give your app a name so you can easily identify it

![](https://uploads.developerhub.io/prod/k8zL/rx64f0sfdrbwl61169peui8xff05fh3ws1t6048zz1bsbb971151xg15eaubi5s4.png)

6. There is no need to modify the other properties. When ready, please click **Register**
7. From the **Overview** page of your newly created application, make a copy of **Application (client) ID**

![](https://uploads.developerhub.io/prod/k8zL/lb4yobfs1dl9cxxj1knuhjb5nhiuey6mzex12cwzi2eqz380ei3ce7gu8j4daeif.png)

8. You now need to specify which permissions should the application have. To do this, please navigate to **API permissions** from the left-side menu
9. Click **Add a permission**

![](https://uploads.developerhub.io/prod/k8zL/l1qfaym2zff9jxl6cwxozus9ncov6wwb5f1uifjqbten9j0pv8b6qibi3dpp7p6u.png)

10. Select **Microsoft Graph** from the right-side menu

![](https://image-archive.developerhub.io/image/upload/v2_5262/m2bcmlqyxnyvrxicdjvt/1626944043.png)

11. Select **Application permissions**

![](https://image-archive.developerhub.io/image/upload/v2_5262/ywegap1dm5zfgdv85g9l/1626944048.png)

12. In order for MetaDefender Storage Security to correctly work please add the following permissions:
    1. Files.ReadWrite.All
    2. Group.Read.All
    3. Sites.Read.All
    4. User.Read.All
13. When ready, click **Add permissions**
14. We need to grant admin consent for the added permissions

![](https://uploads.developerhub.io/prod/k8zL/oawzoop4l6sveyxweeq3jxdwxofuuyi6u69bt1rwn0o7aueon6huvg7bkea55mp1.png)

15. Now that the required permissions are in place, you are ready for the final step. Please navigate to **Certificates & secrets** from the left-side menu
16. Click **New client secret** and choose Expires in 24 months

![](https://uploads.developerhub.io/prod/k8zL/15eh3wo2rfysestwidul0ykjfbaidkeslz5nvfzc5k68f7f4jbh06miideg8poo4.png)

17. Click **Add** and then your will need to make a copy of the generated **secret key** because it will not be available later
18. Now that you have the **Tenant ID,** the **Client ID** and the **Client Secret Key** you can go back in **MetaDefender Storage Security** and finish the OneDrive integration. Congratulations!

![](https://uploads.developerhub.io/prod/k8zL/4c8tjshptjb9vmtf6wsrcmflouiy4es7c5666jsg10jfyazmjk79rdfo65tq04yz.png)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
