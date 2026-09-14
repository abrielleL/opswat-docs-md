<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/how-do-i-check-the-version-of-a-kiosk-hardened-secure-image----i -->

# How do I check the version of a Kiosk Hardened/Secure Image “install.wim” file?

This article applies to all MetaDefender Kiosk Hardened/Secure Image releases deployed on Windows systems.

There are a few ways to check the version of an “install.wim” image, without having to deploy the image on a Kiosk hardware:

## [Solution 1:](/docs/mdkiosk/v4.8.5/knowledge-base/how-do-i-check-the-version-of-a-kiosk-hardened-secure-image----i#solution-1)

Calculating the hash of the “install.wim” image and comparing it to the published hash on [My OPSWAT](https://my.opswat.com/home/metadefender-kiosk)

PowershellCopy> Get-FileHash -Path .\install.wim -Algorithm SHA256
SHA256 4E4912AA809D6DBA50C3D5ADFFF58CFF70113375E08F099C1389C7BB14F03963

In this example, the hash of “install.wim” matches the hash for Kiosk Hardened Image 24.09 K3001.

## [Solution 2: For Secure Image only](/docs/mdkiosk/v4.8.5/knowledge-base/how-do-i-check-the-version-of-a-kiosk-hardened-secure-image----i#solution-2-for-secure-image-only)

Run the Get-WimInfo command to check the description of an “install.wim” image:

PowershellCopy> DISM /Get-WimInfo /WimFile:.\install.wim
Deployment Image Servicing and Management tool
Version: 10.0.26100.1150
Details for image : .\install.wim
Index : 1
Name : Kiosk Secure Image 4.7.1
Description : MD Core 5.11.1 | MD Kiosk 4.7.1 | Release Q4 2024
The operation completed successfully.
## [Solution 3: For Hardened Image 24.06.0 and later](/docs/mdkiosk/v4.8.5/knowledge-base/how-do-i-check-the-version-of-a-kiosk-hardened-secure-image----i#solution-3-for-hardened-image-24060-and-later)

Mount the “install.wim” image and check its registry directly.

- You can mount the image by using DISM GUI.
- Alternatively, mount the image with the following commands:

PowershellCopy> DISM /Mount-Wim /WimFile:<path_to_wim_file> /Index:<index_number> /MountDir:<mount_directory>Note:

Replace <*path_to_wim_file*> with the path to your .wim file, <*index_number*> with the index of the image you want to mount (e.g., 1 for "Windows 10 Kiosk Image"), and <*mount_directory*> with the directory where you want to mount the image.

Inspect the registry:

1. Open the registry editor.
2. Load the registry hive from the mounted image:

- Select HKEY_LOCAL_MACHINE.
- Go to File > Load Hive.
- Navigate to the mounted directory and open Windows\System32\Config\SYSTEM.
- Give it a temporary name (e.g., MountedSystem).

3. Find the hostname:

- Navigate to HKEY_LOCAL_MACHINE\MountedSystem\ControlSet001\Services\Tcpip\Parameters.
- Look for the Hostname and NV Hostname values.

In this example, the hostname of this “install.wim” is K3001-2409-0, so that is its Hardened Image version.

Unload the registry hive:

1. Select the loaded hive (e.g., MountedSystem).
2. Go to File > Unload Hive.

After this, unmount the “install.wim” image:

- Unmount from the DISM GUI (if you mounted it using this method).
- Or, with the following command:

PowershellCopy> DISM /Unmount-Wim /MountDir:<mount_directory> /DiscardSupport:

If you have followed the instructions above but are still unable determine the version of the “install.wim” image for Kiosk Hardened/Secure Image, please follow these instructions on [How To Create a Support Package](https://www.opswat.com/docs/mdkiosk/troubleshooting), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
