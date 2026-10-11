<!-- source: https://www.opswat.com/docs/mdss/4.5.2/integrations/add-a-scality-ring-storage -->

# Add a Scality RING Storage

### 1. Prerequisites

In order to Add a **Scality RING** storage in MDSS, you will need the **Service URL**, **Access Key Id / Secret Access Key** and the **bucket name**.

### 2. Obtaining the Service URL

The Service URL is the S3 endpoint URL of your Scality RING, used to access the S3 services on the RING. It is typically available via the **Supervisor interface** under **S3 Services**.

### 3. Obtaining Access Keys

Access keys are managed through the Scality RING Supervisor's S3 Console.

1. Click the target account’s Actions Key icon to call the Manage access keys dialog. ![](https://uploads.developerhub.io/prod/k8zL/f0cuumjwvjiqke08mps5tq5xpc70581yi41wv5776qodngimul8ndtp03foc7fvx.png)![](https://uploads.developerhub.io/prod/k8zL/1kw29mxt565m5jc43cy2zz1a96qw27cp5rc4hrxi1tuu3zp1rlks0vc6c7077yjj.png)
2. Click Generate a new key. A confirmation dialog will display. ![](https://uploads.developerhub.io/prod/k8zL/lp4m929zx3oit0p2m6tuf96ab6hxft2m9xc1nzxzxpyng44if6y7x4qp3fmfjip0.png)
3. Click Proceed to trigger account access key creation. The dialog will indicate the success of the operation, as well the AccessKey (click Show to view the SecretAccessKey). ![](https://uploads.developerhub.io/prod/k8zL/pzpiibb6t7gs4suzh33nflkix3bbqiyb2af06iceg16mxbi616isrw82tgwxcxlk.png)

> **Warning**
>
> Copy and save SecretAccessKey to a secure location. It is not shown again and cannot be recovered later.

### 4. Obtaining the bucket name

1. **Go to Buckets:** Locate the "Buckets" section
2. **Identify Bucket:** Find your bucket in the list and note its name.

### 5. Adding Scality RING storage in MDSS

In order to integrate Scality RING with MetaDefender Storage Security please follow these steps:

1. From the left side menu, navigate to **Inventory,** click on **Add -> Account **and choose **Scality RING**

![](https://uploads.developerhub.io/prod/k8zL/8udayjz97pwh7p59dmvlok08f4wftcnx8e6eoub32u01e1n4ukxupb9fnibzqhsd.png)

2. Give your [account](https://www.opswat.com/docs/mdss/operations/accounts-and-groups) a name so you can easily identify it later

2. Enter the Service URL for your Scality RING endpoint
3. Enter your **Access Key ID**. Scroll to the end of this page for more details.
4. Enter your **Secret Access Key.** Scroll to the end of this page for more details.
5. (Optional) Enable Autodiscovery
6. Once the account is successfully added, navigate to Inventory -> Add Unit -> Choose the previously created account

![](https://uploads.developerhub.io/prod/k8zL/11c76bb53g6mq1fjdau2f81cryoadubin16ipe2jym23xt6sp4ywqoqf2s8ofm7d.png)

9. Give your unit an unique name
10. Choose Group
11. Enter a valid bucket name
12. Enter a Folder location (optional)
13.

### Necessary policies

These are the necessary policies required in order to add a Scality RING Storage:

- `s3:GetObject`
- `s3:PutObject`
- `s3:GetObjectVersion`
- `s3:ListBucket`
- `s3:ListBucketVersions`
- `s3:GetObjectTagging`
- `s3:GetObjectVersionTagging`
- `s3:PutObjectTagging`
- `s3:PutObjectVersionTagging`
- `s3:DeleteObject`
- `s3:DeleteObjectVersion`

To be able to use client side encryption, additional AWS policies are required:

- `secretsmanager:GetSecretValue`
- `kms:DescribeKey`
- `kms:Decrypt`

To be able to use **server-side encryption with AWS Key Management Service (SSE-KMS)**, additional AWS policies are required:

- `kms:GenerateDataKey`
- `kms:DescribeKey`
- `kms:Decrypt`

To be able to use **autodiscovery**, additional AWS policies are required:

- s3:ListAllMyBuckets

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
