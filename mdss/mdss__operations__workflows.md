<!-- source: https://www.opswat.com/docs/mdss/operations/workflows -->

# Workflows

Each workflow consists of the following configurations:

- File discovery
- File filters
- Scan pool
- File tagging
- Deep CDR
- File remediations
- Other remediations

> **Configurations limitations**
>
> The available configurations are tied to the MetaDefender Cloud/Core available technologies. Providing an API Key when setting up the Scan Pools will list all the available technologies that are configured in MetaDefender Cloud/Core so that configurations can be successfully applied.

> **Prerequisites**
>
> In order to be able to create a workflow, a scan pool is required.

## Creating a Workflow

As a first time user, there is a default workflow that is created during the onboarding process. There can be created as many workflows as required for different use-cases.

> **Default workflow**
>
> The default workflow can't be deleted. There must always be a default workflow configured in the system.

A workflow can be created by navigating to the Workflows page and clicking the "Add new workflow" button. This will reveal a dialog box where the new workflow name must be set and also the type of the workflow.

![](https://uploads.developerhub.io/prod/k8zL/14d0vqmhfxsy1k9vqwaz0wyvqd3bi640syysftjjvgbtrbbd2j0bjt96yw9xyhmw.png)

Once a name is given to the new workflow it will require to choose the type of workflow, afterwards the system will mark it as a draft.

#### Discovery only

The Discovery only workflow will be created with the default settings after pressing Create button

![](https://uploads.developerhub.io/prod/k8zL/4lk7p24bnxc4bf7cfpu48h1kmldolpvwyskxmprhiiycu82fv1ahotricerzhhy7.png)

This type of workflow it is used for storage interaction without scanning the file. This allows a more limited number of remediations and focus only on discovering folder structure and managing it

#### Standard

The standard workflow is saved in the system only after the "Scan pool" is properly configured. While in draft mode, all the other settings nodes are inaccessible until the Scan pool is successfully configured.

![](https://uploads.developerhub.io/prod/k8zL/180jmpg2nr4bi6qg0i5gmp030kvhbun94ij6ujame85crigd2dmkdj6ct9babp6o.png)

Once the Scan pool is successfully configured, the other settings can be updated by clicking on each one individually. The workflow is updated instantly once the "Save changes" button is clicked for each of the settings nodes.

## File Filters

File filters decide which discovered files are sent for scanning. You can limit a workflow to selected file types, a size range and a last-modified date range. A file is scanned only when it passes every filter you set; files that don't are recorded in the scan report as **Skipped by filter**, with the reason, and are not scanned. The node shows **Active** when at least one filter is set.

File types are picked from categories (archives, Office documents, images, executables and others) or entered as custom extensions. The match is based on the file extension only, not on the file's content.

![](https://uploads.developerhub.io/prod/k8zL/xkqi0lvzdm9kuwy6qg85m6by6km6r3e805qyx5r5bbmtey3q8qjsy3xhsstojcq0.png)

For detailed setup instructions and the full list of supported file types, refer to [File Filters](https://www.opswat.com/docs/mdss/configuration/file-filters).

## Scan pool

Each workflow must have a scan pool node that determines which scan pool is used for scanning. It connects to an existing scan pool - such as MetaDefender Core, MetaDefender Distributed Cluster, or MetaDefender Cloud - and allows you to specify a user agent and a workflow rule to control how scanning is performed. A failover scan pool can also be designated to provide an alternative scanning resource when the primary pool is unavailable or unresponsive.

MetaDefender Storage Security uses scan pools to provide a flexible way to initiate scanning processes, leveraging scanning services from MetaDefender Core, MetaDefender Distributed Cluster, or MetaDefender Cloud based on the configured workflow rule.

Each scan pool configuration is tied to a specific scan pool and workflow rule, ensuring consistent scanning behavior across MetaDefender Core, MetaDefender Distributed Cluster, and MetaDefender Cloud instances.

> **IMPORTANT**
>
> The default workflow rule for MetaDefender Core/Distributed Cluster is 'MetaDefender Storage Security'.
>
> For MetaDefender Cloud default rules are 'multiscan' and 'unarchive', please check the following [documentation](https://docs.opswat.com/mdcloud/metadefender-cloud-api-v4#file-upload).

When configuring the scan pool step in a workflow, you can select a scan pool, optionally enable failover to a secondary scan pool for cases where all scan instances from the primary pool are unavailable or unresponsive, and specify the user agent and workflow rule to apply during scanning.

![](https://uploads.developerhub.io/prod/k8zL/syptt7p85k7j9cd3ogjnd9ag3rresw089tmmz560sj8upefa3u5xv0yarkcn0hju.png)

## Technologies

This lists all technologies available in the connected MetaDefender Core/Cloud/Distributed Cluster instance configured in the scan pool step. If settings have changed on the MetaDefender Core/Cloud/Distributed Cluster side, use the **Refresh technologies** button to load the latest available technologies

![](https://uploads.developerhub.io/prod/k8zL/2wispdhamg10qbv1395dnuwdjx1agvircps01xqgy4tdncc1rwdlxmbkx31afppg.png)

## File Tagging

When enabled, File Tagging labels processed files with their security status (clean, sanitized, blocked) to support compliance and audit requirements. You can configure which tags are applied, including the MetaDefender result, file ID, and analysis timestamp and customize the tag name for each. Tags can be reset to their default values at any time using the **Reset tags to default** button.

For instructions on setting up the feature, refer to the [Configure File Tagging](https://www.opswat.com/docs/mdss/configuration/file-tagging).

![](https://uploads.developerhub.io/prod/k8zL/reeekxyt7b6kynthy10rvcmwuvyvlo26i6q49urfkhj2dlpvbgr6otcn9mj2tbyu.png)

## Deep CDR

Applies OPSWAT’s Deep CDR (file sanitization) technology to files.

Enabling the File Sanitization feature creates a secure version of a file by removing potentially harmful content. This process utilizes OPSWAT's Deep Content Disarm and Reconstruction (Deep CDR) technology.

For detailed instructions on configuring this feature, refer to the [Deep CDR user guide](https://www.opswat.com/docs/mdcore/deep-cdr) and [Deep Content Disarm and Reconstruction (Deep CDR)](https://www.opswat.com/docs/mdss/configuration/deep-content-disarm-and-reconstruction--deep-cdr-).

![](https://uploads.developerhub.io/prod/k8zL/oid9nf3jhjpt2f0z8ls5xdbadp6mxb3zjx5smsr8r2wp4b17ecbiipizxj8y174l.png)

## File Definition

What was previously known as Remediation Actions is now called File Definition, which dictates the outcome for each file based on its scan results. Files can be designated as Allowed (approved), Sanitized (cleaned), or Blocked (quarantined).

For detailed setup instructions, refer to the [Configure File Definition](https://www.opswat.com/docs/mdss/configuration/file-definition).

![](https://uploads.developerhub.io/prod/k8zL/mu6ujpuqjfm8b0xf04m388aw37ii0zfmzsviqpdo6t6xzocnkly7b8a4b72zhmov.png)

## File Remediations

File remediation actions are automated post-processing tasks performed on files after they have been scanned. The following remediation options are currently available: Keep, Copy, Move, Delete.

For more information on setting up the feature, refer to the [Keep, Copy, Move or Delete Files](https://www.opswat.com/docs/mdss/configuration/keep-or-move-or-copy-or-delete-files).

#### Important Considerations

- Make sure that the destination buckets for moved or copied files are properly configured and accessible within your environment (in this case Amazon S3)
- Carefully consider your organization's risk tolerance when configuring deletion actions. Implement safeguards like versioning or backups to prevent accidental data loss.
- Develop a clear tagging strategy to facilitate efficient file management and consistency.
- Regularly review and update your remediation actions and tagging configurations to align with your organizational evolving security needs and policies.

![](https://uploads.developerhub.io/prod/k8zL/yfnwlrsc3cbrsn8e3m7c8uqkw3uqttrmusm0jusm5e7quzrqlnud6i077jt6454n.png)

## Other Remediations

#### Delete Empty Folders

Delete a directory if it is empty after remediation (does not delete if the folder was empty to begin with).

For detailed setup instructions, refer to the [Delete Empty Folders](https://www.opswat.com/docs/mdss/configuration/delete-empty-folders).

> **Dependency**
>
> The delete empty folders remediation can be active only if there is at least one of another remediations configured with "Move the file" or "Delete the file".

#### Scan File Versions

> This remediation type is only supported by the SharePoint On-Prem storage unit type.

Retrieve & process all past versions of a file. This comes with a performance cost, as all versions will be scanned like normal files.

For more details about this feature, refer to [Scan File Versions](https://www.opswat.com/docs/mdss/configuration/scan-file-versions).

![](https://uploads.developerhub.io/prod/k8zL/d570pyi2766vt96021xhfqmgj4qpah3j1955pga10foxq9a6vaot0wwb4lg9kc0s.png)

## Error Handling

The remediation process includes automatic retry functionality to handle transient failures.

For detailed configuration steps, refer to the [Remediation Process Retries](https://www.opswat.com/docs/mdss/configuration/remediation-process-retries).

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
