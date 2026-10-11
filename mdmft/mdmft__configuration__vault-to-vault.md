<!-- source: https://www.opswat.com/docs/mdmft/configuration/vault-to-vault -->

# MFT to MFT

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

This feature allows secure and controlled file transfers between different networks. When enabled, all file and folder operations will be sent from the source MFT to the destination MFT server. Based on the various transfer policies, file operation rules can be specified as:

1. All files
2. Only allowed files
3. Only supervisor-approved files (supervisor approval must be enabled)

Warning

If the "All files" option is selected, all files will be mirrored to the secondary MFT, regardless of their state or whether they are blocked.

## [Supported Operations](/docs/mdmft/configuration/vault-to-vault#supported-operations)

Warning

MetaDefender Managed File Transfer™ versions must be identical on both source and destination servers.

File and folder actions performed before the integration of both MetaDefender Managed File Transfer™ systems will not be transferred to the destination MFT. To ensure redundancy for all file and folder actions, it is recommended to set up and integrate both MFT systems simultaneously.

Supported file and folder actions:

| Operation | File | Folder |
| --- | --- | --- |
| Upload (Create) |  |  |
| Share |  |  |
| Move |  |  |
| Rename |  |  |
| Delete |  |  |
| Archiving |  |  |

Supported account operations:

| Operation |
| --- |
| Guest account creation |
| Guest account update |
| Guest account delete |

Warning

If the "Aggregate all file/folder actions" option is disabled, make sure the creator user exists on the destination Managed File Transfer.

Info

Guest accounts created while the "Aggregate all file/folder actions" option is enabled will appear on the destination Managed File Transfer as owned by the user who created the API key.

## [Configuration](/docs/mdmft/configuration/vault-to-vault#configuration)

- Go to "Automation" → "MFT to MFT"

Info

MetaDefender Managed File Transfer™ supports bidirectional integration and communication between MFTs.

1. **Enable MFT to MFT Sync:** Toggle on to enable this feature (default is off).
2. **Enforce Synchronization:** Enable to display bad requests for desynchronization between the two Managed File Transfer instances.

Note

If a data diode is used between the MFT servers, Enforce Synchronization may need to be disabled, as responses from the second MFT may not be received.

Info

When Enforce Synchronization is turned off, the connection status will display as "Unknown."

3. **Configure the Transfer Policy**:

   1. Transfer all files
   2. Transfer only allowed files
   3. Transfer only supervisor-approved files (supervisor approval must be enabled):

      - A file is considered "supervised" if:

        - approved by all required supervisors
        - revoked by a supervisor
        - revoked by an administrator
      - Files that have been blocked by MetaDefender Core™ can be supervised only if they receive an administrator approval
      - All files in a group transfer must be supervised before the request is forwarded to the upstream Managed File Transfer instance, including files stored in the recycle bin. If **Synchronize Each File Individually** is enabled, each file waits only for its own supervision, not for the other files in the group transfer.

Note

Administrators can now revoke blocked files regardless of ownership.

Prior to version 3.1.0, it was not possible to indicate whether or not the administrators inspected blocked files. They could only approve blocked files to make them available to supervisors.

Warning

To transfer only supervisor-approved files, first enable the "Supervisor Approval" feature.

If disabled, the following validation error will be displayed, and the "Update" button will be disabled.

Files will not upload to the destination Managed File Transfer unless:

1. "Supervisor approval" is enabled
2. "Other transfer policy" is selected

4. **File Aggregation:** When this option is enabled, all forwarded actions are treated as if they were requested by a single impersonated user. For example, files will be uploaded to the impersonated user's account, regardless of who initiated the actions on the source Managed File Transfer instance.

Note

The impersonated user must exist on both Managed File Transfer instances. This requires both instances to either integrate with the same Active Directory or have the same local accounts created. If the impersonated user does not exist, all requests will be made on behalf of the user who generated the API key.

Note

Guest accounts created with impersonation will be owned by the impersonated user. If the impersonated user does not exist on the destination Managed File Transfer, the accounts will be owned by the API key owner.

