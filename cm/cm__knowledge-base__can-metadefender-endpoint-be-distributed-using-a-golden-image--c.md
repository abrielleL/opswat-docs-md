<!-- source: https://www.opswat.com/docs/cm/knowledge-base/can-metadefender-endpoint-be-distributed-using-a-golden-image--c -->

# Can MetaDefender Endpoint be distributed using a golden image, cloned VMs or AMIs?

> **Check Your Product:**
>
> This article applies to all MetaDefender Endpoint releases deployed on Windows, Linux, macOS, iOS and Android systems.

> **Pro Tip:**
>
> A golden image is a pre-configured template or archetype  for a virtual machine that can be applied to servers, hard drives and desktops.
>
> The object is to allow administrators to deploy several remote desktops, remote applications and virtual machines based on a single master image.

Yes.

The MetaDefender Endpoint can be distributed using a golden system image, but an additional step must be taken to avoid issues with devices reporting to My OPSWAT Central Management servers.

Whenever the MetaDefender Endpoint starts, it looks at the registry or file system to determine whether an MetaDefender Endpoint unique device ID already exists.

1. Should the Client find one, it will use this to report to the My OPSWAT Central Management  servers.

If multiple managed devices report to the My OPSWAT Central Management  servers using the same device ID, these reports will overwrite each other based on which report was issued most recently.

2. Alternatively, if no device ID is found, the MetaDefender Endpoint will simply generate a new one.

To facilitate the second outcome above, when creating a golden image on **Windows** systems, the device ID must be removed either from the source image or from the new devices (i.e, before or after cloning).

On **Linux** systems, a unique solution is available that allows the golden image to be created before the device ID is assigned.

On **Android**, **iOS** and **macOS**, no action is needed, as a new device ID is generated automatically for each device.

## Preparing an image for Windows systems

### Option 1 (preferred): removing the device ID before cloning

1. Install the MetaDefender Endpoint on your source device.
2. Stop MetaDefender Endpoint service/s on the source device, following the recommended process for your OS.
3. (Optional) Delete the source device via the **My OPSWAT Central Management Console**.
4. Image the source device.
5. Create new device/s from the source image.
6. Start the new device/s.

### Option 2: removing the device ID after cloning

1. Install the MetaDefender Endpoint on your source device.
2. Stop MetaDefender Endpoint service/s on the source device, following the recommended process for your OS.
3. Image the source device.
4. Create new device/s from the source image.
5. Start the new device/s.

## Device ID removal instructions for Windows systems

### Automatically

1. Download the **Remove Gears UID .exe** utility [here.](https://kb-hosting-cs.s3.amazonaws.com/KB/MA/OPSWATClient/Remove_Gears_UID.exe)
2. Run the ***exe***.

### Manually

#### **Windows 32-bit**

1. Open a command prompt as administrator and run: **sc stop opswatgearshelper**
2. Also in the prompt, enter: **sc stop waondemand**

Next, you must delete the device ID from the registry as follows:

3. Open Regedit.
4. Browse to  **\HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\Gears Client\Config**.
5. Open the key named **uuid** and delete the value.
6. Finally, open the key named **HWID** and delete the value.

#### **Windows 64-bit**

1. Open a command prompt as administrator and run: **sc stop opswatgearshelper**
2. Also in the prompt, enter: **sc stop waondemand**

Next, you must delete the device ID from the registry as follows:

3. Open Regedit.
4. Browse to  **\HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\OPSWAT\Gears Client\Config.**
5. Open the key named **uuid** and delete the value.
6. Finally, open the key named **HWID** and delete the value.

> **Support:**
>
> If you have followed the instructions above but are having **Issues Distributing The MetaDefender Endpoint Via A Golden System Image**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form.
