<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/november-04-2026 -->

# November 4th, 2026

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
## [Release Note](/docs/mdsdk/release-notes/november-04-2026#release-note)

### [Release Date](/docs/mdsdk/release-notes/november-04-2026#release-date)

- 04/11/2026

### [SDK Version](/docs/mdsdk/release-notes/november-04-2026#sdk-version)

- **Windows**: 4.3.6830.0

### [Enhancement](/docs/mdsdk/release-notes/november-04-2026#enhancement)

#### [Windows](/docs/mdsdk/release-notes/november-04-2026#windows)

- N/A

### [Bug Fix](/docs/mdsdk/release-notes/november-04-2026#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/november-04-2026#windows)

- Resolved false positive CVE reports for Windows 11 by excluding feature-upgrade offers from the missing patches list in GetProductVulnerability, improving vulnerability assessment accuracy for devices offered OS upgrades.
- Resolved the issue where GetProductVulnerability returned superseded remediation KBs by ensuring a full Windows Update scan is performed when skip_extra_installed_os_patches_checks is enabled, improving the accuracy of automated remediation.
- Fixed an issue where a host application running under Microsoft Application Verifier could stop with a memory leak error (Application Verifier stop 0x900, exception 0x80000003) in libwautils.dll, libwaapi.dll or AppRemover_API.dll when unloading OPSWAT App Remover. App Remover now frees this memory before its libraries unload, including when a product or exclusion list is freed after DestroyAppRemoverCore.
- Resolved the issue where the Windows patch engine could recursively delete files from the drive root during update installations via a new safeguard that prevents cleanup on empty folder paths, improving system stability and data integrity.
- Fixed an issue where a host application could stop unexpectedly with a heap-corruption error (0xC0000374) in libwautils.dll after wa_api_teardown had returned. wa_api_teardown now returns only after Windows has released all SDK objects used for system event notifications.
- [public] Fixed the issue where ESET Endpoint Security 13.1 was not detected in the firewall category.

### [New Application Support](/docs/mdsdk/release-notes/november-04-2026#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/november-04-2026#windows)

- Add automatic patching support for Sysmon on Windows

### [New Application Version Support](/docs/mdsdk/release-notes/november-04-2026#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/november-04-2026#windows)

- V4 | Windows | Add support for Cisco Secure Endpoint version 8.6.4
- V4 | Windows | Add support for Acronis Cyber Protection Agent version 26.10
- Add automatic patching support for Sysmon on Windows
- V4 | Windows | Add support for Check Point Endpoint Security version 89.30.0151
- V4 | Windows | Add support for Trend Micro Deep Security Agent version 20.0.33161
- V4 | Windows | Add support for Sentinel Agent version 26.2.3.158
- V4 | Windows | Add support for Bitdefender Antivirus Plus version 27.0.64.366
- Windows | IsDefaultBrowser on Firefox arm64 return false when the product is set as default browser
- V4 | Windows | Add support for Malwarebytes Anti-Malware version 5.7.3.376
- V4 | Windows | Add support for Transmission version 4.1.4

### [New Method Implementation](/docs/mdsdk/release-notes/november-04-2026#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/november-04-2026#windows)