Guest welcome notifications (if configured for the destination Managed File Transfer) will be sent to the email address of the guest account and the *creator* on the first Managed File Transfer.

4. **Synchronize MetaDefender Core Workflow**: When this option is enabled, it will ensure that synchronization also forwards the explicitly set MetaDefender Core Workflow property for uploaded files. For example if files were uploaded by MetaDefender Kiosk and a custom MetaDefender Core Workflow was used, the destination MFT will try to scan the files with the same rule. If the same workflow is not available on the destination MFT, the default workflow will be used.
5. **Allow Users to Start Manual Synchronization**: When enabled the users can trigger a re-synchronization with the destination MFT.
6. **Synchronize Each File Individually**: When this option is enabled, each file uploaded from the web UI is sent to the destination MFT as soon as its own upload and scan complete, without waiting for the other files of the same upload (default is off). For example, if a user uploads several small files and one large file, the small files reach the destination MFT before the large file finishes uploading. If the user closes the browser before the upload finishes, the files that already finished uploading are still sent, on a best-effort basis. Files uploaded from REST integrations are still sent after the whole upload is complete.

Info

While this option is enabled, destination MFTs do not send upload-successful, shared-with, or folder-updated notifications, because each file arrives as a separate upload. Blocked-file and approval notifications are not affected. Files with a cancelled scan are not synchronized.

Warning

Do not change this option while web UI uploads are in progress. If it is turned off in the middle of an upload, some files of that upload may not be sent to the destination MFT. To send the missing files, use **Sync to Destination MFT**.

### [Connecting with an Upstream Managed File Transfer Instance](/docs/mdmft/configuration/vault-to-vault#connecting-with-an-upstream-managed-file-transfer-instance)

1. Click "Add Destination" to open the setup modal
2. Provide a *Destination Name* that is unique in the destination list
3. Provide the REST URL of the destination Managed File Transfer instance in this exact format: <schema>://<address>:<port>/[vault_rest].

Note

Provide the absolute URL and path to the destination Managed File Transfer's REST service (i.e. //).

4. **Provide an API Key** [generated](/docs/mdmft/configuration/api-keys) on the destination MFT instance. Use this to authorize request from the source Managed File Transfer instance.
5. **Manual Synchronization to Destination:** When enabled, files transferred to the destination MFT are synchronized only when manually triggered by the user.
6. **Skip MetaDefender Core™ scanning on destination MFT**: Enable this option if you want to bypass scanning on the destination MFT for files forwarded from the source MFT, provided the connection uses a system-level API key with enabled "Allow Skip MetaDefender Core™ Scanning" .
7. **Show Destination File Status**: When enabled, the destination MFT's file status for synchronized files can be displayed on the given source MFT.
8. **Skip Supervision on destination MFT**: Enable this option if you want to leave out the supervision process on the destination MFT for files forwarded from the source MFT. The provided system-level API key should have enabled "Allow Skip Supervision" option.
9. **Create Automatically Guest User on destination MFT:** After enabling this option a guest user account will be created if they don't already exist on the destination MFT. When this option is enabled, an additional **Guest Username Suffix** field appears. This optional text is appended to the username when automatically creating the guest account on the destination MFT (e.g., entering `.guest` would result in the account being named `johndoe.guest`). If left empty, the original username is used without any suffix. The suffix can be up to 25 characters long.
10. **Send Email Alert:** When enabled, administrators receive an email alert if the destination MFT disconnects. If the connection afterwards is recovered, a new email alert will go out to administrators about the restoration of the connection.

Info

The **Show Destination File Status** and **Send Email Alert** can be set only if the "Enforce Synchronization" feature is turned on. The users can switch on/off the displaying of the destination MFT file status column on the My Files page table settings view ('cog-wheel' menu).

Info

If the "Enforce Synchronization" feature is turned on, only destinations with valid inputs and successful connections will be added to the list. Any communication errors with the destination MFT will prevent the destinations from being added to the list. Errors may occur due to diodes between the two MFTs or invalid input values, and a specific error message will detail the issue.

