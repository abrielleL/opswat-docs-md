<!-- source: https://www.opswat.com/docs/mddrive/v4.4.2a/process/smart-touch-device-scanning -->

# MetaDefender Drive with Smart Touch Operations - Device Scanning

MetaDefender with Smart Touch offers similar experience to MetaDefender Drive's USB. The initial interface shows slight differences for extra convenience using the mobile form factor.

## [View and Manage Scan Reports](/docs/mddrive/v4.4.2a/process/smart-touch-device-scanning#view-and-manage-scan-reports)

After a scan is complete, the scan results will be displayed on the target system, and MetaDefender Drive with Smart Touch will display **Unsafe Device** or **Safe Device** message, depending on the scan result.

For more details, tab **View Scan Details**. The **Scan Details** page will show an overview of the scan results.

Notice that the result shown in MetaDefender Drive with Smart Touch show the same numbers of findings in MetaDefender Drive for the same scan.

## [Sync Reports for Central Management](/docs/mddrive/v4.4.2a/process/smart-touch-device-scanning#sync-reports-for-central-management)

If MetaDefender Drive is configured with [My OPSWAT Central Management](https://docs.opswat.com/ocm), reports will be automatically synced. Otherwise, a **Sync Error** notification will be displayed.

## Generate [S](https://www.opswat.com/docs/mddrive/process/results--management#sync-reports-for-central-management)upport Packages

To generate a support package for MetaDefender Drive with Smart Touch, ensure your drive is not connected to a target device or performing any operations.

1. Tab **Setting** icon on the **Navigation bar,** then tap **Support Package**.

2. Read the notification careful, the tab **Proceed To Generation**

3. Prepare an external USB (formatted in NTFS/FAT/exFAT) with USB-A-to-C adaptor. Insert it into the type C port of MetaDefender Drive with Smart Touch then tab **Generate Support Package**

4. Wait for the package creation process to complete

5. Once completed, press **Done** and remove the USB storage from Smart Touch.

6. The Support Package will be created and located in the root of your MetaDefender Drive with Smart Touch storage under the ***smclog*** folder.

About the Process

This process is to generate support packages for MetaDefender Drive with **Smart Touch**. To generate a support package for MetaDefender Drive, please follow the instruction on [this page](https://www.opswat.com/docs/mddrive/troubleshooting/generate-support-packages).
