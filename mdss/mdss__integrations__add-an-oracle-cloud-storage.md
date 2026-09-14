<!-- source: https://www.opswat.com/docs/mdss/integrations/add-an-oracle-cloud-storage -->

# Add An Oracle Cloud Storage

Oracle Cloud Storage can be integrated into MetaDefender Storage Security (MDSS) in **two different ways**:

1. **Using the S3-Compatible API** – This method allows MDSS to connect to Oracle Object Storage using S3-style access credentials (Access Key and Secret Key).
2. **Using the Oracle Native SDK (OCI SDK)** – This method uses Oracle’s native authentication system with API keys or IAM roles for a more direct and secure integration.

## [Integration via S3-Compatible](/docs/mdss/integrations/add-an-oracle-cloud-storage#integration-via-s3-compatible)

#### [1. Prerequisites](/docs/mdss/integrations/add-an-oracle-cloud-storage#1-prerequisites)

In order to Add an Oracle Cloud storage in MDSS, you will need the **Oracle Cloud Service URL**, **Access Key Id / Secret Access Key** and the **bucket name**.

#### [2. Obtaining the Service URL](/docs/mdss/integrations/add-an-oracle-cloud-storage#2-obtaining-the-service-url)

1. To construct the URL, you will need to have you bucket's object storage namespace and region. The namespace can be found the navigating to one of your existing buckets and opening it. Afterwards, construct the URL like this: **https://<your_object_storage_namespace>.compat.objectstorage.<your_region>.oraclecloud.com**

#### [3. Obtaining Access Key ID](/docs/mdss/integrations/add-an-oracle-cloud-storage#3-obtaining-access-key-id)

1. Log in to your Oracle Cloud dashboard at **cloud.oracle.com**
2. In the top-right corner, open the **Profile** menu by clicking on your profile icon and afterwards, click on **My profile**
3. From the **Resources** tab**,** navigate to **Customer secret keys** and either click **Generate secret key** or copy an existing one from the list

#### [4. Obtaining Secret Access Key](/docs/mdss/integrations/add-an-oracle-cloud-storage#4-obtaining-secret-access-key)

1. Log in to your Oracle Cloud dashboard at **cloud.oracle.com**
2. In the top-right corner, open the **Profile** menu by clicking on your profile icon and afterwards, click on **My profile**
3. Click **Generate secret key** and give the key any name you like
4. Save the generated key secret somewhere safe. You can only see it at creation

#### [5. Adding the Oracle Cloud storage in MDSS as an S3 Compatible](/docs/mdss/integrations/add-an-oracle-cloud-storage#5-adding-the-oracle-cloud-storage-in-mdss-as-an-s3-compatible)

Once you have the details above, go to your MDSS web page, **Storage Units** page, click **Add storage unit**, click **Oracle,** choose **Oracle S3 Compatible** and fill the form.

## [Integration via Oracle Native SDK (OCI SDK)](/docs/mdss/integrations/add-an-oracle-cloud-storage#integration-via-oracle-native-sdk-oci-sdk)

#### [1. Prerequisites](/docs/mdss/integrations/add-an-oracle-cloud-storage#1-prerequisites)

In order to Add an Oracle SDK storage in MDSS, you will need an **Oracle API Key including UserId, Fingerprint, Tenancy, Region and Private Key, and the bucket name**

1. From the left side menu, navigate to **Storage units**, click on **Add Storage** Unit and choose **Oracle**

2. Choose the **Oracle** option

3. Give your storage a name so you can easily identify it later
4. There are two ways to connect:

   - **via the IAM role from the instance:** please skip to [using IAM Role for authentication](/docs/mdss/integrations/add-an-oracle-cloud-storage#using-iam-role-for-authentication)
   - **using security credentials**
5. Enter your **User Id**, **Fingerprint**, **Tenancy**, **Region** and **Private Key**
6. Enter the **name of the bucket** you wish to process with **MetaDefender Storage Security**.
7. If you wish to only process a particular folder enter the name or path of the folder in the **Folder location** field. Leave this field empty if you wish to process the entire bucket.
8. Select **Continue** in order to finish the process.

#### [Where can I find the Credentials?](/docs/mdss/integrations/add-an-oracle-cloud-storage#where-can-i-find-the-credentials)

To generate the required credentials please follow these steps:

1. Log in to Oracle Console and go to **My Profile** in the top right
2. From there go to **Token and Keys** tab
3. Click **Add API Key**
4. Download the **Private Key** and Click **Add**
5. After that all the required credentials will be generated and can be copied into **MetaDefender Storage Security**

#### [Using IAM Role for authentication](/docs/mdss/integrations/add-an-oracle-cloud-storage#using-iam-role-for-authentication)

Allow your **MetaDefender Storage Security** instance to use the **Instance Principals** to access Object Storage (buckets and objects) securely without embedding credentials.

1. Create a **Dynamic Group** with at least the following matching rule `instance.id = <your instance id>`
2. Create an **IAM Policy** with the following statements

   1. Allow dynamic-group <your-dynamic-group> to manage buckets in tenancy
   2. Allow dynamic-group <your-dynamic-group> to manage objects in tenancy

This setup allows your MDSS instance to securely access Oracle Object Storage using Oracle Cloud’s native identity management system.