Example: Invalid Destination MFT provided while Enforce Synchronization is turned on.

Example: Connected Connection Status for a valid Destination MFT

Example: Unknown Connection Status for a valid Destination MFT, because Enforce Synchronization is turned off

Info

Administrators can use the [user mapping](/docs/mdmft/operating/user-mapping) functionality to map different users across various MFT-to-MFT integrations.

### [Connection Status](/docs/mdmft/configuration/vault-to-vault#connection-status)

The Connection Status of a Destination MFT instance can be determined only if Enforce Synchronization is enabled; otherwise, it will display as "Unknown."

The status of each Destination MFT is automatically checked when the page loads and at regular intervals thereafter. You can also manually check the status for any Destination MFT at any time.

Possible Statutes:

1. **Connected:** The connection is working correctly.
2. **Disconnected:** Enforce Synchronization is turned on but an error has occurred. Hover over the status to see details about the issue.
3. **Unknown:** Enforce Synchronization is turned off and the status cannot be determined.

### [Manual Re-Synchronization - BETA](/docs/mdmft/configuration/vault-to-vault#manual-re-synchronization---beta)

If this feature was enabled within the general MFT to MFT configuration, when a synchronization error occurs and files or folders are missing on the destination MFT, users can initiate a new synchronization by clicking the "Sync to Destination MFT" button in the file action menu.

(**Limitation**: If at least one chunk of the file has reached the destination MFT, or if the file was successfully transferred to MFT2 but was deleted for any reason, re-sending it from MFT1 will not be possible)

Enhancement Roadmap and Current Limitations of the BETA Manual Re-Synchronization Feature

1. Files deleted from the destination MFT cannot be re-synchronized from the source MFT if their IDs are still recorded in the Audit log. To resolve this, the files must be re-uploaded to the source MFT.
2. Manual re-synchronization may overlook certain files if the selected items include nested folders.

Re-synchronization can also be performed for multiple selected files simultaneously (right click or "Bulk Action").

### [Manual Transfer Mode](/docs/mdmft/configuration/vault-to-vault#manual-transfer-mode)

In **Automatic** mode, synchronization continues automatically based on the configured behavior.

In **Manual** mode, synchronization is **user-specific**: each user decides when to trigger synchronization for their own file(s) and/or folder(s).

Use Manual mode when you want stricter operational control, such as validating content before transfer or running synchronization only when needed.

Info

When a user send a request to synchronize files, it will not happen immediately. It is just scheduled to be synchronized.

#### [How to use](/docs/mdmft/configuration/vault-to-vault#how-to-use)

1. Open the MFT2MFT target configuration.
2. Set **Transfer Mode** to **Manual**.
3. Save the target.
4. Users trigger synchronization on demand for their own file(s) and/or folder(s).

### [Visualization](/docs/mdmft/configuration/vault-to-vault#visualization)

If multiple Destination MFTs are configured, administrators can view the MFT-to-MFT configuration in a read-only flow diagram**.** For each Destination MFT, the current connection status is displayed—provided that *Enforce Synchronization* is enabled. Administrators can also instantly see whether *Transfer Policies* are configured for a given Destination MFT.

## [Multi-MFT](/docs/mdmft/configuration/vault-to-vault#multi-mft)

Multi-MFT configuration allows multiple destinations for a multi-MFT solution.

Info

From v3.6.2, all user operations are forwarded except for External Users.

Guest account-related operations are forwarded to the specified destinations.

All other account-related operations are broadcasted to all destinations.

Enable this mode during guest account creation to specify multiple destinations. Guest accounts will be created on all destinations.

Modify destinations while editing guest accounts. Previously uploaded files will be synchronized to newly added destinations.

Warning

If "Enforce Synchronization" is enabled, operations will only fail if not completed on all destinations.

Bi-directional Managed File Transfer (MFT) chains involving three or more MFT systems are not fully supported at this time.

Info

Refer to the [End-User Guide](/docs/mdmft/end-user-guide/guest-users#create-guest-users) for more information on guest user management.
