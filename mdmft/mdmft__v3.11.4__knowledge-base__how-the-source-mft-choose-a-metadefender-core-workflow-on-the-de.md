<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/knowledge-base/how-the-source-mft-choose-a-metadefender-core-workflow-on-the-de -->

# How the Source MFT choose a MetaDefender Core workflow on the Destination MFT side during MFT-to-MFT synchronization?

Summarize Page    Connect to Cursor Connect to VS Code Check Your Version:

This article applies to all versions of MetaDefender Managed File Transfer.

When uploading a file to Source MFT, users cannot manually select a MetaDefender Core workflow on the Destination MFT. The workflow applied is determined by the user account that owns the API key created on the Destination MFT and used by the Source MFT for the synchronization task.

How MFT-to-MFT synchronization works

1. API key requirement To enable MFT-to-MFT synchronization, the Source MFT must use an API key generated on the Destination MFT. Currently, only an Administrator on the Destination MFT can generate this API key.
2. API key ownership The API key is tied to the user account that created it on the Destination MFT.
3. Workflow selection behavior When files are synchronized from the Source MFT to the Destination MFT using this API key:

- The Destination MFT processes the files using the MetaDefender Core workflow associated with the API key owner.
- Workflow selection is user-based on the Destination MFT side.
- The Source MFT does not have the ability to override or specify a different workflow.

Note that when **Synchronize MetaDefender Core Workflow** is enabled, the workflow is determined by the application that originally uploaded the file (for example, MetaDefender Kiosk) during MFT-to-MFT synchronization. The Destination MFT will attempt to scan the file using that Kiosk workflow. If the workflow does not exist on the Destination MFT, the default workflow will be applied instead.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
