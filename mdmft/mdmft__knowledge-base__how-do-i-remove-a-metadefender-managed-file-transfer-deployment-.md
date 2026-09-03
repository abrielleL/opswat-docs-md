<!-- source: https://www.opswat.com/docs/mdmft/knowledge-base/how-do-i-remove-a-metadefender-managed-file-transfer-deployment- -->

# How do I remove a MetaDefender Managed File Transfer deployment via API calls from an activation key (clear up a license slot)?

Summarize Page    Connect to Cursor Connect to VS Code Check Your Version: 

This article applies to all MetaDefender Managed File Transfer versions deployed on Windows systems.

Please Note: 

To deactivate (remove from the License/Activation key) a MetaDefender Managed File Transfer deployment via API calls, you need the following:

- A valid License/Activation Key
- The Deployment ID

Use this API call:

BashCopycurl -X GET https://activation.dl.opswat.com/deactivation?key=<activation-key>&deployment=<deployment unique-ID> 

Set the API parameters as below:

Once you receive a *200 response*, , the license slot will be freed for use with another deployment.

Support: 

For assistance with Activating or Deactivating a deployment via API calls, please follow the instructions at [Creating Support Packages](/docs/mdmft/troubleshooting/how-to-create-support-package) before submitting a [Support Ticket](https://www.opswat.com/support).