- [Microsoft .NET Runtime 10.0] Microsoft Corporation - Update GetVersion implementation for Microsoft .NET Runtime 10.0 (x86)
- [Microsoft .NET Runtime 10.0] Microsoft Corporation - Update GetVersion implementation for Microsoft .NET Runtime 10.0 (x64)
- [Anaconda3] Anaconda, Inc. - Update GetVersion implementation for Anaconda (User)
- [Mozilla Firefox] Mozilla Corporation - Update GetAntiphishingState implementation for Mozilla Firefox (arm64)
- [Mozilla Firefox] Mozilla Corporation - Update SetAntiphishingState implementation for Mozilla Firefox (arm64)
- [Mozilla Firefox] Mozilla Corporation - Update IsDefaultBrowser implementation for Mozilla Firefox (arm64)
- [Mozilla Firefox] Mozilla Corporation - Implement GetPlugins for Mozilla Firefox (arm64)
- [Mozilla Firefox] Mozilla Corporation - Update GetAntiphishingState implementation for Mozilla Firefox (x64)
- [Mozilla Firefox] Mozilla Corporation - Update SetAntiphishingState implementation for Mozilla Firefox (x64)
- [Mozilla Firefox] Mozilla Corporation - Update IsDefaultBrowser implementation for Mozilla Firefox (x64)
- [Mozilla Firefox] Mozilla Corporation - Update GetPlugins implementation for Mozilla Firefox (x64)
- [Mozilla Firefox] Mozilla Corporation - Update GetPlugins implementation for Mozilla Firefox (x86)
- [Mozilla Firefox] Mozilla Corporation - Update IsDefaultBrowser implementation for Mozilla Firefox (x86)
- [Mozilla Firefox] Mozilla Corporation - Update SetAntiphishingState implementation for Mozilla Firefox (x86)
- [Mozilla Firefox] Mozilla Corporation - Update GetAntiphishingState implementation for Mozilla Firefox (x86)
- [NeeView] NeeLaboratory - Implement GetVersion for NeeView
- [Mozilla Firefox] Mozilla Corporation - Implement GetPlugins for Mozilla Firefox (User) (x86)
- [Mozilla Firefox] Mozilla Corporation - Implement IsDefaultBrowser for Mozilla Firefox (User) (x86)
- [Mozilla Firefox] Mozilla Corporation - Implement SetAntiphishingState for Mozilla Firefox (User) (x86)
- [Mozilla Firefox] Mozilla Corporation - Implement GetAntiphishingState for Mozilla Firefox (User) (x86)
- [Mozilla Firefox] Mozilla Corporation - Implement GetPlugins for Mozilla Firefox (User) (x64)
- [Mozilla Firefox] Mozilla Corporation - Implement IsDefaultBrowser for Mozilla Firefox (User) (x64)
- [Mozilla Firefox] Mozilla Corporation - Implement SetAntiphishingState for Mozilla Firefox (User) (x64)
- [Mozilla Firefox] Mozilla Corporation - Implement GetAntiphishingState for Mozilla Firefox (User) (x64)
- [Mozilla Firefox] Mozilla Corporation - Implement GetAntiphishingState for Mozilla Firefox (User) (arm64)
- [Mozilla Firefox] Mozilla Corporation - Implement SetAntiphishingState for Mozilla Firefox (User) (arm64)
- [Mozilla Firefox] Mozilla Corporation - Implement IsDefaultBrowser for Mozilla Firefox (User) (arm64)
- [Mozilla Firefox] Mozilla Corporation - Implement GetPlugins for Mozilla Firefox (User) (arm64)
- [Mogan STEM] XmacsLabs - Implement GetRunningState for Mogan STEM
- [Sysmon] Sysinternals - Update GetVersion implementation for Sysmon
- [Sysmon] Sysinternals - Implement GetVersion for Sysmon
- [Mozilla Firefox] Mozilla Corporation - Update GetVersion implementation for Mozilla Firefox (arm64)
- [Mozilla Firefox] Mozilla Corporation - Update TerminateProcesses implementation for Mozilla Firefox (arm64)
- [Mozilla Firefox] Mozilla Corporation - Update Run implementation for Mozilla Firefox (arm64)
- [Mozilla Firefox] Mozilla Corporation - Update GetRunningState implementation for Mozilla Firefox (arm64)
- [Mozilla Firefox] Mozilla Corporation - Update GetInstallationDirectories implementation for Mozilla Firefox (arm64)
- [Mozilla Firefox] Mozilla Corporation - Implement GetComponents for Mozilla Firefox (arm64)
- [Mozilla Firefox] Mozilla Corporation - Update GetUninstallString implementation for Mozilla Firefox (arm64)
- [Mozilla Firefox] Mozilla Corporation - Update IsAuthentic implementation for Mozilla Firefox (arm64)
- [Mozilla Firefox] Mozilla Corporation - Update GetUninstallHive implementation for Mozilla Firefox (arm64)
- [TeamViewer Host] TeamViewer GmbH - Update TerminateProcesses implementation for TeamViewer Host 15 msi
- [Mozilla Firefox] Mozilla Corporation - Update GetVersion implementation for Mozilla Firefox (User) (arm64)
- [Mozilla Firefox] Mozilla Corporation - Update GetVersion implementation for Mozilla Firefox (User) (x64)
- [Mozilla Firefox] Mozilla Corporation - Update GetVersion implementation for Mozilla Firefox (User) (x86)
- [Mozilla Firefox] Mozilla Corporation - Update TerminateProcesses implementation for Mozilla Firefox (x86)
- [Mozilla Firefox] Mozilla Corporation - Update Run implementation for Mozilla Firefox (x86)
- [Mozilla Firefox] Mozilla Corporation - Update GetRunningState implementation for Mozilla Firefox (x86)
- [Mozilla Firefox] Mozilla Corporation - Update GetVersion implementation for Mozilla Firefox (x86)
- [Mozilla Firefox] Mozilla Corporation - Update GetInstallationDirectories implementation for Mozilla Firefox (x86)
- [Mozilla Firefox] Mozilla Corporation - Implement GetComponents for Mozilla Firefox (x86)
- [Mozilla Firefox] Mozilla Corporation - Implement GetUninstallString for Mozilla Firefox (x86)
- [Mozilla Firefox] Mozilla Corporation - Implement IsAuthentic for Mozilla Firefox (x86)
- [Mozilla Firefox] Mozilla Corporation - Implement GetUninstallHive for Mozilla Firefox (x86)
- [Mozilla Firefox] Mozilla Corporation - Implement GetUninstallHive for Mozilla Firefox (x64)
- [Mozilla Firefox] Mozilla Corporation - Implement IsAuthentic for Mozilla Firefox (x64)
- [Mozilla Firefox] Mozilla Corporation - Implement GetUninstallString for Mozilla Firefox (x64)
- [Mozilla Firefox] Mozilla Corporation - Implement GetComponents for Mozilla Firefox (x64)
- [Mozilla Firefox] Mozilla Corporation - Update GetInstallationDirectories implementation for Mozilla Firefox (x64)
- [Mozilla Firefox] Mozilla Corporation - Update TerminateProcesses implementation for Mozilla Firefox (x64)
- [Mozilla Firefox] Mozilla Corporation - Update Run implementation for Mozilla Firefox (x64)
- [Mozilla Firefox] Mozilla Corporation - Update GetRunningState implementation for Mozilla Firefox (x64)
- [Mozilla Firefox] Mozilla Corporation - Update GetVersion implementation for Mozilla Firefox (x64)
- [DJV2] Humanity - Update GetRunningState implementation for DJV2
- [WsgiDAV] Martin Wendt - Implement GetRunningState for WsgiDAV
- [DBX] t8y2 - Implement GetRunningState for DBX
- [Mozilla Firefox] Mozilla Corporation - Implement GetUninstallHive for Mozilla Firefox (User) (arm64)
- [Mozilla Firefox] Mozilla Corporation - Implement IsAuthentic for Mozilla Firefox (User) (arm64)
- [Mozilla Firefox] Mozilla Corporation - Implement GetUninstallString for Mozilla Firefox (User) (arm64)
- [Mozilla Firefox] Mozilla Corporation - Implement GetComponents for Mozilla Firefox (User) (arm64)
- [Mozilla Firefox] Mozilla Corporation - Implement GetRunningState for Mozilla Firefox (User) (arm64)
- [Mozilla Firefox] Mozilla Corporation - Implement Run for Mozilla Firefox (User) (arm64)
- [Mozilla Firefox] Mozilla Corporation - Implement TerminateProcesses for Mozilla Firefox (User) (arm64)
- [Mozilla Firefox] Mozilla Corporation - Update GetVersion implementation for Mozilla Firefox (User) (x86)
- [Mozilla Firefox] Mozilla Corporation - Implement GetInstallationDirectories for Mozilla Firefox (User) (arm64)
- [Mozilla Firefox] Mozilla Corporation - Update GetVersion implementation for Mozilla Firefox (User) (x64)
- [Mozilla Firefox] Mozilla Corporation - Update GetVersion implementation for Mozilla Firefox (User) (x64)
- [Mozilla Firefox] Mozilla Corporation - Update GetVersion implementation for Mozilla Firefox (User) (x86)
- [Mozilla Firefox] Mozilla Corporation - Implement GetVersion for Mozilla Firefox (User) (arm64)
- [Mozilla Firefox] Mozilla Corporation - Implement GetUninstallHive for Mozilla Firefox (User) (x86)
- [Mozilla Firefox] Mozilla Corporation - Implement IsAuthentic for Mozilla Firefox (User) (x86)
- [Mozilla Firefox] Mozilla Corporation - Implement GetInstallationDirectories for Mozilla Firefox (User) (x86)
- [Mozilla Firefox] Mozilla Corporation - Implement GetComponents for Mozilla Firefox (User) (x86)
- [Mozilla Firefox] Mozilla Corporation - Implement GetUninstallString for Mozilla Firefox (User) (x86)
- [Mozilla Firefox] Mozilla Corporation - Implement TerminateProcesses for Mozilla Firefox (User) (x86)
- [Mozilla Firefox] Mozilla Corporation - Implement Run for Mozilla Firefox (User) (x86)
- [Mozilla Firefox] Mozilla Corporation - Implement GetRunningState for Mozilla Firefox (User) (x86)
- [Mozilla Firefox] Mozilla Corporation - Implement TerminateProcesses for Mozilla Firefox (User) (x64)
- [Mozilla Firefox] Mozilla Corporation - Implement Run for Mozilla Firefox (User) (x64)
- [Mozilla Firefox] Mozilla Corporation - Implement GetRunningState for Mozilla Firefox (User) (x64)
- [Mozilla Firefox] Mozilla Corporation - Implement GetInstallationDirectories for Mozilla Firefox (User) (x64)
- [Mozilla Firefox] Mozilla Corporation - Implement GetComponents for Mozilla Firefox (User) (x64)
- [Mozilla Firefox] Mozilla Corporation - Implement GetUninstallString for Mozilla Firefox (User) (x64)
- [Mozilla Firefox] Mozilla Corporation - Implement IsAuthentic for Mozilla Firefox (User) (x64)
- [Mozilla Firefox] Mozilla Corporation - Implement GetUninstallHive for Mozilla Firefox (User) (x64)
- [Mozilla Firefox] Mozilla Corporation - Implement GetVersion for Mozilla Firefox (User) (x86)
- [Mozilla Firefox] Mozilla Corporation - Implement GetVersion for Mozilla Firefox (User) (x64)
- [Sentinel Agent] SentinelOne - Update GetLastScanTime implementation for Sentinel Agent
- [Mozilla Firefox] Mozilla Corporation - Implement IsDefaultBrowser for Mozilla Firefox (arm64)
- [Trojan Killer] GridinSoft LLC. - Update GetRealTimeProtectionState implementation for Trojan Killer
- [Trojan Killer] GridinSoft LLC. - Update GetDefinitionState implementation for Trojan Killer
- [Trojan Killer] GridinSoft LLC. - Update GetThreats implementation for Trojan Killer
- [Trojan Killer] GridinSoft LLC. - Update GetLastScanTime implementation for Trojan Killer
- [Trojan Killer] GridinSoft LLC. - Update EnableRTP implementation for Trojan Killer
- [Trojan Killer] GridinSoft LLC. - Update UpdateDefinitions implementation for Trojan Killer
- [Trojan Killer] GridinSoft LLC. - Update Scan implementation for Trojan Killer
- [Tera Term] TeraTerm Project T. Teranishi - Update GetVersion implementation for Tera Term (User)
- [ESET Endpoint Security] ESET - Update SetFirewallState implementation for ESET Endpoint Security
- [ESET Endpoint Security] ESET - Update GetFirewallState implementation for ESET Endpoint Security
- [PHP] The PHP Group - Implement GetInstallationDirectories for PHP NTS 8.3
- [PHP] The PHP Group - Implement GetInstallationDirectories for PHP NTS 8.2
- [PHP] The PHP Group - Implement GetInstallationDirectories for PHP NTS 8.4
- [BiglyBT] Bigly Software - Implement GetVersion for BiglyBT
- [PHP] The PHP Group - Implement GetInstallationDirectories for PHP NTS 8.5
- [PHP] The PHP Group - Implement GetUninstallHive for PHP NTS 8.2
- [PHP] The PHP Group - Implement GetUninstallHive for PHP NTS 8.3
- [PHP] The PHP Group - Implement GetUninstallHive for PHP NTS 8.4
- [PHP] The PHP Group - Implement GetUninstallHive for PHP NTS 8.5
- [PHP] The PHP Group - Implement GetVersion for PHP NTS 8.5
- [PHP] The PHP Group - Implement GetVersion for PHP NTS 8.4
- [PHP] The PHP Group - Implement GetVersion for PHP NTS 8.3
- [PHP] The PHP Group - Implement GetVersion for PHP NTS 8.2
- [PHP] The PHP Group - Implement GetUninstallHive for PHP NTS 8.2
- [PHP] The PHP Group - Implement GetUninstallHive for PHP NTS 8.3
- [PHP] The PHP Group - Implement GetUninstallString for PHP NTS 8.5
- [PHP] The PHP Group - Implement GetUninstallString for PHP NTS 8.4
- [PHP] The PHP Group - Implement GetUninstallString for PHP NTS 8.3
- [PHP] The PHP Group - Implement GetUninstallString for PHP NTS 8.2
- [PHP] The PHP Group - Implement TerminateProcesses for PHP NTS 8.2
- [PHP] The PHP Group - Implement TerminateProcesses for PHP 8.3
- [PHP] The PHP Group - Implement GetRunningState for PHP 8.3
- [PHP] The PHP Group - Implement GetRunningState for PHP NTS 8.3
- [PHP] The PHP Group - Implement Run for PHP NTS 8.3
- [PHP] The PHP Group - Implement TerminateProcesses for PHP NTS 8.3
- [PHP] The PHP Group - Implement GetRunningState for PHP 8.4
- [PHP] The PHP Group - Implement Run for PHP 8.4
- [PHP] The PHP Group - Implement GetRunningState for PHP NTS 8.4
- [PHP] The PHP Group - Implement Run for PHP NTS 8.4
- [PHP] The PHP Group - Implement TerminateProcesses for PHP NTS 8.4
- [PHP] The PHP Group - Implement TerminateProcesses for PHP 8.5
- [PHP] The PHP Group - Implement GetRunningState for PHP NTS 8.5
- [PHP] The PHP Group - Implement GetRunningState for PHP NTS 8.2
- [PHP] The PHP Group - Implement Run for PHP NTS 8.2
- [PHP] The PHP Group - Implement Run for PHP 8.3
- [PHP] The PHP Group - Implement GetRunningState for PHP 8.2
- [PHP] The PHP Group - Implement Run for PHP 8.2
- [PHP] The PHP Group - Implement TerminateProcesses for PHP 8.2
- [PHP] The PHP Group - Implement TerminateProcesses for PHP 8.4
- [PHP] The PHP Group - Implement Run for PHP 8.5
- [PHP] The PHP Group - Implement TerminateProcesses for PHP NTS 8.5
- [PHP] The PHP Group - Implement GetRunningState for PHP 8.5
- [PHP] The PHP Group - Implement Run for PHP NTS 8.5
