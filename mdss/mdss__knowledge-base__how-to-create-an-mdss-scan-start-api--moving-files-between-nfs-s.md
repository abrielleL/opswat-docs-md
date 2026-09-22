<!-- source: https://www.opswat.com/docs/mdss/knowledge-base/how-to-create-an-mdss-scan-start-api--moving-files-between-nfs-s -->

# How to create an MDSS Scan Start API: Moving Files Between NFS Storages After Sanitization

# [**Overview**](/docs/mdss/knowledge-base/how-to-create-an-mdss-scan-start-api--moving-files-between-nfs-s#overview)

This knowledge base documents how to initiate on-demand scans via the MetaDefender Storage Security (MDSS) API and have sanitized or allowed files automatically moved to a different storage unit: NFS → NFS. The move/copy/delete actions are executed by the workflow’s **Remediations** configuration, not by the scan-start call itself.

To move files post-scan, ensure your **Workflow** has the correct **Remediations** defined. The `/api/scan/start` endpoint only triggers discovery/scanning; it does not choose the destination. See “Configure the Workflow” below.

# [**API Endpoint**](/docs/mdss/knowledge-base/how-to-create-an-mdss-scan-start-api--moving-files-between-nfs-s#api-endpoint)

> **POST**
>
> `/api/scan/start`

Starts an on-demand (instant) scan on one or more storage units. The destination of post-scan file movement is controlled by the Workflow’s Remediations.

## [**Request Body Schema**](/docs/mdss/knowledge-base/how-to-create-an-mdss-scan-start-api--moving-files-between-nfs-s#request-body-schema)

- `workflowId` (string, required) — Workflow to use
- `priority` (number, optional) — Queueing priority
- `storageIds` (array[string], required) — Source storage unit IDs
- `name` (string, optional) — Friendly scan name
- `ScanPartition` (string, optional) — JSON string specifying a subset (folder/prefix). See examples per storage type

The property name is case-sensitive: use **ScanPartition**. The value is a *string* that contains JSON. Do not send an object for `ScanPartition`, or you will get a “could not be converted to System.String” validation error.

## [**Minimal working examples (sanitized placeholders)**](/docs/mdss/knowledge-base/how-to-create-an-mdss-scan-start-api--moving-files-between-nfs-s#minimal-working-examples-sanitized-placeholders)

## [**Windows path (NFS/SMB mounted path) — folder subset**](/docs/mdss/knowledge-base/how-to-create-an-mdss-scan-start-api--moving-files-between-nfs-s#-windows-path-nfssmb-mounted-path--folder-subset)

Prefer forward slashes to avoid escaping:

`POST http://localhost/api/scan/start
Content-Type: application/json
{
 "workflowId": "<workflow-id>",
 "priority": 1,
 "storageIds": ["<source-storage-id>"],
 "ScanPartition": "{\"Folder\":\"C:/mdss-demo/source/inbound\"}",
 "name": "PartitionScan_WindowsPath"
}`

Backslash version (double-escaped):

`"ScanPartition": "{\"Folder\":\"C:\\\\mdss-demo\\\\source\\\\inbound\"}"`

If **Further Assistance** is required, please proceed to log a [support case or chat with one of our support engineers](https://my.opswat.com/support).
