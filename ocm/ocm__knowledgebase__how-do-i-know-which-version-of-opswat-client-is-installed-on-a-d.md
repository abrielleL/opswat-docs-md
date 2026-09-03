<!-- source: https://www.opswat.com/docs/ocm/knowledgebase/how-do-i-know-which-version-of-opswat-client-is-installed-on-a-d -->

# How do I know which version of MetaDefender Endpoint is installed on a device?

This article applies to all MetaDefender Endpoint releases deployed on Windows, Linux, macOS, iOS or Android systems.

Pro Tip:

The version of MetaDefender Endpoint installed on a device can be confirmed either remotely via the OPSWAT Central Management Console, or locally via the device OS.

## [MetaAccess Console](/docs/ocm/knowledgebase/how-do-i-know-which-version-of-opswat-client-is-installed-on-a-d#metaaccess-console)

1. Log into the **OPSWAT Central Management Console** and navigate to the **Inventory>Devices** tab.
2. Enter the device ID, username, group name, IP address, or MAC address into the search field and run the **Search**.
3. Once located, Client version details will be listed in the **Agent Version** column, as illustrated below.

4. Client/Agent version and type is also shown in the **System Information** box when we view device details. In this view, users can also check which SDK version the client is running, as illustrated below.

Pro Tip:

Unless the automatic updates are disabled (via the **OPSWAT Central Management Console>Settings>Global Settings>Device Agents** tab), the Persistent MetaDefender Endpoint will update automatically as new versions are released.

If the device is offline for an extended period, the version will update as soon as the device is back online.

The On-Demand MetaDefender Endpoint will not automatically update, regardless of whether the account is set to do so.

## [From Windows On-Demand and Persistent Client, tray icon enabled](/docs/ocm/knowledgebase/how-do-i-know-which-version-of-opswat-client-is-installed-on-a-d#from-windows-on-demand-and-persistent-client-tray-icon-enabled)

1. Open the Windows **Start** menu.
2. Search for **MetaDefender Endpoint**.
3. Right-click the Client **Tray Icon**.
4. Select the **About** option to view the device Client version details.

Pro Tip:

Information listed in the About dialogue includes:

- **the agent version**
- **the SDK version (OESIS Framework version)**
- **hostname**
- **username**
- **OS information**
- **IP address**
- **MAC address**
- **the server the Client is communicating with**
- **the account the device is associated with**
- **the last time the Client communicated with the OPSWAT Central Management Cloud.**
## [From Windows Persistent Client, tray icon disabled](/docs/ocm/knowledgebase/how-do-i-know-which-version-of-opswat-client-is-installed-on-a-d#from-windows-persistent-client-tray-icon-disabled)

**MetaDefender Endpoint version**

Users can check on the Client version via the registry at the relevant location below:

- For Windows 32-bit:

  - Go to **HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Gears Client\Config**, and key **, MSIPackageVersion.**
- For Windows 64-bit:

  - Go to **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\OPSWAT\Gears Client\Config**, and key **MSIPackageVersion**

### [**SDK version (OESIS Framework version)**](/docs/ocm/knowledgebase/how-do-i-know-which-version-of-opswat-client-is-installed-on-a-d#sdk-version-oesis-framework-version)

- For Windows 32-bit:

  - Go to **C:\Program Files\OPSWAT\OnDemand\ondemands\oesis** and check the product version/file version of any dll file.
- For Windows 64-bit:

  - Go to **C:\Program Files (x86)\OPSWAT\OnDemand\ondemands\oesis** and check the product version/file version of any dll file.

## [From macOS Persistent Client, tray icon disabled](/docs/ocm/knowledgebase/how-do-i-know-which-version-of-opswat-client-is-installed-on-a-d#from-macos-persistent-client-tray-icon-disabled)

1. Open **Finder** and go to **/Applications/OPSWAT GEARS Client**.
2. CTRL Click **OPSWAT Gears** and select **Get Info**, to see all application data, as illustrated in the screenshot below.

## [From Linux Client](/docs/ocm/knowledgebase/how-do-i-know-which-version-of-opswat-client-is-installed-on-a-d#from-linux-client)

### [**Check Client version via command**](/docs/ocm/knowledgebase/how-do-i-know-which-version-of-opswat-client-is-installed-on-a-d#check-client-version-via-command)

1. Open a **Terminal** and run the command: **opswat-client -i**
2. Client version details will be listed as command output.

### [**Check Client version via file name**](/docs/ocm/knowledgebase/how-do-i-know-which-version-of-opswat-client-is-installed-on-a-d#check-client-version-via-file-name)

1. Go to **/usr/bin/opswatclient/bin**
2. Product version will be included with the file name.

   - For example, **file name: dax-15.5.4.0** (where the product version is 15.5.4.0).

## [From iOS/Android Mobile App](/docs/ocm/knowledgebase/how-do-i-know-which-version-of-opswat-client-is-installed-on-a-d#from-iosandroid-mobile-app)

1. Open the **OPSWAT app**.
2. Click on the **Menu** icon in the top right-hand corner of the screen.
3. Select **About** to view the version details.

Support:

If you have any difficulty **Accessing Device Client Version Information**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
