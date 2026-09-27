<!-- source: https://www.opswat.com/docs/mdendpoint/v2608/release-notes/archived-release-notes -->

# Archived Release Notes

## Release Date: Dec 26, 2023

**Windows Persistent Client (** **7.6.2312.402** **)**

1. **New features:**
   - **MD Core Integration for User Information Display:**
     - We have implemented MD Core integration to enhance the scanning processing page. Now, you can view detailed user information, including the username, providing more context during the scanning process.
2. **Enhancements**:
   - **Reverted HID Protection Feature:**
     - Reversed the HID (Human Interface Device) protection feature to its default state of being disabled. Users can now enable it based on their specific needs.
3. **Bugs fixed:**
   - **Improved UI for Malware Scan:**
     - Addressed UI issues on the Malware Scan screen for a more seamless and visually enhanced user experience.
   - **Enhanced Percentage Calculation during Scans:**
     - Resolved issues related to percentage calculation during scans, ensuring accurate and reliable progress tracking.
   - **Copy to Android Device Issue:**
     - Resolved a bug where copying files to Android devices was failing. This fix ensures a smoother file copying process to Android devices.
4. Built-in SDK signature version: 4.3.3829.0

## Release Date: Nov 15, 2023

**Windows Persistent Client (** **7.6.2310.382** **)**

1. New features:
   - Added support HID protection.
   - Added support burn data to CD drive option.
   - Added support maximize/minimize the OPSWAT Client UI.
   - Added support wipe files in a USB drive.
2. Enhancements:
   - Updated UI text for translating to Hebrew and Arabic
   - Handle blocked files in manifest file.
3. Bugs fixed:
   - The OPSWAT Client service is crashed when copying files with having password.
   - Could not list files on the mobile drive.
   - Fixed copying sanitized files to a network drive
   - Fixed issue that is not available rule for scanning.
   - Show 0 KB for selected files from Google Drive to a USB drive.
4. Built-in SDK signature version: 4.3.3732.0

## Release Date: Sep 6, 2023

**Windows Persistent Client (** **7.6.2308.348** **)**

1. New features:
   - Added support ejecting an USB inside the OPSWAT Client UI.
2. Enhancements:
   - OPSWAT Client enhances batch processing within Media Scan Resolved issues and improved user interface for a smoother experience.
3. Built-in SDK signature version: 4.3.3644.0

## Release Date: May 24, 2023

**Windows Persistent Client (** **7.6.2305.273** **)**

1. New features:
   - Added support Encrypted USB DataTraveler 4000 G2.
   - Added more detail for scanning time on Client UI.
2. Enhancements:
   - Added device group information to the About box.
   - Refinements to the layout and messaging in the OPSWAT Client UI.
   - Added more details to the Scanning Report regarding encrypted files and skipped files.
   - Enhanced scanning for System Volume Information files.
3. Bugs fixed**:**
   - The file cannot be copied if there is a Chinese character in the file name.
4. Built-in SDK signature version: 4.3.3368.0

## Release Date: Mar 15, 2023

**Windows Persistent Client (** **7.6.2302.176** **)**

1. New features:
   - Added feature to retain the folder structure of files copied from their USB location to the destination folder on the local drive.
2. Enhancements:
   - Refinement of the UI across the various screens.
   - Added more details to the scan results for each scanned file.
   - Enhanced the user experience when scanning files via the Removable Media Protection feature.
   - Added the ability for the user to view the Allowed Files in the Removable Media scan report.
3. Bugs fixed**:**
   - OPSWAT Client UI crashes when there is a % character in the content.
4. Built-in SDK signature version: 4.3.3368.0

**Windows On-demand (** **7.3.2302.85** **)**

1. Enhancements:
   - Updated OESIS SDK.
   - Improved compliance evaluation of files in the system for ignored threats.
2. Built-in SDK signature version: 4.3.3368.0

**macOS Persistent: (** **10.4.2302.53** **)**

1. Enhancements:
   - Improved compliance evaluation of files in the system for ignored threats.
   - Addressed a few security issues.
2. Built-in SDK signature version: 4.3.2892.0

**macOS On-demand (** **10.5.2210.12** **)**

1. Enhancements:
   - Improved compliance evaluation of files in the system for ignored threats.
   - Addressed a few security issues.
2. Built-in SDK signature version: 4.3.2892.0

## Release Date: December 21, 2022

**Windows Persistent Client (** **7.6.2211.139** **)**

1. New features:
   - Added support USB allow list
   - Added support for the encrypted IronKey S1000 USB.
   - Added the Custom Information into the About Box.
   - Added support to show a notification when a device's status is change from Compliant-to-Non-Compliant (and vice versa).
   - Added support for right-to-left languages and multiple languages (Hebrew, Arabic) in the Removable Media Protection Client
   - Updated Anti-Screen Capture to better target the "mstsc" or "mstsc.exe" process, when configured by the Admin.
2. Enhancements:
   - Refinement of the UI across the various screens.
3. Bugs fixed**:**
   - OPSWAT Client UI crashes when the admin disables Malware Detection.
   - OPSWAT Client can't scan files when the admin configures the max size of a file scan greater than 2048 MB.
4. Built-in SDK signature version: 4.3.3152.0

**Windows On-demand (** **7.3.2210.34** **)**

1. Enhancements:
   - Added the Custom Information into the About Box.
