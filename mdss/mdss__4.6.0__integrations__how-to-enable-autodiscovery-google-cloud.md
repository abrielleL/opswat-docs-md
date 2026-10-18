<!-- source: https://www.opswat.com/docs/mdss/4.6.0/integrations/how-to-enable-autodiscovery-google-cloud -->

# How to Enable Autodiscovery

This guide provides step-by-step instructions for enabling Autodiscovery for Google Cloud storage in MetaDefender Storage Security.

Autodiscovery automatically detects and adds GCP buckets as storage units, saving time and reducing configuration errors.

## Prerequisites

Before enabling Autodiscovery, ensure you have:

1. Valid GCP credentials file with sufficient permissions
2. Permissions as stated in [Add a Google Cloud Storage](https://www.opswat.com/docs/mdss/integrations/add-a-google-cloud-storage)

#### Method 1: Enable Autodiscovery When Adding an Account

- Navigate to **Inventory** › **Accounts** and click **Add account**
- Select the **Google Cloud** provider
- Fill out the form with valid GCP credentials
- Turn on the **Autodiscovery** switch and select the **Destination Group** where the discovered buckets will be added

![](https://uploads.developerhub.io/prod/k8zL/bhq33lnwh6bbmszkr8dkplxr3146r7jj8xyggveeghpctp40o3cw10j4e8fstnpn.png)

- Continue to the **Summary** step. Autodiscovery starts in the background and the discovered buckets are added as storage units to the destination group. Click **View in inventory** to open the account, or **Finish**

![](https://uploads.developerhub.io/prod/k8zL/y8664e2ksxxuhe1m82f0o24m8euaf43eaqpm7v4sxk0919533g1plr2e35v6wl7i.png)

To learn more, please consult the [Autodiscovery](https://www.opswat.com/docs/mdss/operations/autodiscovery) documentation.

> **ADDING SPECIFIC BUCKETS ONLY**
>
> To add only specific buckets, leave **Autodiscovery** disabled, click **Add unit** on the **Summary** step, and choose **Single unit** or **Multiple units**.

#### Method 2: Enable Autodiscovery for an Existing Account

- Navigate to **Inventory** › **Accounts** and open the account you want to start autodiscovery for
- Open the **Settings** tab
- Turn on the **Autodiscovery** switch and select the **Destination Group**
- Upload the GCP credentials file in the **Credentials** field
- Click **Update**

![](https://uploads.developerhub.io/prod/k8zL/cxr7gtp0ufxnert1tg5hpw1ka207e4ni5tru940ruuj4iaslwcir4nuqb2dt6hqg.png)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
