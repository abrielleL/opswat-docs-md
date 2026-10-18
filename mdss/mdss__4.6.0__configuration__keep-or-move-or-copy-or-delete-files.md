<!-- source: https://www.opswat.com/docs/mdss/4.6.0/configuration/keep-or-move-or-copy-or-delete-files -->

# Keep, Copy, Move or Delete Files

## Configuring Keep/Copy/Move/Delete Remediation Actions

- Navigate to **Workflows** from the left-side navigation menu.
- Select the workflow for which you want to configure these remediation actions.
- Select the node for which you want to configure these remediation actions (Allowed Original, Allowed Sanitized, Blocked Original, Blocked Sanitized)
- Click on the box of the specific node.

> **Note**
>
> 1. Sanitization fails, and MD Core is configured to block the file on failure - The file verdict becomes Blocked with Sanitization failed as the reason; in this case, the original Blocked branch actions apply
> 2. Sanitization fails, and MD Core is not configured to block the file on failure - The file verdict remains unchanged; the file is left in the storage unit, no branch actions are applied
>
> Move operations are performed as a copy-then-delete sequence rather than a native move; if the upload step fails, the source file is left unchanged and the deletion is not attempted.

## Technical Considerations

- Move and Re-processing **->** when a sanitized file is moved from Storage A to Storage B, it will not be re-sanitized on Storage B, even if Deep CDR is enabled there.
  - Similarly, if Real-Time Processing is enabled on Storage B, the moved file will not be processed again.
- File Overwriting **->** moving a file with the same name and path as an existing file on the destination storage will overwrite the existing file.
- By default, "Keep" is the selected option -> which will keep the file as is.
- For the sanitized versions (Allowed Sanitized, Blocked Sanitized), Copy and Delete options are unavailable.

