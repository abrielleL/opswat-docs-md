<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/why-does-metadefender-core-show-a--calculate-hash-error--when-sc -->

# Why Does MetaDefender Core Show a 'Calculate hash error' When Scanning Malicious Files?

This article applies to all MetaDefender Core V5 releases deployed on Windows systems.

### [**Issue**](/docs/mdcore/knowledge-base/why-does-metadefender-core-show-a--calculate-hash-error--when-sc#issue)

When testing the upload of a malicious file to MetaDefender Core, the system unexpectedly allows the file and displays the following error during scanning:

Archive Extraction: Extraction error Extraction Result Failure Category: Calculate hash error Error Details: Can't get fileinfo to calculate hash: 'Can't open file for reading'

### [**Root Cause**](/docs/mdcore/knowledge-base/why-does-metadefender-core-show-a--calculate-hash-error--when-sc#root-cause)

The error occurs because local antivirus software on the system is detecting and handling the malware file before MetaDefender Core can access it. As a result, MetaDefender Core is unable to read the file and generate the necessary hash for scanning.

This typically happens when Real-Time Protection (RTP) is enabled on the local antivirus, causing the file to be quarantined or blocked immediately after upload.

### [**Solution**](/docs/mdcore/knowledge-base/why-does-metadefender-core-show-a--calculate-hash-error--when-sc#solution)

- **Verify file integrity**

  - Confirm that the file you submitted is complete and accessible.
  - Re-upload the file if needed and check if the error re-occurs.
- **Check anti-virus / real-time protection interference**

  - If you are using any anti-virus or endpoint protection on the same machine as MetaDefender Core, check whether the real-time protection has locked or removed the file before the hash calculation.
  - Consider temporarily disabling real-time protection for testing, or exclude the upload/temp folders of MetaDefender Core from the real-time scan.
  - Note: Do **not** exclude `engineprocess.exe` if Windows Defender (or any AV) is used both as the *local AV* and as an *AV-engine inside MetaDefender Core*. (See related KB for exclusion guidelines.)
- **Check folder permissions and storage capacity**

  - Ensure the service account running MetaDefender Core has read/write access to the upload folder and temp directory.
  - Verify there is sufficient free disk space in the partition that holds the upload/temp folder.
  - If the file is large or part of an archive, ensure it can be extracted and processed.
- **Review Core logs for additional details**

  - On Windows: check `C:\Program Files\OPSWAT\MetaDefender Core\logs\*` for messages around the “Calculate hash error”.
  - On Linux: check `/var/log/metadefender-core/` (or equivalent) for more context.
- **Retest the submission**

  - After applying the above checks/remediations, resubmit the file for scanning.
  - If the error disappears, you have resolved the root cause.
  - If the error persists, collect the upload file, the logs (with debug if possible) and open a support case with OPSWAT.

Support:

If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
