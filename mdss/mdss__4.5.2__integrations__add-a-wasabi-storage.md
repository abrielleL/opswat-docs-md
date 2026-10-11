<!-- source: https://www.opswat.com/docs/mdss/4.5.2/integrations/add-a-wasabi-storage -->

# Add A Wasabi Storage

### 1. Prerequisites

In order to Add a **Wasabi** storage in MDSS, you will need the **Wasabi Service URL**, **Access Key Id / Secret Access Key** and the **bucket name**. If you want to enable **path style addressing** for the bucket, tick the checkbox.

### 2. Obtaining the Service URL

1. **Login:** Sign into your Wasabi account at [https://console.wasabisys.com/](https://console.wasabisys.com/)
2. **Find Bucket Region:** In the bucket management section, note your bucket's region.
3. **Construct URL:** Format your service URL as `https://s3.<bucket-region>.wasabisys.com`, replacing `<bucket-region>` with your bucket's actual region.
4. [Wasabi service URL docs](https://docs.wasabi.com/docs/service-urls-for-wasabis-storage-regions?highlight=service%20url)

![](https://uploads.developerhub.io/prod/k8zL/bs3ysrkh9hpga0xvur2kbpx0qi6l03pmjc8n6p2vjsru8abg7i6odek61l0g77hm.png)

### 3. Obtaining Access Keys

1. **Access Console:** Go to the Wasabi console dashboard.
2. **Find Access Keys:** Look for "Access Keys" in the main menu ([https://console.wasabisys.com/access_keys/](https://console.wasabisys.com/access_keys))
3. **Generate Keys:** Create a new set of keys, following any provided guidelines.
4. **Record Keys:** Securely note down your Access Key ID and Secret Access Key.

### 4. Obtaining the bucket name

1. **Login:** Sign into Wasabi and navigate to the dashboard.
2. **Go to Buckets:** Locate the "Buckets" section ([https://console.wasabisys.com/file_manager/](https://console.wasabisys.com/file_manager/))
3. **Identify Bucket:** Find your bucket in the list and note its name.

### 5. Adding Wasabi storage in MDSS

Once you have the details above, go to your MDSS web page, **Inventory** tab, click **Add account **choose **Wasabi** and fill the form.

![](https://uploads.developerhub.io/prod/k8zL/3gxtz3vdkky4xc6m8hm0dcv9n3jji1gnibr9cevum1o0opazrgpbews9uqbo89bs.png)

Once the account is successfully added, please add the storage unit. Navigate to Inventory -> Add Unit -> Choose previously created Wasabi account:

1. Give your storage unit an unique name
2. Choose the group
3. Enter a valid bucket name
4. Enter folder location (optional)

![](https://uploads.developerhub.io/prod/k8zL/7r1rl4x5mpt29av3sto0c7mh51dsh97dw9lrc38hyjuuw1hii6nx7wrixv2r96p7.png)

> **Info**
>
> Supports both virtual-host and path-based style addressing

### 6. Limitations

> **Real-Time Scans and File Renaming in Wasabi Storage**
>
> Due to a known issue with the Wasabi web interface, renaming a file does not change its "Last Modified" field. Consequently, MDSS cannot initiate real-time scans when files are renamed within Wasabi storage. This limitation stems from MDSS's reliance on detecting changes to the "Last Modified" field to trigger scans, which does not occur in this specific scenario with Wasabi storage.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
