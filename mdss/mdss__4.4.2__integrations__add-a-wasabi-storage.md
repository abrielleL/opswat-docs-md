<!-- source: https://www.opswat.com/docs/mdss/4.4.2/integrations/add-a-wasabi-storage -->

# Add A Wasabi Storage

### [1. Prerequisites](/docs/mdss/4.4.2/integrations/add-a-wasabi-storage#1-prerequisites)

In order to Add a **Wasabi** storage in MDSS, you will need the **Wasabi Service URL**, **Access Key Id / Secret Access Key** and the **bucket name**. If you want to enable **path style addressing** for the bucket, tick the checkbox.

### [2. Obtaining the Service URL](/docs/mdss/4.4.2/integrations/add-a-wasabi-storage#2-obtaining-the-service-url)

1. **Login:** Sign into your Wasabi account at <https://console.wasabisys.com/>
2. **Find Bucket Region:** In the bucket management section, note your bucket's region.
3. **Construct URL:** Format your service URL as `https://s3.<bucket-region>.wasabisys.com`, replacing `<bucket-region>` with your bucket's actual region.
4. [Wasabi service URL docs](https://docs.wasabi.com/docs/service-urls-for-wasabis-storage-regions?highlight=service%20url)

### [3. Obtaining Access Keys](/docs/mdss/4.4.2/integrations/add-a-wasabi-storage#3-obtaining-access-keys)

1. **Access Console:** Go to the Wasabi console dashboard.
2. **Find Access Keys:** Look for "Access Keys" in the main menu ([https://console.wasabisys.com/access_keys/](https://console.wasabisys.com/access_keys))
3. **Generate Keys:** Create a new set of keys, following any provided guidelines.
4. **Record Keys:** Securely note down your Access Key ID and Secret Access Key.

### [4. Obtaining the bucket name](/docs/mdss/4.4.2/integrations/add-a-wasabi-storage#4-obtaining-the-bucket-name)

1. **Login:** Sign into Wasabi and navigate to the dashboard.
2. **Go to Buckets:** Locate the "Buckets" section (<https://console.wasabisys.com/file_manager/>)
3. **Identify Bucket:** Find your bucket in the list and note its name.

### [5. Adding Wasabi storage in MDSS](/docs/mdss/4.4.2/integrations/add-a-wasabi-storage#5-adding-wasabi-storage-in-mdss)

Once you have the details above, go to your MDSS web page, **Storage Units** page, click **Add storage unit**, choose **Wasabi** and fill the form.

Info

Supports both virtual-host and path-based style addressing

### [6. Limitations](/docs/mdss/4.4.2/integrations/add-a-wasabi-storage#6-limitations)

Real-Time Scans and File Renaming in Wasabi Storage

Due to a known issue with the Wasabi web interface, renaming a file does not change its "Last Modified" field. Consequently, MDSS cannot initiate real-time scans when files are renamed within Wasabi storage. This limitation stems from MDSS's reliance on detecting changes to the "Last Modified" field to trigger scans, which does not occur in this specific scenario with Wasabi storage.
