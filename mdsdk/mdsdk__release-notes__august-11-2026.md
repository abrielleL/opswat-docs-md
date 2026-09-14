<!-- source: https://www.opswat.com/docs/mdsdk/release-notes/august-11-2026 -->

# August 11th, 2026

## [Release Note](/docs/mdsdk/release-notes/august-11-2026#release-note)

### [Release Date](/docs/mdsdk/release-notes/august-11-2026#release-date)

- 11/08/2026

### [SDK Version](/docs/mdsdk/release-notes/august-11-2026#sdk-version)

- **Windows**: 4.3.6463.0
- **Linux**: 4.3.5466.0
- **Mac**: 4.3.5851.0

### [Enhancement](/docs/mdsdk/release-notes/august-11-2026#enhancement)

#### [Windows](/docs/mdsdk/release-notes/august-11-2026#windows)

- Add signature-level "data_source" field to moby.json
- Add EPSS (Exploit Prediction Scoring System) score in vulnerability data

#### [Linux](/docs/mdsdk/release-notes/august-11-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/august-11-2026#mac)

- MacOS | New DetectProducts flag to scan products across all users (active & inactive)

### [Bug Fix](/docs/mdsdk/release-notes/august-11-2026#bug-fix)

#### [Windows](/docs/mdsdk/release-notes/august-11-2026#windows)

- Fixed a process crash occurring when `wa_api_free` was called after a failed initialization by guarding internal resource lookups and ensuring proper state cleanup, improving application stability and reliability for SDK integrations.
- Resolved the incorrect reporting of CVE-2024-54534 as "not vulnerable" on older Java 8 builds via a data-only update to the affected-version range, improving detection accuracy across all Java 8 versions prior to 8u451.
- Fixed a thread handle leak in the internet connectivity check used by GetRealTimeProtectionState , GetDefinitionState , and other APIs.

#### [Linux](/docs/mdsdk/release-notes/august-11-2026#linux)

- Fixed a process crash occurring when `wa_api_free` was called after a failed initialization by guarding internal resource lookups and ensuring proper state cleanup, improving application stability and reliability for SDK integrations.

#### [Mac](/docs/mdsdk/release-notes/august-11-2026#mac)

- Fixed a process crash occurring when `wa_api_free` was called after a failed initialization by guarding internal resource lookups and ensuring proper state cleanup, improving application stability and reliability for SDK integrations.

### [New Application Support](/docs/mdsdk/release-notes/august-11-2026#new-application-support)

#### [Windows](/docs/mdsdk/release-notes/august-11-2026#windows)

- Add detection support for Datto/CentraStage RMM (Remote control category)
- V4 | Add support for new version for existing products PaperCut NG version 23-25 major version
- Add support VA for Claude on Windows and macOS
- Add third-party product support (detection + patching) for Claude Desktop and Claude Code (Anthropic) on Windows and macOS
- V4 | Windows | Add support for WinRAR 7.x
- V4| Add support for new version for existing products PaperCut MF version 22-25 major version

#### [Linux](/docs/mdsdk/release-notes/august-11-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/august-11-2026#mac)

- [W:3] macOS | Add support detection for ShellGPT
- [W:3] macOS | Add support detection for OpenAI CLI
- Add support VA for Claude on Windows and macOS
- Add third-party product support (detection + patching) for Claude Desktop and Claude Code (Anthropic) on Windows and macOS
- [W:3] macOS | Add support detection for Msty

### [New Application Version Support](/docs/mdsdk/release-notes/august-11-2026#new-application-version-support)

#### [Windows](/docs/mdsdk/release-notes/august-11-2026#windows)

- Add detection support for Datto/CentraStage RMM (Remote control category)
- V4 | Add support for new version for existing products PaperCut NG version 23-25 major version
- V4 | Windows | Add support for Microsoft OneDrive version 26.134.0713.0003
- Add support VA for Claude on Windows and macOS
- Add third-party product support (detection + patching) for Claude Desktop and Claude Code (Anthropic) on Windows and macOS
- V4 | Windows | Add support for WinRAR 7.x
- V4| Add support for new version for existing products PaperCut MF version 22-25 major version

#### [Linux](/docs/mdsdk/release-notes/august-11-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/august-11-2026#mac)

- [W:3] macOS | Add support detection for ShellGPT
- [W:3] macOS | Add support detection for OpenAI CLI
- Add support VA for Claude on Windows and macOS
- Add third-party product support (detection + patching) for Claude Desktop and Claude Code (Anthropic) on Windows and macOS
- [W:3] macOS | Add support detection for Msty
- V4 | Mac | Add support for macOS version 26.6

### [New Method Implementation](/docs/mdsdk/release-notes/august-11-2026#new-method-implementation)

#### [Windows](/docs/mdsdk/release-notes/august-11-2026#windows)