![](https://uploads.developerhub.io/prod/k8zL/c53bebiaa4hn5e2sycwb48akguf1z8cmn0jeq34z6cqypewr2s7erxox21f0p0he.png)

## Keeping/Moving Sanitized Files

Sanitized files, created by OPSWAT's Deep CDR, can be moved to one or more storage units (up to a maximum of 5 destinations per remediation type).

**Note:** The File Sanitization feature must be enabled to configure this action - see Enabling Deep CDR: [Deep Content Disarm and Reconstruction (Deep CDR)](https://www.opswat.com/docs/mdss/configuration/deep-content-disarm-and-reconstruction--deep-cdr-)

1. Click on the **Sanitized** **Remediation (Allowed Sanitized or Blocked Sanitized)** node to open the modal window
2. Choose the action:
   1. **"Keep the file"** -> the sanitized file is kept in the source storage location
   2. "**Move the file**" -> the sanitized file is moved to another storage unit (or units). Configure the destination storage(s) as described below.
3. Configure the **destination storage** (only for option b):
   - Select one or multiple storage unit destinations out of the dropdown list
     - Additionally, narrow down the destination for certain types of storages (SharePoint Cloud, OneDrive, Box, SharePoint On-Premises), depending on how they are integrated
   - Note: A valid connection with the destination storage(s) is required.
   - Select **Keep folder structure** to maintain the source's structure.

![](https://uploads.developerhub.io/prod/k8zL/eykay5y4r8wrlieurqljsqfmmo19mjkhn4uxbmvnhb5lp6e0dfs82addmhj03uee.png)

## Keeping/Copying/Moving/Deleting Files that are Unsupported by Deep CDR

Deep CDR does not support all file types. Unsupported files can be kept, deleted, moved or copied to one or more storage units (up to a maximum of 5 destinations per remediation type).

**Note:** The File Sanitization feature must be enabled to configure this action - see Enabling Deep CDR: [Deep Content Disarm and Reconstruction (Deep CDR)](https://www.opswat.com/docs/mdss/configuration/deep-content-disarm-and-reconstruction--deep-cdr-)

1. Click on the **Unsupported Remediation (Allowed Unsupported or Blocked Unsupported)** node to open the modal window
2. Choose the action:
   1. **"Keep the file"** -> the file is kept in the source storage location
   2. **"Copy the file"** -> the file is copied to another storage unit (or units). Configure the destination storage unit(s) as described below
   3. "**Move the file**" -> the file is moved to another storage unit (or units). Configure the destination storage unit(s) as described below
   4. **"Delete the file"** -> the file is deleted
3. Configure the **destination storage** (only for options b and c):
   - Select one or multiple storage unit destinations out of the dropdown list
     - Additionally, narrow down the destination for certain types of storages (SharePoint Cloud, OneDrive, Box, SharePoint On-Premises), depending on how they are integrated
   - Note: A valid connection with the destination storage(s) is required.
   - Select **Keep folder structure** to maintain the source's structure.

     ![](https://uploads.developerhub.io/prod/k8zL/d2oj0nf3n6f0tkv4zt1oz319hgo17uxyexpwurc5mvz4pqhdxztbm9p4xpfuq1wl.png)

## Keeping/Copying/Moving/Deleting Allowed Original Files

Files marked as **allowed** during processing can be deleted, copied or moved to one or more storage units (up to a maximum of 5 destinations per remediation type).

1. Click on the **Allowed Original** **Remediation** node to open the modal window
2. Choose the action:
   1. **Keep the file** -> the allowed file is kept in the same location
   2. **Copy the file** -> the allowed file is copied to another storage unit (or units). Configure the destination storage(s) as described below.
   3. **Move the file** -> the allowed file is moved to another storage unit (or units). Configure the destination storage(s) as described below.
   4. **Delete the file** -> the allowed file is deleted.
3. Configure the destination storage (only for options b and c):
   - Select one or multiple storage unit destinations out of the dropdown list
     - Additionally, narrow down the destination for certain types of storages (SharePoint Cloud, OneDrive, Box, SharePoint On-Premises), depending on how they are integrated
   - Note: A valid connection with the destination storage(s) is required
   - Select **Keep folder structure** to maintain the source's structure.

## Keeping/Copying/Moving/Deleting Blocked Original Files

Files marked as **blocked** during processing can be deleted, copied or moved to one or more storage units (up to a maximum of 5 destinations per remediation type).

1. Click on the **Blocked Original** **Remediation** node to open the modal window
2. Choose the action:
   1. **Keep the file** -> the blocked file is kept in the same location
   2. **Copy the file** -> the blocked file is copied to another storage unit (or units). Configure the destination storage(s) as described below.
   3. **Move the file** -> the blocked file is moved to another storage unit (or units). Configure the destination storage(s) as described below.
   4. **Delete the file** -> the blocked file is deleted.
3. Configure the destination storage:
   - Select one or multiple storage unit destinations out of the dropdown list
     - Additionally, narrow down the destination for certain types of storages (SharePoint Cloud, OneDrive, Box, SharePoint On-Premises), depending on how they are integrated
   - Note: A valid connection with the destination storage(s) is required
   - Select **Keep folder structure** to maintain the source's structure.

![](https://uploads.developerhub.io/prod/k8zL/sflxosypvi925myfs33cttch2wc5e2noaqzei88somvpcpfonpqhf91hie7p5aol.png)

## Storage types with additional configuration needed

> **INFO**
>
> For a number of the possible storage integrations - SharePoint Cloud, OneDrive, Box, SharePoint On-Premises - extra specifications may be necessary when selecting them as destinations as follows:
>
> - If the **SharePoint Cloud** integration only has the **Site** specified, you will be asked to  enter the name of the **Document Library** to which the files should be moved/copied
> - If the **OneDrive** integration only has the **Group** specified, you will be asked to enter the name or email of the **User** to which the files should be moved/copied
> - If the **SharePoint On-Premises integration** only has the **Site URL** specified, you will be asked to  enter the name of the **Document Library** to which the files should be moved/copied
> - If the **Box** integration has the **All Users** or **A specific group** selected, you will be asked to enter the name or email of the **User** to which the files should be moved/copied

## Restrictions

> **Destination storage restrictions**
>
> Marking a storage as a destination for a remediation restricts certain actions on that storage such as deleting it, or altering its configuration in a way that makes the remediation invalid (in the case of destination storages that support users or libraries as a remediation configuration).

> **Scan restrictions**
>
> Starting a scan requires a valid workflow configuration.
>
> The configuration can become invalid if one of the technologies that was enabled and used on the workflow is no longer available on the configured Scan Pool.

## Handling Remediation Issues

When remediation actions are configured in a workflow and a user initiates a scan using that workflow, there is a possibility that some files may be discovered and scanned by the **Scan Instance** but fail during the application of remediation actions.

In such cases, the scan report will indicate a **Remediation Failed** status.

![](https://uploads.developerhub.io/prod/k8zL/d62pxd45jqamom8d51uufcjcxz1cz67sbaffopp8nfmkj4i3059c54zhitvep96c.png)

To obtain further details about this issue, users can filter the files marked as **Remediation Failed** and click on individual files to access their specific reports.

On the right side of the report, the **Remediation Actions** tab will display all remediation actions taken on the file, including their success or failure.

![](https://uploads.developerhub.io/prod/k8zL/eeo7ah93yceow0w3t82lzbux58t8btsh30vf63zugy5hy5b3lsv88m729h5zv2sl.png)

To diagnose the cause of the failure, users can click on the failed remediation to view the specific exception that led to the failure.

Typically, for Move or Copy remediation actions, the issue is related to the destination storage. If sanitization has failed, refer to the Unsupported files and sanitization failures handling section for details on which branch actions apply.

## **Troubleshooting Reference**

| Issue | Common causes | First steps |
| ---- | ---- | ---- |
| Copy/Move failures | Storage permissions, network connectivity, disk space | Check storage health, verify credentials |
| Sanitization failures | File type not enabled, sanitized version upload issue | Check Scan Instance configuration |
| Performance issues | Multiple destinations, large files, network latency | Review remediation complexity, optimize storage placement |
| Configuration Errors | Invalid storage selections, missing permissions | Validate workflow configuration, test connections |

## Integration considerations

#### Storage requirements

- Make sure the destination storages have sufficient capacity (recommend 2x source storage size)
- Verify network bandwidth between source and destination storages

#### **Security Best Practices**

- Use service accounts with minimum required permissions
- Enable encryption for sensitive file transfers
- Regular security audits of remediation workflows

Next steps after configuring remediation actions:

Test Workflows -> run test scans with sample files to verify remediation behavior

Plan scaling -> consider future storage and performance requirements

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
