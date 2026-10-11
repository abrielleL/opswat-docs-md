<!-- source: https://www.opswat.com/docs/mdss/4.5.2/integrations/how-to-enable-autodiscoveryyn1740 -->

# How to Enable Autodiscovery

## This guide provides step-by-step instructions for enabling Autodiscovery for SharePoint Online in MetaDefender Storage Security.

Autodiscovery automatically detects and adds SharePoint Online sites as storage units, saving time and reducing configuration errors.

## Prerequisites

Before enabling Autodiscovery, ensure you have:

1. Valid SharePoint Online credentials with sufficient permissions
2. Permissions as stated in [Add a SharePoint Online Storage](https://www.opswat.com/docs/mdss/integrations/add-a-sharepoint-storage)

#### Method 1: Enable Autodiscovery During Storage Unit Addition

- Navigate to **Storage Units** page
- Click **Add Storage Unit** button
- Select **SharePoint Online** Storage Type
- Select **Storage Discovery** and click **Continue**

![](https://uploads.developerhub.io/prod/k8zL/zzgwqu9g1hmhsmm34hf8dq78v64zv31aem2g82povwzm7t2yl19x2c5yhdoadu8q.png)

- Fill out the form with valid SharePoint Online credentials and click **Continue**

![](https://uploads.developerhub.io/prod/k8zL/g0miq75ux2j8t4pvqtzbvfszke2chnah9k6mo6cjzvv8lh80qbtng2phsn9122i2.png)

- In the next step, select your integration method. You have two choices: Autodiscovery and Manual Selection.
  - **Autodiscovery** for convenience, this option automatically adds all the sites MDSS finds
  - **Manual Selection** for precise control, this option lets users choose specific sites from the discovered list to integrate.

![](https://uploads.developerhub.io/prod/k8zL/7sbnxusgcrf2b38ulnvaxdc7s90ld0t973lo14n9ja43xecqxudb3wbji8bwu2ow.png)

To learn more about each integration type, please consult the [Autodiscovery](https://www.opswat.com/docs/mdss/operations/autodiscovery) documentation.

> **NO SITES FOUND**
>
> If there were no sites found, you will be presented with a third option - **Add Individually** - which will reveal the credentials form to manually add the storage by using the site name.

- If selecting **Autodiscovery** option:
  - Click **Continue** and an informative message will be displayed that the autodiscovery process has started in the background. You can safely close the modal and the storages will be added in background to the Storage Units page

![](https://uploads.developerhub.io/prod/k8zL/zqwovowgh5g0qnxctfegcptubcm4s6ne9cffu27ns4710nvoqtyk2wv6qcm3fheo.png)

![](https://uploads.developerhub.io/prod/k8zL/2nledlkp8twpth08xqpbmkyzm07ohdhn8r1jm3qblucakohnavxmbr5mqb3bm3sd.png)

- If selecting **Manual Selection** option:
  - Click **Continue**
  - Select the sites you want to add from the discovered list
  - Click **Continue**

![](https://uploads.developerhub.io/prod/k8zL/mip4kzf98vz8cag1puo1nbdr4b5m90dpzivrcsm7nrgpmja7pgjor32wqlzk14wn.png)

![](https://uploads.developerhub.io/prod/k8zL/1rk78wfuolqqu45ru83cmols4lswtklp8r99yqlmlll965tqaislo7fyrt7to4vj.png)

![](https://uploads.developerhub.io/prod/k8zL/mlruc3d3bl0n5ejbgjfreo9n2pixq4o966sgweovg8d66v6zxnq3tfr3zmmu4rje.png)

> **ERROR ADDING A STORAGE THAT WAS SELECTED DURING MANUAL SELECTION**
>
> In case there was an error while trying to add your storage, you will see the error message in the Storage card while hovering over the (i) icon.

#### Method 2: Enable Autodiscovery for an Existing Account

- Navigate to **Storage Units** page
- Identify a storage that's using the account you want to start autodiscovery for
- Click on the 3-dots button from the storage's card and select **Manage Storage Unit**
- From the top toggle, select **Change account info**
- Turn on autodiscovery by toggling the **Enable storage auto** **discovery** switch![](https://uploads.developerhub.io/prod/k8zL/01bp40dfo0ium5or24ac8fvgqg43god6p87eyvgci1xjv5cgagikx6e8nzwqalh1.png)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
