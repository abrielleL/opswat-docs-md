<!-- source: https://www.opswat.com/docs/mddrive/getting-started/scan-from-metadefender-drive-in-session -->

# Getting Started with MetaDefender Drive In-Session

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

MetaDefender Drive is ready to use right out of the box. While your Windows OS is running, insert your OPSWAT MetaDefender Drive into the device's USB Type-A port

1. Navigate to the ***root*** folder inside the MetaDefender Drive partition and locate the ***MetaDefender Drive In-Sesion Scan.exe*** file

3. When click it, In-Session will initialize with a splashing screen

Launching In-Session from Smart Touch

If you are running In-Session from Drive with Smart Touch, on Smart Touch screen you will see it status changes to **In-Session Scan Detected**

3. Then the application starts into **Overview** with option to run **Posture Check** which is a combination check where **Deep Compliance** will be triggered first and then **Malware scan** after
4. Find more details about different scan types and how to handle the reports from [Perform In-Session Scans](/docs/mddrive/process/processing-your-device-with-metadefender-drive-in-session)

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

### [Modify Smart Scan Settings](/docs/mddrive/getting-started/scan-from-metadefender-drive-in-session#modify-smart-scan-settings)

Smart Scan allows you to quickly add a preset scan type with a memorable name along with scan paths, it parities with the [Settings → Smart Scan](/docs/mddrive/configuration/preferences---smartscan-settings) of Bare Metal.

- Click to Edit Settings next to Smart Scan checkbox
- Change to a wanted name for this type of scan with accompanied description
- Require One Time Passcode to unlock
- Select at least 1 engine to include
- Select at least 1 direct to for setting
- Save Settings to apply

## [Manage In-Session settings with Central Management](/docs/mddrive/getting-started/scan-from-metadefender-drive-in-session#manage-in-session-settings-with-central-management)

If MetaDefender Drive has been enrolled to OPSWAT Central Management, all of the settings for In-Session can be remotely configured from there. This requires Central Management v.10.7.26091 at minimum.

## [View collected information of the scanned devices from Central Management](/docs/mddrive/getting-started/scan-from-metadefender-drive-in-session#view-collected-information-of-the-scanned-devices-from-central-management)

After reports are synced, from **Central Management**, navigate to **Solution → Portable Malware Scanning → Dashboard → Scanned Host.** Click a scanned host, the collected information will be shown under **System Information.**

To keep MetaDefender Drive In-Session up-to-date and manged, follow these instructions

- [MetaDefender Drive Toolkit](/docs/mddrive/getting-started/drive-toolkit)
- [Manage MetaDefender Drives with OPSWAT Management](/docs/mddrive/configuration/managing-drives-with-central-management)
