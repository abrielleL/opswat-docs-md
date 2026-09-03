<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/knowledge-base/how-do-i-troubleshoot-adconnector-issues -->

# How do I troubleshoot ADConnector issues?

This article applies to the current NAC API, and NAC AD Connector Service installed on Windows Server

## [Issue: The ADConnector does not seem to be sending Single Sign-On events](/docs/manac/nac-v8.1.1/knowledge-base/how-do-i-troubleshoot-adconnector-issues#issue-the-adconnector-does-not-seem-to-be-sending-single-sign-on-events)

1. Ensure that logon events (Event ID: 4624) are appearing in the security logs by going to **Event Viewer>Windows Logs>Security**, as illustrated in the image below.

- Under the **Details** tab, you should see the username and IP address listed as **TargetUserName** and **IpAddress** respectively.

2. Ensure that your security event log is not too full as, if it is, the ADConnector will no longer forward data.

- To adjust your logging settings, open the **Event Viewer>Windows Logs**, right-click on **Security** and select the **Properties** option.
- In the dialog window, ensure that the **Maximum** log size is sufficient for your system, and that either **Overwrite events as needed (older events first)** or **Archive the log when full, do not overwrite events** is selected, as illustrated below.

3. Check that the **Connector** is pointing to the internal IP address of the NAC appliance.

- Open **Windows Registry Editor** and ensure that **HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\ADConnector\serverURL** is pointed to the internal IP address of the appliance.
- The URL should be in the format of **http://<ip_address>:8090/restfulservices/addUpdateSession**.
- Replace **<ip_address>** with the actual internal IP address of the NAC appliance. In a cluster environment, this will be the **sessiontracker manager.**

4. If all else fails, enable debug logging, then send the **Debug Log** to **OPSWAT Support** as outlined in the support box at the end of this article.

- To enable the debug log, create a new **DWORD** value in **HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\ADConnector**, entitled **Log**, then set its value to **5**.
- Once the **DWORD** value is created, **Restart** the **ADConnector** service. This will create a file named **ADSSO_Log.txt** (or **ADConnector_Log.txt** in later versions) in the install location (**C:\Program Files\OPSWAT\ADConnector** by default).
- Once the log file is generated, set the value of the new registry key back to **0** to disable debug logging.

5. If the **ADDSO_Log.txt** (or **ADConnector_Log.txt**) file contains the following entry, this is due to a Powershell restriction that is preventing the installer from creating a necessary registry key.

logCopy[2/14/2017 10:13:02 AM] at System.Convert.FromBase64String(String s)
at ADEventListener.ADEventWatcher.Start()Note for long-time customers

If your NAC deployment was setup before 2020, occurrences of "OPSWAT" in paths above may appear as "ImpulsePoint" on your system.

To remediate the issue, follow the instructions below.

- Open a **Powershell** as administrator.
- Run the command **Get-Executionpolicy** to see the current execution policy setting.

- If it is restricted, as in the example above, run the command **Set-Executionpolicy Unrestricted**, then confirm with **Y**.

- Now, re-run the **Windows Services Installer**, then return to **Powershell**.
- Run the command **Set-Executionpolicy Restricted** to change the settings back to a secure state.

## [Issue: The ADConnector service does not start automatically on reboot](/docs/manac/nac-v8.1.1/knowledge-base/how-do-i-troubleshoot-adconnector-issues#issue-the-adconnector-service-does-not-start-automatically-on-reboot)

1. Open Services and search for a service named **ADConnector**.
2. Ensure that the **Startup Type** is listed as **Automatic (Delayed Start)**.

Note for long-time customers

If your NAC deployment was setup before 2020, the service in the screenshot above may be named "Impulse Point ADConnector" instead of just "ADConnector"

Support:

If you have followed the instructions above but continue to experience difficulties when **Troubleshooting ADConnector Issues**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
