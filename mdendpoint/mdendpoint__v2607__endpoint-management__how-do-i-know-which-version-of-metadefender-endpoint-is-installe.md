<!-- source: https://www.opswat.com/docs/mdendpoint/v2607/endpoint-management/how-do-i-know-which-version-of-metadefender-endpoint-is-installe -->

# How do I know which version of MetaDefender Endpoint is installed on a device?

> **Check Your Product:**
>
> This article applies to all MetaDefender Endpoint releases deployed on Windows, Linux, macOS, iOS or Android systems.

> **Success**
>
> The version of MetaDefender Endpoint installed on a device can be confirmed either remotely via the My OPSWAT Console, or locally via the device OS.

## MetaDefender IT-OT Access Console

1. Log into the My OPSWAT **Console** and navigate to the **Inventory>Devices** tab.
2. Enter the device ID, username, group name, IP address, or MAC address into the search field and run the **Search**.
3. Once located, Client version details will be listed in the **Agent Version** column, as illustrated below.

![](https://uploads.developerhub.io/prod/2x2P/wr825nfq5dwx75ozpv4gj1rhqa3fjfmm0zlj9jgzlo3026p3cmtq1kzanxef5xwn.png)

4. Client/Agent version and type is also shown in the **System Information** box when we view device details. In this view, users can also check which SDK version the client is running, as illustrated below.

![](https://uploads.developerhub.io/prod/9jd0/13h7yf869xc4bifojpzj0vkaxzv6gu2mh81nlxfximdxc1vet7ilkhrcvfnvyx6q.png)

> **Pro Tip:**
>
> Unless the automatic updates are disabled (via the **My OPSWAT Console>Settings>Global Settings>Device Agents** tab), the Persistent MetaDefender Endpoint will update automatically as new versions are released.
>
> If the device is offline for an extended period, the version will update as soon as the device is back online.
>
> The On-Demand MetaDefender Endpoint will not automatically update, regardless of whether the account is set to do so.

![](https://uploads.developerhub.io/prod/2x2P/ufcie0jjfry7qi39tmiby783a6wylf4htz662pryb88hbwr3vfmj8hkcili1ls6l.png)

## From Windows On-Demand and Persistent Client, tray icon enabled

1. Open the Windows **Start** menu.
2. Search for **MetaDefender Endpoint**.
3. Right-click the Client **Tray Icon**.
4. Select the **About** option to view the device Client version details.

![](https://uploads.developerhub.io/prod/2x2P/3nhrtqnpgmutnodvelhxvpvl33nyblphfwfvw1g0wfbwxb9z48s7vrbbluplsxaf.png)

> **Pro Tips:**
>
> Information listed in the About dialogue includes:
>
> - **the agent version**
> - **the SDK version (OESIS Framework version)**
> - **hostname**
> - **username**
> - **OS information**
> - **IP address**
> - **MAC address**
> - **the server the MetaDefender Endpoint is communicating with**
> - **the account the device is associated with**
> - **the last time the** **MetaDefender Endpoint** **communicated with the My OPSWAT Cloud.**

## From Windows Persistent Client, tray icon disabled

**MetaDefender Endpoint version**

Users can check on the Client version via the registry at the relevant location below:

- For Windows 32-bit:
  - Go to **HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Gears Client\Config**, and key **, MSIPackageVersion.**
- For Windows 64-bit:
  - Go to **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\OPSWAT\Gears Client\Config**, and key **MSIPackageVersion**

### **SDK version (OESIS Framework version)**

- For Windows 32-bit:
  - Go to **C:\Program Files\OPSWAT\OnDemand\ondemands\oesis** and check the product version/file version of any dll file.
- For Windows 64-bit:
  - Go to **C:\Program Files (x86)\OPSWAT\OnDemand\ondemands\oesis** and check the product version/file version of any dll file.

## From macOS Persistent Client, tray icon disabled

1. Open **Finder** and go to **/Applications/OPSWAT GEARS Client**.
2. CTRL Click **OPSWAT Gears** and select **Get Info**, to see all application data, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/2x2P/rnfq5fldckomkg3guq160hxwjebqa0pbmpjmdh00wr70ik17x1kuormf8jtzbi2o.png)

## From Linux Client

### **Check Client version via command**

1. Open a **Terminal** and run the command: **opswat-client -i**
2. Client version details will be listed as command output.

### **Check Client version via file name**

1. Go to **/usr/bin/opswatclient/bin**
2. Product version will be included with the file name.
   - For example, **file name: dax-15.5.4.0** (where the product version is 15.5.4.0).

## From iOS/Android Mobile App

1. Open the **OPSWAT App**.
2. Click on the **Menu** icon in the top right-hand corner of the screen.
3. Select **About** to view the version details.

> **Support:**
>
> If you have any difficulty **Accessing Device Client Version Information**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).
