<!-- source: https://www.opswat.com/docs/mdss/4.5.2/integrations/how-to-enable-autodiscoveryyn1 -->

# How to Enable Autodiscovery

## This guide provides step-by-step instructions for enabling Autodiscovery for Google Cloud storage in MetaDefender Storage Security.

Autodiscovery automatically detects and adds GCP buckets as storage units, saving time and reducing configuration errors.

## Prerequisites

Before enabling Autodiscovery, ensure you have:

1. Valid GCP credentials file with sufficient permissions
2. Permissions as stated in [Add a Google Cloud Storage](https://www.opswat.com/docs/mdss/integrations/add-a-google-cloud-storage)

#### Method 1: Enable Autodiscovery During Storage Unit Addition

- Navigate to **Storage Units** page
- Click **Add Storage Unit** button
- Select **Google Cloud** Storage Type
- Select **Storage Discovery** and click **Continue**

![](https://uploads.developerhub.io/prod/k8zL/zzgwqu9g1hmhsmm34hf8dq78v64zv31aem2g82povwzm7t2yl19x2c5yhdoadu8q.png)

- Fill out the form with valid GCP credentials and click **Continue**

![](https://uploads.developerhub.io/prod/k8zL/d38rb9ss1xg3qi5uiv51i9dsw90f213d843bv2v8qw30dahsv019ol52kwj6mw9n.png)

- In the next step, select your integration method. You have two choices: Autodiscovery and Manual Selection.
  - **Autodiscovery** for convenience, this option automatically adds all the buckets MDSS finds
  - **Manual Selection** for precise control, this option lets users choose specific buckets from the discovered list to integrate.

![](https://uploads.developerhub.io/prod/k8zL/grv5u7a70atxl8iw17ev4hqako0nsz62jn73dc28sx26whcbuk4miis0sn840roc.png)

To learn more about each integration type, please consult the [Autodiscovery](https://www.opswat.com/docs/mdss/operations/autodiscovery) documentation.

> **NO BUCKETS FOUND**
>
> If there were no buckets found, you will be presented with a third option - **Add Individually** - which will reveal the credentials form to manually add the storage by using the bucket name.

- If selecting **Autodiscovery** option:
  - Click **Continue** and an informative message will be displayed that the autodiscovery process has started in the background. You can safely close the modal and the storages will be added in background to the Storage Units page

![](https://uploads.developerhub.io/prod/k8zL/3cgykb3vyl34xc6ryy0tub7mdr5ly97muaf975n7q2olft8lxojdtdcqh9vqlarg.png)

![](https://uploads.developerhub.io/prod/k8zL/2nledlkp8twpth08xqpbmkyzm07ohdhn8r1jm3qblucakohnavxmbr5mqb3bm3sd.png)

- If selecting **Manual Selection** option:
  - Click **Continue**
  - Select the buckets you want to add from the discovered list
  - Click **Continue**

![](https://uploads.developerhub.io/prod/k8zL/7n5i8j4mypkfxntzuva0e715mo9sl6pranhy5819zv9ajzjwwhv3nrek7c92mpzy.png)

![](https://uploads.developerhub.io/prod/k8zL/jemufigim9phyeloyk3kkex6j23ebghr7464zfcihtul3ib14w2l8cp58u0sa688.png)

![](https://uploads.developerhub.io/prod/k8zL/quple6e1dmzdp18nowei70j3nslmf7lksmv3cz3pf8u4orm5jud2mu9zk81e2h18.png)

> **ERROR ADDING A STORAGE THAT WAS SELECTED DURING MANUAL SELECTION**
>
> In case there was an error while trying to add your storage, you will see the error message in the Storage card while hovering over the (i) icon.

#### Method 2: Enable Autodiscovery for an Existing Account

- Navigate to **Storage Units** page
- Identify a storage that's using the account you want to start autodiscovery for
- Click on the 3-dots button from the storage's card and select **Manage Storage Unit**
- From the top toggle, select **Change account info**
- Turn on autodiscovery by toggling the **Enable storage autodiscovery** switch

![](https://uploads.developerhub.io/prod/k8zL/34nek1rcextfoxt3a5q77d8vhjr5navowq2wtjj93ms8xngrg9xulwnvnutdf4hq.png)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
