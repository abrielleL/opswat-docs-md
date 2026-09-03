<!-- source: https://www.opswat.com/docs/mddrive/getting-started/scan-from-metadefender-drive-in-session -->

# Perform an In-Session Scan

## [Run MetaDefender Drive In-Session](/docs/mddrive/getting-started/scan-from-metadefender-drive-in-session#run-metadefender-drive-in-session)

1. While your device OS is running, insert your OPSWAT MetaDefender Drive into the device's USB Type-A port.
2. Navigate to the ***root*** folder inside the MetaDefender Drive partition and locate the ***MetaDefender Drive In-Sesion Scan.exe*** file

3. When click it, In-Session will initialize with a splashing screen
4. Then the application starts into **Overview** tab, showing the quick view of history in the last 30 days and the Device information. More details about the device will be reported in **Device Information** tab as well.

**View collected information of the scanned devices from Central Management**

If MetaDefender Drive is enrolled and managed by Central Management, after reports are synced, from **Central Management**, navigate to **Solution → Portable Malware Scanning → Dashboard → Scanned Host.** Click a scanned host, the collected information will be shown under **System Information.**

3. Click **Malware Scan** tab, you will see all of scan modes available for MetaDefender Drive In-Session

Info

Engines for In-Session scan will not be updated when In-Session is running. Engines must be updated in advanced by

- Engines update in MetaDefender Drive Toolkit, following the instructions [here](https://www.opswat.com/docs/mddrive/maintenance/update-engines)
- Engines update in MetaDefender Drive when booting it up, following the instructions [here](https://www.opswat.com/docs/mddrive/getting-started/boot-from-metadefender-drive#engines)

4. Wait until all of the embedded engines display the **Ready** status. Click the **(i)** icon to see the embedded engines provided with the version. Those engines are only available after Drive has been updated either by Drive Toolkit or by Update from Drive's UI.

## [Memory Scan](/docs/mddrive/getting-started/scan-from-metadefender-drive-in-session#memory-scan)

To scan all the libraries loaded into the memory:

1. Click the **Memory Scan** tab, then click **Start**

2. Once the scan is completed, the results of scanning all the libraries loaded into the memory will be displayed.

## [**Full Scan**](/docs/mddrive/getting-started/scan-from-metadefender-drive-in-session#full-scan)

To run a full system scan:

1. Click the **Full Scan** tab, then click **Start**

2. After scan completes, the full scan report will show:

## [Custom Scan](/docs/mddrive/getting-started/scan-from-metadefender-drive-in-session#custom-scan)

To select specific partitions, folders, or files to scan:

1. Click the **Custom Scan** tab, select the paths you want to include in the custom scan, then click **Start**.

2. When a Scan is in progress, you can click View Scan Path.

   It will open a popup to view what directories are under scan session
3. Once the scan is completed, the detailed results of the selected paths will be displayed, as in the following screenshot displaying scan results of C: and D: partitions on Windows 10
