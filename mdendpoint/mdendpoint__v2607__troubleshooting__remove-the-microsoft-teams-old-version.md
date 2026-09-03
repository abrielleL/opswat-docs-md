<!-- source: https://www.opswat.com/docs/mdendpoint/v2607/troubleshooting/remove-the-microsoft-teams-old-version -->

# Workaround to remove the Microsoft Teams old version at WindowsApps folder

## Issue Summary

During our analysis, we identified that **multiple versions of Microsoft Teams** may coexist on the same machine after upgrading to the new Teams application.

- **Microsoft Teams (Work or School):** Updated correctly to the latest version `25227.203.3915.2444`.
- **Microsoft Teams (Old Version):** Previous versions are not removed automatically by Microsoft after upgrade.
  - Example: `23119.303.2080.2726`
  - Or version is less than 25122.1415.3698.6812

These old versions remain under the path: `C:\Program Files\WindowsApps\MicrosoftTeams_<version>`

We detect these versions as vulnerable and flags them under:

- **NVD: CVE-2025-53783**

## Root Cause

- Microsoft upgrade process does not consistently remove legacy Teams folders from `WindowsApps`.
- This leads to outdated binaries being present and detected as vulnerable.

## Temporary Workaround

A script has been prepared to mitigate the issue by moving old Teams folders.

### Steps:

- Create the script (in the .bat file format) using this

```json
@echo off
SETLOCAL ENABLEDELAYEDEXPANSION
:: Path to WindowsApps
set "WINAPPS=C:\Program Files\WindowsApps"
:: Loop through folders starting with MicrosoftTeams or microsoftTeams
for /d %%F in ("%WINAPPS%\MicrosoftTeams*") do (
 :: Take ownership
 takeown /f "%%F" /r /d y >nul 2>&1
 :: Grant full control to current user
 icacls "%%F" /grant %username%:F /t >nul 2>&1
 :: Delete folder
 rmdir /s /q "%%F" >nul 2>&1
)
:: End silently
EXIT /B
```

- Run the script with Administrator privileges.
  - The script will only move old Microsoft Teams version folders.
- Recheck compliance status from the tray icon

⚠️ **Note:** This is a temporary workaround and should not be considered a permanent fix.

## Next Steps

We are currently working to support an additional method to uninstall directly from MetaDefender Endpoint as an alternative to the current workaround.
