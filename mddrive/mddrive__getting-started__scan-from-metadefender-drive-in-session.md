<!-- source: https://www.opswat.com/docs/mddrive/getting-started/scan-from-metadefender-drive-in-session -->

# Getting Started with MetaDefender Drive In-Session

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Perform an In-Session Scan](/docs/mddrive/getting-started/scan-from-metadefender-drive-in-session#perform-an-in-session-scan)

While your device OS is running, insert your OPSWAT MetaDefender Drive into the device's USB Type-A port.

1. Navigate to the ***root*** folder inside the MetaDefender Drive partition and locate the ***MetaDefender Drive In-Sesion Scan.exe*** file

3. When click it, In-Session will initialize with a splashing screen

Launching In-Session from Smart Touch

If you are running In-Session from Drive with Smart Touch, on Smart Touch screen you will see it status changes to **In-Session Scan Detected**

3. Then the application starts into **Overview** with option to run **Posture Check** which is a combination check where **Deep Compliance** will be triggered first and then **Malware scan** after

3. **Deep Compliance** checks if **Operating System Update** in **Anti-Malware, Encryption**
4. Any compliant issues will be reported in **Deep Compliance** tab, and can be expanded to provide more details
5. The issue will also be reflected in **Device Information** tab as well, along with other details about the device being checked

**View collected information of the scanned devices from Central Management**

If MetaDefender Drive is enrolled and managed by Central Management, after reports are synced, from **Central Management**, navigate to **Solution → Portable Malware Scanning → Dashboard → Scanned Host.** Click a scanned host, the collected information will be shown under **System Information.**

7. After **Compliance Check** is done, you can also chose to **Proceed with Malware Scan**
8. Click **Malware Scan** tab, you will see all of scan modes available for MetaDefender Drive In-Session

Engines for In-Session

Engines for In-Session scan will not be updated when In-Session is running. Engines must be updated in advanced by

- Engines update in MetaDefender Drive Toolkit, following the instructions [here](https://www.opswat.com/docs/mddrive/maintenance/update-engines)
- Engines update in MetaDefender Drive when booting it up, following the instructions [here](https://www.opswat.com/docs/mddrive/getting-started/boot-from-metadefender-drive#engines)

9. Wait until all of the embedded engines display the **Ready** status. Click the **(i)** icon to see the embedded engines provided with the version. Those engines are only available after Drive has been updated either by Drive Toolkit or by Update from Drive's UI.

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

## [**Device Final Verdict**](/docs/mddrive/getting-started/scan-from-metadefender-drive-in-session#device-final-verdict)

The device will be marked Unsafe when Deep Compliance or Malware check report any issue.

## [Settings for MetaDefender Drive In-Session](/docs/mddrive/getting-started/scan-from-metadefender-drive-in-session#settings-for-metadefender-drive-in-session)

The Settings provides configuration for In-Session. The settings will be applied on the next run after saving.

### [Posture Check Operations Options](/docs/mddrive/getting-started/scan-from-metadefender-drive-in-session#posture-check-operations-options)

- Enable/Disable **Deep Compliance**
- The **Malware Scan** that follows up after **Compliance Check**

### [Options for Deep Compliance](/docs/mddrive/getting-started/scan-from-metadefender-drive-in-session#options-for-deep-compliance)

- **AntiMalware** local existence and compliance
- **Disk encryption** is enabled or not
- **Operating System** is up-to-date or outdated

### [Options to display Malware Scan type](/docs/mddrive/getting-started/scan-from-metadefender-drive-in-session#options-to-display-malware-scan-type)

- Show/Hide Memory Scan
- Show/Hide Full Scan
- Show/Hide Custom Scan

## [Manage In-Session settings with Central Management](/docs/mddrive/getting-started/scan-from-metadefender-drive-in-session#manage-in-session-settings-with-central-management)

If MetaDefender Drive has been enrolled to OPSWAT Central Management, In-Session can be remotely configured from there

## [View collected information of the scanned devices from Central Management](/docs/mddrive/getting-started/scan-from-metadefender-drive-in-session#view-collected-information-of-the-scanned-devices-from-central-management)

After reports are synced, from **Central Management**, navigate to **Solution → Portable Malware Scanning → Dashboard → Scanned Host.** Click a scanned host, the collected information will be shown under **System Information.**
