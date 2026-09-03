<!-- source: https://www.opswat.com/docs/mddrive/advanced-usages/low-spec-hardware -->

# Running from hardware below the recommendation

MetaDefender Drive runs on devices with hardware below the [recommended specification](https://docs.opswat.com/mddrive/getting-started/system-requirements-and-compatibility), extending its compatibility to scan and secure legacy and outdated devices.

When you boot MetaDefender Drive from a machine whose processor count, memory or USB port speed falls below the recommended specification:

You will be notified that engine upgrades aren't available on hardware below the recommendation. The recommended set of engines and technologies is decided in tiers by the detected hardware: the fewer processors, the less memory and the slower the USB port, the smaller the set. On the lowest tier the recommendation narrows to two anti-malware engines with FileType, and Vulnerability Analysis, Data Leak Prevention and Country of Origin Audit are turned off. You will also be asked to confirm that you want to use MetaDefender Drive with the recommended engines, then click ***Continue***, or ***Proceed to Standard Mode*** to accept the slow performance.

**Warning**

> Booting MetaDefender Drive for the first time must be done from a device with specifications above the minimum requirements. to ensure that engines are successfullyeployed and ready to use.
>
> Booting from a low spec device for the first time can lead to issues, including:
>
> - Drive failing to load the scanning engines
> - Engines jumping into the *"Fail_Permanently"* status
> - Drive unable to perform any scan

On the engines page, you will notice that only the recommended engines for your hardware are initiated. You can then move to the dashboard and start a scan.

Before the scan, engines and utilities (Vulnerability Analysis, Data Leak Prevention, and Country of Origin Audit) outside the recommended set will not be available. Click **Start Custom Scanning** to start a scan:

You will see a warning reminding you that some engines haven't been updated or initiated. Since you are running on hardware below the recommendation and can't update engines, you can ignore this warning and click **Yes** to proceed with scanning:

Track the scan progress and process the results:
