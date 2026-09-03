<!-- source: https://www.opswat.com/docs/supply-chain/operating/bitbucket-cloud -->

# Bitbucket Cloud

1. Login to the Bitbucket Cloud account and navigate to the repository that needs event based scanning.
2. Open the Menu on the left and select "Repository settings", ex:

![](https://uploads.developerhub.io/prod/jdK6/m5cc3xxjdubdmakdxegdjmoiic81cvqgsdoxmrmd1arl4ju6p552sfygcga8uuxe.png)

3. In the new submenu that appears on the left, click on the "Webhooks" under "Workflows", and the following screen will be displayed:

![](https://uploads.developerhub.io/prod/jdK6/cz57flt5npusal12umsh6hj12t813i1awrnposdhkpng5i0naeq34b2o5wc1aiw5.png)

4. Click the button "Add webhook", the user is now presented with the webhook configurations page from below:

![](https://uploads.developerhub.io/prod/jdK6/mxtieuvhuk5n0spreaao0pv7vq6quxg7scez1gkgsogsv0626x5vw2gdmup37n58.png)

- In the "Title" field, type in an arbitrary name of the webhook;
- Insert the previously obtained MDSSC Webhook URL(generated for this repository) to the "URL" field;
- Insert your MDSSC ApiKey to the "Secret" field;

> **Attention:**
>
> Do not push the "Generate secret" button ! Use the ApiKey, of the user that generated the Webhook URL.

- Configure the triggers that are required by the use case

![](https://uploads.developerhub.io/prod/jdK6/lkkqvz4sdx3lyxbcbdgkbmcou8mt8lv8ja3j2auplztfgp30uwztmpuel88e9pzw.png)
