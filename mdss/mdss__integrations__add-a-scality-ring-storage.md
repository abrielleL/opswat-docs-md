<!-- source: https://www.opswat.com/docs/mdss/integrations/add-a-scality-ring-storage -->

# Add a Scality RING Storage

### [1. Prerequisites](/docs/mdss/integrations/add-a-scality-ring-storage#1-prerequisites)

In order to Add a **Scality RING** storage in MDSS, you will need the **Service URL**, **Access Key Id / Secret Access Key** and the **bucket name**.

### [2. Obtaining the Service URL](/docs/mdss/integrations/add-a-scality-ring-storage#2-obtaining-the-service-url)

The Service URL is the S3 endpoint URL of your Scality RING, used to access the S3 services on the RING. It is typically available via the **Supervisor interface** under **S3 Services**.

### [3. Obtaining Access Keys](/docs/mdss/integrations/add-a-scality-ring-storage#3-obtaining-access-keys)

Access keys are managed through the Scality RING Supervisor's S3 Console.

1. Click the target account’s Actions Key icon to call the Manage access keys dialog.
2. Click Generate a new key. A confirmation dialog will display.
3. Click Proceed to trigger account access key creation. The dialog will indicate the success of the operation, as well the AccessKey (click Show to view the SecretAccessKey).

Warning

Copy and save SecretAccessKey to a secure location. It is not shown again and cannot be recovered later.

### [4. Obtaining the bucket name](/docs/mdss/integrations/add-a-scality-ring-storage#4-obtaining-the-bucket-name)

1. **Go to Buckets:** Locate the "Buckets" section
2. **Identify Bucket:** Find your bucket in the list and note its name.

### [5. Adding Scality RING storage in MDSS](/docs/mdss/integrations/add-a-scality-ring-storage#5-adding-scality-ring-storage-in-mdss)

In order to integrate Scality RING with MetaDefender Storage Security please follow these steps:

1. From the left side menu, navigate to **Inventory,** click on **Add -> Account** and choose **Scality RING**

2. Give your [account](/docs/mdss/operations/accounts-and-groups) a name so you can easily identify it later

2. Enter the Service URL for your Scality RING endpoint
3. Enter your **Access Key ID**. Scroll to the end of this page for more details.
4. Enter your **Secret Access Key.** Scroll to the end of this page for more details.
5. (Optional) Enable Autodiscovery
6. Once the account is successfully added, navigate to Inventory -> Add Unit -> Choose the previously created account

9. Give your unit an unique name
10. Choose Group
11. Enter a valid bucket name
12. Enter a Folder location (optional)

### [Necessary policies](/docs/mdss/integrations/add-a-scality-ring-storage#necessary-policies)

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
