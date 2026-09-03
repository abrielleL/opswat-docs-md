<!-- source: https://www.opswat.com/docs/supply-chain/integrations/add-a-gitea-service -->

# Add A Gitea Service

In order to integrate **Gitea** with MetaDefender Software Supply Chain, please follow these steps:

1. From the left side menu, navigate to **Inventory** and choose **Gitea**.
2. Give your connection a name so you can easily identify it later.

![](https://uploads.developerhub.io/prod/jdK6/7z1vgfnttefhda60er3xbon9u2oivbuv9izi7ydn9vr5ia0weysfnobl5s4sauj4.png)

3. Enter your **Gitea domain**.
4. Enter your **Gitea Access Token**. Scroll to the end of this page for more details.
5. Select **Add Connection** in order to finish the process.

### Where I can find the Access Token?

1. Log in to your **Gitea** instance.
2. Click on your profile picture icon avatar (top-right corner).
3. Select **Settings** from the dropdown menu.
4. In Settings page, click on **Applications** tab in the left sidebar.
5. Scroll down to the **Generate New Token** section.
6. Enter a descriptive **name** so you can easily identify it later.
7. Set the mandatory scopes for **repo**:
   - **Read**: Required for read-only access and scanning actions.
   - **Write**: Required if you want to enable remediation actions.
8. Click on **Generate Token.**
9. Store the token somewhere safe because you will not be able to view it again.
