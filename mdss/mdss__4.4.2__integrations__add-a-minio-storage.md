<!-- source: https://www.opswat.com/docs/mdss/4.4.2/integrations/add-a-minio-storage -->

# Add a MinIO Storage

The minimum supported MinIO version is **RELEASE.2020-09-10T22-05-01Z**.

In order to integrate **MinIO** with MetaDefender Storage Security please follow these steps:

1. From the left side menu, navigate to **Storage units,** click on **Add Storage Unit** and choose **S3 Compatible**

2. Give your [account](/operations/accounts-and-groups) a name so you can easily identify it later
3. Give your storage a name so you can easily identify it later
4. Enter your **Access Key ID**. Scroll to the end of this page for more details.
5. Enter your **Secret Access Key.** Scroll to the end of this page for more details.
6. Choose a the **region endpoint** where your S3 endpoint is located.
7. Enter the **name of the bucket** you wish to process with MetaDefender Storage Security.
8. If you want to enable **path style addressing** for the bucket, tick the checkbox.
9. If you wish to only process a particular folder enter the name or path of the folder in the **Folder location** field. Leave this field empty if you wish to process the entire bucket.
10. Select **Continue** in order to finish the process.

### Where can I find the Access Key ID and Secret Access Key

To generate an Access Key ID / Secret Access Key pair please follow these steps:

1. Log in to **MinIO Console** and go to **Access Keys**
2. Copy an existing Access Key ID and Secret Key or generate a new one by clicking **Create New Key.**
