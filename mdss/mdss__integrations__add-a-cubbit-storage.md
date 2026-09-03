<!-- source: https://www.opswat.com/docs/mdss/integrations/add-a-cubbit-storage -->

# Add A Cubbit Storage

### [1. Prerequisites](/docs/mdss/integrations/add-a-cubbit-storage#1-prerequisites)

In order to Add a **Cubbit** storage in MDSS, you will need the **Cubbit Service URL,** **Access Key Id,** **Secret Access Key** and the **bucket name**.

### [2. Obtaining the Service URL](/docs/mdss/integrations/add-a-cubbit-storage#2-obtaining-the-service-url)

1. Enter **s3.cubbit.eu** as the REST Endpoint or if you have a custom tenant **s3.[your-tenant].cubbit.eu.**

### [3. Obtaining Access Keys](/docs/mdss/integrations/add-a-cubbit-storage#3-obtaining-access-keys)

1. **Access Console:** Go to the Cubbit console dashboard.
2. **Find Access Keys:** Look for **API keys** in the side menu
3. **Generate Keys:** Create a new set of keys, following any provided guidelines.
4. **Record Keys:** Securely note down your **Access Key ID** and **Secret Access Key**.

### [4. Obtaining the bucket name](/docs/mdss/integrations/add-a-cubbit-storage#4-obtaining-the-bucket-name)

1. **Login:** Sign into Cubbit and navigate to the dashboard.
2. **Identify Bucket:** Find your bucket in the list and note its name.

### [5. Adding Cubbit storage in MDSS](/docs/mdss/integrations/add-a-cubbit-storage#5-adding-cubbit-storage-in-mdss)

Once you have the details above, go to your MDSS web page, **Storage Units** page, click **Add storage unit**, choose **Cubbit** and fill the form.

### [6. Limitations](/docs/mdss/integrations/add-a-cubbit-storage#6-limitations)

Bucket Versioning not supported

Due to a known issue with the Cubbit, any action that MDSS does to delete a version of the file will not work as expected. This will not affect in any way a user that doesn't use bucket versioning
