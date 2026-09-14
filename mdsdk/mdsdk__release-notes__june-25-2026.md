<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/june-25-2026 -->

# June 25th, 2026

## [Release Note](/docs/mdsdk/release-notes/june-25-2026#release-note)

### [Release Date](/docs/mdsdk/release-notes/june-25-2026#release-date)

- 25/06/2026

### [SDK Version](/docs/mdsdk/release-notes/june-25-2026#sdk-version)

- **Windows**: 4.3.6259.0
- **Linux**: 4.3.5255.0
- **Mac**: 4.3.5645.0

### [Enhancement](/docs/mdsdk/release-notes/june-25-2026#enhancement)

#### [Windows](/docs/mdsdk/release-notes/june-25-2026#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/june-25-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/june-25-2026#mac)

- N/A

### [Bug Fix](/docs/mdsdk/release-notes/june-25-2026#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/june-25-2026#windows)

- GetProductVulnerability: improved missing-patch detection. Fixed two cases of under-reported CVEs:

## [KBs that Windows Update flags as missing are no longer dismissed when another source reports them installed (catches pending-reboot / partial installs)](/docs/mdsdk/release-notes/june-25-2026#kbs-that-windows-update-flags-as-missing-are-no-longer-dismissed-when-another-source-reports-them-installed-catches-pending-reboot--partial-installs)

## [KBs scoped out on older OS builds are now recovered via the OS build version, so their CVEs are reported (e.g. Windows 10 1803)](/docs/mdsdk/release-notes/june-25-2026#kbs-scoped-out-on-older-os-builds-are-now-recovered-via-the-os-build-version-so-their-cves-are-reported-eg-windows-10-1803)

- Security fix: AppRemover / removal module. Updated the bundled AppRemover kernel helper driver to version 10.3.5429.0. The driver's control device is now restricted to administrative callers, resolving a local privilege-escalation issue where a non-administrative user on the same machine could send commands to the driver.
- Resolved the issue where temporary files were not cleaned up when no user was logged in by removing the dependency on non-elevated impersonation for cache cleanup, improving system reliability and storage management for headless server environments.

#### [Linux](/docs/mdsdk/release-notes/june-25-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/june-25-2026#mac)

- N/A

### [New Application Support](/docs/mdsdk/release-notes/june-25-2026#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/june-25-2026#windows)

- N/A

#### [Linux](/docs/mdsdk/release-notes/june-25-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/june-25-2026#mac)

- N/A

### [New Application Version Support](/docs/mdsdk/release-notes/june-25-2026#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/june-25-2026#windows)

- Request Rapid7 license renewal to support GetRealtimeProtectionState & GetDefinitionState
- V4 | Windows | Add support for Mozilla Firefox (arm64) version 152.0.2

#### [Linux](/docs/mdsdk/release-notes/june-25-2026#linux)

- V4 | Linux | Add support for Zoom version 7.1.0
- V4 | Linux | Add support for Visual Studio Code version 1.126.0
- V4 | Linux | Add support for Signal version 8.15.0
- V4 | Linux | Add support for Mozilla Firefox version 152.0.2

#### [Mac](/docs/mdsdk/release-notes/june-25-2026#mac)

- N/A

### [New Method Implementation](/docs/mdsdk/release-notes/june-25-2026#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/june-25-2026#windows)

- [Avast Premium Security] AVAST Software a.s. - Update GetThreats implementation for Avast Premium Security
- [ESET Internet Security] ESET - Update SetFirewallState implementation for ESET Internet Security
- [Microsoft Visual C++ v14 Redistributable] Microsoft Corporation - Implement GetVersion for Microsoft Visual C++ v14 Redistributable (x64)
- [BlueStacks] BlueStack Systems, Inc. - Implement TerminateProcesses for BlueStacks
- [BlueStacks] BlueStack Systems, Inc. - Implement GetRunningState for BlueStacks
- [Hex Workshop] BreakPoint Software, Inc. - Implement TerminateProcesses for Hex Workshop
- [Hex Workshop] BreakPoint Software, Inc. - Implement GetRunningState for Hex Workshop
- [Hex Workshop] BreakPoint Software, Inc. - Implement Run for Hex Workshop
- [Resource Hacker] Angus Johnson - Implement TerminateProcesses for Resource Hacker
- [Resource Hacker] Angus Johnson - Implement GetRunningState for Resource Hacker
- [Resource Hacker] Angus Johnson - Implement Run for Resource Hacker
- [SmartFTP] SmartSoft Ltd. - Implement Run for SmartFTP
- [Safari] Apple Inc. - Implement Run for Safari
- [Tera Term] TeraTerm Project T. Teranishi - Implement Run for Tera Term
- [Tera Term] TeraTerm Project T. Teranishi - Implement GetVersion for Tera Term
- [GrafanaEnterprise] Grafana Labs - Implement GetRunningState for GrafanaEnterprise
- [GrafanaEnterprise] Grafana Labs - Implement TerminateProcesses for GrafanaEnterprise
- [GrafanaEnterprise] Grafana Labs - Implement Run for GrafanaEnterprise
- [GrafanaEnterprise] Grafana Labs - Update GetVersion implementation for GrafanaEnterprise
- [CrashPlan] Code42 Software - Update TerminateProcesses implementation for CrashPlan
- [NoMachine] NoMachine - Implement Run for NoMachine
- [NoMachine] NoMachine - Implement TerminateProcesses for NoMachine
- [NoMachine] NoMachine - Implement GetRunningState for NoMachine

#### [Linux](/docs/mdsdk/release-notes/june-25-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/june-25-2026#mac)

- N/A
