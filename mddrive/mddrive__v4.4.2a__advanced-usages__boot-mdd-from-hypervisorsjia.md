<!-- source: https://www.opswat.com/docs/mddrive/v4.4.2a/advanced-usages/boot-mdd-from-hypervisorsjia -->

# Boot VMWare Workstation

The following is a demonstration of booting your device using a VMWare Workstation. Walkthrough videos are also available for VMWare Workstations 16 and VMWare Workstations 17.

Info

Some of the screenshots in the following example might look different, depending on the version you use.

1. To ensure your VMWare Workstation is ready to boot MetaDefender Drive, open the **Settings** of the virtual machine, and set the **Firmware type** to **UEFI**

2. Power On your VM by right-clicking and selecting **Power** → **Power On to Firmware**.

3. Connect the MetaDefender Drive to the virtual machine by right-clicking and selecting **Removable Devices** → **<the inserted MetaDefender Drive>** → **Connect (Disconnect from Host)**

4. Click **OK** when prompted to confirm inserting the MetaDefender Drive into the host virtual machine.

5. Select **Enter Setup** from **Boot Manager**

6. Select **Boot from a file**

7. Locate the MetaDefender Drive and select it

8. Select **<EFI>**

9. Select **<BOOT>**

10. Select **grubx64.efi**, then wait for your virtual machine to boot

.