2. Built-in SDK signature version: 4.3.3152.0

**macOS Persistent: (** **10.4.2209.18** **)**

1. Enhancements:
   - Added the Custom Information into the About Box.
   - Enhanced logging for troubleshooting.
2. Built-in SDK signature version: 4.3.2726.0

**macOS On-demand ( 10.5.2210.12 )**

1. Enhancements:
   - Added the Custom Information into the About Box.
   - Enhanced logging for troubleshooting.
2. Built-in SDK signature version: 4.3.2726.0

## Release Date: October 5, 2022

**Windows Persistent Client (** **7.6.2209.65** **)**

1. Enhancements:
   - Added support to choose files via Windows File Explorer when copying files from the computer to the USB drive.
   - Refinement of the UI across the various screens.
   - Refinement of the CLI Client commands.
2. Bugs fixed**:**
   - OPSWAT Client UI crashes when the admin disables Malware Detection.
   - OPSWAT Client can't scan files when the admin configures the max size of a file scan greater than 2048 MB.
3. Built-in SDK signature version: 4.3.3041.0

**Windows On-demand ( 7.3.2209.29** **)**

1. Enhancements:
   - Updated OESIS SDK
2. Built-in SDK signature version: 4.3.3041.0

**macOS Persistent: (** **10.4.2209.18** **)**

1. Enhancements:
   - Updated OESIS SDK
2. Built-in SDK signature version: 4.3.2401.0

**macOS On-demand (** **10.5.2209.9** **)**

1. Enhancements:
   - Updated OESIS SDK
2. Built-in SDK signature version: 4.3.2401.0

## Release Date: August 24, 2022

**Windows Persistent Client ( 7.6.2208.31 )**

1. New features:
   - Show notification when a device's compliance status changes.
2. Enhancements:
   - Added ability to scan encrypted files and drives during a manual scan.
   - Refinement of the UI across the various screens
   - Added more details in the scan report after scanning the removable media.
   - Added support to search for files to copy on the removable media.
   - Added support to show hidden files in the Client UI.
   - Provide a consistent version of our OPSWAT Clients across the platforms.
   - Added support for processing the MD Core Allow/Block list.
   - Added support for treating infected files blocked by Windows Defender as infected files.
   - Enhanced some security issues.
   - Show notification when a device's compliance status changes.
3. Bugs fixed:
   - Retry for some error cases when scanning many files.
   - OPSWAT Client tray is not displayed automatically (Windows 11).
   - Service crashes after running for a long time
   - OPSWAT Client UI doesn't pop up automatically when plugging a USB flash drive
4. Built-in SDK signature version: 4.3.3041.0

**Windows On-demand ( 7.3.2208.17** **)**

1. New features:
   - Show notification when a device's compliance status changes.
2. Enhancements
   - Provide a consistent version of our OPSWAT Clients across the platforms.
   - Enhanced some security issues.
   - Show notification when a device's compliance status changes.
3. Built-in SDK signature version: 4.3.3041.0

**macOS Persistent: ( 10.4.2208.9** **)**

1. New features:
   - Show notification when a device's compliance status changes.
2. Enhancements:
   - Provide a consistent version of our OPSWAT Clients across the platforms.
   - Enhanced some security issues.
   - Hides the "No action needed" and "Action required" items on the tray menu when the compliance check is disabled.
3. Built-in SDK signature version: 4.3.2623.0

**macOS On-demand ( 10.5.2208.4** **)**

1. New features:
   - Show notification when a device's compliance status changes.
2. Enhancements:
   - Provide a consistent version of our OPSWAT Clients across the platforms.
   - Enhanced some security issues.
3. Built-in SDK signature version: 4.3.2623.0

## Release Date: June 29, 2022

**Windows Persistent Client ( 7.6.575.0 )**

1. Enhancements:
   - Allow the user to choose to overwrite or skip any files that have a conflict when copying files
   - Show file size on the Removable Media page
   - Refinement of the UI across the various screens
   - Enhanced report processing to improve server workload
2. Bugs fixed:
   - Can't show the OPSWAT Client UI when the user doesn't have permission to run a CMD application
   - Retry for some error cases when scanning many files
   - Tray icon is missing from the system tray
   - Missing log files when OneDrive is enabled on the device
3. Built-in SDK signature version: 4.3.2868.0

**Windows On-demand ( 7.3.677.0 )**

1. Enhancements
   - Enhanced report processing to improve server workload
2. Bugs fixed:
   - Missing log files when OneDrive is enabled on the device
   - Tray icon is missing from the system tray
3. Built-in SDK signature version: 4.3.2868.0

**macOS Persistent: ( 10.4.385.0 )**

1. New features:
   - Support preference file with the macOS Client installer
2. Enhancements:
   - Enhanced report processing to improve server workload
3. Built-in SDK signature version: 4.3.2401.0

**macOS On-demand ( 10.5.308.0 )**

1. Enhancements:
   - Enhanced report processing to improve server workload
2. Built-in SDK signature version: 4.3.2401.0

## Release Date: May 4, 2022

**Windows Persistent Client ( 7.6.552.0 )**

1. New features:
   - Support OPTIONS request for Cross-Domain API
2. Enhancements:
   - Refinement of the UI across the various screens
   - Apply the proxy configuration immediately
   - Add scanning status on PDF report
   - Add hostname information into the metadata header for MD Core
   - Update text of scanning result on the PDF report
