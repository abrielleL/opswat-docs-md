<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-do-i-remove-metadefender-endpoint-from-my-device- -->

# How do I remove MetaDefender Endpoint from my device?

> **Check Your Product:**
>
> This article applies to all MetaDefender Endpoint releases deployed on Windows, Linux, macOS, iOS or Android systems.

> **Pro Tip:**
>
> MetaDefender Endpoint can be removed/uninstalled from a device either remotely via the My OPSWAT Central Management Console, or locally via the device OS.
>
> For instructions on remote Client uninstall via the My OPSWAT Central Management Console, please see [How can I delete a device from My OPSWAT Central Management?](https://www.opswat.com/docs/cm/knowledge-base/how-can-i-delete-a-device-from-my-opswat-central-management-)

> **Please Note:**
>
> Users who uninstall MetaDefender Endpoint using one of the manual processes listed below should be aware that some log files and registry items will be kept on the system for possible future use.
>
> To remove MetaDefender Endpoint along with all logs and registries, the automated uninstallation method is recommended.
>
> While remote removal is fully automated for the persistent MetaDefender Endpoint, users should be aware that:
>
> - If an on-demand client is removed remotely via the My OPSWAT Central Management Console, it may also need to be removed locally via the device OS.
> - If an on-demand client is stopped or removed locally via the device OS, it should also be removed via the My OPSWAT Central Management Access console.
> - The above option should be used in the event that you have not configured a policy to automatically delete ‘lost’ devices after a specified duration. If you have, My OPSWAT Central Management would automatically and remotely remove the Client after a period, as configured, and no action would be needed on the endpoint side.
>
> To ensure that all components of the MetaDefender Endpoint have been removed from your system, please see [How can I make sure MetaDefender Endpoint is completely removed from my endpoint?](https://www.opswat.com/docs/cm/knowledge-base/how-can-i-make-sure-metadefender-endpoint-is-completely-removed-)

Removing an installed MetaDefender Endpoint either remotely via the My OPSWAT Central Management Console, or locally via the device OS, will result in the following:

- The MetaDefender Endpoint will no longer be on the device.
- My OPSWAT Central Management will no longer track or display the device on the Console.
- The My OPSWAT Central Management account license previously assigned to that device is free to be applied to another device.

## Windows Client: automated uninstallation (works on Windows-installed Client only)

**For Windows On-Demand Client**

1. Download our **MetaDefender IT Uninstaller** tool [Here](https://opswat-gears-cloud-clients.s3.us-west-2.amazonaws.com/PublicTool/OPSWAT+Client+Uninstaller+Tool+v9.0.exe).
2. With administrator privileges, run the installer.

> **Please Note:**
>
> Your local anti-malware may require you to add an exception in order to run the uninstaller, please do so if needed.

### **For Windows Persistent Client**

1. Open the **Control Panel** and use either **Programs and Features**, **Add/Remove Programs**, or **Program Uninstall**, depending on your version of Windows.
2. Select **MetaDefender Endpoint**, then right-click and choose **Uninstall**, or double click (depending on Windows version) to uninstall it.

## Windows On-Demand MetaDefender Endpoint: manual uninstallation

1. If the MetaDefender Endpoint is running, right-click the MetaDefender Endpoint **Icon** on the tray.
2. From the drop-down menu, select the **Exit** option to stop the MetaDefender Endpoint.
3. Follow the instructions for remote device removal via **My OPSWAT Central Management Console**, please see [How can I delete a device from My OPSWAT Central Management?](https://www.opswat.com/docs/cm/knowledge-base/how-can-i-delete-a-device-from-my-opswat-central-management-)

## macOS Persistent Client: manual uninstallation

1. Open **Finder** and go to **Applications/OPSWAT GEARS Client**.
2. Expand the folder, then select the **Uninstall** option, as highlighted in the screenshot below.
3. Enter your **Administrator Password** when prompted, then wait for the uninstall to complete.

![](https://uploads.developerhub.io/prod/1yda/uzojax9c977c5sy2g2cii0o4oxae0evo40pr65qnj734w13iaewyvejuy7dcjrqg.png)

4. Follow the instructions for remote device removal via **My OPSWAT Central Management Console**, please see [How can I delete a device from My OPSWAT Central Management?](https://www.opswat.com/docs/cm/knowledge-base/how-can-i-delete-a-device-from-my-opswat-central-management-)

## macOS On-Demand Client: manual uninstallation

1. If the MetaDefender Endpoint is running, CTRL click the Client **Icon** on the dock.
2. From the drop-down menu, select the **Exit** option to stop the MetaDefender Endpoint.
3. Follow the instructions for remote device removal via **My OPSWAT Central Management Console**, please see [How can I delete a device from My OPSWAT Central Management?](https://www.opswat.com/docs/cm/knowledge-base/how-can-i-delete-a-device-from-my-opswat-central-management-)

## macOS On-Demand Client: slient uninstallation

### Without PIN Code enabled

```bash
cd /Applications/OPSWAT\ GEARS\ Client/OPSWAT\ GEARS.app/Contents/Resources
sudo ./opswat-gears-od /u
```

![](https://uploads.developerhub.io/prod/1yda/qnm5tpdhwcxamat0d5c8vavff1519yuxv9p0yzz7vnww8w0s9y8uu0etg4mjvj9j.png)

### With PIN Code enabled

```bash
cd /Applications/OPSWAT\ GEARS\ Client/OPSWAT\ GEARS.app/Contents/Resources
sudo ./opswat-gears-od /u /pin <pin code>
```

![](https://uploads.developerhub.io/prod/1yda/7vt6cdvo44r6bxtacn0yff0u1bc5xfhqen10ulo33usv5efnepihytdu4wmx0d1n.png)

## Linux Debian-based Client: manual uninstallation

1. Open a **Terminal** and run the command: **sudo /usr/bin/dpkg -r opswatclient**
2. Follow the instructions for remote device removal via **My OPSWAT Central Management Console**, please see [How can I delete a device from My OPSWAT Central Management?](https://www.opswat.com/docs/cm/knowledge-base/how-can-i-delete-a-device-from-my-opswat-central-management-)

## Linux Redhat-based Client: manual uninstallation

1. Open a Terminal and run the command: **sudo rpm -e opswatclient**
2. Follow the instructions for remote device removal via **My OPSWAT Central Management Console**, please see [How can I delete a device from My OPSWAT Central Management?](https://www.opswat.com/docs/cm/knowledge-base/how-can-i-delete-a-device-from-my-opswat-central-management-)

## OPSWAT Mobile App: manual uninstallation

1. Uninstall/delete the **OPSWAT App** from the device, following the device-appropriate method for application removal.
2. Follow the instructions for remote device removal via **My OPSWAT Central Management Console**, please see [How can I delete a device from My OPSWAT Central Management?](https://www.opswat.com/docs/cm/knowledge-base/how-can-i-delete-a-device-from-my-opswat-central-management-)

## Windows Command Prompt: manual uninstallation

1. Open a Command prompt, then run the relevant command below:
   - In cases where a PIN is required to uninstall:

```powershell
GearsInstaller.exe /u /p <password>
```

- In cases where no PIN is required to uninstall:

```powershell
GearsInstaller.exe /u /p “” (to show the uninstall dialogue)

GearsInstaller.exe /u /p “” /s (to not show the uninstall dialogue)
```

2. If the uninstallation is unsuccessful, one of the following error codes will apply:

| Error Code | Description |
| ---- | ---- |
| 0 | Success |
| 1 | Failed |
| 2 | Invalid parameters |
| 3 | Uninstall action is blocked |
| 4 | Incorrect password |
| 5 | User cancelled (*only for Uninstall by dialog)* |
| 6 | Update in progress |

3. Following successful uninstallation, follow the instructions for remote device removal via **My OPSWAT Central Management Console**, please see [How can I delete a device from My OPSWAT Central Management?](https://www.opswat.com/docs/cm/knowledge-base/how-can-i-delete-a-device-from-my-opswat-central-management-)

## Linux Command Prompt: silent uninstallation (works on persistent Client only)

1. Access the **OPSWAT GEARS Client** application folder and expand it.
2. Click on the **Uninstall.app** option inside the folder.
3. Follow the instructions for remote device removal via **My OPSWAT Central Management Console**, please see [How can I delete a device from My OPSWAT Central Management?](https://www.opswat.com/docs/cm/knowledge-base/how-can-i-delete-a-device-from-my-opswat-central-management-)

Otherwise, to run a silent uninstall via Root command line, do the following:

1. Open a **Terminal** as Root user, then navigate to the **OPSWAT GEARS Client** folder.
2. Then enter the command/s below:

> **Please Note:**
>
> The second command below only applies when you have enabled the **Require PIN when a user uninstalls agents on a device** option via the **My OPSWAT Central Management Console>Settings>Global>Device Agent>Agent.**

- **/u, /uninstall**
- **/pin <PIN code>** when prompted following the above command.

3. Follow the instructions for remote device removal via **My OPSWAT Central Management Console**, please see [How can I delete a device from My OPSWAT Central Management?](https://www.opswat.com/docs/cm/knowledge-base/how-can-i-delete-a-device-from-my-opswat-central-management-)

> **Support:**
>
> If you have followed the relevant instructions above but are **Unable To Remove Or Uninstall The MetaDefender Endpoint From A Device**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form.
