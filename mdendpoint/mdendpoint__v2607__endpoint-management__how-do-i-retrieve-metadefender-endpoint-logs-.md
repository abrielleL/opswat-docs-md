<!-- source: https://www.opswat.com/docs/mdendpoint/v2607/endpoint-management/how-do-i-retrieve-metadefender-endpoint-logs- -->

# How do I retrieve MetaDefender Endpoint logs?

> **Check Your Product**
>
> This article applies to all MetaDefender Endpoint releases deployed on Windows, macOS, Linux, iOS, and Android systems

> **Please Note:**
>
> When troubleshooting an issue on a device, OPSWAT Support will usually request that the user send us the MetaDefender Endpoint logs from their machine.
>
> There are two ways to retrieve MetaDefender Endpoint logs:
>
> - **OPTION 1:** Collect logs directly from the client device by selecting the option "Export Logs" in the tray-icon of MetaDefender Endpoint.
> - **OPTION 2:** Retrieve the logs remotely via My OPSWAT Central Management
>   - requires the user to have administrator privileges on the associated My OPSWAT Central Management account
>   - requires that the device is enrolled & connected to the My OPSWAT Central Management server
>   - is only applicable for Windows/macOS Persistent MetaDefender Endpoint clients

## OPTION 1: Collect logs directly from the MetaDefender Endpoint device

### Automatic Collection

> **Please Note:**
>
> This option is only available for Windows and macOS Persistent MetaDefender Endpoint clients

#### **Windows (****Persistent MetaDefender Endpoint****)**

