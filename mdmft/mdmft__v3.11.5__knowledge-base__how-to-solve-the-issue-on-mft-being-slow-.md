<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/knowledge-base/how-to-solve-the-issue-on-mft-being-slow- -->

# How to solve the issue of MFT being slow?

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool Check Your Version:

This article applies to MetaDefender MFT Version 3.8.3 releases deployed on Windows systems.

## [Resolving AuditLog and FileAuditLog Flooding in MetaDefender MFT](/docs/mdmft/v3.11.5/knowledge-base/how-to-solve-the-issue-on-mft-being-slow-#resolving-auditlog-and-fileauditlog-flooding-in-metadefender-mft)

### [Overview](/docs/mdmft/v3.11.5/knowledge-base/how-to-solve-the-issue-on-mft-being-slow-#overview)

Certain MetaDefender MFT versions generate excessive entries in `AuditLog` and `FileAuditLog` due to redundant processing of already-deleted files. This behavior can degrade performance and cause significant database bloat.

### [Affected Versions](/docs/mdmft/v3.11.5/knowledge-base/how-to-solve-the-issue-on-mft-being-slow-#affected-versions)

- **Issue 1**: 3.6.3 to 3.7.2
- **Issue 2**: All versions before 3.8.3

### [Fix Versions](/docs/mdmft/v3.11.5/knowledge-base/how-to-solve-the-issue-on-mft-being-slow-#fix-versions)

- **Issue 1 resolved in**: 3.7.3
- **Issue 2 resolved in**: 3.8.3

### [Summary of Issues](/docs/mdmft/v3.11.5/knowledge-base/how-to-solve-the-issue-on-mft-being-slow-#summary-of-issues)

- **Issue 1**: Files marked as "permanently deleted" were unnecessarily reprocessed and logged.
- **Issue 2**: Deleting folders also moved “permanently deleted” files to the Recycle Bin, resulting in toggled states and excessive logging.

## [Recommended Solutions](/docs/mdmft/v3.11.5/knowledge-base/how-to-solve-the-issue-on-mft-being-slow-#recommended-solutions)

### [Automatic Cleanup (from version 3.9.2 onward)](/docs/mdmft/v3.11.5/knowledge-base/how-to-solve-the-issue-on-mft-being-slow-#automatic-cleanup-from-version-392-onward)

Version 3.9.2 introduces a built-in mechanism to automatically clean up these log entries, either during or after installation. While the cleanup script may still be needed in some edge cases, it is generally less preferred compared to this automatic method.

### [Script-Based Cleanup (for affected versions)](/docs/mdmft/v3.11.5/knowledge-base/how-to-solve-the-issue-on-mft-being-slow-#script-based-cleanup-for-affected-versions)

#### [Steps:](/docs/mdmft/v3.11.5/knowledge-base/how-to-solve-the-issue-on-mft-being-slow-#steps)

1. **Stop the MFT services**
2. **Run the cleanup script**:

   - Download the attached script file.
   - Launch **SQL Server Management Studio (SSMS)**.
   - Connect to the MFT database.
   - Open the script (via `File > Open > File` or `Ctrl+O`).
   - Execute the script.
3. **Wait for the script to finish execution.** This may take several minutes, or up to 35–40 minutes, depending on the database size.
4. **Upgrade MFT to version 3.8.3 or higher** if not already done.
5. **Restart the MFT services**

Important:

Always perform a full database backup before running the cleanup script. Contact OPSWAT Support for guidance if needed.

### [In Time-Critical Situations](/docs/mdmft/v3.11.5/knowledge-base/how-to-solve-the-issue-on-mft-being-slow-#in-time-critical-situations)

In rare cases, running the cleanup script may not be acceptable due to performance constraints. In such situations, **removing all audit logs** may be the only feasible option.

Customers should be made aware of the implications of this and should:

- Ensure a **manual database backup** is available for future audits.
- **Syslog integration** is in place, so audit events are retained on the syslog server.

Support:

If you have followed all of the steps above but are still unable to resolve the issue. Please follow these instructions on [Creating Support Packages - MetaDefender Managed File Transfer](https://www.opswat.com/docs/mdmft/troubleshooting/how-to-create-support-package) before [creating a support case or chatting with our support engineer.](https://my.opswat.com/support)
