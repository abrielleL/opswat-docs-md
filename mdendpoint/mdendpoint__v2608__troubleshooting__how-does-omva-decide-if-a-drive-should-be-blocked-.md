<!-- source: https://www.opswat.com/docs/mdendpoint/v2608/troubleshooting/how-does-omva-decide-if-a-drive-should-be-blocked- -->

# How does OMVA decide if a drive should be blocked?

> **Check Your Version:**
>
> This article applies to the Opswat Media Validation Agent

## OMVA drive detection

- During **initial installation** or **after a system reboot**, OMVA checks all drives connected to the machine to determine whether a device is internal or external by looking at its **bus type**.
- If a drive is considered **external**, OMVA will block it and attempt to validate its manifest before unblocking.
- After this initial check, OMVA will continue monitoring **plug events** to block and validate any new devices that are connected.

## Allowed Bus Types

OMVA will **not block** devices if their bus type matches one of the following:

- `BusTypeScsi`
- `BusTypeAtapi`
- `BusTypeAta`
- `BusTypeSsa`
- `BusTypeRAID`
- `BusTypeSata`
- `BusTypeVirtual`
- `BusTypeFileBackedVirtual`
- `BusTypeNvme`
- `BusTypeiScsi`

## How to Check the Bus Type of Your Drive

You can verify the bus type of your drive using the following commands:

**PowerShell:**

```powershell
Get-WmiObject -Namespace root\microsoft\windows\storage -Class MSFT_PhysicalDisk |
Select-Object DeviceId, FriendlyName, MediaType, BusType
```

![](https://uploads.developerhub.io/prod/2x2P/v4bm8ihxle8z8zbg9e7dpkki7m5k4fbbpigyuxsh7xxk0v4hk25knmr90qke05w7.png)

**Command Prompt:**

```c
wmic diskdrive get Caption, DeviceID, InterfaceType, MediaType
```

![](https://uploads.developerhub.io/prod/2x2P/pkbjdh8veql5s4ckgxu2xgz9w03qwf9s3v8vngeey7lw9fplzmyddx1vmt8la7r8.png)

These commands will show the **BusType** and **MediaType** associated with your device.

## Common Bus Types Reference

| ID | Constant Name | Bus / Device Type |
| ---- | ---- | ---- |
| 0 | BusTypeUnknown | Unknown / not reported |
| 1 | BusTypeScsi | SCSI (Small Computer System Interface) |
| 2 | BusTypeAtapi | ATAPI (IDE devices like CD/DVD drives) |
| 3 | BusTypeAta | ATA (IDE/PATA hard drives) |
| 4 | BusType1394 | IEEE 1394 / FireWire |
| 5 | BusTypeSsa | Serial Storage Architecture (legacy) |
| 6 | BusTypeFibre | Fibre Channel (FC storage) |
| 7 | BusTypeUsb | USB (flash drives, external HDDs, etc.) |
| 8 | BusTypeRAID | RAID (logical device via RAID controller) |
| 9 | BusTypeiScsi | iSCSI (storage over IP network) |
| 10 | BusTypeSas | SAS (Serial Attached SCSI) |
| 11 | BusTypeSata | SATA (common HDDs/SSDs) |
| 12 | BusTypeSd | Secure Digital (SD cards) |
| 13 | BusTypeMmc | MultiMediaCard |
| 14 | BusTypeVirtual | Virtual disk (VMs, Hyper-V, etc.) |
| 15 | BusTypeFileBackedVirtual | File-backed virtual storage |
| 16 | BusTypeSpaces | Storage Spaces (Windows logical pools) |
| 17 | BusTypeNvme | NVMe (PCIe SSDs) |
| 18 | BusTypeSCM | Storage Class Memory (NVDIMM, Optane) |
| 19 | BusTypeUfs | UFS (Universal Flash Storage, common in smartphones) |
| 20 | BusTypeMax | Upper bound marker (not a device) |
| 127 | BusTypeMaxReserved | Reserved (not a device, upper range cap) |

> **Support:**
>
> If **Further Assistance** is required, please proceed to log a [**support case or chat with one of our support engineers**](https://my.opswat.com/support).

---

[All pages in this documentation](https://www.opswat.com/docs/mdendpoint/llms.txt)