1. Download OPSWAT’s **Log Collecto**r tool, [Here](https://kb-hosting-cs.s3.amazonaws.com/KB/MA/OPSWATClient/OPSWAT_Client_-_Log_Collector.zip).
2. Extract and run the downloaded file.
3. The zipped log file, which may be very large, will automatically be placed on your desktop, to be forwarded to the OPSWAT team.

#### **macOS (****Persistent MetaDefender Endpoint****)**

1. Download OPSWAT’s **Log Collecto**r tool, [Here](https://kb-hosting-cs.s3.amazonaws.com/KB/MA/OPSWATClient/Mac-Metadefender-Endpoint-Support.zip).
2. Extract and run the downloaded file.
3. The zipped log file, which may be very large, will automatically be placed on your desktop, to be forwarded to the OPSWAT team.

---

### Manual Collection

#### **Windows (**Persistent MetaDefender Endpoint)

1. Go to the relevant locations below to collect the required logs from File Explorer:

- Client logs:
  - Type *%ProgramData%* \OPSWAT\Gears\logs** into the path bar and hit **Enter**
- Crash dumps:
  - Type %ProgramData%** \OPSWAT\Gears\logs\reports** into the path bar and hit **Enter**
- SDK logs:
  - Type %ProgramData%** \OPSWAT\Gears\sdk** into the path bar and hit **Enter**
- OPG (verification file) logs:
  - Type %HOMEPATH%** \AppData\Local\OPSWAT\Gears\logs** into the path bar and hit **Enter**

2. Copy the required logs, to be compressed (if necessary) and forward to the OPSWAT team.

#### **Windows (On-Demand MetaDefender Endpoint)**

1. Go to the relevant locations below to collect the required logs:

- Client logs:
  - Go to the folder where the MetaDefender Endpoint executable file is located
  - Collect the file named **gears-ondemand.log**
- Crash dumps:
  - Type %HOMEPATH%** \AppData\Local\CrashDump** into the path bar and hit **Enter**

If the On-demand MetaDefender Endpoint is triggered by third-party vendors, go to the relevant locations below to collect the required logs:

- Pulse Secure Host Checker:
  - Type %AppData%** \Pulse Secure\Host Checker\policy_*****##*** into the path bar and hit **Enter** (for example: *C:\Users\bob\AppData\Roaming\Pulse Secure\Host Checker\policy_1*)
- Omnissa Horizon Client (formerly known as VMWare Horizon Client)
  - Depending on the version oh Horizon Client in use, both the On-Demand MetaDefender Endpoint executable file and the log file can be found in one of the locations below:

**C:\Users<username>\AppData\Local\Omnissa\Omnissa Horizon Client\Code Cache<uuid>**  while Horizon Client session is still on

![](https://uploads.developerhub.io/prod/2x2P/j2b6gm7ncmcurr9z2x3tgdct3c42lgrusi1rn8jv6239znev8jqm8ivy6gx3zx12.png)

For Omnissa Horizon Client log : **C:\Users<username>\AppData\Local\Omnissa\Horizon\logs**

![](https://uploads.developerhub.io/prod/2x2P/4s4a153ykp009ngqoqgrzutld7c927mitm8s6sbfohfmyom9nzndywlvbv9wd1dw.png)

2. Copy the required logs, to be compressed (if necessary) and forward to the OPSWAT team.

#### **macOS (****Persistent MetaDefender Endpoint****)**

1. Open **Finder** and go to **/Library/Logs/Gears/logs**, as illustrated in the screenshot below:

![](https://uploads.developerhub.io/prod/2x2P/j1attjej4n9ryl6jgtq0w45u7j3r0od3l3w7ijlzj7qsc2khtm1kmeki2126qyjm.png)

2. Copy the required logs, to be compressed (if necessary) and forward to the OPSWAT team.

#### **macOS (****On-Demand MetaDefender Endpoint****)**

1. Go to the relevant locations below to collect the required logs:

- Client logs:
  - For MetaDefender Endpoint version 10.5.218.0 or earlier, go to **/Desktop/gears-ondemand.log**
  - For MetaDefender Endpoint version 10.5.222.0 or later, go to **/Users/{*****username*****}/Library/Logs/Gears/logs**
- Crash dumps:
  - Open Finder and go to **/Library/Logs/DiagnosticReports**

When running the macOS On-Demand MetaDefender Endpoint as Root, go to the locations below to collect the required logs:

- MetaDefender Endpoint logs:
  - Go to **/var/root/Desktop/gears-ondemand.log**
- Additional malware logs:
  - Go to **/Library/Logs/Gears/logs/Metascan-Client-V2.log**

2. Copy the required logs, to be compressed (if necessary) and forward to the OPSWAT team.

If on-demand Client is triggered by third-party vendors, go to the relevant location/s below to collect the required log/s:

Omnissa Horizon Client (formerly known as VMWare Horizon Client)

**/Users/<User name>/Library/Logs/Gears/logs/<License Key>/GEARS-Ondemand.log**

![](https://uploads.developerhub.io/prod/2x2P/kmybqbby9e9pdk5pm8bhzp005ezdylmweluctusy60raii9wr13bwgbviwf9z0xt.png)

For Omnissa Horizon Client log: **/Users/<username>/Library/Logs/Omnissa Horizon Client/**

![](https://uploads.developerhub.io/prod/2x2P/83qvm8ldf09ii6ogdom1mcu43s6fglrx8e3d8ik4xmuxd5bqb582k56w3ybti10h.png)

#### **Linux V4 (Version 15.x.y.z)**

1. Go to the location below to collect the required log:

- Client logs:
  - Go to **/var/log/opswatclient**

2. Copy the required log, to be compressed (if necessary) and forward to the OPSWAT team.

#### **Linux V3 (Version 14.0.x.y)**

1. Go to the relevant locations below to collect the required logs:

- Client logs:
  - Go to **/var/log/gears/log**
- Error logs:
  - Go to **/var/log/gears.err**
- Configuration logs:
  - Go to **/etc/gears/gears.json**

2. Copy the required logs, to be compressed (if necessary) and forward to the OPSWAT team.

#### **Android/iOS**

On mobile devices, logs are stored in memory, but can be emailed directly from the OPSWAT Mobile App by selecting the **Report a Bug** option.

---

## OPTION 2: Retrieve logs remotely via the My OPSWAT Central Management Console

> **Please Note:**
>
> This method:
>
> - requires administrator privileges on the associated My OPSWAT Central Management account
> - requires that the device is enrolled & connected to the My OPSWAT Central Management server
> - is only applicable to Windows/macOS Persistent MetaDefender Endpoint clients
> - to learn which versions support this command, [Read This](https://www.opswat.com/docs/cm/knowledge-base/why-can-t-i-apply-certain-actions-on-some-of-my-managed-devices-).

As a My OPSWAT Central Management account administrator, follow the steps below:

1. Log into the My OPSWAT Central Management Console and navigate to **Inventory>Devices**.
2. Use the **Search** field to locate the relevant MetaDefender Endpoint device.
3. Click on the chosen device, then access the **Select Action** drop-down menu in the top right-hand corner of the screen, directly under your username.
4. Select the **Fetch log** option, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/2x2P/tj1h6zt5k67i8vley4kfdge4a4dqayzf2zew21ib0ity82csx01xwjv8u5fi4ks2.png)

5. To view the log you fetched: Go to **Inventory>Devices>selected device>Events>Device Logs**, as illustrated below.

![](https://uploads.developerhub.io/prod/2x2P/tqw4k6ul9syk34j3e8xh63sq23p03mn5ghqqq40ali64mvs7xy1e92wq3vyzm2px.png)

> **Please Note:**
>
> When a MetaDefender Endpoint device is connected to My OPSWAT Central Management Cloud, the device will collect the log files and submit them directly to the My OPSWAT Central Management Cloud.

> **Support:**
>
> If you have any queries, concerns or issues around **Collecting** **MetaDefender Endpoint** **Logs To Send To OPSWAT Support** or to **Send Log Files To OPSWAT Suppor**t, please open a [Support Case](https://www.opswat.com/support) via phone, online chat or form. If you have been asked to send Client logs to OPSWAT Support as part of the troubleshooting process, but they are too large to email or attach to the support ticket, please use the **Large File** submission feature on the OPSWAT Support Portal, [Here](https://go.opswat.com/s/cases).
