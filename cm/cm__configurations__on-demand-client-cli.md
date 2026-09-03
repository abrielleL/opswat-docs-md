<!-- source: https://www.opswat.com/docs/cm/configurations/on-demand-client-cli -->

# On-demand Client CLI

The On-Demand MetaDefender Endpoint offers a command-line interface that allows a user to control how the on-demand should be run.

Your solution can trigger our agent to run onetime and get device status to grant a device access to your resources. [Pulse Secure integration](https://www.opswat.com/docs/cm/integrations/pulse-secure-s-host-checker) as an example.

## Windows Usage

1. Open a command prompt (as administrator if using admin version)
2. Navigate to the directory containing the On-demand MetaDefender IT Access executable
3. Run the executable with one or more options (license_key and server_code must be provided either in the executable name or in the options), for example:

OPSWAT_GEARS_Client_Admin.exe /key [license_key] /host [server_code] [options]

or

OPSWAT_GEARS_Client_Admin _[server_code]-[license_key].exe [options]

## macOS Usage

1. Open a terminal
2. Navigate to the directory containing the on-demand MetaDefender IT Access zip file
3. Navigate into the compressed archive: $ cd OPSWAT\ GEARS.app/Contents/Resources/
4. Run the executable with one or more options (server_code is required; license_key will be read from the config in the zip file unless provided as an option), for example: $ ./opswat-gears-od /host [server_code] [options]

## Options

| Argument | Value Type | Example | Minimum version |  | Description |
| ---- | ---- | ---- | ---- | ---- | ---- |
|  |  |  | Windows | macOS | Description |
| /silent |  | /silent |  |  | Silent mode. No dialog pop-ups are shown. |
| /log | Number | /log 0 |  |  | **Possible value:** - 0 - Disable logging. - 1 - Enable logging. (Windows: Creates log in executable’s directory. macOS: Creates a log on the current user’s desktop except when running as root). |
| /groupid | String | /groupid group_ID | **7.3.519.0** | **10.5.221.0** | Specify a group ID to assign a device to a group. |
| /key | String | /key license_key |  |  | Specify a MetaDefender IT Access license key (overwrite the license key in the MetaDefender Endpoint's file name if presented; required if not presented in the file name). |
| /host | String | /host server_url |  |  | Specify a server where the MetaDefender Endpoint should connect to (overwrite the server url in the MetaDefender Endpoint's file name if presented; required if not presented in the file name. It should be in HEXA format. You can use any tool to convert a string to a HEXA string. **For example:** if your server URL is [https://ocm.yourdomain.com](https://ocm.yourdomain.com), you should use /host 68747470733a2f2f6f636d2e796f7572646f6d61696e2e636f6d If your devices are connecting to MetaDefender IT Access US tenant, you can use "3445" as a server URL magic code, for example /host 3445 |
| /mkey | String | /mkey metadefender_cloud_key |  |  | Specify a MetaDefender Cloud key to use for malware scanning (overwrite the MetaDefender Cloud key associated with an account that MetaDefender IT Access license key is specified). |
| /quick |  | /quick |  |  | Exclude DLLs and libraries during malware scan. |
| /runonce | Number | /runonce 1 |  |  | Indicate the client should exit after completing a compliance check and malware scan if any. By default, the client continuously runs until a device is restarted or a user exits the client. **Possible value:** - 1 - Run once and exit. Open the remediation page in the default browser only if an unknown device is detected. - 2 - Run once and exit and open the remediation page in a default browser - 3 - Run once and exit and open the remediation page in a default browser if threats are detected - 4 - Run once and exit and open the remediation page in a default browser if the device is non-compliant |
| -/runwhile | String | /runwhile "/p:notepad.exe /o:and /s:1" | **7.3.489.0** | **10.5.212.0** | Indicate the client should run while conditions are still met. Conditions format is "condition [</o[perator]:<and&#124;or> <condition 1> <condition 2> ...]" **Supported conditions:** - /p[rocess]:<process_name>: Run the MetaDefender Endpoint while the process <process_name> is running - /s[tasus]:<0&#124;1>: Run while status is compliant (1) or is non-compliant (0) - *Note:** If both runonce and runwhile arguments are specified, the client will exit when one of the below condition is met: - The client has done compliance check once - specified conditions in runwhile argument are violated. |
| /rempage | Number | /rempage 1 |  |  | Indicate if the client should show a remediation page. This option overrides /runonce option **Possible value:** - 1: show the remediation page - 0: don't show remediation page. |
| /skip_request_files_permission | 0 or 1 |  |  | **10.5.250.0** | Only applies for mac OS client. Skip requesting permission to access specific files/folders on macOS devices. **Possible value:** - 0 (default): always request permission to access specific files/folders on macOS devices - 1: Skip requesting permission to access specific files/folders on macOS devices. In this case, the client will have limited access to files/folder to check compliance and scan those files/folders. |
| /compliance_check | Number | /compliance_check 1 | **7.3.598.0** | **10.5.250.0** | Run compliance check with customized actions. - 1 - Run compliance check with check application security only - 2 - Run compliance check with scan threats only - 3 - Run compliance check with check application security and scan threats - 4 - Run compliance check with check OS update only - 5 - Run compliance check with check application security and OS update - 6 - Run compliance check with scan threats and check OS update - 7 - Run compliance check with check application security, scan threats, and check OS update Only applies for runOnce arguments |
| /notrayicon | n/a | /notrayicon | **7.3.598.0** |  | Only applies for Windows client hide the client's trayicon on system tray |
| /h or /help | n/a | /help |  |  | Show the help menu. |
| /reassessment | 0 or 1 | /reassessment 1 | **7.3.636.0** |  | Reset device compliant status when starting OnDemand agent |
| /trayicon | 0 or 1 | /trayicon 1 |  | **10.5.294.0** | Only applies for macOS client to show or hide the client's tray icon on system tray. - 0 - Hide tray icon. - 1 - Show tray icon |

## Exit Codes

0 No errors.

2 Manual exit.

4 Condition meets: Device status is non-compliant.

5 Condition meets: Device status is compliant.

8 Condition meets: Monitored process exiting.

12 Condition meets: Monitored process exiting and Device status is non-compliant

13 Condition meets: Monitored process exiting and Device status is compliant

## Example

Note: all below examples are using the [OPSWAT MetaDefender IT-OT Access Tenant B](https://www.opswat.com/docs/cm/kb/where-is-metaaccess-hosted-) (/host 3445). If your account is connecting to MetaDefender IT Access Tenant EU or OPSWAT Central Management server, you can use any tools to convert the full URL to a HEXA string. For example

- your account is set up in [https://gears-eu.opswat.com](https://gears-eu.opswat.com), you should use /host 68747470733a2f2f67656172732d6564752e6f70737761742e636f6d
- You use OPSWAT Central Management to manage your devices, and its URL is [https://ocm.yourdomain.com](https://ocm.yourdomain.com), you should use /host 68747470733a2f2f6f636d2e796f7572646f6d61696e2e636f6d

**Case 1:** Run the MetaDefender Endpoint in silent mode while Horizon Client is running and device status is compliant.

- Windows: OPSWAT_GEARS_Client.exe /silent /key your_license_key /host 3445 /runwhile /p:vmware-view.exe /o:and /s:1
