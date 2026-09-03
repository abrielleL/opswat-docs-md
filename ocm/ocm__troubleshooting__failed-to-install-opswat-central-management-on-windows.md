<!-- source: https://www.opswat.com/docs/ocm/troubleshooting/failed-to-install-opswat-central-management-on-windows -->

# Failed to install OPSWAT Central Management on Windows

| Term | Detail |
| --- | --- |
| Problem | Failed to re-install OPSWAT Central Management |
| Cause | The installer could not copy some files to the system because they might still exist on the system from a previous version. The installer detected that the required ports for OPSWAT Central Management are unavailable. The Windows system's Powershell version does not support the UNC file path format. |
| Troubleshooting | The installer stopped prematurely and showed the error message " Installation ended prematurely because of an error." |
| Solution | Delete all leftover files and folders in the installation folder of OPSWAT Central Management. It may require a Windows restart in some cases. |

**Cause 1: The installer could not copy some files to the system because they might still exist on the system from a previous version.** The installation wizard failed with the error " OPSWAT Central Management <version> Setup Wizard ended prematurely" as in the below screenshot.

A possible cause is that a previous uninstallation process failed to remove all files from the installation folder because some of these files were locked by still-running processes. The solution is to manually delete the installation folder (C:\Program Files\OPSWAT\Central by default) before reinstallation.

If Windows Explorer returns a "Folder in Use" or "Files in Use" error, this means that OPSWAT Central Management's services are still running in the background and locking these files. Please restart Windows and try again.

**Cause 2: The installer detected that the required ports for OPSWAT Central Management are unavailable.**

If prior to the error " OPSWAT Central Management <version> Setup Wizard ended prematurely" as shown above, the installer also display another error as shown below.

In this case, these ports are occupied by some background services. A possible cause is that these are OPSWAT Central Management's services which were not stopped correctly by the installer. Please restart Windows and try again. If these ports are still unavailable, please check if there are other services unrelated to OPSWAT Central Management occupying these ports,

**Cause 3: The Windows system's PowerShell version does not support UNC path.**

In PowerShell, test the system by using the command:

Get-ChildItem "\\?\C:\Program Files"

The command failed with an invalid path error because the path "C:\Program Files" is written in UNC format.

OPSWAT Central Management uses the UNC file path format during installation in order to bypass Windows's default 260-character limit for the file path. However, older versions of PowerShell do not properly support the UNC file path format. This problem most likely happens on older versions of Windows such as Windows Server 2012 R2.

As PowerShell updates are delivered as part of the broader Windows updates, please use Windows Update to update your Windows installation.
