<!-- source: https://www.opswat.com/docs/mdss/operations/workflows -->

# Workflows

Each workflow consists of the following configurations:

- File discovery
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

The Discovery only workflow will be created with the default settings after pressing Create button.

![](https://uploads.developerhub.io/prod/k8zL/t52l3stevklhnak6ecxgaunjuhv74n8epx7ydfqknrncwiyxpphemyz8p642k6kd.png)

This type of workflow it is used for storage interaction without scanning the file. This allows a more limited number of remediations and focus only on discovering folder structure and managing it

#### Standard

The standard workflow is saved in the system only after the "Scan pool" is properly configured. While in draft mode, all the other settings nodes are inaccessible until the Scan pool is successfully configured.

![](https://uploads.developerhub.io/prod/k8zL/k6d0itelbxw747zsxb3b2r2zy44txeoj5k1fqb3n996vb0rme6w1kb3xz9a1ahdo.png)

Once the Scan pool is successfully configured, the other settings can be updated by clicking on each one individually. The workflow is updated instantly once the "Save changes" button is clicked for each of the settings nodes.

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

![](https://uploads.developerhub.io/prod/k8zL/jjr3mocakb82sj5wrdi54by3kpe534844f6q95qtnsotytw9y7zwnl3plqs95fkj.png)

## Technologies

This lists all technologies available in the connected MetaDefender Core/Cloud/Distributed Cluster instance configured in the scan pool step. If settings have changed on the MetaDefender Core/Cloud/Distributed Cluster side, use the **Refresh technologies** button to load the latest available technologies

![](https://uploads.developerhub.io/prod/k8zL/ujjaglpckh3m72jfmq7lyh0de211ovz6njtnyvwkmk4qswt1f985i56uowt9nq5j.png)

## File Tagging

When enabled, File Tagging labels processed files with their security status (clean, sanitized, blocked) to support compliance and audit requirements. You can configure which tags are applied, including the MetaDefender result, file ID, and analysis timestamp and customize the tag name for each. Tags can be reset to their default values at any time using the **Reset tags to default** button.

For instructions on setting up the feature, refer to the [Configure File Tagging](https://www.opswat.com/docs/mdss/configuration/file-tagging).

![](https://uploads.developerhub.io/prod/k8zL/dkkpebhan9txxuqoownvc51lu1zebl70omlcqagtaumcty68c994vj5bjhgqhws7.png)

## Deep CDR

Applies OPSWAT’s Deep CDR (file sanitization) technology to files.

Enabling the File Sanitization feature creates a secure version of a file by removing potentially harmful content. This process utilizes OPSWAT's Deep Content Disarm and Reconstruction (Deep CDR) technology.

For detailed instructions on configuring this feature, refer to the [Deep CDR user guide](https://www.opswat.com/docs/mdcore/deep-cdr) and [Deep Content Disarm and Reconstruction (Deep CDR)](https://www.opswat.com/docs/mdss/configuration/deep-content-disarm-and-reconstruction--deep-cdr-).

![](https://uploads.developerhub.io/prod/k8zL/nhyovuwr6qljrkw7w33b7t2sij97ketcw61ipv6waspm1u5nyeow1xjwaaf4b9xo.png)

## File Definition

What was previously known as Remediation Actions is now called File Definition, which dictates the outcome for each file based on its scan results. Files can be designated as Allowed (approved), Sanitized (cleaned), or Blocked (quarantined).

For detailed setup instructions, refer to the [Configure File Definition](https://www.opswat.com/docs/mdss/configuration/file-definition).

![](https://uploads.developerhub.io/prod/k8zL/yg3fstn813wwsqyrsfb9slbjaz1u4mwzmp5eoy4ywltjc1bw2yq590lmckuea6cc.png)

## File Remediations

File remediation actions are automated post-processing tasks performed on files after they have been scanned. The following remediation options are currently available: Keep, Copy, Move, Delete.

For more information on setting up the feature, refer to the [Keep, Copy, Move or Delete Files](https://www.opswat.com/docs/mdss/configuration/keep-or-move-or-copy-or-delete-files).

#### Important Considerations

- Make sure that the destination buckets for moved or copied files are properly configured and accessible within your environment (in this case Amazon S3)
- Carefully consider your organization's risk tolerance when configuring deletion actions. Implement safeguards like versioning or backups to prevent accidental data loss.
- Develop a clear tagging strategy to facilitate efficient file management and consistency.
- Regularly review and update your remediation actions and tagging configurations to align with your organizational evolving security needs and policies.

![](https://uploads.developerhub.io/prod/k8zL/i36wn36r70fl3y6r4cl2qjezxrwtu5mt499prrvn7qndxja35mrxa7xvzuksdqwe.png)

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

![](https://uploads.developerhub.io/prod/k8zL/f302tlxnlwwjue94rew3hirf4u2wketeuzoj0ichpq2c4zkefysd9loyar06631u.png)

## Error Handling

The remediation process includes automatic retry functionality to handle transient failures.

For detailed configuration steps, refer to the [Remediation Process Retries](https://www.opswat.com/docs/mdss/configuration/remediation-process-retries).

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
