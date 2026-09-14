<!-- source: https://www.opswat.com/docs/mddrive/maintenance/update-engines-in-airgap -->

# Update MetaDefender Drive Offline In AirGapped Environment

## [Update MetaDefender Drive Offline](/docs/mddrive/maintenance/update-engines-in-airgap#update-metadefender-drive-offline)

In isolated (air-gapped) environments, MetaDefender Drive, MetaDefender Drive Toolkit, and Smart Touch cannot connect to the OPSWAT update servers. This section explains how to keep the scanning engines and product versions up to date without an internet connection.

Offline engine updates rely on **MetaDefender Update Downloader**, OPSWAT's tool for downloading engine definitions in isolated environments. This applies to MetaDefender Drive, MetaDefender Drive Toolkit, and Smart Touch — in **Ready To Scan** mode, Smart Touch works as a MetaDefender Drive, so its engines are updated the same way. Only the Smart Touch application itself is updated with a separate offline update package downloaded from My OPSWAT.

## [How the Offline Update Works](/docs/mddrive/maintenance/update-engines-in-airgap#how-the-offline-update-works)

1. On a system with internet access, use MetaDefender Update Downloader to download the MetaDefender Drive engine packages.
2. Transfer the downloaded packages to the isolated environment using portable media.
3. Apply the updates using one of the methods below, depending on the product you are updating.

## [Step 1: Set Up MetaDefender Update Downloader](/docs/mddrive/maintenance/update-engines-in-airgap#step-1-set-up-metadefender-update-downloader)

The instructions in this section are written with the assumption that an Update Downloader instance is up and running in your organization's network. If you haven't installed MetaDefender Update Downloader yet, you can find it at: [MetaDefender Update Downloader](https://www.opswat.com/docs/mddownloader).

Info

Update Downloader provides the engine packages. If you only need to update the Smart Touch application itself, skip this step — that update package is downloaded from My OPSWAT instead.

Info

MetaDefender Drive with Smart Touch will work like a regular MetaDefender Drive when you swich it to "**Device Scanning**" mode.

## [Step 2: Choose Your Update Method](/docs/mddrive/maintenance/update-engines-in-airgap#step-2-choose-your-update-method)

| If you are updating... | Then follow... |
| --- | --- |
| Engines or the MetaDefender Drive image, and you have access to MetaDefender Drive Toolkit | [Update Engines and Drive Image Offline Using Drive Toolkit](https://www.opswat.com/docs/mddrive/maintenance/offline-update-for-metadefender-drive-toolkit) |
| Engines directly on a MetaDefender Drive device or a Smart Touch device in Ready To Scan mode, without Drive Toolkit | [Update Engines Offline Directly on MetaDefender Drive](https://www.opswat.com/docs/mddrive/maintenance/offline-update-for-metadefender-drive) |
| Update Smart Touch Offline | [Update MetaDefender Drive with Smart Touch Offline](/docs/mddrive/maintenance/offline-update-smart-touch) |

## [Alternative: Update Engines and Drive Image Without Update Downloader](/docs/mddrive/maintenance/update-engines-in-airgap#alternative-update-engines-and-drive-image-without-update-downloader)

If your environment allows MetaDefender Drive to reach a My OPSWAT Central Management on premise server or a MetaDefender Kiosk that is als connecting to a My OPSWAT Central Management server, you can update the engines and the Drive image without using Update Downloader:

- **From My OPSWAT Central Management**: a MetaDefender Drive enrolled to a Central Management server (7.8 or later) can fetch both engine definition updates and Drive software upgrade packages from that server. Enable the **Update definitions from this OCM** and **Update version from this OCM** options when enrolling. See [Manage MetaDefender Drives with OPSWAT Management](https://www.opswat.com/docs/mddrive/configuration/managing-drives-with-central-management) and [Enroll MetaDefender Drive to Central Management Server from MetaDefender Drive User Interface](https://www.opswat.com/docs/mddrive/configuration/enroll-cm-from-drive).
- **From MetaDefender Kiosk**: from MetaDefender Drive v4.4.5 and MetaDefender Drive Toolkit v3.8.5, inserting a MetaDefender Drive into a Kiosk with the Drive integration enabled can update the engines and upgrade the Drive version in the same insertion, alongside syncing scan reports. This requires the integration to be configured on the Kiosk side. See [Use MetaDefender Drive with MetaDefender Kiosk](https://www.opswat.com/docs/mddrive/configuration/use-metadefender-drive-with-kiosk).

Info

If a MetaDefender Drive is configured to download updates from My OPSWAT Central Management that is not accessible on boot, it is recommended to use MetaDefender Drive Toolkit to update the scanning engines.
