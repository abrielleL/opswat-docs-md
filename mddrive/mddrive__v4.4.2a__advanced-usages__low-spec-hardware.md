<!-- source: https://www.opswat.com/docs/mddrive/v4.4.2a/advanced-usages/low-spec-hardware -->

# Running from hardware below the recommendation

MetaDefender Drive runs on devices with hardware below the [recommended specification](https://docs.opswat.com/mddrive/getting-started/system-requirements-and-compatibility), extending its compatibility to scan and secure legacy and outdated devices.

When you boot MetaDefender Drive from a machine with 4GB of RAM or less:

You will be notified that engine upgrades aren't available while using low specs devices. You will also be asked to confirm that you want to use MetaDefender Drive with Avira as the only anti-malware engine enabled, then click ***Continue***, or ***Proceed to Standard Mode*** to accept the slow performance

Warning

Booting MetaDefender Drive for the first time must be done from a device with specifications above the minimum requirements. to ensure that engines are successfully deployed and ready to use.

Booting from a low spec device for the first time can lead to issues, including:

- Drive failing to load the scanning engines
- Engines jumping into the *"Fail_Permanently"* status
- Drive unable to perform any scan

On the engines page, you will notice that only the previously selected engine is initiated. You can then move to the dashboard and start a scan.

Before the scan, engines and utilities (Vulnerability Analysis, Data Leak Prevention, and Country of Origin Audit) other than the selected engine will not be available. Click **Start Custom Scanning** to start a scan:

You will see a warning reminding you that some engines haven't been updated or initiated. Since you are operating in Lite Mode and can't update engines, you can ignore this warning and click **Yes** to proceed with scanning:

Track the scan progress and process the results:

Settings Modification is Disabled in Lite Mode

When running in Lite Mode, MetaDefender Drive uses preset settings and preferences that can't be changed.

The configured integrations, such as OPSWAT Central Management and MetaDefender Managed File Transfer, are preserved but not changeable. So, in Lite Mode, your MetaDefender Drive is still managed, and you can still transfer your clean files to Managed File Transfer and external USB drives.

MetaDefender Drive activation is not eligible in Lite Mode. Users must activate MetaDefender Drive when booting it from a machine with hardware that meets or is above the recommended specifications.
