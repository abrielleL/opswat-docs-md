<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/knowledge-base/how-do-i-troubleshoot-dhcp-syslog-service-issues -->

# How do I troubleshoot DHCP Syslog Service issues?

This article applies to latest NAC DHCP Syslog service installed on Windows Server.

## [Issue: DHCP Syslog Service does not start automatically on boot](/docs/manac/nac-v8.1.1/knowledge-base/how-do-i-troubleshoot-dhcp-syslog-service-issues#issue-dhcp-syslog-service-does-not-start-automatically-on-boot)

1. Open Services and search for a service named **DHCP Server**.

2. Ensure that the **Startup Type** is listed as **Automatic (Delayed Start)**.

## [Issue: A range of issues that could be the result of a DHCP logging error](/docs/manac/nac-v8.1.1/knowledge-base/how-do-i-troubleshoot-dhcp-syslog-service-issues#issue-a-range-of-issues-that-could-be-the-result-of-a-dhcp-logging-error)

1. To confirm that DHCP logs are being created, you must first verify the Windows DHCP Server log settings, specifically the location where the DHCP server writes out its log files.
2. To confirm this location, open the **Registry Editor** and locate **HKLM\SYSTEM\CurrentControlSet\Services\DHCPServer\Parameters\DhcpLogFilePath**.
3. If the DHCP Server is under default settings, the key may not be present - this is normal and, in such cases, the log files will be written to **C:/windows/system32/dhcp**.
4. If the key is present, record the location to which the log files are written by noting the path in the **Data** column (highlighted in yellow below).

5. Navigate to the recorded path to confirm the presence of the DHCP Server logs. SafeConnect DHCP Syslog uses this same path to locate the log files.
6. Search the location for log files beginning with **DhcpSrvLog-XXX** (where XXX represents the day of the week).

These logs should be updating in real time, so if the latest **Date Modified** timestamp is more than a minute or two old, the registry key value for “DhcpLogFilesMaxSize” (highlighted in green in screenshot for step 4), may need to be increased.

7. After increasing the value, **Restart** the **DHCP Server** service.

Support:

If you have followed the instructions above but continue to experience difficulties when **Troubleshooting DHCP Syslog Service Issues**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
