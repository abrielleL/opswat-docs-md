<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/broadcom-changes-affect-patching-support-for-VMware-products -->

# How do recent Broadcom changes affect manual and auto-patching support for VMware products?

## [Summary](/docs/mdsdk/knowledge-base/broadcom-changes-affect-patching-support-for-VMware-products#summary)

Broadcom has implemented significant changes to the download and installation flow for VMware Workstation products. These updates impact both VMware Workstation Player and Workstation Pro.

- **Workstation Player <=16** is no longer maintained, and its download link has been removed. SDK can no longer support manual or auto-patching for this version.
- **Workstation Player 17+** is bundled with Workstation Pro and is no longer available as a standalone product. Only detection and vulnerability assessment (VA) are supported.
- **Workstation Pro (all versions)** continues to be fully supported.

### [Support matrix](/docs/mdsdk/knowledge-base/broadcom-changes-affect-patching-support-for-VMware-products#support-matrix)

| Product version | Detection | Vulnerability Assessment | Manual Patching | Auto-patching |
| --- | --- | --- | --- | --- |
| VMWare Workstation Player <=15 | Support | Support | Not support | Not support |
| VMware Workstation Player 16 | Support | Support | Not support | Not support |
| VMware Workstation Player >=17 | Support | Support | Not support | Not support |
| VMware Workstation Pro (all versions) | Support | Support | Support | Support |

### [Recommendation](/docs/mdsdk/knowledge-base/broadcom-changes-affect-patching-support-for-VMware-products#recommendation)

- Customers using VMware Workstation Player <=16 should manually migrate to VMware Workstation Pro 17+ or use the SDK to patch the current VMware Workstation Pro to version 17+.

## [Key Changes from Broadcom](/docs/mdsdk/knowledge-base/broadcom-changes-affect-patching-support-for-VMware-products#key-changes-from-broadcom)

### [1. New Download Flow](/docs/mdsdk/knowledge-base/broadcom-changes-affect-patching-support-for-VMware-products#1-new-download-flow)

Broadcom no longer supports the traditional binary download method. Instead, a new centralized download site with a verification layer has been introduced.

Reference: [Broadcom Announcement: Changes to How You Download VMware Software Binaries](https://blogs.vmware.com/cloud-foundation/2025/03/24/download-changes-vmware-software-binaries/)

### [2. Product Consolidation and Licensing](/docs/mdsdk/knowledge-base/broadcom-changes-affect-patching-support-for-VMware-products#2-product-consolidation-and-licensing)

- Currently, VMWare Workstation Pro is free for personal use, which leads to the discontinuation of their lesser counterparts VMware Workstation Player and VMware Fusion Player.
- The Workstation Player is now bundled with Workstation Pro. When users install or update Workstation Pro, the Player version is automatically included and updated.

Related Articles:

[Open a Virtual Machine in VMware Workstation Player](https://techdocs.broadcom.com/us/en/vmware-cis/desktop-hypervisors/workstation-pro/17-0/using-vmware-workstation-pro/configuring-and-managing-virtual-machines/moving-virtual-machines/open-a-virtual-machine-in-vmware-player.html)

[VMware Workstation Pro: Now Free for Personal Use](https://blogs.vmware.com/workstation/2024/05/vmware-workstation-pro-now-available-free-for-personal-use.html)

### [3. Broadcom's Update on Workstation Player Support (Updated in Nov 2025)](/docs/mdsdk/knowledge-base/broadcom-changes-affect-patching-support-for-VMware-products#3-broadcoms-update-on-workstation-player-support-updated-in-nov-2025)

- Broadcom no longer maintains or distributes VMware Workstation Player as a standalone product for version 16 and above.
- The download link for Workstation Player version 16 has been removed, and version 17+ is only available as part of Workstation Pro.
- As a result, SDK patching support for Workstation Player version 16 has been discontinued.

## [Impact on Product Support (Updated in Nov 2025)](/docs/mdsdk/knowledge-base/broadcom-changes-affect-patching-support-for-VMware-products#impact-on-product-support-updated-in-nov-2025)

- **VMware Workstation Player <=16:** Detection and VA supported. Manual and auto-patching no longer supported due to the removal of the download link.
- **VMware Workstation Player >=17:** Detection and VA supported. Manual and auto-patching not supported.
- **VMware Workstation Pro (all versions):** Fully supported for Detection, VA, manual patching, and auto-patching.
- *Note: The VMWare Workstation Player >=17 will be updated along with VMWare Workstation Pro, when users install/patch VMWare Workstation Pro on their endpoints.*

**Revised recommendation:**

- Customers using VMware Workstation Player <=16 should manually migrate to VMware Workstation Pro 17+ or use the SDK to patch the current VMware Workstation Pro to version 17+.
- VMware Workstation Pro remains the recommended path forward for continued patching and support.