3. Bugs fixed:
   - Retry for some error cases when scanning files
   - The tray icon is unresponsive when exporting agent log and the service is restarting
4. Built-in SDK signature version: 4.3.2671.0

**Windows On-demand (7.3.672.0)**

1. New features
   - Support OPTIONS request for Cross-Domain API
2. Built-in SDK signature version: 4.3.2790.0

**macOS Persistent: (10.4.376 .0)**

1. New features:
   - Support OPTIONS request for Cross-Domain API
2. Built-in SDK signature version: 4.3.2351.0

**macOS On-demand (10.5.301.0)**

1. New features:
   - Support OPTIONS request for Cross-Domain API
2. Built-in SDK signature version: 4.3.2351.0

## Release Date: March 15, 2022

**Windows Persistent Client (7.6.541.0)**

1. New features:
   - Added support for delay of compliance-check until user logs into the device
   - New CLI option for mdcl-cli.exe to auto-exit at the end of processing
   - Support new version of Cross-domain API
   - Support Cross-Origin Resource Sharing (CORS) with new Cross-domain API
   - Open the Client UI when (left) clicking the tray icon.
   - Preserve the email address on the password recovery screen.
2. Enhancements:
   - Renew domain certificate [eapi.opswatgears.com](http://eapi.opswatgears.com/)
   - Enhance UX on Vulnerabilities page
   - Enhance security issues
   - Update metadata on binary files
   - Refinement of the UI across the various screens.
3. Bugs fixed:
   - OPSWAT Client can't send report when the custom script output has special characters
   - OPSWAT Client tray icon sometimes disappears
   - Misspelling in the OPSWAT Client UI
   - File data ID is not found for some files when scanning certain directories
   - The tray icon is unresponsive when exporting agent log
4. Built-in SDK signature version: 4.3.2671.0

**Windows On-demand (7.3.669.0)**

1. New features:
   - Support new version of Cross-domain API
   - Support Cross-Origin Resource Sharing (CORS) with new Cross-domain API
   - Open the Client UI when (left) clicking the tray icon.
2. Enhancements:
   - Renew domain certificate [eapi.opswatgears.com](http://eapi.opswatgears.com/)
   - Update metadata on binary files
3. Bugs fixed:
   - OPSWAT Client tray icon sometimes disappears
   - The tray icon is unresponsive when exporting agent log
4. Built-in SDK signature version: 4.3.2671.0

**macOS Persistent: (10.4.369.0)**

1. New features:
   - Added support for delay of compliance-check until user logs into the device
   - Support new version of Cross-domain API
   - Support Cross-Origin Resource Sharing (CORS) with new Cross-domain API
2. Enhancements:
   - Renew domain certificate [eapi.opswatgears.com](http://eapi.opswatgears.com/)
   - Support silent uninstall for the macOS Client
   - Support silent uninstall via the command-line.
   - Support over-install of the agent for deployment on OCM.
3. Bugs fixed:
   - OPSWAT Client can't send report when the custom script output has special characters
   - OPSWAT Client tray icon sometimes disappears
   - Misspelling in the OPSWAT Client UI
   - File data ID is not found for some files when scanning certain directories
   - The tray icon is unresponsive when exporting agent log
4. Built-in SDK signature version: 4.3.2265.0

**macOS On-demand (10.5.297.0)**

1. New features:
   - Support new version of Cross-domain API
   - Support Cross-Origin Resource Sharing (CORS) with new Cross-domain API
2. Enhancements:
   - Renew domain certificate [eapi.opswatgears.com](http://eapi.opswatgears.com/)
3. Built-in SDK signature version: 4.3.2265.0

## Release Date: January 19, 2022

**Windows Persistent Client (7.6.528.0)**

1. Bugs fixed:
   - OPSWAT Client can't stop services with password via CLI command
   - OPSWAT Client sometimes shows a blank UI
   - OPSWAT Client tray icon is sometimes crashed when a user opens its About box
   - Misspelling in the PDF report
   - OPSWAT SDP sometimes stucks at loading page
   - The client service is crashed after running for long time
2. Enhancements:
   - Enhance user experience on the Malware Detection, SDP and Removable Media Security screen
   - Detect network drives on UI after installed\upgraded Client
   - Some minor updates on UI
   - Enhance UX when scanning files
   - Custom Information not showing more than 3 lines in pop-up
   - Enhance security issues
   - Improvement of the user's install experience
   - Enhance performance on scanning applications on Vulnerability and Software Updates page
   - Open main UI from OPSWAT Client shortcut in Start menu
   - Hide the header when prompting for SDP SSO login in the embedded browser
3. Built-in SDK signature version: 4.3.2503.0

#### **Windows On-demand (7.3.661.0)**

1. Bugs fixed
   - OPSWAT Client tray icon is sometimes crashed when a user opens its About box
2. Enhancements:
   - Enhance security issues
3. Built-in SDK signature version: 4.3.2503.0

#### **macOS Persistent (10.4.363.0)**

1. Bug fixed
   - Machine appears to not be connected to server but passes posture check
   - OPSWAT Client was crashed at gear app and tray icon disappear on macOS 10.14
2. Enhancements:
   - Enhance security issues
   - Auto-upgrade to a specific OPSWAT Client/OESIS version
   - Update rebranding SDP on tray menu
   - Should show notifications when export log done / fail
3. Built-in SDK signature version: 4.3.2206.0

**macOS On-demand (10.5.294.0)**

1. Enhancements:
   - Support parameter to show/hide tray icon
   - Enhance security issues
   - Show notifications when export log done / fail
2. Built-in SDK signature version: 4.3.2206.0

## Release Date: December 8, 2021

**Windows Persistent Client (7.6.513.0)**

1. Bugs fixed:
   - UI displays not well with 150% scaling setting
   - OPSWAT Client UI showing as a blank screen
   - OPSWAT Client cannot export PDF and CSV report when deleting history
   - OPSWAT Client UI cannot get instruction link
   - OPSWAT Client UI does not align properly
   - OPSWAT Client UI cannot open from tray icon
2. Enhancements:
   - OPSWAT Client evaluates SOH report before sending
   - OPSWAT Client removes action record when removing history on the UI
   - OPSWAT Client adds explanation to scanning report
3. Built-in SDK signature version: 4.3.2503.0

#### **Windows On-demand (7.3.656.0)**

1. Bugs fixed
   - Device displayed multiple times in console when running the agent on a device with invalid serial number, system permissions, and parameter set to run once.
2. Enhancements:
   - OPSWAT Client evaluates SOH report before sending
3. Built-in SDK signature version: 4.3.2503.0

#### **macOS Persistent (10.4.359.0)**

1. Bug fixed
   - OPSWAT Client failed to fetch log
2. Enhancements:
   - OPSWAT Client evaluates SOH report before sending
3. Built-in SDK signature version: 4.3.2123.0

**macOS On-demand (10.5.288.0)**

1. Bug fixed
   - OPSWAT Client does not exit when logging out of macOS
2. Enhancements:
   - OPSWAT Client evaluates SOH report before sending
3. Built-in SDK signature version: 4.3.2123.0

## Release Date: November 4, 2021

#### **Windows Persistent Client (7.6.504.0)**

1. OPSWAT Client User Interface (UI):
   - Removed Home and Compliance page on UI
2. Enhancements:
   - Update installer look
   - Updated security issues
3. Built-in SDK signature version: 4.3.2466 .0

#### **Windows On-demand (7.3.653.0)**

1. Enhancements:
   - Updated security issues
2. Built-in SDK signature version: 4.3.2466 .0

## Release Date: October 27, 2021

#### **Windows Persistent Client (7.6.496.0)**

1. OPSWAT Client User Interface (UI):
   - Updated Malware detection page.
   - Updated Removable Media Security page.
2. Bugs fixed:
   - OPSWAT Client crashed when the tray icon and application UI were disabled.
   - OPSWAT Client displayed wrong color tray icon when using light mode in Windows 10.
   - OPSWAT Client can not run Custom check on Windows 10 sometimes.
   - OPSWAT Client showed missing DLL error-popup when rechecking compliance.
3. Enhancements:
   - OPSWAT Client supports communication with TLS 1.3 + SAN certificate servers.
   - OPSWAT Client runs custom check when running on-demand compliance check.
   - OPSWAT Client remembers local SDP login ID between SDP sessions.
   - Added SDP shortcut to Windows Start menu.
   - Enhanced some security issues.
4. Built-in SDK signature version: 4.3.2411.0

#### **Windows On-demand (7.3.646.0)**

1. Bugs fixed
   - OPSWAT Client could not retrieve the old Device ID when running OD client with Horizon.
   - OPSWAT Client displayed wrong color tray icon when using light mode in Windows 10.
   - OPSWAT Client sometimes cannot run Custom check on Windows 10.
2. Enhancements:
   - OPSWAT Client runs custom check when running on-demand compliance check.
   - OPSWAT Client supports communication with TLS 1.3 + SAN certificate servers.
   - Enhanced some security issues.
3. Built-in SDK signature version: 4.3.2411 .0

#### **macOS Persistent (10.4.350.0)**

1. Bug fixed
   - OPSWAT Client sometimes crashed
2. Enhancements:
   - OPSWAT Client runs custom check when running on-demand compliance check.
3. Built-in SDK signature version: 4.3.2068 .0

#### **macOS On-demand (10.5.282.0)**

1. Bug fixed
   - OPSWAT Client sometimes crashed.
2. Enhancements:
   - OPSWAT Client runs custom check when running on-demand compliance check.
3. Built-in SDK signature version: 4.3.2068 .0

## Release Date: September 15, 2021

**Windows Persistent Client (7.6.488.0)**

1. OPSWAT Client User Interface (UI):
   - Enhance loading speed of protected apps
   - New look of malware detection page
   - OPSWAT Client UI supports export scan logs
   - OPSWAT Client UI supports Tutorial of SDP
2. Bugs fixed:
   - OPSWAT Client caused high CPU when scanning
   - OPSWAT Client wasn't able to copy files to destination includes environment variable
   - OPSWAT Client wasn't able to copy files to destination having long path name
   - OPSWAT Client service restarted unexpectedly
   - OPSWAT Client showing wrong message when uploading file to MD Vault
   - OPSWAT Client returned Not Found error on Cross domain API
3. Enhancements
   - Added more support to rebrand on App UI
   - Added more details in scan report
   - Enhanced some security issues
4. Built-in SDK signature version: 4.3.2348.0

**Windows On-demand Client ( 7.3.640.0)**

1. Enhancements:
   - Support multi on-demand instance
   - Added new CLI parameter to reset device compliant status when starting OnDemand agent
   - Enhanced some security issues
2. Bugs fixed:
   - OPSWAT Client returned Not Found error on Cross domain API
3. Built-in SDK signature version: 4.3.2348.0

**macOS Persistent Client ( 10.4.343.0)**

1. Enhancements:
   - Enhanced some security issues
2. Built-in SDK signature version: 4.3.1949.0

**macOS On-demand ( 10.5.272.0)**

1. Enhancements:
   - Support multi on-demand instance
   - Enhanced some security issues
2. Built-in SDK signature version: 4.3.1949.0

## Release Date: August 4, 2021

**Windows Persistent Client (7.6.472.0)**

1. Privacy Data: the client will not report missing patches if a policy doesn't enable missing patches check and an account turns on the application setting under *Settings > Global > Account > Privacy Settings*.
2. Bugs fixed:
   - OPSWAT Client service stuck in "Starting" state.
   - OPSWAT Client wasn't working with proxies that couldn't manage certification revocation lookups.
   - OPSWAT Client tray icon wouldn't always update to the current OPSWAT Client status.
   - OPSWAT Client wasn't reporting its version when the Compliancy scan was disabled.
   - OPSWAT Client's update process.
   - OPSWAT Client UI not handling screen resolutions properly.
3. Enhancements:
   - Added support to elevate the command line scanner's (mdcl-cli.exe) priority via a new "process_priority=[real_time|high|above_normal|normal|low]" parameter.
   - Support the ability to disable scanning files when copying to external media.
   - OPSWAT Client now has the newest UI, including integration of the SDP UI into the OPSWAT Client.
   - New rebranding package has been updated
4. Built-in SDK signature version: 4.3.2277.0

**Windows On-demand Client (7.3.626.0)**

1. Privacy Data: the client will not report missing patches if a policy doesn't enable missing patches check and an account turns on the application setting under *Settings > Global > Account > Privacy Settings*.
2. Bugs fixed:
   - OPSWAT Client service stuck after restarting.
   - OPSWAT Client wasn't working with proxies that couldn't manage certification revocation lookups.
3. Enhancements:
   - Support the ability to disable scanning files when copying to external media.
4. Built-in SDK signature version: 4.3.2277.0

**macOS Persistent Client (10.4.328.0)**

1. Privacy Data: the client will not report missing patches if a policy doesn't enable missing patches check and an account turns on the application setting under *Settings > Global > Account > Privacy Settings*.
2. Bugs fixed:
   - OPSWAT Client tray icon wouldn't always update to the current OPSWAT Client status.
   - OPSWAT Client needs to properly report unsupported apps in the Vulnerabilities report.
3. Enhancements:
   - OPSWAT Client now support the Parallels VM system.
4. Built-in SDK signature version: 4.3.1904.0

**macOS On-demand (10.5.256.0)**

1. Privacy Data: the client will not report missing patches if a policy doesn't enable missing patches check and an account turns on the application setting under *Settings > Global > Account > Privacy Settings*.
2. Bugs fixed:
   - OPSWAT Client needs to properly report unsupported apps in the Vulnerabilities report.
3. Enhancements:
   - OPSWAT Client now supports the Parallels VM system.
4. Built-in SDK signature version: 4.3.1904.0

## Release Date: June 8, 2021

**Windows Persistent Client (7.6.459.0)**

1. Support uninstalling the OPSWAT Client with a password via the command-line.
2. Added additional anti-tampering features:
   - Disable option stop/restart service on Service Manager.
   - Require a password (via CLI command) to stop OPSWAT Client's services.
3. Provide a Client tray-icon menu to export log files to the desktop.
4. Updated Client tray-icon to reflect device status.
5. Removed unneeded Mozilla Firefox components.
6. Bugs fixed:
   - The client reported patch management and other applications even when the application privacy setting is turned on and those are not enabled on a policy.
   - Properly apply branding package for tray-icon when App UI is disabled and re-enabled again.
   - USB is not accessible after disabling Removable Media Protection feature.
   - Copy from network share to USB was not working.
   - Tray icon on the client was missing.
7. Built-in SDK signature version: 4.3.2212 .0

**Windows On-demand Client (7.3.615.0)**

1. Provide a Client tray-icon menu to export log files to the desktop, thereby, making it easier for users to send logs.
2. Updated Client tray-icon to reflect device status.
3. Removed Mozilla Firefox components.
4. Bugs fixed:
   - The client reported patch management and other applications even when application privacy setting is turned on and those are not enabled on a policy.
5. Built-in SDK signature version: 4.3.2212 .0

**macOS Persistent Client (10.4.325.0)**

1. Provide a Client tray-icon menu to export log files to the desktop, thereby, making it easier for users to send logs.
2. Updated Client tray-icon to reflect device status.
3. Bugs fixed:
   - The client always reported patch management and other applications even when the application privacy setting is turned on and those are not enabled on a policy.
   - The client set its keychain as a default keychain sometimes.
   - SDP is not removed when the Client is uninstalled.
4. Built-in SDK signature version: 4.3.1734.0

**macOS On-demand Client (10.5. 254 .0)**

1. Provide a Client tray-icon menu to export log files to the desktop, thereby, making it easier for users to send logs.
2. Updated Client tray-icon to reflect device status.
3. Bugs fixed:
   - The client always reported patch management and other applications even when the application privacy setting is turned on and those are not enabled on a policy.
   - The client set its keychain as a default keychain sometimes.
   - SDP is not removed when the Client is uninstalled.
4. Built-in SDK signature version: 4.3.1734.0

## Release Date: April 21, 2021

**Windows Persistent Client (7.6.453.0)**

1. Only reports applications in categories enabled in a policy if an account turns on privacy setting for applications
2. Support rebranding OPSWAT Client UI
3. Support s can file when copying from PC to USB
4. Bugs fixed:
   - The client did not update a device's active MAC address in registry
5. Built-in SDK signature version: 4.3.2140.0

**Windows On-demand Client (7.3.608.0)**

1. OPSWAT Client only reports applications in categories enabled in a policy if an account turns on privacy setting for applications
2. Built-in SDK signature version: 4.3.2140.0

**macOS Persistent Client (10.4.319.0)**

1. OPSWAT Client only reports applications in categories enabled in a policy if an account turns on privacy setting for applications
2. Bugs fixed:
   - The client could not run a custom check sometimes
3. Built-in SDK signature version: 4.3.1734.0

**macOS On-demand Client (10.5.252.0)**

1. OPSWAT Client only reports applications in categories enabled in a policy if an account turns on privacy setting for applications
2. Bugs fixed:
   - The client could not run a custom check sometimes
3. Built-in SDK signature version: 4.3.1734.0

## Release: March 16, 2021

**Windows Persistent Client (7.6.441.0)**

1. The agent auto-upgrades SDK based on the SDK auto-upgrade setting on an account.
2. Support users to scan files/folders with MetaDefender from the command line.
3. Support malware scan with MetaDefender on boot sectors.
4. Bugs fixed:
   - The client could not upgrade itself sometimes.
   - The Cross-domain API didn't work well when a user have not rebooted a device for a long time.
   - SDP service was auto-restarted once a day.
5. Built-in SDK signature version: 4.3.1748.0
6. Known issues:
   - Windows 7 and Windows Server 2008 devices must install [KB2533623](https://support.microsoft.com/en-us/help/2533623/microsoft-security-advisory-insecure-library-loading-could-allow-remot) and [KB3033929](https://support.microsoft.com/en-us/help/3033929/microsoft-security-advisory-availability-of-sha-2-code-signing-support) in order to upgrade to the latest version.
   - If a user exits the agent tray icon, the agent can’t popup approved actions when a user inserts a portable media.
   - A user needs to enable Show Notifications on the agent tray icon to see notifications about portable media.
   - The agent has not supported the portable media feature if user 2 logs into a device while user 1 is still logged in.
   - OPSWAT Client does not support iTunes drive. If a user inserts an iOS device on an endpoint that has iTunes installed, the user will still have access to the phone via iTunes.
   - OPSWAT Client can't detect mobile devices, the user needs to unplug and plug in the mobile device again.

**Windows On-demand Client (7.3.598.0)**

1. Add new CLI arguments
   - */compliance_check <value>:* specifies which compliance check (health check, scan malware with MetaDefender, patch management) the client should do when a user runs the client with the runonce option.
   - /notrayicon: tells the client to hide the OPSWAT Client tray icon
2. Support on-demand compliance check triggered from MetaAccess/OPSWAT Central Management console.
3. Support malware scan with MetaDefender on boot sectors
4. Bugs fixed:
   - The client failed to start if a product name in the runwhile option has spaces
   - The Cross-domain API didn't work well when a user have not rebooted a device for a long time.
5. Built-in SDK signature version: 4.3.1748.0

**macOS Persistent Client (10.4.317.0)**

1. The agent auto-upgrades SDK based on the SDK auto-upgrade setting on an account
2. Built-in SDK signature version: 4.3.1532.0

**macOS On-demand Client (10.5.250.0)**

1. Add new CLI arguments
   - */compliance_check <value>:* specifies which compliance check (health check, scan malware with MetaDefender, patch management) the client should do when a user runs the client with the runonce option.
   - /notrayicon: tells the client to hide the OPSWAT Client tray icon
   - /skip_request_files_permission <0|1>: tells the client to skip requesting permission from users
2. Support on-demand compliance check triggered from MetaAccess/OPSWAT Central Management console.
3. Built-in SDK signature version: 4.3.1532.0

## Release: February 02, 2021

**Windows Persistent Client (7.6.429.0)**

1. Custom script
   - Secure a custom script when the OPSWAT Client executes the script. Note that this is only applied for a single script.
   - Check integrity of a custom script when the OPSWAT Client executes the script.
2. Removable media protection
   - Ignore removable media that is not formatted based on a policy settings.
   - Add support Kanguru Defender Manager Elite USB+.
3. Client User Interface:
   - Enhanced a rebranding package settings to allow admins to hide/show app management screen on the Client UI. This feature is only available to customers who licensed either MetaAccess/OCM.
   - Enhanced user experience.
4. Minor enhancements:
   - Support Chinese in the Advanced Malware Scan report.
   - Report a log to MetaAccess/OCM servers when the client blocks a removable media device.
5. Bugs fixed:
   - The client did not terminate powershell process if a user uninstalls the client while the client is executing the custom script
6. Built-in SDK signature version: 4.3.1714.0
7. **Known issues:**
   - Windows 7 and Windows Server 2008 devices must install [KB2533623](https://support.microsoft.com/en-us/help/2533623/microsoft-security-advisory-insecure-library-loading-could-allow-remot) and [KB3033929](https://support.microsoft.com/en-us/help/3033929/microsoft-security-advisory-availability-of-sha-2-code-signing-support) in order to upgrade to the latest version.
   - If a user exits the agent tray icon, the agent can’t popup approved actions when a user inserts a portable media.
   - A user needs to enable Show Notifications on the agent tray icon to see notifications about portable media.
   - The agent has not supported portable media feature if user 2 logs into a device while user 1 is still logged in.
   - OPSWAT Client does not support iTunes drive. If a user inserts an iOS device on an endpoint which has iTunes installed, the user will still have access to the phone via iTunes.
   - OPSWAT Client can't detect mobile devices, the user needs to unplug and plug in the mobile device again.

**Windows On-demand Client (7.3.588.0)**

1. Custom script
   - Secure a custom script when the OPSWAT Client executes the script. Note that this is only applied for a single script.
   - Check integrity of a custom script when the OPSWAT Client executes the script.
2. Minor enhancement:
   - Support both runwhile and runone options in the command line. The client will exit if either the client has done the first device compliance check or conditions in the runwhile option are met.
3. Bugs fixed:
   - The client did not terminate powershell process if a user uninstalls the client while the client is executing the custom script.
   - The client did not popup the remediation page with runonce 3 option even malware is detected.
4. Built-in SDK signature version: 4.3.1714.0

**macOS Persistent Client (10.4.313.0)**

1. Custom script
   - Secure a custom script when the OPSWAT Client executes the script. Note that this is only applied for a single script.
   - Check integrity of a custom script when the OPSWAT Client executes the script.
2. Built-in SDK signature version: 4.3.1532.0

**macOS On-demand Client (10.5.246.0)**

1. Custom script
   - Secure a custom script when the OPSWAT Client executes the script. Note that this is only applied for a single script.
   - Check integrity of a custom script when the OPSWAT Client executes the script.
2. Minor enhancement:
   - Now support both runwhile and runone options in the command line. The client will exit if either the client has done the first device compliance check or conditions in runwhile option meet.
3. Built-in SDK signature version: 4.3.1532.0

## Release: December 28, 2020

**Windows On-demand Client (7.3.558.0)**

1. Fixed an issue that OPSWAT Client cannot run cross domain API on non-admin on-demand agent
2. Built-in SDK signature version: 4.3.1646.0

## Release: December 23, 2020

**Windows Persistent Client (7.6.391.0)**

1. Support anti-keylogger and screen capture protection on a device based on a policy. When a user takes a screenshot, the user will see a message that (s)he is not allowed to take a screen shot.
2. Introduce OPSWAT Client User Interface to allow users interact with
   1. Malware Detection: Users can on-demand scan a device based on the policy settings or other options, such as Full scan, Memory scan, custom scan User can view history scan
   2. Removable Media: Users can view what media OPSWAT Client is blocking and perform allowed actions on a media Users can view action history
   3. App management: Users can view all applications installed on a device. The OPSWAT Client lets users know status of each app (out of date, vulnerable status) Users can upgrade or uninstall an application in one single pane of glass. 3.
3. Support retain the last group the device was assigned to for next time it enrolls to an account.
4. Security enhancement: change the algorithm used to store/exchange sensitive data that secures your account.
5. Minor enhancements: support ignore_raw_media to allow users burn CD/DVD
6. Bugs fixed:
   1. The client reported wrong version.
   2. The client was not signed properly. This caused a user gets a popup when the client runs sometime.
   3. The client didn't send report if it's failed to get configuration from MetaAccess/OCM.
   4. The client couldn't deploy or upgrade SDP component if the logged in user is a standard user.
7. 7. Built-in SDK signature version: 4.3.1646.0

## Release: December 15, 2020

**Windows Persistent ( 7.6.374.0)**

1. Fixed an issue that the client failed to upgrade to a newer version and couldn't start again.
2. Enhanced the OPSWAT Client to support run multiple scripts for custom check. The admin needs to upload a zip package that includes multiple scripts.
3. Support setting for open report file after scanning
4. Fix CD/DVD burning issue
5. Built-in SDK signature version: 4.3.1614.0

**Windows Ondemand (7.3.541.0)**

1. Enhanced the OPSWAT Client to support run multiple scripts for custom check. The admin needs to upload a zip package that includes multiple scripts.
2. Built-in SDK signature version: 4.3.1614.0

## Release: October 28, 2020

**Windows Persistent Client (7.6.350.0)**

1. Enhanced communication to MetaAccess/OPSWAT Central Management servers.
2. Skip scanning a file based on file exception setting configured on a policy. This setting is only available on OPSWAT Central Management 7.10+.
3. Security enhancement.
4. Built-in SDK signature version: 4.3.1513.0
5. **Known issues:**
   - Windows 7 and Windows Server 2008 devices must install [KB2533623](https://support.microsoft.com/en-us/help/2533623/microsoft-security-advisory-insecure-library-loading-could-allow-remot) and [KB3033929](https://support.microsoft.com/en-us/help/3033929/microsoft-security-advisory-availability-of-sha-2-code-signing-support) in order to upgrade to the latest version
   - If a user exits the agent tray icon, the agent can’t popup approved actions when a user inserts a portable media
   - A user needs to enable Show Notifications on the agent tray icon to see notifications about portable media
   - The agent has not supported portable media feature if user 2 logs into a device while user 1 is still logged in
   - OPSWAT Client does not support iTunes drive. If a user inserts an iOS device on an endpoint which has iTunes installed, the user will still have access to the phone via iTunes
   - OPSWAT Client can't detect mobile devices, the user needs to unplug and plug in the mobile device again

**Windows On-demand Agent (7.3.525.0)**

1. Enhanced communication to MetaAccess/OPSWAT Central Management servers.
2. Skip scanning a file based on file exception setting configured on a policy. This setting is only available on OPSWAT Central Management 7.10+.
3. Security enhancement.
4. Built-in SDK signature version: 4.3.1513.0

**macOS Persistent Agent (10.4.294.0)**

1. Skip scanning a file based on file exception setting configured on a policy. This setting is only available on OPSWAT Central Management 7.10+.
2. Built-in SDK signature version: 4.3.1415.0

**macOS on-demand Agent (10.5.222.0)**

1. Skip scanning a file based on file exception setting configured on a policy. This setting is only available on OPSWAT Central Management 7.10+.
2. Built-in SDK signature version: 4.3.1415.0

## Release Date: August 18, 2020

**Windows Persistent Client (7.6.330.0)**

1. Custom script can be run as a defined privilege in a policy which the device is assigned to.
2. Custom script is now stored in a secure form instead of plain text.
3. Add a signature to a cross-domain API's response to allow 3rd party to validate whether the API response comes from OPSWAT Client.
4. Report what OPSWAT Client copied from local drives to a removable media if the devices are assigned to a policy that enables this feature.
5. Bug Fixed:
   - OPSWAT Client couldn't connect to the server if the device was removed because it had stayed unseen for a long time on the server.
   - Users couldn't open sanitized files OPSWAT Client copied due to the client having created the new files with system privilege.
   - The client sometimes didn't show the **Action Required** message even if the device has issues and is non-compliant.
   - Memory leak in OPSWAT Client.
   - File path was shown incorrectly if it includes Hebrew characters.
6. Updated built-in SDK signature: 4.3.1416.0
7. **Known issues:**
   - Windows 7 and Windows Server 2008 devices must install [KB2533623](https://support.microsoft.com/en-us/help/2533623/microsoft-security-advisory-insecure-library-loading-could-allow-remot) and [KB3033929](https://support.microsoft.com/en-us/help/3033929/microsoft-security-advisory-availability-of-sha-2-code-signing-support) in order to upgrade to the latest version.
   - If a user exits the agent tray icon, the agent can’t popup approved actions when a user inserts a portable media.
   - A user needs to enable the **Show Notifications** option on the agent tray icon to see notifications about portable media.
   - The agent does not support portable media feature if a second user logs into a device while a first user is still logged in.
   - OPSWAT Client does not support iTunes drive. If a user inserts an iOS device on an endpoint which has iTunes installed, the user will still have access to the phone via iTunes.
   - If OPSWAT Client can't detect the plugged-in mobile device, the user needs to unplug and plug in the mobile device again.

**Windows On-demand Agent (7.3.507.0)**

1. Custom script can be run as a defined privilege in a policy which the device is assigned to. If the specified privilege in the policy is higher than the privilege the client runs as, it will try to run as the higher privilege if allowed.
2. Custom script is now stored in a secure form instead of plain text.
3. Add a signature to a cross-domain API's response to allow 3rd party to validate whether the API response comes from OPSWAT Client.
4. Bugs fixed
   - OPSWAT Client couldn't connect to the server if the device was removed due to unseen for a long time on the server.
   - The client sometimes didn't show the **Action Required** message even if the device has issues and is non-compliant.
5. Updated built-in SDK signature: 4.3.1416.0

**macOS Persistent Agent (10.4.289.0)**

1. Custom script can be run as a defined privilege in a policy which the device is assigned to. If the specified privilege in the policy is higher than the privilege the client runs as, it will try to run as the higher privilege if allowed.
2. Custom script is now stored in a secure form instead of plain text.
3. Add a signature to a cross-domain API's response to allow 3rd party to validate whether the API response comes from OPSWAT Client.
4. Bugs fixed
   - The client couldn't upgrade sometimes.
   - The client didn't popup the remediation page when the device is non-compliant after the fresh installation.
5. Updated built-in SDK signature: 4.3.1301.0

**macOS on-demand Agent (10.5.217.0)**

1. Custom script can be run as a defined privilege in a policy which the device is assigned to. If the specified privilege in the policy is higher than the privilege the client runs as, it will try to run as the higher privilege if allowed.
2. Custom script is now stored in a secure form instead of plain text.
3. Add a signature to a cross-domain API's response to allow 3rd party to validate whether the API response comes from OPSWAT Client.
4. Bugs fixed
   - The client didn't popup the remediation page when the device is non-compliant after a fresh installation.
5. Updated built-in SDK signature: 4.3.1301.0

---

[All pages in this documentation](https://www.opswat.com/docs/mdendpoint/llms.txt)
