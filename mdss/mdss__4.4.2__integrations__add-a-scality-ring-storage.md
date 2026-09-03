<!-- source: https://www.opswat.com/docs/mdss/4.4.2/integrations/add-a-scality-ring-storage -->

# Add a Scality RING Storage

### [1. Prerequisites](/docs/mdss/4.4.2/integrations/add-a-scality-ring-storage#1-prerequisites)

In order to Add a **Scality RING** storage in MDSS, you will need the **Service URL**, **Access Key Id / Secret Access Key** and the **bucket name**.

### [2. Obtaining the Service URL](/docs/mdss/4.4.2/integrations/add-a-scality-ring-storage#2-obtaining-the-service-url)

The Service URL is the S3 endpoint URL of your Scality RING, used to access the S3 services on the RING. It is typically available via the **Supervisor interface** under **S3 Services**.

### [3. Obtaining Access Keys](/docs/mdss/4.4.2/integrations/add-a-scality-ring-storage#3-obtaining-access-keys)

Access keys are managed through the Scality RING Supervisor's S3 Console.

1. Click the target account’s Actions Key icon to call the Manage access keys dialog.
2. Click Generate a new key. A confirmation dialog will display.
3. Click Proceed to trigger account access key creation. The dialog will indicate the success of the operation, as well the AccessKey (click Show to view the SecretAccessKey).

Warning

Copy and save SecretAccessKey to a secure location. It is not shown again and cannot be recovered later.

### [4. Obtaining the bucket name](/docs/mdss/4.4.2/integrations/add-a-scality-ring-storage#4-obtaining-the-bucket-name)

1. **Go to Buckets:** Locate the "Buckets" section
2. **Identify Bucket:** Find your bucket in the list and note its name.

### [5. Adding Scality RING storage in MDSS](/docs/mdss/4.4.2/integrations/add-a-scality-ring-storage#5-adding-scality-ring-storage-in-mdss)

Once you have the details above, go to your MDSS web page, **Storage Units** page, click **Add storage unit**, choose **Scality RING** and fill the form.
