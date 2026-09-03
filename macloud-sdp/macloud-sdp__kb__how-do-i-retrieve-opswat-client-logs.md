<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/how-do-i-retrieve-opswat-client-logs -->

# How do I retrieve MetaDefender Endpoint logs?

This article applies to all MetaDefender Endpoint releases deployed on Windows, macOS, Linux, iOS and Android systems.

Please Note:

When troubleshooting an issue on a device, OPSWAT Support will usually request that the user send us the MetaDefender Endpoint logs from their machine.

There are two ways to retrieve the MetaDefender Endpoint logs:

- **OPTION 1:** Collect the logs directly from the Client device by selecting the option "Export Logs" in the tray-icon of MetaDefender Endpoint.
- **OPTION 2:** Retrieve the logs remotely. This method:

  - requires that the user have administrator privileges on the associated MetaDefender IT Access account
  - requires that the device be connected to the MetaDefender IT Access server
  - is only applicable to Windows/macOS Persistent MetaDefender Endpoint.
## [OPTION 1: Collect the logs directly from the MetaDefender Endpoint device](/docs/macloud-sdp/kb/how-do-i-retrieve-opswat-client-logs#option-1-collect-the-logs-directly-from-the-metadefender-endpoint-device)

### [Automatic Collection](/docs/macloud-sdp/kb/how-do-i-retrieve-opswat-client-logs#automatic-collection)

Please Note:

This option is only available for Windows and macOS Persistent MetaDefender Endpoint.

#### [**Windows (**Persistent MetaDefender Endpoint**)**](/docs/macloud-sdp/kb/how-do-i-retrieve-opswat-client-logs#windows-persistent-metadefender-endpoint)

