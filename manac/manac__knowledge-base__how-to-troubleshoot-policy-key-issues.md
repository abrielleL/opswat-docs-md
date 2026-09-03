<!-- source: https://www.opswat.com/docs/manac/knowledge-base/how-to-troubleshoot-policy-key-issues -->

# How to Troubleshoot Policy Key Issues?

Important Policy Key announcements:

[NAC announcements](https://docs.opswat.com/manac/release-notes/announcements#announcement)

## [Problem: Incorrectly Failing for 'Policy Key is not Installed'](/docs/manac/knowledge-base/how-to-troubleshoot-policy-key-issues#problem-incorrectly-failing-for-policy-key-is-not-installed)

### [Solution 1: Is the Policy Key installed correctly?](/docs/manac/knowledge-base/how-to-troubleshoot-policy-key-issues#solution-1-is-the-policy-key-installed-correctly)

On Windows:

1. Open File Explorer.
2. Navigate to 'C:\Program Files(x86)'
3. Ensure the directory SafeConnect exists.
4. Ensure there is a file in the directory called SCClient.exe. If not, re-install the policy key and restart the device.

On Mac:

1. Open Finder and choose Applications.
2. Check if an application exists called SafeConnect.
3. Right click the application and select "Show Package Contents".
4. Ensure that under Contents > MacOS, there exists a file called scClient and scManagerD If not, re-install the policy key and restart the device.

### [Solution 2: Is the Policy Key running?](/docs/manac/knowledge-base/how-to-troubleshoot-policy-key-issues#solution-2-is-the-policy-key-running)

On Windows:

1. Open the Task Manager and navigate to the Processes tab.
2. Check the box “Show processes from all users” at the bottom left.
3. Click on the “Name” column heading to sort.
4. Look for SafeConnectClient.exe and scManager.sys, both should be present.

On Mac:

1. Open Activity Monitor (Finder > Applications > Utilities > Activity Monitor).
2. Choose “Show All Processes” under the "View" menu Click on the “ProcessName” column heading to sort.
3. Look for two services named "SafeConnect", one ran by the Admin user and one by the root user. Both should be present.
4. If you have only recently installed the Macintosh Policy Key, both processes may be called SafeConnect.

### [Solution 3: If the Policy Key is running, but still failing incorrectly.](/docs/manac/knowledge-base/how-to-troubleshoot-policy-key-issues#solution-3-if-the-policy-key-is-running-but-still-failing-incorrectly)

- **Check the device's time and date**

  - If the device's time and/or date is incorrect, update the system time and/or date to current and restart the machine.
- **Check Windows Updates**

  - If there are any Windows Updates pending, complete those updates and check to see if the Policy Key is working again.
- **Ensure Anti-Virus/Firewall is not impeding Policy Key communication**

  - Add an exemption to any Anti-Virus or Firewall for the directory "Program Files(x86)\SafeConnect" and/or the file "ServiceInstaller.exe" within that directory.

### [Solution 4: If the Policy Key is not running](/docs/manac/knowledge-base/how-to-troubleshoot-policy-key-issues#solution-4-if-the-policy-key-is-not-running)

- **Check Anti-Virus Quarantine section**

  - In some cases, an Anti-Virus might quarantine files that are required by the Policy Key. Confirm that within your Anti-Virus program's quarantine section, there are no files/directories that have a name of SafeConnect or SCClient.
- **Ensure the policy key is set for startup**

  - **PC:**

    - Enter "msconfig"
    - Click on the "Startup" tab
    - Sort by the "Name" column and find SafeConnect/SCClient

      - **If you cannot find SafeConnect in startup:**

        - Navigate to C:\Program Files(x86)\SafeConnect
        - Right click on "SafeConnectClient.exe" and select "Create Shortcut"
        - Right click on the file and select "Cut" or use keyboard shortcut CTRL + X
        - Press Win + R
        - Enter "shell:startup"
        - Right click and select "Paste" or use keyboard shortcut CTRL + V Restart the device
  - **MAC:**

    - Open System Preferences and click "Users & Groups"
    - Click Login Items
    - Ensure SafeConnect/SCClient exists there
    - **If you cannot find SafeConnect in startup:**

      - Click the + icon in the "Login Items" tab you previously navigated to
      - Choose "Applications" from the left panel and click on SafeConnect Click Add

*If the above is resolved or working as it should and the issue is still happening, follow the steps below.*

### [Solution 5: Ensure the device does not have Malware](/docs/manac/knowledge-base/how-to-troubleshoot-policy-key-issues#solution-5-ensure-the-device-does-not-have-malware)

- Run an Anti-Virus scan using a known Anti-Virus
- Run an Anti-Malware scan (Malwarebytes is an option for this)
- Ensure no Malware is found

**Do you see a certificate error or connection error when navigating to the Policy Key Download Page during the time the device is failing policy (Not in open access)?** A certificate error is shown:

- This may indicate that the endpoint does not have the "Go Daddy Class 2 Certification Authority Root Certificate" installed. Please ensure you have the latest OS updates applied to your system.
- You can download and install this certificate from godaddy's website: Godaddy Root Certificate

  - **A connection error occurs**

    - This may indicate that the endpoint does not have a proper route to the SafeConnect appliance or an alternate network connection issue is occurring.
    - In this case, please submit a ticket to OPSWAT Support with a Policy Key log at level 5, as shown below and please provide OPSWAT

*Support the error shown when attempting to reach the Policy Key download page, preferably in a screenshot:* [*my.opswat.com*](https://my.opswat.com)

- **To collect a policy key log**

  - Navigate to the necessary location based off your OS

    - Windows: "Program Files(x86)\SafeConnect"
    - MAC: Applications > Right click SafeConnect > Click "Show Package Contents" > Contents/MacOS
  - Policy Key logging is written to `LogFile.txt` in this directory.
- **If you are requested to enable further debugging (Log Level 5) for the Policy Key by OPSWAT Support**

  - Update the config.xml file with the following values: `<LoggingLevel>5</LoggingLevel><LoggingLimit>50240</LoggingLimit>`
  - Wait for the issue to occur again
  - Wait a few minutes after the issue occurs and save`LogFile.txt` to upload to support ticket at The Support Portal
- **If you do not see a LogFile.txt in that directory after 5-10 minutes**

  - Try re-downloading the Policy Key from your SafeConnect appliance and/or rebooting the machine. Then, you will need to set the logging level again.

*If this article was unable to solve your problem, please submit a support ticket at OPSWAT portal with the policy key log attached.*
