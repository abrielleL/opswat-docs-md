<!-- source: https://www.opswat.com/docs/mdss/integrations/add-a-cloudian-storage -->

# Add a Cloudian Storage

In order to integrate Cloudian On-Premises with MetaDefender Storage Security please follow these steps:

1. From the left side menu, navigate to **Inventory,** click on **Add Account** and choose **S3 Compatible**

2. Give your [account](/docs/mdss/operations/accounts-and-groups) a name so you can easily identify it later
3. Enter the Service URL for your Cloudian endpoint
4. Enter your **Access Key ID**. Scroll to the end of this page for more details.
5. Enter your **Secret Access Key.** Scroll to the end of this page for more details.
6. If you want to enable **path style addressing** for the bucket, tick the checkbox.
7. (Optional) Enable Autodiscovery
8. Once the account is successfully added, navigate to Inventory -> Add Unit -> Choose the account

9. Give your unit an unique name
10. Choose Group
11. Enter a valid bucket name
12. Enter a Folder location (optional)

### [Where can I find the Access Key ID and Secret Access Key](/docs/mdss/integrations/add-a-cloudian-storage#where-can-i-find-the-access-key-id-and-secret-access-key)

To generate an Access Key ID / Secret Access Key pair please follow these steps:

1. Log in to **Cloudian Console** and go to **Security Credentials**
2. From the S3 Access Credentials zone, copy an existing Access Key ID and Secret Key or generate a new one by clicking **Create New Key.**
