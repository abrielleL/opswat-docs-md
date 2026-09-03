<!-- source: https://www.opswat.com/docs/mdss/operations/workflows -->

# Workflows

Each workflow consists of the following configurations:

- File discovery
- Scan pool
- File tagging
- Deep CDR
- File remediations
- Other remediations

Configurations limitations

The available configurations are tied to the MetaDefender Cloud/Core available technologies. Providing an API Key when setting up the Scan Pools will list all the available technologies that are configured in MetaDefender Cloud/Core so that configurations can be successfully applied.

Prerequisites

In order to be able to create a workflow, a scan pool is required.

## [Creating a Workflow](/docs/mdss/operations/workflows#creating-a-workflow)

As a first time user, there is a default workflow that is created during the onboarding process. There can be created as many workflows as required for different use-cases.

Default workflow

The default workflow can't be deleted. There must always be a default workflow configured in the system.

A workflow can be created by navigating to the Workflows page and clicking the "Add new workflow" button. This will reveal a dialog box where the new workflow name must be set and also the type of the workflow.

Once a name is given to the new workflow it will require to choose the type of workflow, afterwards the system will mark it as a draft.

#### [Discovery only](/docs/mdss/operations/workflows#discovery-only)

The Discovery only workflow will be created with the default settings after pressing Create button.

This type of workflow it is used for storage interaction without scanning the file. This allows a more limited number of remediations and focus only on discovering folder structure and managing it

#### [Standard](/docs/mdss/operations/workflows#standard)

The standard workflow is saved in the system only after the "Scan pool" is properly configured. While in draft mode, all the other settings nodes are inaccessible until the Scan pool is successfully configured.

Once the Scan pool is successfully configured, the other settings can be updated by clicking on each one individually. The workflow is updated instantly once the "Save changes" button is clicked for each of the settings nodes.

## [Scan pool](/docs/mdss/operations/workflows#scan-pool)

Each workflow must have a scan pool node that determines which scan pool is used for scanning. It connects to an existing scan pool - such as MetaDefender Core, MetaDefender Distributed Cluster, or MetaDefender Cloud - and allows you to specify a user agent and a workflow rule to control how scanning is performed. A failover scan pool can also be designated to provide an alternative scanning resource when the primary pool is unavailable or unresponsive.

MetaDefender Storage Security uses scan pools to provide a flexible way to initiate scanning processes, leveraging scanning services from MetaDefender Core, MetaDefender Distributed Cluster, or MetaDefender Cloud based on the configured workflow rule.

Each scan pool configuration is tied to a specific scan pool and workflow rule, ensuring consistent scanning behavior across MetaDefender Core, MetaDefender Distributed Cluster, and MetaDefender Cloud instances.

IMPORTANT

The default workflow rule for MetaDefender Core/Distributed Cluster is 'MetaDefender Storage Security'.

For MetaDefender Cloud default rules are 'multiscan' and 'unarchive', please check the following [documentation](https://docs.opswat.com/mdcloud/metadefender-cloud-api-v4#file-upload).

When configuring the scan pool step in a workflow, you can select a scan pool, optionally enable failover to a secondary scan pool for cases where all scan instances from the primary pool are unavailable or unresponsive, and specify the user agent and workflow rule to apply during scanning.

## [Technologies](/docs/mdss/operations/workflows#technologies)

This lists all technologies available in the connected MetaDefender Core/Cloud/Distributed Cluster instance configured in the scan pool step. If settings have changed on the MetaDefender Core/Cloud/Distributed Cluster side, use the **Refresh technologies** button to load the latest available technologies

## [File Tagging](/docs/mdss/operations/workflows#file-tagging)

When enabled, File Tagging labels processed files with their security status (clean, sanitized, blocked) to support compliance and audit requirements. You can configure which tags are applied, including the MetaDefender result, file ID, and analysis timestamp and customize the tag name for each. Tags can be reset to their default values at any time using the **Reset tags to default** button.

For instructions on setting up the feature, refer to the [Configure File Tagging](/docs/mdss/configuration/file-tagging).

## [Deep CDR](/docs/mdss/operations/workflows#deep-cdr)

Applies OPSWAT’s Deep CDR (file sanitization) technology to files.

Enabling the File Sanitization feature creates a secure version of a file by removing potentially harmful content. This process utilizes OPSWAT's Deep Content Disarm and Reconstruction (Deep CDR) technology.

For detailed instructions on configuring this feature, refer to the [Deep CDR user guide](https://www.opswat.com/docs/mdcore/deep-cdr) and [Deep Content Disarm and Reconstruction (Deep CDR)](/docs/mdss/configuration/deep-content-disarm-and-reconstruction--deep-cdr-).

## [File Definition](/docs/mdss/operations/workflows#file-definition)

What was previously known as Remediation Actions is now called File Definition, which dictates the outcome for each file based on its scan results. Files can be designated as Allowed (approved), Sanitized (cleaned), or Blocked (quarantined).

For detailed setup instructions, refer to the [Configure File Definition](/docs/mdss/configuration/file-definition).

## [File Remediations](/docs/mdss/operations/workflows#file-remediations)

File remediation actions are automated post-processing tasks performed on files after they have been scanned. The following remediation options are currently available: Keep, Copy, Move, Delete.

For more information on setting up the feature, refer to the [Keep, Copy, Move or Delete Files](/docs/mdss/configuration/keep-or-move-or-copy-or-delete-files).

#### [Important Considerations](/docs/mdss/operations/workflows#important-considerations)

- Make sure that the destination buckets for moved or copied files are properly configured and accessible within your environment (in this case Amazon S3)
- Carefully consider your organization's risk tolerance when configuring deletion actions. Implement safeguards like versioning or backups to prevent accidental data loss.
- Develop a clear tagging strategy to facilitate efficient file management and consistency.
- Regularly review and update your remediation actions and tagging configurations to align with your organizational evolving security needs and policies.

## [Other Remediations](/docs/mdss/operations/workflows#other-remediations)

#### [Delete Empty Folders](/docs/mdss/operations/workflows#delete-empty-folders)

Delete a directory if it is empty after remediation (does not delete if the folder was empty to begin with).

For detailed setup instructions, refer to the [Delete Empty Folders](/docs/mdss/configuration/delete-empty-folders).

Dependency

The delete empty folders remediation can be active only if there is at least one of another remediations configured with "Move the file" or "Delete the file".

#### [Scan File Versions](/docs/mdss/operations/workflows#scan-file-versions)

This remediation type is only supported by the SharePoint On-Prem storage unit type.

Retrieve & process all past versions of a file. This comes with a performance cost, as all versions will be scanned like normal files.

For more details about this feature, refer to [Scan File Versions](/docs/mdss/configuration/scan-file-versions).

## [Error Handling](/docs/mdss/operations/workflows#error-handling)

The remediation process includes automatic retry functionality to handle transient failures.

For detailed configuration steps, refer to the [Remediation Process Retries](/docs/mdss/configuration/remediation-process-retries).
