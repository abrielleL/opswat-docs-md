<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/knowledge-base/why-i-am-getting-error-removing-item-from-smb-server-when-using- -->

# Why I am getting error removing item from SMB server when using SMB pull job?

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

When executing an SMB pull job in MetaDefender Managed File Transfer (MFT) versions **3.8.1 to 3.9.1**, you may encounter the following error message in the job log: ”Error removing item: <filename>

Error deleting files on source”

This occurs even if the SMB pull job itself is successful.

## [Cause:](/docs/mdmft/v3.11.5/knowledge-base/why-i-am-getting-error-removing-item-from-smb-server-when-using-#cause)

This issue is caused by a bug in MFT versions **3.8.1 to 3.9.1**, where the system fails to remove successfully transferred files from the SMB source as expected.

## [Fix:](/docs/mdmft/v3.11.5/knowledge-base/why-i-am-getting-error-removing-item-from-smb-server-when-using-#fix)

This issue has been identified and is scheduled to be fixed in MFT version 3.9.3, which is targeted for release by late April 2025.

Support:

If **Further Assistance** is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/support).
