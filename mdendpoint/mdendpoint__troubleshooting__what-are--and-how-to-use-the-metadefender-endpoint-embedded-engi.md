<!-- source: https://www.opswat.com/docs/mdendpoint/troubleshooting/what-are--and-how-to-use-the-metadefender-endpoint-embedded-engi -->

# What are, and how to use the MetaDefender Endpoint Embedded Engines?

> **Check Your Version:**
>
> This article applies to MetaDefender Endpoint releases subsequent to version 7.6.2411.603. deployed on Windows systems when connected to MyOPSWAT Central Management v10.

MetaDefender Endpoint Embedded Engines are local anti-malware engines that run directly on the Windows endpoint. They enable MetaDefender Endpoint to perform threat scanning locally, reducing reliance on remote scan sources such as MetaDefender Core or MetaDefender Cloud for supported local scanning workflows. For any privacy concerns, this ensures files do not leave the local device for scanning.

This capability is particularly valuable in environments where endpoints may be offline, remote, restricted, or air-gapped, but still require malware scanning.

In removable media scenarios, the embedded antivirus engines can be used to take over when connectivity is unavailable, allowing files to continue being scanned without interruption.

## What can you scan with the Embedded Engines?

On Windows, MetaDefender Endpoint’s malware scanning capabilities include the following scan types:

- **Memory Scan**: scans memory, including processes and libraries currently loaded in memory
- **Full System Scan**: scans memory and local drives
- **Custom Scan**: can scan local files/folders, boot sectors, attached drives, removable drives, and network drives
- **Removable media:** removable media files remain scannable even when internet connectivity is interrupted or unavailable
- **Download Protection:** can scan files that have been downloaded from the internet

## Licensing

Embedded Engines is not a free/base feature. Embedded engine threat detection is only available to customers who have a MetaDefender Endpoint Plus license. For that reason, Embedded Engines should be treated as a licensed Threat Detection capability.

## How to activate Embedded Engines in My OPSWAT Central Management v10

Embedded Engines in **My OPSWAT Central Management v10**, can be enabled for all features that require scanning files.

### Peripheral Media Protection

1. In the left hand menu, in the *Solution *section, expand **Peripheral Media Protection**
2. Open **Policies**
3. Select the target policy
4. Set **Peripheral Media Protection** to *Active*
5. Expand **Scan Workflow**
6. Click **Add Scan Server**
7. In **Select a scan source**, choose **Embedded Engines**
8. Click** Add**
9. Save the policy

### Malware Scan

1. In the left hand menu, in the *Solution *section, expand **Endpoint Security**
2. Open **Policies**
3. Select the target policy under the **Endpoint Security** tab
4. Select the** Malware Scan **tab
5. Set **Malware Scan** to *Active *and expand the feature
6. Expand **Scan Workflow**
7. Click **Add Scan Server**
8. In **Select a scan source**, choose **Embedded Engines**
9. Click** Add**
10. Save the policy

### Download Protection

1. In the left hand menu, in the *Solution *section, expand **Endpoint Security**
2. Open **Policies**
3. Select the target policy under the **Download Protection **tab
4. Set **Download Protection** to *Active*
5. Expand **Scan Workflow**
6. Click **Add Scan Server**
7. In **Select a scan source**, choose **Embedded Engines**
8. Click** Add**
9. Save the policy

## What are the embedded engines available to use?

When **Embedded Engines** is selected as the scan source in **OCM v10**, the following local engines are available for use, based on the configuration screen shown:

- **Bitdefender**
- **ClamAV**
- **ESET**
- **OPSWAT Predictive AI**

These engines are configured directly under the **Add Scan Server** window when **Embedded Engines** is chosen as the scan source. This allows administrators to define which local detection engines MetaDefender Endpoint will use for endpoint-side threat scanning.

## How to select which scanning method to use in MetaDefender Endpoint

**Peripheral Media Protection**

![](https://uploads.developerhub.io/prod/2x2P/gwvk1l90s3g3bcf3ns6txpxwcwbzpjrqkebxe5tw0ti1f6sb6jae5b16i58gtanj.png)

**Malware Scan**

![](https://uploads.developerhub.io/prod/2x2P/znu9ndryfauovrp2gscfxttp0lhfr2uh57g5feyqedlh1hrv4a0rfmdzev3ys7yd.png)

**Download Protection**

![](https://uploads.developerhub.io/prod/2x2P/iz7p4heugzb4bzodokidr1yr9vo9qvei40ar33o6ekdim5rvk5vcepsxr3bbvj0h.png)

> **Support:**
>
> If **Further Assistance** is required, please proceed to log a [**support case or chat with one of our support engineers**](https://my.opswat.com/support).

---

[All pages in this documentation](https://www.opswat.com/docs/mdendpoint/llms.txt)
