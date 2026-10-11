<!-- source: https://www.opswat.com/docs/mdss/integrations/how-to-enable-autodiscovery-sharepoint-online -->

# How to Enable Autodiscovery

This guide provides step-by-step instructions for enabling Autodiscovery for SharePoint Online in MetaDefender Storage Security.

Autodiscovery automatically detects and adds SharePoint Online sites as storage units, saving time and reducing configuration errors.

## Prerequisites

Before enabling Autodiscovery, ensure you have:

1. Valid SharePoint Online credentials with sufficient permissions
2. Permissions as stated in [Add a SharePoint Online Storage](https://www.opswat.com/docs/mdss/integrations/add-a-sharepoint-storage)

#### Method 1: Enable Autodiscovery When Adding an Account

- Navigate to **Inventory** › **Accounts** and click **Add account**
- Select the **SharePoint** provider
- Fill out the form with valid SharePoint Online credentials
- Turn on the **Autodiscovery** switch and select the **Destination Group** where the discovered sites will be added

![](https://uploads.developerhub.io/prod/k8zL/jh1lg442iyxzzlt685w4490g6e9lsz832a205gec33gcv2gqgl5h5cql67vkv0o9.png)

- Continue to the **Summary** step. Autodiscovery starts in the background and the discovered sites are added as storage units to the destination group. Click **View in inventory** to open the account, or **Finish**

![](https://uploads.developerhub.io/prod/k8zL/mfm8fq9fa8pcyo6xcuwe3j5zgukucg6h7vsx1ya9f1p9mfjrgeizum8iys6t2d1n.png)

To learn more, please consult the [Autodiscovery](https://www.opswat.com/docs/mdss/operations/autodiscovery) documentation.

> **ADDING SPECIFIC SITES ONLY**
>
> To add only specific sites, leave **Autodiscovery** disabled, click **Add unit** on the **Summary** step, and choose **Single unit** or **Multiple units**.

#### Method 2: Enable Autodiscovery for an Existing Account

- Navigate to **Inventory** › **Accounts** and open the account you want to start autodiscovery for
- Open the **Settings** tab
- Turn on the **Autodiscovery** switch and select the **Destination Group**
- Enter the **Client Secret**
- Click **Update**

![](https://uploads.developerhub.io/prod/k8zL/r74nmysoy3kswnn15mw2zmg2kptyujku2wr2bq9vblojgelur35663jgsue8bxxj.png)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
