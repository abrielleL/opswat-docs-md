<!-- source: https://www.opswat.com/docs/mdendpoint/v2608/endpoint-management/how-do-i-know-what-version-of-metadefender-endpoint-is-installed -->

# How do I know what version of MetaDefender Endpoint is installed on a device?

> **Check Your Product**
>
> This article applies to all MetaDefender Endpoint releases deployed on Windows, Linux, macOS, iOS or Android systems.

> **Pro Tips:**
>
> The version of MetaDefender Endpoint installed on a device can be confirmed either remotely via the MetaDefender IT-OT Access Console, or locally via the device OS.

## MetaAccess Console

1. Log into the **MetaDefender IT-OT Access Console** and navigate to the **Inventory>Devices** tab.
2. Enter the device name into the search field and run the **Search**.
3. Once located, Client version details will be listed in the **Agent Version** column, as illustrated below.

![](https://uploads.developerhub.io/prod/2x2P/1miv6phw9lvax4e9cindl16yahw767h0j3c14q7mdf2pqhlkkdvyld2lso80ibml.png)

4. Client/Agent version is also shown in the **System Information** box when we view device details. In this view, users can also check which SDK version the client is running, as illustrated below.

![](https://uploads.developerhub.io/prod/2x2P/az0pv5ipy3xbiwor4fk02anpepd5ngmy53gchgwhjxakajtcede8qzc7dd1tliwt.png)

> **Pro Tips:**
>
> Unless the automatic updates are disabled (via the **MetaDefender IT-OT Access Console>Settings>Global>Device Agents** tab), the Persistent MetaDefender Endpoint will update automatically as new versions are released.
>
> If the device is offline for an extended period, the version will update as soon as the device is back online.
>
> The On-Demand MetaDefender Endpoint will not automatically update, regardless of whether the account is set to do so.
>
> For more information on updating the Persistent and On-Demand MetaDefender Endpoint from the endpoint side, please Read This.

## From Windows On-Demand and Persistent Client, tray icon enabled

1. Open the tray icon list.
2. Search for **MetaDefender Endpoint.**
3. Right-click the Client tray icon.
4. Select the **About option to** view the detailed information of Endpoint version of the devices.

![](https://uploads.developerhub.io/prod/2x2P/69h3twamkd9c4lj7n4ww0bjnn8rjtjb0q1kqiiq3fp98n9o0m01eejj3b4cqbpfc.png)

> **Pro Tips:**
>
> Information listed in the About dialogue includes:
>
> - the agent version
> - Active Policy
> - the SDK version (OESIS Framework version)
> - hostname
> - username
> - OS information
> - IP address
> - the server the Client is communicating with
> - the account the device is associated with
> - the last time the Client communicate with the MetaAccess Cloud.

## From Windows Persistent Client, tray icon disabled

### **MetaDefender Endpoint version**

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

![](https://uploads.developerhub.io/prod/2x2P/osxh3hue0smuta19epru4ktomuxcu03ux1d5l95xyru3lz4lw2x6rzmzoz4s1k1j.png)

## From Linux Client

### **Check Client version via command**

1. Open a **Terminal** and run the command: **opswat-client -i**
2. Client version details will be listed as command output.

### **Check Client version via file name**

1. Go to **/usr/bin/opswatclient/bin**
2. Product version will be included with the file name.

- For example, **file name: dax-15.5.4.0** (where the product version is 15.5.4.0).

## From iOS/Android Mobile App

1. Open the **OPSWAT app**.
2. Click on the **Menu** icon in the top right-hand corner of the screen.
3. Select **About** to view the version details.

> **Support:**
>
> If you have any difficulty **Accessing Device Client Version Information**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).

---

[All pages in this documentation](https://www.opswat.com/docs/mdendpoint/llms.txt)