1. Download OPSWAT’s **Log Collecto**r tool, [Here](https://kb-hosting-cs.s3.amazonaws.com/KB/MA/OPSWATClient/OPSWAT_Client_-_Log_Collector.zip).
2. Run the downloaded file.
3. The zipped log file, which may be very large, will automatically be placed on your desktop, to be forwarded to the OPSWAT team.

#### [**macOS (**Persistent MetaDefender Endpoint**)**](/docs/macloud-sdp/kb/how-do-i-retrieve-opswat-client-logs#macos-persistent-metadefender-endpoint)

1. Download OPSWAT’s **Log Collecto**r tool, [Here](https://kb-hosting-cs.s3.amazonaws.com/KB/MA/OPSWATClient/Mac-Metadefender-Endpoint-Support.zip).
2. Run the downloaded file.
3. The zipped log file, which may be very large, will automatically be placed on your desktop, to be forwarded to the OPSWAT team.

### [Manual Collection](/docs/macloud-sdp/kb/how-do-i-retrieve-opswat-client-logs#manual-collection)

#### [**Windows (**Persistent MetaDefender Endpoint)](/docs/macloud-sdp/kb/how-do-i-retrieve-opswat-client-logs#windows-persistent-metadefender-endpoint)

1. Go to the relevant location/s below to collect the required log/s:

- Client logs:

  - Type  into the path bar and hit **Enter**.
  - Then add **\OPSWAT\Gears\logs** to complete the path.
- Crash dumps:

  - Type  into the path bar and hit **Enter**.
  - Then add **\OPSWAT\Gears\logs\reports** to complete the path.
- SDK logs:

  - Type  into the path bar and hit **Enter**.
  - Then add **\OPSWAT\Gears\sdk** to complete the path.
- OPG (verification file) logs:

  - Type  into the path bar and hit **Enter**.
  - Then add _ _**\Appdata\Local\OPSWAT\Gears\Logs** to complete the path.

2. Copy the required log/s, to be compressed (if necessary) and forwarded to the OPSWAT team.

#### [**Windows (On-Demand MetaDefender Endpoint)**](/docs/macloud-sdp/kb/how-do-i-retrieve-opswat-client-logs#windows-on-demand-metadefender-endpoint)

1. Go to the relevant location/s below to collect the required log/s:

- Client logs:

  - Go to the folder where the MetaDefender Endpoint executable file is stored.
  - Then locate the file named **gears-ondemand.log**
- Crash dumps:

  - Type  into the path bar and hit **Enter**.
  - Then add **\AppData\Local\CrashDump** to complete the path.

If On-demand MetaDefender Endpoint is triggered by third-party vendors, go to the relevant location/s below to collect the required log/s:

- Pulse Secure Host Checker:

  - Type  into the path bar and hit **Enter**.
  - Then add **\Pulse Secure\Host Checker\policy_XXX** to complete the path. (so, for example: **C:\Users\bob\AppData\Roaming\Pulse Secure\Host Checker\policy_1**)
- VMWare Horizon Client:

  - Depending on which Horizon Client version you run, both the On-Demand MetaDefender Endpoint executable file and the log file can be found in one of the locations below:

    - **C:\Users<username>\AppData\Local\VMware Horizon View Client\Code Cache<uuid>**
    - **C:\Program Files (x86)\VMWare\VMware Horizon View Client\Code Cache<uuid>**

2. Copy the required log/s, to be compressed (if necessary) and forwarded to the OPSWAT team.

#### [**macOS (**Persistent MetaDefender Endpoint**)**](/docs/macloud-sdp/kb/how-do-i-retrieve-opswat-client-logs#macos-persistent-metadefender-endpoint)

1. Open **Finder** and go to **/Library/Logs/Gears/logs**, as illustrated in the screenshot below.

2. Copy the required log/s, to be compressed (if necessary) and forwarded to the OPSWAT team.

#### [**macOS (**On-Demand MetaDefender Endpoint**)**](/docs/macloud-sdp/kb/how-do-i-retrieve-opswat-client-logs#macos-on-demand-metadefender-endpoint)

1. Go to the relevant location/s below to collect the required log/s:

- Client logs:

  - For MetaDefender Endpoint version 10.5.218.0 or earlier, go to **/Desktop/gears-ondemand.log**
  - For MetaDefender Endpoint version 10.5.222.0 or later, go to **/Users/{username}/Library/Logs/Gears/logs**
- Crash dumps:

  - Open Finder and go to **/Library/Logs/DiagnosticReports**

When running the macOS On-Demand MetaDefender Endpoint as Root, go to the location/s below to collect the required log/s:

- MetaDefender Endpoint logs:

  - Go to **/var/root/Desktop/gears-ondemand.log**
- Additional malware logs:

  - Go to **/Library/Logs/Gears/logs/Metascan-Client-V2.log**

2. Copy the required log/s, to be compressed (if necessary) and forwarded to the OPSWAT team.

#### [**Linux V4 (Version 15.x.y.z)**](/docs/macloud-sdp/kb/how-do-i-retrieve-opswat-client-logs#linux-v4-version-15xyz)

1. Go to the location below to collect the required log:

- Client logs:

  - Go to **/var/log/opswatclient**

2. Copy the required log, to be compressed (if necessary) and forwarded to the OPSWAT team.

#### [**Linux V3 (Version 14.0.x.y)**](/docs/macloud-sdp/kb/how-do-i-retrieve-opswat-client-logs#linux-v3-version-140xy)

1. Go to the relevant location/s below to collect the required log/s:

- Client logs:

  - Go to **/var/log/gears/log**
- Error logs:

  - Go to **/var/log/gears.err**
- Configuration logs:

  - Go to **/etc/gears/gears.json**

2. Copy the required log/s, to be compressed (if necessary) and forwarded to the OPSWAT team.

#### [**Android/iOS**](/docs/macloud-sdp/kb/how-do-i-retrieve-opswat-client-logs#androidios)

On mobile devices, logs are only stored in the memory, but can be emailed directly from the OPSWAT Mobile App by selecting the **Submit Feedback** option.

## [OPTION 2: Retrieve the logs remotely via the MetaDefender IT Access Console](/docs/macloud-sdp/kb/how-do-i-retrieve-opswat-client-logs#option-2-retrieve-the-logs-remotely-via-the-metadefender-it-access-console)

Please Note:

This method:

- requires administrator privileges on the associated MetaDefender IT Access account
- requires that the device be connected to the MetaDefender IT Access server
- is only applicable to Windows/macOS Persistent MetaDefender Endpoint
- to learn which versions support this command, [Read This](/docs/macloud-sdp/kb/why-cant-i-apply-certain-actions-on-some-of-my-managed-devices).

As MetaDefender IT Access account administrator, follow the steps below:

1. Log into the MetaDefender IT Access Console and navigate to **Inventory>Devices**.
2. Use the **Search** field to locate the relevant MetaDefender Endpoint device.
3. Click on the chosen device, then access the **Select Action** drop-down menu in the top right-hand corner of the screen, directly under your username.
4. Select the **Fetch log** option, as illustrated in the screenshot below.

5. To view the log you fetched: Go to **Inventory>Devices>Relevant Device>Events>Device Logs**, as illustrated below.

Please Note:

When a MetaDefender Endpoint device is connected to the MetaDefender IT Access Cloud, the device will collect the log files and submit them directly to the MetaDefender IT Access Cloud.

Support:

If you have any queries, concerns or issues around **Collecting** **MetaDefender Endpoint** **Logs To Send To OPSWAT Support** or to **Send Log Files To OPSWAT Suppor**t, please open a [Support Case](https://my.opswat.com/portal/support) via phone, online chat or form. If you have been asked to send Client logs to OPSWAT Support as part of the troubleshooting process, please submit it in the case upload function.
