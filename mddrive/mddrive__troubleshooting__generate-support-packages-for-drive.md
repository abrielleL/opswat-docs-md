<!-- source: https://www.opswat.com/docs/mddrive/troubleshooting/generate-support-packages-for-drive -->

# Generate Support Packages for MetaDefender Drive

The following are 3 different approaches to generate support packages from a malfunctioning MetaDefender Drive, starting by the easiest to the hardest:

### [1. Generate a Support Package using MetaDefender Drive Toolkit](/docs/mddrive/troubleshooting/generate-support-packages-for-drive#1-generate-a-support-package-using-metadefender-drive-toolkit)

If you haven't installed MetaDefender Drive Toolkit yet, you can download it from [this link](https://installer-cdn.opswat.com/MD_Drive_Toolkit/3.0/update_infra/main/MetaDefenderDriveToolkit.zip)*.*

1. Launch MetaDefender Drive Toolkit by right-clicking the *MetaDefenderDriveToolkit.exe* file and selecting **Run as Administrator**.
2. Navigate to **Advanced Options** → **Support**.
3. Select the drive you want to gathers its logs into a support package, identified by its serial number, and click **Generate Support Package**.
4. Track the progress until it shows the **Completed** status. The needed time will depend on how much reports and logs being located on the Drive's storages.
5. Simply click **Show in folder** button will open the relevant folder for you to find the generated Support Package.

You can also generate support packages for multiple MetaDefender Drives using this method.

### [2. Generate a Support Package during when MetaDefender Drive Malfunctions](/docs/mddrive/troubleshooting/generate-support-packages-for-drive#2-generate-a-support-package-during-when-metadefender-drive-malfunctions)

If you face an issue while MetaDefender Drive is running, follow these steps:

1. Press and hold the keyboard keys `⌥`+ `⇧`+ `F3` for 5 seconds**.**
2. Wait for the support package generation to complete and reset your system.

Generate a Support Package from a malfunctioning MetaDefender Drive

### [3. Generate a Support Package while MetaDefender Drive is running](/docs/mddrive/troubleshooting/generate-support-packages-for-drive#3-generate-a-support-package-while-metadefender-drive-is-running)

1. Click the arrow icon at the bottom right corner, and click the Generate button from the Quick Actions menu.

Generate a Support Package while MetaDefender Drive is running

2. Click **Generate** when prompted to confirm generating a support package.

Confirmation prompt of generating a Support Package while MetaDefender Drive is running

3. Wait until the support package is generated completely at the main storage of Drive

4. When plugging Drive into a Windows, browse to Drive's storage, the generated ***SupportPackage*** file will be seen there (with no file extension), along with another ***SupportPackage.sha256***.

**Note**:

- The **Support Package** is a compressed diagnostic archive generated from MetaDefender Drive that consolidates the information OPSWAT Technical Support requires to investigate device issues — including system logs, configuration files, process core dumps, and partition directory listings. The package is intended exclusively for transmission to OPSWAT and must not be modified or extracted independently. It does not contain the contents of any scanned media (USB drives or other external devices scanned by MetaDefender Drive) — only diagnostic data about the Drive appliance itself.
- The accompanying **SupportPackage.sha256** file contains the SHA-256 cryptographic hash of the archive, used to verify that the package has not been corrupted or tampered with during transfer.

### [4. Export Logs for MetaDefender Drive In-Session](/docs/mddrive/troubleshooting/generate-support-packages-for-drive#4-export-logs-for-metadefender-drive-in-session)

1. From within MetaDefender Drive In-Session main window, select the menu **(...)** and click **Export Logs**
2. Follow the instruction on the message:

   1. Navigate to the mounted partition (from where you run the MetaDefender Drive In-Session).
   2. Go to tools/CTR/exported_logs and find the latest zip file.
