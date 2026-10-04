<!-- source: https://www.opswat.com/docs/mddrive/configuration/preferences---scan-settings -->

# Preferences → Scan Settings

MetaDefender Drive enables users to adjust general scan settings, including the file sizes and scan timeouts. To adjust these settings, navigate to **Settings** → **Preferences** → **Scan Settings** page, and click **Edit Settings.**

The available settings in the **Scan Settings** window are:

- **Max File Size to scan** [in megabytes]:

  - The default maximum size of a single file per scan is set to 200MB
  - The maximum file size per scan depends on the available space of the MetaDefender Drive.
- **Max Minutes to Scan a File** [in minutes]
- **Max Minutes per Engine to Scan a File** [in minutes]
- **Enable Differential Scan**

  - **Disabled** [unchecked]:

    - Different Scan is not activated
    - No hash database recorded after each scan.
    - If Differential Scan was enabled before, after disabling, all of scan history (and the stored hashes will be wiped
    - The File Integrity Check works as usual when baseline for a scan is set
  - **Enabled** [checked]:

    - Differential Scan is activated
    - Hashes database will be recorded and accumulated after each scan so that in the next scans any existing hash that are valid within the set "Baseline Hash Valid Period" will be skipped, result in a faster scan

Baseline Hash Valid Period (in days)

- This value only allow 3 days on the MetaDefender Drive 64 GB and 365 days for MetaDefender Drive 2 (1TB)
- Baseline hashes are not backed up when upgrading or re-flashing

For more details about how to use **Differential Scan**, please refer to [Speeding Up Scans with Differential Scan](/docs/mddrive/knowledge-base/speeding-up-scans-with-differential-scan)

- **Enable Operator Skip Files**

  - **Disabled** [unchecked]: Operator **WILL NOT** be able to skip files during scan
  - **Enabled** [checked]: Operator **WILL** be able to skip files during scan

For more details about how to make use of option **Skip Files**, please refer to [Configure MetaDefender Drive and Perform Pre-Boot Scans](/docs/mddrive/process/processing-your-device-with-metadefender-drive)
