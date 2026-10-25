<!-- source: https://www.opswat.com/docs/mddrive/v4.4.10/knowledge-base/can-metadefender-drive-scan-vm--virtual-machine--files-without-b -->

# Can MetaDefender Drive Scan VM (Virtual Machine) Files Without Booting the Guest OS?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**Check Your Version:** This article applies to all MetaDefender Drive releases

Yes. It is possible to scan VM (Virtual Machine) files with MetaDefender Drive without attaching the drive to a VM and booting the guest operating system so the engine can access the partitions inside the VM.

There are two options:

**Option 1: Scan the virtual disk files directly (no boot required)**

MetaDefender Drive's archive extraction engine treats virtual disk formats as archives. If the VM files (VMDK, VHD, VDI) are located on a disk that MetaDefender Drive is scanning, the engine can open them and scan the files inside the guest partitions.

**Warning:** VDI, VHD, and VMDK are supported archive formats, but this method is not recommended when scanning from the MetaDefender Drive USB itself. Extracting large virtual disks requires temporary storage space that the Drive may not have, depending on the size of the virtual disk.

**Option 2: Boot MetaDefender Drive inside the hypervisor**

This method does not boot the guest OS. Instead:

1. Attach MetaDefender Drive to the VM in VMware Workstation or QEMU
2. Power the VM on to firmware
3. Boot the VM from the Drive's grubx64.efi

MetaDefender Drive's own OS then sees the VM's virtual disks as raw block devices and scans their partitions natively with no size limitation and no risk of executing anything from the guest.

**Support:** If you have questions, concerns or want to report issues regarding **MetaDefender** **Drive**, please open a [Support Case](https://my.opswat.com/support-services) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s/).
