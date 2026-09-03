<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/why-are-metadefender-core-and-postgresql-services-shutting-down- -->

# Why are MetaDefender Core and PostgreSQL services shutting down unexpectedly?

This article applies to all MetaDefender Core releases deployed on Windows.

**Issue:** MetaDefender Core and PostgreSQL services shut down unexpectedly due to the deletion or inaccessibility of the temporary directory `C:\Windows\temp\ometascan\`. This is likely caused by a scheduled system reboot or automated cleanup task that removed or cleared the temporary folder.

**Root Cause:** The root cause was the deletion or inaccessibility of the temporary directory `C:\Windows\Temp\ometascan\` used by nginx. Investigation and identification of the scheduled task/script that triggered the shutdown and the missing temp folder issue, confirmed by log analysis and event viewer data, was key to the solution.

**Resolution:** Ensure that the temporary directory `C:\Windows\Temp\ometascan\` is not deleted or cleared by any scheduled tasks, cleanup tools, antivirus software, or group policies.

**Prevention:**

- Ensure that the temporary directory `C:\Windows\Temp\ometascan\` is not deleted or cleared by any scheduled tasks, cleanup tools, antivirus software, or group policies.
- Review and modify scheduled tasks or scripts running to prevent them from removing or interfering with the MetaDefender Core temporary folder.
- Exclude the MetaDefender Core installation path (`C:\Program Files\OPSWAT`) and temporary directory (`C:\Windows\Temp`) from antivirus and security software scans or cleanup routines.
- Monitor and verify that the MetaDefender Core and PostgreSQL services start normally after system reboots or scheduled restarts.
- Collect and review Windows Event Viewer logs related to Task Scheduler to identify any tasks that might affect the service.
- Follow OPSWAT’s recommended system configuration guidelines and antivirus exclusion instructions available at: [Recommended System Configuration](/docs/mdcore/v5.21.0/installation/recommended-system-configuration)

**Workarounds:** Restart the MetaDefender Core service manually if it fails to start automatically, ensuring it is run under an account with appropriate permissions (e.g., Administrator).

**Steps to Resolve:**

- Review and modify scheduled tasks or scripts running to prevent them from removing or interfering with the MetaDefender Core temporary folder.
- Exclude the MetaDefender Core installation path (`C:\Program Files\OPSWAT`) and temporary directory (`C:\Windows\Temp`) from antivirus and security software scans or cleanup routines.
- Monitor and verify that the MetaDefender Core and PostgreSQL services start normally after system reboots or scheduled restarts.
- Collect and review Windows Event Viewer logs related to Task Scheduler to identify any tasks that might affect the service.
- Follow OPSWAT’s recommended system configuration guidelines and antivirus exclusion instructions available at: [Recommended System Configuration](/docs/mdcore/v5.21.0/installation/recommended-system-configuration)
- If the temporary folder is missing, investigate what process or script is removing it and disable or adjust that process accordingly.
- Restart the MetaDefender Core service manually if it fails to start automatically, ensuring it is run under an account with appropriate permissions (e.g., Administrator).
- Keep the MetaDefender Core updated and monitor logs for any recurring errors.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
