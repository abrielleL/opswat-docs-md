<!-- source: https://www.opswat.com/docs/mdss/4.5.2/integrations/how-to-enable-autodiscovery -->

# How to Enable Autodiscovery

This guide provides step-by-step instructions for enabling Autodiscovery for Azure Blob storage in MetaDefender Storage Security.

Autodiscovery automatically detects and adds Azure Blob containers as storage units, saving time and reducing configuration errors.

## [Prerequisites](https://www.opswat.com/docs/mdss/integrations/how-to-enable-autodiscoveryyn1#prerequisites)

Before enabling Autodiscovery, ensure you have:

1. Valid Azure Blob credentials with sufficient permissions
2. Permissions as stated in [Add an Azure Blob storage](https://www.opswat.com/docs/mdss/integrations/add-an-azure-blob-storage)

#### Method 1: Enable Autodiscovery During Storage Unit Addition

- Navigate to **Storage Units** page
- Click **Add Storage Unit** button
- Select **Azure Blob** Storage Type
- Select **Storage Discovery** and click **Continue**

![](https://uploads.developerhub.io/prod/k8zL/ky63mjl04s0ava0qkih1l2jkxirs7dyymgi869ru4vm9e82yitmkkkjvd4el28c1.png)

- Fill out the form with valid Azure Blob credentials and click **Continue**

![](https://uploads.developerhub.io/prod/k8zL/2mi9kexvtkea22q2rpoe5e6nhgxymocyqhpe0ybd9nmlxxevvsfuss4wq7lt2uzu.png)

- In the next step, select your integration method. You have two choices: Autodiscovery and Manual Selection.
  - **Autodiscovery** for convenience, this option automatically adds all the containers that MDSS finds
  - **Manual Selection** for precise control, this option lets users choose specific containers from the discovered list to integrate.

![](https://uploads.developerhub.io/prod/k8zL/kcr7vgobbkn82b8f7m1x3zfr9shq0k5o18ls8sy2031yvqfeku6c0le5hlr7k7r1.png)

To learn more about each integration type, please consult the [Autodiscovery](https://www.opswat.com/docs/mdss/operations/autodiscovery) documentation.

> **NO CONTAINERS FOUND**
>
> If there were no containers found, you will be presented with a third option - **Add Individually** - which will reveal the credentials form to manually add the storage by using the site name.

- If selecting the **Autodiscovery** option:
  - Click **Continue,** and an informative message will be displayed that the autodiscovery process has started in the background. You can safely close the modal, and the storage units will be added in the background to the Storage Units page

![](https://uploads.developerhub.io/prod/k8zL/ucwi8h28o2b6eaftcraz9hffdu5an26ug603vrk0rffyhnqqbt8v256aequc4z6i.png)

![](https://uploads.developerhub.io/prod/k8zL/npv8ndiihym5zhvy9v7uh1q8w7zilw0se5qsuikzvca6uv8mzn9tgzpvjca8s03d.png)

- If selecting **Manual Selection** option:
  - Click **Continue**
  - Select the containers you want to add from the discovered list
  - Click **Continue**

![](https://uploads.developerhub.io/prod/k8zL/wxd02yhpkpe874b7v9nd3yf41szc1bkzq2e9q7umcqr0wjqhz9ksdvumcawxxets.png)

![](https://uploads.developerhub.io/prod/k8zL/yd1h0ly1ft5ezb2gatcaetrtzga8nhif7knlxjwyaujnfv2af0pwgiqxctmpmwdg.png)

![](https://uploads.developerhub.io/prod/k8zL/jg6cfy0jsen7pdsh96tm6x4y8ond39y4m7h2evsb1yd3a3opqeme0i7n7a7aj9jl.png)

> **ERROR ADDING A STORAGE THAT WAS SELECTED DURING MANUAL SELECTION**
>
> In case there was an error while trying to add your storage, you will see the error message in the Storage card while hovering over the (i) icon.

#### Method 2: Enable Autodiscovery for an Existing Account

- Navigate to the **Storage Units** page
- Identify a storage that's using the account you want to start autodiscovery for
- Click on the 3-dots button from the storage card and select **Manage Storage Unit**
- From the top toggle, select **Change account info**
- Turn on autodiscovery by toggling the **Enable storage auto** **discovery** switch

![](https://uploads.developerhub.io/prod/k8zL/rkdgrefu2eav64x1znkobo0a13k8b39comx7kautjeyrjuonktdps41zcjrra6mx.png)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
