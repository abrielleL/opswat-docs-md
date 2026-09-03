<!-- source: https://www.opswat.com/docs/mdendpoint/endpoint-management/how-do-i-retrieve-the-metadefender-logs- -->

# How do I retrieve the MetaDefender logs?

> **Check Your Product:**
>
> This article applies to all OCM v7.5.0+ releases deployed on Windows or Linux systems, and all  MetaDefender Endpoint releases deployed on Windows, macOS, Linux, iOS and Android systems.

> **Info**
>
> When troubleshooting an issue on a device, OPSWAT Support will usually request that the user send us the OPSWAT Client logs from their machine.
>
> There are two ways to retrieve the Client logs:
>
> - **OPTION 1:** Collect the logs directly from the Client device.
> - **OPTION 2:** Retrieve the logs remotely. This method:
>   - requires that the user have administrator privileges on the associated OPSWAT Central Management account
>   - requires that the device be connected to the OPSWAT Central Management server
>   - is only applicable to Windows/macOS persistent Client.

OPTION 1: Collect the logs directly from the Endpoint device

### Automatic Collection

> **Please Note:**
>
> This option is only available for Windows and macOS persistent OPSWAT Client.

#### **Windows (Persistent Client)**

1. Download OPSWAT’s **Log Collecto**r tool, [Here](https://onlinehelp.opswat.com/centralmgmtv7/attachments_4089863_1_Windows_-_Collect_logs_tool.zip).
2. Run the downloaded file.
3. The zipped log file, which may be very large, will automatically be placed on your desktop, to be forwarded to the OPSWAT team.

#### **macOS (Persistent Client)**

1. Download OPSWAT’s **Log Collecto**r tool, [Here](https://onlinehelp.opswat.com/centralmgmtv7/attachments_4089864_1_macOS_-_Collect_logs_tool.zip).
2. Run the downloaded file.
3. The zipped log file, which may be very large, will automatically be placed on your desktop, to be forwarded to the OPSWAT team.

### Manual Collection

#### **Windows (Persistent Client)**

1. Go to the relevant location/s below to collect the required log/s:

- Client logs:
  - Type %ProgramData% into the path bar and hit **Enter**.
  - Then add **\OPSWAT\Gears\logs** to complete the path.
- Crash dumps:
  - Type %ProgramData% into the path bar and hit **Enter**.
  - Then add **\OPSWAT\Gears\logs\reports** to complete the path.
- SDK logs:
  - Type %ProgramData% into the path bar and hit **Enter**.
  - Then add **\OPSWAT\Gears\sdk** to complete the path.
- OPG (verification file) logs:
  - Type %HOMEPATH% into the path bar and hit **Enter**.
  - Then add _ _**\Appdata\Local\OPSWAT\Gears\Logs** to complete the path.

2. Copy the required logs, to be compressed (if necessary) and forwarded to the OPSWAT team.

#### **Windows (On-Demand Client)**

1. Go to the relevant location/s below to collect the required log/s:

- Client logs:
  - Go to the folder where the MetaDefender Endpoint executable file is stored.
  - Then locate the file named **gears-ondemand.log**
- Crash dumps:
  - Type %HOMEPATH% into the path bar and hit **Enter**.
  - Then add **\AppData\Local\CrashDump** to complete the path.

If on-demand Client is triggered by third-party vendors, go to the relevant location/s below to collect the required log/s:

- Pulse Secure Host Checker:
  - Type %AppData% into the path bar and hit **Enter**.
  - Then add **\Pulse Secure\Host Checker\policy_XXX** to complete the path. (so, for example: **C:\Users\bob\AppData\Roaming\Pulse Secure\Host Checker\policy_1**)
- Omnissa Horizon Client (formerly known as VMWare Horizon Client)
  - Depending on which Horizon Client version you run, both the on-demand MetaDefender Endpoint executable file and the log file can be found in one of the locations below:

** C:\Users&lt;username>\AppData\Local\Omnissa\Omnissa Horizon Client\Code Cache&lt;uuid>\  while Horizon Client session is still on **

![](https://uploads.developerhub.io/prod/2x2P/j2b6gm7ncmcurr9z2x3tgdct3c42lgrusi1rn8jv6239znev8jqm8ivy6gx3zx12.png)

For Omnissa Horizon Client log : **C:\Users&lt;username>\AppData\Local\Omnissa\Horizon\logs**

![](https://uploads.developerhub.io/prod/2x2P/4s4a153ykp009ngqoqgrzutld7c927mitm8s6sbfohfmyom9nzndywlvbv9wd1dw.png)

2. Copy the required log/s, to be compressed (if necessary) and forwarded to the OPSWAT team.

#### **macOS (Persistent Client)**

1. Open **Finder** and go to **/Library/Logs/Gears/logs**, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/9jd0/26o22774svwmzanqgzuaz7uika6gl70bjlm2zn703czcw7dal8ll7bfvgv4vt27q.png)

#### macOS (On-Demand Client)

If on-demand Client is triggered by third-party vendors, go to the relevant location/s below to collect the required log/s:

- Omnissa Horizon Client (formerly known as VMWare Horizon Client)

**/Users/<User name>/Library/Logs/Gears/logs/<License Key>/GEARS-Ondemand.log**

![](https://uploads.developerhub.io/prod/2x2P/kmybqbby9e9pdk5pm8bhzp005ezdylmweluctusy60raii9wr13bwgbviwf9z0xt.png)

For Omnissa Horizon Client log: **/Users/<username>/Library/Logs/Omnissa Horizon Client/**

![](https://uploads.developerhub.io/prod/2x2P/83qvm8ldf09ii6ogdom1mcu43s6fglrx8e3d8ik4xmuxd5bqb582k56w3ybti10h.png)
