<!-- source: https://www.opswat.com/docs/supply-chain/integrations/add-a-gitlab-service -->

# Add A GitLab Service

In order to integrate **GitLab** with MetaDefender Software Supply Chain, please follow these steps:

1. From the left side menu, navigate to **Inventory** and choose **GitLab**.
2. Give your connection a name so you can easily identify it later.

![](https://uploads.developerhub.io/prod/jdK6/crgtcqpayuw9e9s7e8tcrv4xhkxhfw1zwe4q1tvqi804c59ey637vhskmqg47bf1.png)

3. Enter your **GitLab domain**. The default one is: [https://gitlab.com/](https://gitlab.com)
4. Enter your **GitLab Access Token**. Scroll to the end of this page for more details.
5. Select **Add Connection** in order to finish the process.

### Where I can find the Access Token?

1. Log in to your **GitLab** instance.
2. Click on your profile picture (top-right corner).
3. Select **Edit Profile**.
4. From the left sidebar, click **Access Tokens.**
5. Enter a **name** so you can easily identify it later and a **expiration date** (optional but recommended)
6. Set the mandatory scopes:
   - **api**: Required if you want to enable soft-delete remediation actions
   - **read_api**: Required for read-only access
   - **read_repository**: Required for read-only access and scanning actions.
   - **write_repository**: Required if you want to enable soft-delete remediation actions.
7. Click on **Create personal access token.**
8. Store the token somewhere safe because you will not be able to view it again.
