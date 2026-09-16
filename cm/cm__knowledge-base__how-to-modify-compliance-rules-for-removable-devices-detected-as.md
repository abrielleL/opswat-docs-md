<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-to-modify-compliance-rules-for-removable-devices-detected-as -->

# How to Modify Compliance Rules for Removable Devices Detected as Internal Local Disk in My OPSWAT Central Management?

> **Info: **This article applies to all My OPSWAT Central Management versions.

## **Overview**

In some cases, Windows may classify removable drives (e.g., USB drives) as Local Disk, which can affect how My OPSWAT Central Management applies compliance rules. OPSWAT does not control this classification — it is determined by the Windows operating system.

![](https://uploads.developerhub.io/prod/97qW/7qmtou3fyamp6swpa9hya5yovszc83khb4ppnmopthboo5waw8928mvqm0dfne6p.png)

Windows Explorer may label both internal and external drives as “Local Disk,” but the OS provides additional metadata that distinguishes between them. My OPSWAT Central Management retrieves this information from the OS registry to evaluate compliance policies.

![](https://uploads.developerhub.io/prod/97qW/8xxfhtomq8tg78ej3whtt5lds4akt98978hetjfvuvt3qqwv0ms94wlh8301kopz.png)

This article explains how Windows identifies drives and how to configure compliance policies in My OPSWAT Central Management to properly handle removable devices detected as local disks.

## **How Windows Identifies Drives**

### **Internal Disks (SATA/SCSI/NVMe):**

- Reported with Bus Number, Target ID, and LUN in Device Manager.
- Exposed under WMI class Win32_DiskDrive with interface type SCSI/SATA.

### **External USB Disks:**

- Reported as USB Mass Storage Device in Device Manager.
- Exposed under WMI class Win32_DiskDrive with interface type USB.

#### **Example**

- Netac WH51 → Detected as USB Mass Storage Device (external).
- ADATA ED600 → Detected with SCSI parameters (Bus/Target/LUN), consistent with internal enumeration.

## **Steps to Configure: Adjusting Compliance Rules in My OPSWAT Central Management**

Since MetaDefender Endpoint relies on the OS classification, the compliance behavior must be tuned through policy configuration.

1. **Modify Encryption Compliance Behavior:** Go to Deep Compliance > Encryption > Treat as Warning these Conditions. Configure the policy so that:
   1. Devices marked as compliant → Treated as non-critical.
   2. Devices marked as non-compliant → Treated as critical.

![](https://uploads.developerhub.io/prod/97qW/ijhbuz7ohar4pqkq0bqs10cnqw3gy3h7s7nzb6kjspzclje7s8uu1rcynvwusxb8.png)

2. **Configure Device Rules** : Navigate to **Rules** → Adjust rules to better handle devices that are misclassified.

![](https://uploads.developerhub.io/prod/97qW/ff5239nifsuwl9bhwn97qqtuo62x4ca9y888vnls9haclx9zv4nsk4l39xcjzi4s.png)

3. Go to **Advanced Endpoint Protection > Enable Threat Detection for Windows > Removable Media Protection > Allow list** → Add device details such as:
   1. **Vendor**
   2. **Product ID**
   3. **Device Instance Path**

This ensures that specific removable devices are permitted even if detected as local disks.

![](https://uploads.developerhub.io/prod/97qW/ngwuu5zpl7cqkmd3ndkkt79espr5em8ojkiluurr8q7bgfuapdv0shlndxojnu7m.png)

To claim the device info, you can simply retrieve it in MetaDefender Endpoint

![](https://uploads.developerhub.io/prod/97qW/w19b6sfnxepw6rzy7nk7oo2txoef1rl5vxw7qsmw4fmxqenckc5nw2g9akicd83s.png)

## **Verify the Change**

After applying these configurations, the removable device will be accessible and treated as compliant within My OPSWAT Central Management, even if Windows classifies it as a local disk.

> **Support:**
>
> If you require further assistance, please follow these instructions on [How to Create Support Package?](https://www.opswat.com/docs/mdcore/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/support).
