<!-- source: https://www.opswat.com/docs/mdmft/troubleshooting/cli-installation -->

# CLI Installation

Summarize Page    Connect to Cursor Connect to VS Code
### [Persistent Popup in Silent Mode on Windows Server](/docs/mdmft/troubleshooting/cli-installation#persistent-popup-in-silent-mode-on-windows-server)

Users may encounter a persistent popup even when utilizing the /silent mode on a Windows Server machine. This issue is related to Windows User Account Control (UAC). Adjusting the UAC severity level from the displayed window can resolve this.

#### [Resolution](/docs/mdmft/troubleshooting/cli-installation#resolution)

1. While in /silent mode, if a popup persists, it may be due to Windows UAC.
2. Manually adjust the UAC severity level in the window to resolve the popup issue.

This solution ensures smooth execution in /silent mode on Windows Server machines.
