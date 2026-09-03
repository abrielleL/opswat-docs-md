<!-- source: https://www.opswat.com/docs/myop/release-notes/what-new -->

# What's New

OPSWAT Central Management v.7 and My OPSWAT On-Premises (My OPSWAT Central Management v.8) will reach End of Sale on July 31, 2025, and End of Life on January 31, 2027. We encourage you to upgrade to My OPSWAT Central Management v.10 before January 31, 2027, to ensure continued support and access to the latest features.

More details can be found [here](/docs/myop/knowledge-base/end-of-sale-and-end-of-life-cm7-and-cm8).

| Version: 2025.4.1-OP  Release date: Nov 26, 2025, UTC | My OPSWAT On-premises enables customers to deploy a self-managed My OPSWAT server in an air-gapped environment to manage OPSWAT products remotely, improve data flows visibility, and provide better reports for each product, solution and account. |
| --- | --- |
| **Product Management** | Version: 2025.4.1  Detailed release notes can be found [here](https://www.opswat.com/docs/product-management/v2025.4.1/get-started/user-guide). |
| **New Feature** |  |
| History data migration to CMv10 | Administrators can now enable migration of MDCore scan history and Kiosk session scan data from My OPSWAT Central Management v8 to Central Management v10. |
| **Known Limitations** |  |
| [Import/Export](/docs/myop/configuration/import-export) | There's a 10 GB size limit when importing data.  **Workaround**: Please make sure that during export, the size of the exported .zip file is less than 10 GB to allow a successful import. |
| Upgrading via the [Upgrade My OPSWAT](/docs/myop/deployment/upgrade) function does not update the new system requirements for the virtual appliance. | Due to how the upgrade mechanism functions, the new system requirements cannot be applied retroactively to the virtual appliance.  **Workaround:** Please note that you can still manually adjust the CPU and Memory resource assigned to the virtual appliance on the hypervisor.  For disk storage, please refer to the KB [How to increase the disk storage for the My OPSWAT On-premises virtual appliance?](/docs/myop/knowledge-base/kb-virtual-appliance-extend-disk-storage) |
