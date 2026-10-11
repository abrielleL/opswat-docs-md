<!-- source: https://www.opswat.com/docs/mdss/integrations/add-a-cubbit-storage -->

# Add A Cubbit Storage

### 1. Prerequisites

In order to Add a **Cubbit** storage in MDSS, you will need the **Cubbit Service URL,** **Access Key Id,** **Secret Access Key** and the **bucket name**.

![](https://uploads.developerhub.io/prod/k8zL/hibl7fo462a5n4nkc3xalm8ryxv6m1wihusi9l61t0t4qwtisbl8jdh5p56qlc2m.png)

### 2. Obtaining the Service URL

1. Enter **s3.cubbit.eu** as the REST Endpoint or if you have a custom tenant **s3.[your-tenant].cubbit.eu.**

### 3. Obtaining Access Keys

1. **Access Console:** Go to the Cubbit console dashboard.
2. **Find Access Keys:** Look for **API keys** in the side menu
3. **Generate Keys:** Create a new set of keys, following any provided guidelines.
4. **Record Keys:** Securely note down your **Access Key ID** and **Secret Access Key**.

### 4. Obtaining the bucket name

1. **Login:** Sign into Cubbit and navigate to the dashboard.
2. **Identify Bucket:** Find your bucket in the list and note its name.

### 5. Adding Cubbit storage in MDSS

Once you have the details above, go to your MDSS web page, **Inventory** tab, click **Add New** > **Account**, choose **Cubbit** and fill the form.

### 6. Limitations

> **Bucket Versioning not supported**
>
> Due to a known issue with the Cubbit, any action that MDSS does to delete a version of the file will not work as expected. This will not affect in any way a user that doesn't use bucket versioning

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
