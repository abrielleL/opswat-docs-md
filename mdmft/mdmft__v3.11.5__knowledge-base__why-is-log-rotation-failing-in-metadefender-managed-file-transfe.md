<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/knowledge-base/why-is-log-rotation-failing-in-metadefender-managed-file-transfe -->

# Why is Log Rotation Failing in MetaDefender Managed File Transfer?

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool Check Your Version:

This article applies to MetaDefender Managed File Transfer version 3.9.3 releases deployed on Windows systems

**Issue:** When log rotation is configured to **“By Date”**, the rotation process depends on the service running continuously through midnight to trigger the rotation. If the service or machine is stopped and restarted the next day, the rotation does not occur because the process relies on uninterrupted service uptime.

Additionally, there were intermittent process conflicts that caused log rotation and retention to malfunction temporarily. This issue was identified as a bug by the development team and has been **fixed in version 3.10.0**.

**Resolution:**

Upgrade **MetaDefender Managed File Transfer (MD MFT)** to **version 3.10.0**, where the log rotation and retention mechanisms have been fixed.

After upgrading:

1. Configure log rotation according to your preferred method (e.g., **by date** or **by size**).
2. If issues occur when using **rotation by date**, follow these steps:

   - Stop all MD MFT services.
   - Back up and delete all existing log files.
   - Start all MD MFT services again.

This procedure clears potential process conflicts and allows log rotation to resume properly.

**Additional Notes:**

Currently, **log rotation and retention do not apply to the “Helper” and “Caching” logs**. These components primarily monitor internal service operations and are not connected to the database.

However, it is important to note that although these logs are not affected by rotation settings, their size typically remains small — usually **below 50 MB even after several months of use**. This is because:

- They have no retry mechanisms (unlike other services).
- Their logging activity is limited to simple operational status updates.

As such, their growth is minimal, and rotation is generally unnecessary. If full rotation is still required for compliance or storage reasons, you may request an enhancement from the development team.

**Workarounds:** If encountering issues with log rotation by date:

- Stop all MD MFT services.
- Backup and delete all current log files.
- Start all MD MFT services again.

This workaround clears any process conflicts and allows proper log rotation to resume.

**Prevention:** Upgrade MetaDefender Managed File Transfer to version 3.10.0, where the log rotation issues have been fixed.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
