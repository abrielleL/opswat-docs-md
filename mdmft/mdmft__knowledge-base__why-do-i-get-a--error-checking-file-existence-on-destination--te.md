<!-- source: https://www.opswat.com/docs/mdmft/knowledge-base/why-do-i-get-a--error-checking-file-existence-on-destination--te -->

# Why do I get a "Error checking file existence on destination, terminating: invalid path." on PUSH Job automation?

Summarize Page    Connect to Cursor Connect to VS Code

**Notes:**

- This applies to all MetaDefender Managed File Transfer version capable of SFTP integration
- This article covers PUSH jobs integration issues on MetaDefender Managed File Transfer
## [**Problem:**](/docs/mdmft/knowledge-base/why-do-i-get-a--error-checking-file-existence-on-destination--te#problem)

Certain environments may restrict the level of access/permissions on their SFTP servers to the point where the creation of sub-folders inside a destination SFTP folder is not allowed. This is particularly an issue when a sub-folder is created on MFT that does not exists on the destination SFTP parent folder. When this occurs, you will see the following error in the job execution history:

> Error checking file existence on destination, terminating: invalid path

## [**Solution:**](/docs/mdmft/knowledge-base/why-do-i-get-a--error-checking-file-existence-on-destination--te#solution)

These are the possible ways that can help mitigate this issue:

1. Check the permissions on the parent folder on the SFTP server. Execute permissions will be required for the creation of sub-folders.
2. Pre-create the sub-folder on the SFTP server. If you require sub-folders on the parent folder, create these sub-folders in advanced. With this, no create sub-folder action will be needed during the execution of the PUSH job from Managed File Transfer.
3. Alternatively, if sub-folders are not required, upload your files directly to the parent folder in Managed File Transfer.

**Support:**

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/support).
