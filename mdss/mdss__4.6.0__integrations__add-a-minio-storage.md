<!-- source: https://www.opswat.com/docs/mdss/4.6.0/integrations/add-a-minio-storage -->

# Add a MinIO Storage

> **Info**
>
> The minimum supported MinIO version is **RELEASE.2020-09-10T22-05-01Z**.

In order to integrate MinIO with MetaDefender Storage Security please follow these steps:

1. From the left side menu, navigate to **Inventory**, click **Add New** > **Account**, choose **S3 Compatible** and click **Next**

![](https://uploads.developerhub.io/prod/k8zL/e2eu1r6wkvb8r1uq1vlqv9qqox4sbh25ekcthfkqlb19xn5eu9vf69hek5xsh1wj.png)

2. Give your [account](https://www.opswat.com/docs/mdss/operations/accounts-and-groups) a name so you can easily identify it later
3. Enter the Service URL for your MinIO endpoint
4. Enter your **Access Key ID**. Scroll to the end of this page for more details.
5. Enter your **Secret Access Key.** Scroll to the end of this page for more details.
6. If you want to enable **path style addressing** for the bucket, tick the checkbox.
7. (Optional) Enable Autodiscovery
8. Once the account is successfully added, navigate to **Inventory**, click **Add New** > **Unit**, choose the account and click **Next**

![](https://uploads.developerhub.io/prod/k8zL/5xbjdexhbmihatm278prsleykao42ylk9647z3fj5574i6lq7ikbjx7h505okhaw.png)

9. Give your unit an unique name
10. Choose Group
11. Enter a valid bucket name
12. Enter a Folder location (optional)

### Where can I find the Access Key ID and Secret Access Key

To generate an Access Key ID / Secret Access Key pair please follow these steps:

1. Log in to **MinIO Console** and go to **Access Keys**
2. Copy an existing Access Key ID and Secret Key or generate a new one by clicking **Create New Key.**

![](https://uploads.developerhub.io/prod/k8zL/e0df11ktrr1c63ibm6oq75on1yjjuknpfgaj21qw89pkuvjqe5xupyyn7bhhkrd9.png)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
