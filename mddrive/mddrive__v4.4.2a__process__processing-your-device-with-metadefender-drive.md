<!-- source: https://www.opswat.com/docs/mddrive/v4.4.2a/process/processing-your-device-with-metadefender-drive -->

# Configure MetaDefender Drive and Perform Pre-Boot Scans

## [Scan Types and Configurations](/docs/mddrive/v4.4.2a/process/processing-your-device-with-metadefender-drive#scan-types-and-configurations)

MetaDefender Drive offers three scan options, with flexible configurations and scanning engine selection, to optimize the performance and the results depending on each dataset.

Dashboard page showing the 3 available scan options

- **Quick Scan:** scans the most critical paths with a single malware engine of your choice. The file paths covered by Quick Scan can be [configured](https://www.opswat.com/docs/mddrive/configuration/preferences---quickscan-settings) from **Settings** > **Quick Scan**.

Info

File path configuration is only available on Windows. Support for other operating systems will be added in subsequent releases.

- **Full Scan:** scans all the mounted and unlocked disk partitions using all the enabled engines.

Engines and Technologies

The total number of engines and technologies included for a full device scan depends on the engines and technologies enabled under **Settings** → **Preferences**.

- **Custom Scan:** runs based on user-defined selection of technologies, anti-malware engines, options, and filesystem paths.

Engines Availability

Engines that aren't ready to be used (due to ongoing update or initialization) will appear grayed out and can't be included in a custom scan.

## [Perform the Scan](/docs/mddrive/v4.4.2a/process/processing-your-device-with-metadefender-drive#perform-the-scan)

During a MetaDefender Drive scan, each file is run through the embedded MetaDefender system to be scanned and analyzed with multiple antivirus, vulnerability, and utility engines. Users can track the scan progress, with an estimated completion percentage on the progress bar. The displayed **Time Remaining** value is estimated based on previous rates of processing and file sizes, and may be updated while the scan is running.

Once the scan is complete, the user can click the **View Report** button to see the scan report.

Scan Duration

There is no fixed time for each scan. It can take a few minutes to up to several hours, depending on the hardware specs of the target device and the size of the data being scanned. Please take a look at the [performance metrics](https://docs.opswat.com/mddrive/process/performance-measurement) for reference.

If the target machine is equipped with 4GB of memory or less, it is recommended to select ***Lite Mode*** when prompted. If Lite Mode wasn't selected, it is advised to only run a **Custom Scan** with only one anti-malware engine enabled.

A scan in progress with 18 **Potentially Infected Files** detected

A scan in progress with 12 **Potentially Vulnerable Files** detected that might be a reason for a Zero Day Exploit

A scan in progress with 4 **Files with Sensitive Data** detected

A scan in progress with 19 **Country of Origin** suspected files detected
