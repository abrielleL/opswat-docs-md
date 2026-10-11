<!-- source: https://www.opswat.com/docs/mddrive/configuration/preferences---scan-settings -->

# Preferences → Scan Settings

View as Markdown Ask ChatGPT about this page Ask Claude about this page

MetaDefender Drive enables users to adjust general scan settings, including the **file size** and **scan timeout**. To adjust these settings, navigate to **Settings** → **Preferences** → **Scan Settings** page, and click **Edit Settings.**

The available settings in the **Scan Settings** window are:

- **Max File Size to scan** [in megabytes]:

  - The default maximum size of a single file per scan is set to 200MB.
  - The maximum file size per scan depends on the available space of the MetaDefender Drive.
- **Max Minutes to Scan a File** [in minutes]
- **Max Minutes per Engine to Scan a File** [in minutes]
- **Enable Differential Scan**

  - **Unchecked** [Disabled ]:

    - **Differential Scan** is not activated.
    - No hash database is recorded after each scan.
    - If **Differential Scan** was enabled before, after disabling, all of the scan history (and the stored hashes will be wiped.
    - The File Integrity Check works as usual when a baseline for a scan is set.
  - **Checked** [Enabled]:
  - - **Differential Scan** is activated.
    - Hashes database will be recorded and accumulated after each scan so that in the next scans any existing hash that are valid within the set "Baseline Hash Valid Period" will be skipped, resulting in a faster scan.

Baseline Hash Valid Period (in days)

- This value only allow 3 days on the MetaDefender Drive 64 GB and 365 days for MetaDefender Drive 2 (1TB)
- Baseline hashes are not backed up when upgrading or re-flashing

For more details about how to use **Differential Scan**, please refer to the [Speeding Up Scans with Differential Scan](/knowledge-base/speeding-up-scans-with-differential-scan) page.

- **Enable Operator Skip Files**

  - **Unchecked** [Disabled]: Operators WILL NOTbe able to skip files during scan
  - **Checked** [Enabled]: Operators WILL be able to skip files during scan

For more details on using the **Skip Files** option, please refer to the [Configure MetaDefender Drive and Perform Pre-Boot Scans](/process/processing-your-device-with-metadefender-drive) page.
