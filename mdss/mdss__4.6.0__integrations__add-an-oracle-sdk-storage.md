<!-- source: https://www.opswat.com/docs/mdss/4.6.0/integrations/add-an-oracle-sdk-storage -->

# Add An Oracle SDK Storage

### 1. Prerequisites

In order to Add an Oracle SDK storage in MDSS, you will need an **Oracle API Key including UserId, Fingerprint, Tenancy, Region and Private Key, and the bucket name**

1. From the left side menu, navigate to **Inventory**, click **Add New** > **Account**, choose **Oracle** and click **Next**

![](https://uploads.developerhub.io/prod/k8zL/h0it0vp8gyp8q1qcn5ragv39wcyufuwfpuxdacsgbp7sehu0lc94aaodasrvd0b0.png)

2. Choose the **Oracle** option

![](https://uploads.developerhub.io/prod/k8zL/5fxwwcc0c3qtdydqb2mizsk1tkyjazurtr04wddhyq3ly8ccljb4k0529ti8wyts.png)

3. Give your storage a name so you can easily identify it later
4. There are two ways to connect:
   - **via the IAM role from the instance:** please skip to [using IAM Role for authentification](#using-iam-role-for-authentication)
   - **using security credentials**
5. Enter your **User Id**, **Fingerprint**, **Tenancy**, **Region** and **Private Key**
6. Enter the **name of the bucket** you wish to process with **MetaDefender Storage Security**.
7. If you wish to only process a particular folder enter the name or path of the folder in the **Folder location** field. Leave this field empty if you wish to process the entire bucket.
8. Select **Continue** in order to finish the process.

## Where can I find the Credentials?

To generate the required credentials please follow these steps:

1. Log in to Oracle Console and go to **My Profile** in the top right
2. From there go to **Token and Keys** tab
3. Click **Add API Key**
4. Download the **Private Key** and Click **Add**
5. After that all the required credentials will be generated and can be copied into **MetaDefender Storage Security**

## Using IAM Role for authentication

Allow your **MetaDefender Storage Security** instance to use the **Instance Principals** to access Object Storage (buckets and objects) securely without embedding credentials.

1. Create a **Dynamic Group**  with at least the following matching rule `instance.id = <your instance id>`
2. Create an **IAM Policy** with  the following statements
   1. Allow dynamic-group <your-dynamic-group> to manage buckets in tenancy
   2. Allow dynamic-group <your-dynamic-group> to manage objects in tenancy

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
