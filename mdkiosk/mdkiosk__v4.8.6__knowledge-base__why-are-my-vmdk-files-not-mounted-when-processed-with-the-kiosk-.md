<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/why-are-my-vmdk-files-not-mounted-when-processed-with-the-kiosk- -->

# Why Are My VMDK Files Not Mounted When Processed with the Kiosk?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Kiosk V4 releases deployed on Windows systems.

### [**Overview**](/docs/mdkiosk/v4.8.6/knowledge-base/why-are-my-vmdk-files-not-mounted-when-processed-with-the-kiosk-#overview)

You may encounter an issue where your Virtual Machine Disk (VMDK) files are **not being mounted** for processing on the Kiosk, even when all prerequisites, including optional utilities like Paragon Drivers, are correctly installed.

This article outlines the root cause and steps to resolve this issue.

---

### [**Root Cause**](/docs/mdkiosk/v4.8.6/knowledge-base/why-are-my-vmdk-files-not-mounted-when-processed-with-the-kiosk-#root-cause)

For VMDK images, **Kiosk uses the VMware Virtual Storage Volume Driver (vstor2)** to mount the disk. This driver is typically installed during the Kiosk setup process. However, in some cases, the driver may be missing or corrupted

---

### [**Symptoms**](/docs/mdkiosk/v4.8.6/knowledge-base/why-are-my-vmdk-files-not-mounted-when-processed-with-the-kiosk-#symptoms)

You may see log entries similar to the following:

HtmlCopy[5820] [INFO] [Jul 14, 10:51:16:446] VMDK.cpp#64 VMDK::Mount(): {E41667DD-57FB-4B05-B40B-5BF39D88A5F9} Failed to mount: E:\ClientVM-Win11-Temp.vmdk - Volume mount failure: Driver not found

---

**Diagnosis Steps**

1. **Verify Driver Presence**

   Check whether the `vstor2` driver exists at the following path `C:\Windows\System32\drivers\vstor2-x64.sys`. If the file **does not exist**, the driver is not installed.
2. **Review Logs**

   Review the Kiosk logs for messages indicating a **"Volume mount failure"** or **"Driver not found"** as shown above.

---

**Resolution**

If the driver is missing or corrupted, you can manually install it by following these steps:

1. Open a **Command Prompt** as **Administrator**.
2. Run the following installation script `C:\ProgramData\OPSWAT\Metadefender\VDDK\vstor2install.bat`

This script reinstalls the vstor2 driver required for VMDK mounting.

---

**Post-Installation**

After running the script:

- Restart the Kiosk service or reboot the system.
- Retry the VMDK file mounting to confirm successful installation.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chat with one of our support engineers**](https://my.opswat.com/support).

###
