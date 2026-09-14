<!-- source: https://www.opswat.com/docs/netwalldiode/v1.13.2/knowledge-base/what-is-the-file-handling-behavior-and-protocol-support-in-metad -->

# What is the file handling behavior and protocol support in MetaDefender Optical Diode?

This article applies to all versions of MetaDefender Optical Diode.

### [1. Protocol Support for NAS Access](/docs/netwalldiode/v1.13.2/knowledge-base/what-is-the-file-handling-behavior-and-protocol-support-in-metad#1-protocol-support-for-nas-access)

Q: *Can Optical Diode read files from a NAS using CIFS (SMB) or NFS? And does it support secure transmission methods like NFS 4.1 with Kerberos or NFS 3.0 with TLS?*

| Protocol/Method | Supported |
| --- | --- |
| CIFS (SMB) | Yes |
| NFS | No |
| Kerberos | No |

{% /table %}

### [2. File Transfer Order for Simultaneous Uploads](/docs/netwalldiode/v1.13.2/knowledge-base/what-is-the-file-handling-behavior-and-protocol-support-in-metad#2-file-transfer-order-for-simultaneous-uploads)

Q: *If two users upload files to the same NAS folder at the same time, how does Optical Diode handle the transfers?*

- Files are transferred in the order they arrive, not based on which user uploaded them.
- Optical Diode performs alphanumeric sorting of file names, as returned by the operating system.

  - For example, if three files are detected at once, the one that comes first alphabetically will be transferred first.
- This behavior applies when files are uploaded to the same configured channel on NetWall.

### [3. Handling Large or Slowly Uploaded Files](/docs/netwalldiode/v1.13.2/knowledge-base/what-is-the-file-handling-behavior-and-protocol-support-in-metad#3-handling-large-or-slowly-uploaded-files)

Q: *How does Optical Diode handle large files that take a long time to upload (e.g., over 100 seconds)?*

- Optical Diode waits until the upload is complete before initiating the transfer.
- File handling process:

  1. NetWall scans the file share every *X* seconds (*default: 10 seconds*, configurable in UI).
  2. When a new file is detected, NetWall records its name, size, and access time.
  3. On the next scan, if these attributes remain unchanged, the file is transferred.
  4. If the file changes during transfer, it is re-transferred to ensure integrity.

This approach ensures incomplete files are not transferred. It mirrors the behavior of systems that use rename/move operations to signal upload completion.

### [4. Confirming File Transfer Completion](/docs/netwalldiode/v1.13.2/knowledge-base/what-is-the-file-handling-behavior-and-protocol-support-in-metad#4-confirming-file-transfer-completion)

Q: *How can we confirm when a file transfer is complete?*

- Use the File Transfer History section in the NetWall UI to view logs of all completed transfers.
- If the "delete after transfer" option is enabled, files will be automatically deleted from the Blue-side file share upon successful transfer.

This provides a clear confirmation that a file has been fully transferred, similar to previous systems using rename/move to mark completion.

Support:

If Further Assistance is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

MetaDefender
