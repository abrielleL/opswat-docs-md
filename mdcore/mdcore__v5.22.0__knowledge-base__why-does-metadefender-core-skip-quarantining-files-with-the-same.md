<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/why-does-metadefender-core-skip-quarantining-files-with-the-same -->

# Why does MetaDefender Core skip quarantining files with the same hash?

This article applies to all MetaDefender Core releases deployed on Windows and Linux systems.

After scanning a known malicious file:

- The first instance of the file is successfully quarantined.
- A second instance of the same file (from another device or scan) is blocked, but not added again to the quarantine repository.
- Users may wonder why the second file does not appear in quarantine storage.

### [**Resolution:**](/docs/mdcore/v5.22.0/knowledge-base/why-does-metadefender-core-skip-quarantining-files-with-the-same#resolution)

No action is required. The system’s skipping of duplicate quarantine entries is:

- Expected by design.
- Safe, since blocking and handling still occur as configured.
- Reduce disk space consumption.

As a result, there is no supported configuration to change this quarantine behavior.

### [**Best practice**](/docs/mdcore/v5.22.0/knowledge-base/why-does-metadefender-core-skip-quarantining-files-with-the-same#best-practice)

- Keep hash calculation enabled in workflows
- Do not modify quarantine behavior unless directed by OPSWAT Support
- Validate failures by checking that blocked files are removed from the source device

Support:

If you require further assistance, please follow these instructions on [How to Create Support Package?](https://www.opswat.com/docs/mdcore/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/support).
