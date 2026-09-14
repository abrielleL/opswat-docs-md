<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/what-does-the-windows-update-offline-data-support -->

# What does the Windows Update Offline data support?

## [Overview](/docs/mdsdk/knowledge-base/what-does-the-windows-update-offline-data-support#overview)

Windows Update Offline data is a dataset provided by the MDES SDK and is represented through several files within the Analog package. For example:

- In the `server` folder, Windows Update Offline data is included in the `patch_system_aggregation` file.
- In the `client` folder, the Windows Update Offline data is represented by the `wuo.dat` file.

This dataset allows customers to flexibly query available Microsoft KBs in both the Internet and non-Internet environment, helping endpoints determine which Microsoft updates are required for patching.

Currently, Windows Update Offline data focuses on supporting Windows operating systems newer than Windows 7 and a set of modern, widely-used applications, as outlined in the following sections.

## [Supported Classification](/docs/mdsdk/knowledge-base/what-does-the-windows-update-offline-data-support#supported-classification)

| Classification | Supported |
| --- | --- |
| Critical Updates | ❌ |
| Definition Updates | ❌ |
| Driver Sets | ❌ |
| Drivers | ❌ |
| Feature Packs | ❌ |
| Security Updates | ✅ |
| Service Packs | ✅ |
| Tools | ❌ |
| Update Rollups | ✅ |
| Updates | ❌ |
| Upgrades | ❌ |

## [Supported Operating Systems & Applications](/docs/mdsdk/knowledge-base/what-does-the-windows-update-offline-data-support#supported-operating-systems--applications)

| Operating System/Application | Supported | Microsoft EOS |
| --- | --- | --- |
| Windows Server 2025 | ✅ | ❌ |
| Windows Server 2022 | ✅ | ❌ |
| Windows Server 2019 | ✅ | ❌ |
| Windows Server 2016 | ✅ | ❌ |
| Windows Server 2012 R2 | ✅ | ❌ |
| Windows Server 2012 | ✅ | ❌ |
| Windows Server 2008 R2 | ✅ | ✅ |
| Windows Server 2008 | ✅ | ✅ |
| Windows 11 | ✅ | ❌ |
| Windows 10 LTSB | ✅ | ❌ |
| Windows 10 | ✅ | ❌ |
| Windows 8.1 | ✅ | ✅ |
| Windows 8 | ✅ | ✅ |
| Windows 7 | ✅ | ✅ |
| .NET 6.0 | ✅ | ✅ |
| .NET 7.0 | ✅ | ✅ |
| .NET 8.0 | ✅ | ❌ |
| .NET 9.0 | ✅ | ❌ |
| Microsoft Exchange Server 2019 | ✅ | ❌ |
| Microsoft Exchange Server 2016 | ✅ | ❌ |
| Microsoft Exchange Server 2013 | ✅ | ✅ |
| Microsoft Exchange Server 2010 | ✅ | ✅ |
| Microsoft Exchange Server 2007 | ✅ | ✅ |
| Microsoft Exchange Server 2003 | ✅ | ✅ |
| Microsoft Exchange 2000 Server | ✅ | ✅ |
| Microsoft SQL Server Express 2019 | ✅ | ❌ |
| Microsoft SQL Server 2019 | ✅ | ❌ |
| Microsoft SQL Server Express 2017 | ✅ | ❌ |
| Microsoft SQL Server 2017 | ✅ | ❌ |
| Microsoft SQL Server Express 2016 | ✅ | ❌ |
| Microsoft SQL Server 2016 | ✅ | ❌ |
| Microsoft SQL Server Express 2014 | ✅ | ❌ |
| Microsoft SQL Server 2014 | ✅ | ❌ |
| Microsoft SQL Server Express 2012 | ✅ | ❌ |
| Microsoft SQL Server 2012 | ✅ | ❌ |
| Microsoft SQL Server | ✅ | ❌ |
| Microsoft SQL Server 2008 R2 | ✅ | ✅ |
| Microsoft SQL Server Express 2008 | ✅ | ✅ |
| Microsoft Visual Studio 2015 | ✅ | ❌ |
| Microsoft Visual Studio 2013 | ✅ | ✅ |
| Microsoft Visual Studio 2012 | ✅ | ✅ |
| Microsoft Office 2016 (MSI) | ✅ | ❌ |
| Microsoft Office 2013 (MSI) | ✅ | ✅ |
| Microsoft Office 2010 (MSI) | ✅ | ✅ |
| Microsoft Office 2007 (MSI) | ✅ | ✅ |
| Silverlight | ✅ | ✅ |
