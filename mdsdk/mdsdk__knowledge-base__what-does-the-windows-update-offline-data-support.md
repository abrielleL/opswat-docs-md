<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/what-does-the-windows-update-offline-data-support -->

# What does the Windows Update Offline data support?

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Overview](/docs/mdsdk/knowledge-base/what-does-the-windows-update-offline-data-support#overview)

Windows Update Offline data is a dataset provided by the MDES SDK and is represented through several files within the Analog package. For example:

- In the `server` folder, `patch_system_aggregation.json` holds every supported KB, including security, non-security, and out-of-band updates, with download links and hashes for offline distribution.
- In the `client` folder, `wuo.dat` contains security updates only, while `wuov2.dat` (with a delta variant, `wuov2_delta.dat`) contains both security and non-security updates, including out-of-band releases. Use `wuov2.dat` when you need non-security coverage.

This dataset lets customers query, download, and install Microsoft KBs in both Internet and offline environments. It covers security and non-security updates, including out-of-band releases, so an endpoint can stay fully up to date through Windows Update Offline even when the Windows Update service is disabled.

Currently, Windows Update Offline data focuses on supporting Windows operating systems newer than Windows 7 and a set of modern, widely-used applications, as outlined in the following sections.

## [Supported Classification](/docs/mdsdk/knowledge-base/what-does-the-windows-update-offline-data-support#supported-classification)

`wuo.dat` covers Security Updates, Service Packs, and Update Rollups. `wuov2.dat` covers those same security classifications plus Critical Updates and Updates (non-security and out-of-band). `patch_system_aggregation.json` carries all supported classifications. Preview KBs are not supported, and non-security updates generally carry no CVE data.

| Classification | Supported |
| --- | --- |
| Critical Updates | ✅ |
| Definition Updates | ❌ |
| Driver Sets | ❌ |
| Drivers | ❌ |
| Feature Packs | ❌ |
| Security Updates | ✅ |
| Service Packs | ✅ |
| Tools | ❌ |
| Update Rollups | ✅ |
| Updates | ✅ |
| Upgrades | ❌ |

## [Supported Operating Systems & Applications](/docs/mdsdk/knowledge-base/what-does-the-windows-update-offline-data-support#supported-operating-systems--applications)

| Signature ID | Operating System/Application | Supported | Microsoft EOS |
| --- | --- | --- | --- |
| 1103 | Windows Server 2025 | ✅ | ❌ |
| 1103 | Windows Server 2022 | ✅ | ❌ |
| 1103 | Windows Server 2019 | ✅ | ❌ |
| 1103 | Windows Server 2016 | ✅ | ❌ |
| 1103 | Windows Server 2012 R2 | ✅ | ❌ |
| 1103 | Windows Server 2012 | ✅ | ❌ |
| 1103 | Windows Server 2008 R2 | ✅ | ✅ |
| 1103 | Windows Server 2008 | ✅ | ✅ |
| 1103 | Windows 11 | ✅ | ❌ |
| 1103 | Windows 10 LTSB | ✅ | ❌ |
| 1103 | Windows 10 | ✅ | ❌ |
| 1103 | Windows 8.1 | ✅ | ✅ |
| 1103 | Windows 8 | ✅ | ✅ |
| 1103 | Windows 7 | ✅ | ✅ |
|  | .NET 6.0 | ✅ | ✅ |
|  | .NET 7.0 | ✅ | ✅ |
|  | .NET 8.0 | ✅ | ❌ |
|  | .NET 9.0 | ✅ | ❌ |
| 3405 | Microsoft Exchange Server 2019 | ✅ | ❌ |
| 3405 | Microsoft Exchange Server 2016 | ✅ | ❌ |
| 3405 | Microsoft Exchange Server 2013 | ✅ | ✅ |
| 3405 | Microsoft Exchange Server 2010 | ✅ | ✅ |
| 3405 | Microsoft Exchange Server 2007 | ✅ | ✅ |
| 3405 | Microsoft Exchange Server 2003 | ✅ | ✅ |
| 3405 | Microsoft Exchange 2000 Server | ✅ | ✅ |
| 4069 | Microsoft SQL Server 2022 | ✅ | ❌ |
| 3377 | Microsoft SQL Server Express 2019 | ✅ | ❌ |
| 3427 | Microsoft SQL Server 2019 | ✅ | ❌ |
| 3378 | Microsoft SQL Server Express 2017 | ✅ | ❌ |
| 3436 | Microsoft SQL Server 2017 | ✅ | ❌ |
| 3430 | Microsoft SQL Server Express 2016 | ✅ | ❌ |
| 3386 | Microsoft SQL Server 2016 | ✅ | ❌ |
| 3376 | Microsoft SQL Server Express 2014 | ✅ | ❌ |
| 1704 | Microsoft SQL Server 2014 | ✅ | ❌ |
| 3375 | Microsoft SQL Server Express 2012 | ✅ | ❌ |
| 1825 | Microsoft SQL Server 2012 | ✅ | ❌ |
| 1731 | Microsoft SQL Server | ✅ | ❌ |
| 3398 | Microsoft SQL Server 2008 R2 | ✅ | ✅ |
| 3374 | Microsoft SQL Server Express 2008 | ✅ | ✅ |
| 3159 | Microsoft Visual Studio 2015 | ✅ | ❌ |
| 3158 | Microsoft Visual Studio 2013 | ✅ | ✅ |
| 3137 | Microsoft Visual Studio 2012 | ✅ | ✅ |
| 3243 | Microsoft Office 2016 (MSI) | ✅ | ❌ |
| 3247 | Microsoft Office 2013 (MSI) | ✅ | ✅ |
| 3245 | Microsoft Office 2010 (MSI) | ✅ | ✅ |
| 3363 | Microsoft Office 2007 (MSI) | ✅ | ✅ |
| 179 | Silverlight | ✅ | ✅ |
| 4063 | Microsoft Sharepoint Server Subscription Edition | ✅ | ❌ |
| 4064 | Microsoft Sharepoint Server 2019 | ✅ | ❌ |
| 4065 | Microsoft Sharepoint Server 2016 | ✅ | ❌ |

Support

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