- [Rocket.Chat] Rocket.Chat Support - Implement GetVersion for Rocket.Chat
- [Datto RMM] Datto, Inc - Implement Run for Datto RMM
- [Datto RMM] Datto, Inc - Implement TerminateProcesses for Datto RMM
- [CentraStage] Datto, Inc - Implement Run for CentraStage
- [CentraStage] Datto, Inc - Implement TerminateProcesses for CentraStage
- [Poly Studio] Hewlett-Packard - Implement GetVersion for Poly Studio
- [Poly Studio] Hewlett-Packard - Implement TerminateProcesses for Poly Studio
- [Poly Studio] Hewlett-Packard - Implement GetRunningState for Poly Studio
- [Poly Studio] Hewlett-Packard - Implement Run for Poly Studio
- [Tableau] Tableau Software - Update GetVersion implementation for Tableau
- [Microsoft Edge] Microsoft Corporation - Update GetVersion implementation for Microsoft Edge 80+
- [3CX Phone System] 3CX Ltd - Update GetRunningState implementation for 3CX Phone System
- [3CX Phone System] 3CX Ltd - Update Run implementation for 3CX Phone System
- [CentraStage] Datto, Inc - Implement GetRunningState for CentraStage
- [Datto RMM] Datto, Inc - Implement GetRunningState for Datto RMM
- [3CX Phone System] 3CX Ltd - Implement Run for 3CX Phone System
- [3CX Phone System] 3CX Ltd - Implement TerminateProcesses for 3CX Phone System
- [3CX Phone System] 3CX Ltd - Implement GetRunningState for 3CX Phone System
- [Fiddler Web Debugger] Telerik - Implement Run for Fiddler Web Debugger
- [Fiddler Web Debugger] Telerik - Implement GetVersion for Fiddler Web Debugger
- [Fiddler Web Debugger] Telerik - Implement TerminateProcesses for Fiddler Web Debugger
- [Fiddler Web Debugger] Telerik - Implement GetRunningState for Fiddler Web Debugger
- [WinRAR] Alexander Roshal - Update Run implementation for WinRAR (x86)
- [WinRAR] Alexander Roshal - Update GetUninstallHive implementation for WinRAR (x86)
- [WinRAR] Alexander Roshal - Update Run implementation for WinRAR (x64)
- [Tableau Reader] Tableau Software - Update GetVersion implementation for Tableau Reader
- [Sysmon] Sysinternals - Implement GetRunningState for Sysmon
- [ONLYOFFICE Desktop Editors] Ascensio System SIA - Implement GetRunningState for ONLYOFFICE Desktop Editors
- [ONLYOFFICE Desktop Editors] Ascensio System SIA - Implement TerminateProcesses for ONLYOFFICE Desktop Editors
- [GoTo] GoTo Group, Inc. - Implement GetVersion for GoTo
- [Password Safe] Rony Shapiro - Implement GetVersion for Password Safe
- [DeepL] DeepL SE - Implement GetVersion for DeepL
- [GoTo] GoTo Group, Inc. - Implement GetVersion for GoTo
- [HP Support Assistant] HP Development Company, L.P. - Update TerminateProcesses implementation for HP Support Assistant
- [Figma] Figma, Inc. - Implement GetRunningState for Figma
- [Figma] Figma, Inc. - Implement TerminateProcesses for Figma
- [Duo Desktop] Duo Security - Implement GetRunningState for Duo Desktop
- [Duo Desktop] Duo Security - Implement TerminateProcesses for Duo Desktop
- [RealVNC Connect] RealVNC - Implement GetVersion for RealVNC Connect
- [RealVNC Connect] RealVNC - Implement GetRunningState for RealVNC Connect
- [RealVNC Connect] RealVNC - Implement TerminateProcesses for RealVNC Connect
- [GoodSync] Siber System Inc. - Implement GetRunningState for GoodSync
- [GoodSync] Siber System Inc. - Implement TerminateProcesses for GoodSync
- [UltraEdit] IDM Computer Solutions, Inc. - Implement GetVersion for UltraEdit
- [Box Drive] Box, Inc. - Implement TerminateProcesses for Box Drive
- [Box Drive] Box, Inc. - Implement GetRunningState for Box Drive
- [PSPad editor] Jan Fiala - Implement GetVersion for PSPad editor
- [CutePDF Writer] Acro Software Inc. - Implement GetVersion for CutePDF Writer

#### [Linux](/docs/mdsdk/release-notes/august-11-2026#linux)

- N/A

#### [Mac](/docs/mdsdk/release-notes/august-11-2026#mac)

- [Navi] Karl Valencia - Implement GetInstallationDirectories for Navi
- [Navi] Karl Valencia - Implement TerminateProcesses for Navi
- [Navi] Karl Valencia - Implement GetRunningState for Navi
- [Playground For LM] Wang ZeCheng - Implement GetInstallationDirectories for Playground For LM
- [Playground For LM] Wang ZeCheng - Implement TerminateProcesses for Playground For LM
- [Playground For LM] Wang ZeCheng - Implement GetRunningState for Playground For LM
- [ShellGPT] TheR1D - Implement GetVersion for ShellGPT
- [ShellGPT] TheR1D - Implement GetInstallationDirectories for ShellGPT
- [ShellGPT] TheR1D - Implement GetInstallationDirectories for ShellGPT
- [OpenAI CLI] OpenAI - Implement GetVersion for OpenAI CLI
- [OpenAI CLI] OpenAI - Implement GetInstallationDirectories for OpenAI CLI
- [Claude] Anthropic PBC - Implement GetVersion for Claude
- [Zabbix Agent] Zabbix LLC - Update GetVersion implementation for Zabbix Agent
