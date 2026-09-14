<!-- source: https://www.opswat.com/docs/mdss/4.4.2/operations/workflows -->

# Workflows

Each workflow consists of the following configurations:

- Scan configuration
- File tagging
- Deep CDR
- File remediations
- Other remediations

Configuration limitations

The available configurations are tied to the MetaDefender Cloud/Core available technologies. Providing an API Key when setting up the Scan Pools will list all the available technologies that are configured in MetaDefender Cloud/Core so that configurations can be successfully applied.

Prerequisites

In order to be able to create a workflow, a scan pool is required.

## [Creating a Workflow](/docs/mdss/4.4.2/operations/workflows#creating-a-workflow)

As a first time user, there is a default workflow that is created during the onboarding process. There can be created as many workflows as required for different use-cases.

Default workflow

The default workflow can't be deleted. There must always be a default workflow configured in the system.

A workflow can be created by navigating to the Workflows page and clicking the "Create Workflow" button. This will reveal a dialog box where the new workflow name must be set and also the type of the workflow.

Once a name is given to the new workflow it will require to choose the type of workflow, afterwards the system will mark it as a draft.

#### [Discovery only](/docs/mdss/4.4.2/operations/workflows#discovery-only)

The Discovery only workflow will be created with the default configuration after pressing Create button.

This type of workflow it is used for storage interaction without scanning the file. This allows a more limited number of remediations and focus only on discovering folder structure and managing it

#### [Standard](/docs/mdss/4.4.2/operations/workflows#standard)

The standard workflow is saved in the system only after the "Scan Configuration" is properly configured. While in draft mode, all the other configuration nodes are inaccessible until the Scan Configuration is successfully configured.

Once the Scan Configuration is successfully configured, the other configurations can be updated by clicking on each one individually. The workflow is updated instantly once the "Save changes" button is clicked for each of the configuration nodes.

## [Scan Configuration](/docs/mdss/4.4.2/operations/workflows#scan-configuration)

Each workflow must have a scan configuration set up which specifies the Scan Pool that should be used for scanning. The Scan Configuration is built up by a set of rules for an already configured Scan Pool (MetaDefender Cloud/Core). A Failover Scan Pool can also be set for the new Scan Configuration.

MetaDefender Storage Security employs scan configurations to offer a versatile method for initiating scanning processes using various workflow rules from either MetaDefender Core or MetaDefender Cloud.

Scan configurations are linked with scan pools to ensure uniform configuration across all instances of MetaDefender Core/Cloud.

IMPORTANT

The default workflow rule for MetaDefender Core is 'MetaDefender Storage Security'.

For MetaDefender Cloud default rules are 'multiscan' and 'unarchive', please check the following [documentation](https://docs.opswat.com/mdcloud/metadefender-cloud-api-v4#file-upload).

When creating a new scan configuration, you can select a name, associate it with a scan pool, and optionally designate a secondary scan pool for failover in cases where all scan instances from the primary pool are unavailable or unresponsive.

## [Technologies](/docs/mdss/4.4.2/operations/workflows#technologies)

This lists all the available technologies that are available in the MetaDefender Cloud/Core instance that was set previously in the Scan Configuration.

If an update was made in the MetaDefender Cloud/Core instance, the "Refresh technologies" button will sync the technologies with the ones from the instance.

## [File Tagging](/docs/mdss/4.4.2/operations/workflows#file-tagging)

Adds metadata tags to files in S3-like storage units, providing processing information.

For detailed configuration instructions, refer to the [Configure File Tagging](/docs/mdss/4.4.2/configuration/file-tagging).

## [Deep CDR](/docs/mdss/4.4.2/operations/workflows#deep-cdr)

Applies OPSWAT’s Deep CDR (file sanitization) technology to files.

Enabling the File Sanitization feature creates a secure version of a file by removing potentially harmful content. This process utilizes OPSWAT's Deep Content Disarm and Reconstruction (Deep CDR) technology.

For detailed configuration instructions, refer to the [Deep CDR user guide](https://www.opswat.com/docs/mdcore/deep-cdr) and [Deep Content Disarm and Reconstruction (Deep CDR)](/docs/mdss/4.4.2/configuration/deep-content-disarm-and-reconstruction--deep-cdr-).

## [File Definition](/docs/mdss/4.4.2/operations/workflows#file-definition)

What was previously known as Remediation Actions is now called File Definition, which dictates the outcome for each file based on its scan results. Files can be designated as Allowed (approved), Sanitized (cleaned), or Blocked (quarantined).

For detailed configuration instructions, refer to the [Configure File Definition](/docs/mdss/4.4.2/configuration/file-definition).

## [File Remediations](/docs/mdss/4.4.2/operations/workflows#file-remediations)

File remediation actions are automated post-processing tasks performed on files after they have been scanned. The following remediation options are currently available: Keep, Copy, Move, Delete.

For detailed configuration instructions, refer to the [Keep, Copy, Move or Delete Files](/docs/mdss/4.4.2/configuration/keep-or-move-or-copy-or-delete-files).

#### [Important Considerations](/docs/mdss/4.4.2/operations/workflows#important-considerations)

- Make sure that the destination buckets for moved or copied files are properly configured and accessible within your environment (in this case Amazon S3)
- Carefully consider your organization's risk tolerance when configuring deletion actions. Implement safeguards like versioning or backups to prevent accidental data loss.
- Develop a clear tagging strategy to facilitate efficient file management and consistency.
- Regularly review and update your remediation actions and tagging configurations to align with your organizational evolving security needs and policies.

## [Other Remediations](/docs/mdss/4.4.2/operations/workflows#other-remediations)

#### [Delete Empty Folders](/docs/mdss/4.4.2/operations/workflows#delete-empty-folders)

Delete a directory if it is empty after remediation (does not delete if the folder was empty to begin with).

For detailed configuration instructions, refer to the [Delete Empty Folders](/docs/mdss/4.4.2/configuration/delete-empty-folders).

Dependency

The delete empty folders remediation can be active only if there is at least one of another remediations configured with "Move the file" or "Delete the file".

#### [Scan File Versions](/docs/mdss/4.4.2/operations/workflows#scan-file-versions)

Retrieve & process all past versions of a file. This comes with a performance cost, as all versions will be scanned like normal files.

For more details about this feature, refer to [Scan File Versions](/docs/mdss/4.4.2/configuration/scan-file-versions).

## [Error Handling](/docs/mdss/4.4.2/operations/workflows#error-handling)

The remediation process includes automatic retry functionality to handle transient failures.

For detailed configuration instructions, refer to the [Remediation Process Retries](/docs/mdss/4.4.2/configuration/remediation-process-retries).
