<!-- source: https://www.opswat.com/docs/mdss/4.4.2/configuration/keep-or-move-or-copy-or-delete-files -->

# Keep, Copy, Move or Delete Files

## [Configuring Keep, Copy/Move/Delete Remediation Actions](/docs/mdss/4.4.2/configuration/keep-or-move-or-copy-or-delete-files#configuring-keep-copymovedelete-remediation-actions)

- Navigate to **Workflows** from the left-side navigation menu.
- Select the workflow for which you want to configure these remediations actions.
- Select the node for which you want to configure these remediations (Allowed Original, Allowed Sanitized, Blocked Original, Blocked Sanitized)
- Click on the box of the specific node.

Note

If a remediation action fails for the sanitized file, the original file will **not** be deleted. When Move is selected, the original file is copied instead.

## [Technical Considerations](/docs/mdss/4.4.2/configuration/keep-or-move-or-copy-or-delete-files#technical-considerations)

- Move and Re-processing **->** when a sanitized file is moved from Storage A to Storage B, it will not be re-sanitized or re-encrypted on Storage B, even if Deep CDR is enabled there.

  - Similarly, if Real-Time Processing is enabled on Storage B, the moved file will not be processed again.
- File Overwriting **->** moving a file with the same name and path as an existing file on the destination storage will overwrite the existing file.
- By default, "Keep" is the selected option -> which will keep the file as is.
- For the sanitized versions (Allowed Sanitized, Blocked Sanitized), Copy and Delete options are unavailable.

## [Keeping/Moving Sanitized Files](/docs/mdss/4.4.2/configuration/keep-or-move-or-copy-or-delete-files#keepingmoving-sanitized-files)

Sanitized files, created by OPSWAT's Deep CDR, can be moved to one or more storage units (up to a maximum of 5 destinations per remediation type).

**Note:** The File Sanitization feature must be enabled to configure this action - see Enabling Deep CDR: [Deep Content Disarm and Reconstruction (Deep CDR)](/docs/mdss/4.4.2/configuration/deep-content-disarm-and-reconstruction--deep-cdr-)

1. Click on the **Sanitized** **Remediation (Allowed Sanitized or Blocked Sanitized)** node to open the modal window
2. Choose the action:

   1. **" Keep the file"** -> the sanitized file is kept in the source storage location
   2. "**Move the file**" -> the sanitized file is moved to another storage unit (or units). Configure the destination storage(s) as described below.
3. Configure the **destination storage** (for b option only):

   - Select one or multiple storage unit destinations out of the dropdown list

     - Additionally, narrow down the destination for certain types of storages (SharePoint Cloud, OneDrive, Box, SharePoint On-Premises), depending on how they are integrated
   - Note: A valid connection with the destination storage(s) is required.
   - Select **Keep folder structure** to maintain the source's structure.

## [Keeping/Copying/Moving/Deleting Allowed Original Files](/docs/mdss/4.4.2/configuration/keep-or-move-or-copy-or-delete-files#keepingcopyingmovingdeleting-allowed-original-files)

Files marked as **allowed** during processing can be deleted, copied or moved to one or more storage units (up to a maximum of 5 destinations per remediation type).

1. Click on the **Allowed Original** **Remediation** node to open the modal window
2. Select "**Keep the file**" to keep the file in the same storage, "**Move the file**" to move the file to another storage unit (or units), "**Copy the file**" to copy the file to another storage unit (or units), or "**Delete the file**" to delete it.
3. Choose the action:

   1. **Keep the file** -> the allowed file is kept in the same location
   2. **Copy the file** -> the allowed file is copied to another storage unit (or units). Configure the destination storage(s) as described below.
   3. **Move the file** -> the allowed file is moved to another storage unit (or units). Configure the destination storage(s) as described below.
   4. **Delete the file** -> the allowed file is deleted.
4. Configure the destination storage(for option b and c):

   - Select one or multiple storage unit destinations out of the dropdown list

     - Additionally, narrow down the destination for certain types of storages (SharePoint Cloud, OneDrive, Box, SharePoint On-Premises), depending on how they are integrated
   - Note: A valid connection with the destination storage(s) is required
   - Select **Keep folder structure** to maintain the source's structure.

## [Copying/Moving/Deleting Blocked Original Files](/docs/mdss/4.4.2/configuration/keep-or-move-or-copy-or-delete-files#copyingmovingdeleting-blocked-original-files)

Files marked as **blocked** during processing can be deleted, copied or moved to another storage unit.

1. Click on the **Blocked Original** **Remediation** node to open the modal window
2. Select "**Keep the file**" to keep the file in the same storage, "**Move the file**" to move the file to another storage unit (or units), "**Copy the file**" to copy the file to another storage unit (or units), or "**Delete the file**" to delete it.
3. Choose the action:

   1. **Keep the file** -> the blocked file is kept in the same location
   2. **Copy the file** -> the blocked file is copied to another storage unit (or units). Configure the destination storage(s) as described below.
   3. **Move the file** -> the blocked file is moved to another storage unit (or units). Configure the destination storage(s) as described below.
   4. **Delete the file** -> the blocked file is deleted.
4. Configure the destination storage:

   - Select one or multiple storage unit destinations out of the dropdown list

     - Additionally, narrow down the destination for certain types of storages (SharePoint Cloud, OneDrive, Box, SharePoint On-Premises), depending on how they are integrated
   - Note: A valid connection with the destination storage(s) is required
   - Select **Keep folder structure** to maintain the source's structure.

## [Storage types with additional configuration needed](/docs/mdss/4.4.2/configuration/keep-or-move-or-copy-or-delete-files#storage-types-with-additional-configuration-needed)

INFO

For a number of the possible storage integrations - SharePoint Cloud, OneDrive, Box, SharePoint On-Premises - extra specifications may be necessary when selecting them as destinations as follows:

- If the **SharePoint Cloud** integration only has the **Site** specified, you will be asked to enter the name of the **Document Library** to which the files should be moved/copied to
- If the **OneDrive** integration only has the **Group** specified, you will be asked to enter the name or email of the **User** to which the files should be moved/copied to
- If the **SharePoint On-Premises integration** only has the **Site URL** specified, you will be asked to enter the name of the **Document Library** to which the files should be moved/copied to
- If the **Box** integration has the **All Users** or **A specific group** selected, you will be asked to enter the name or email of the **User** to which the files should be moved/copied to
## [Destination storage restrictions](/docs/mdss/4.4.2/configuration/keep-or-move-or-copy-or-delete-files#destination-storage-restrictions)

IMPORTANT

Marking a storage as a destination for a remediation restricts certain actions on that storage such as deleting it, or altering it's configuration in a way that makes the remediation invalid (in the case of destination storages that support users or libraries as a remediation configuration).

## [Scan restrictions](/docs/mdss/4.4.2/configuration/keep-or-move-or-copy-or-delete-files#scan-restrictions)

IMPORTANT

Starting a scan requires a valid workflow configuration.

The configuration can become invalid if one of the technologies that was enabled and used on the workflow is no longer available on the configured Scan Pool.

## [Handling Remediation Issues](/docs/mdss/4.4.2/configuration/keep-or-move-or-copy-or-delete-files#handling-remediation-issues)

When remediation actions are configured in a workflow and a user initiates a scan using that workflow, there is a possibility that some files may be discovered and scanned by the **Scan Instance** but fail during the application of remediation actions.

In such cases, the scan report will indicate a **Remediation Failed** status.

To obtain further details about this issue, users can filter the files marked as **Remediation Failed** and click on individual files to access their specific reports.

On the right side of the report, the **Remediation Actions** tab will display all remediation actions taken on the file, including their success or failure.

To diagnose the cause of the failure, users can click on the failed remediation to view the specific exception that led to the failure.

Typically, for Move or Copy remediation actions, the issue is related to the destination storage.

If the sanitization has failed, the action for the original file will start.

## [**Troubleshooting Reference**](/docs/mdss/4.4.2/configuration/keep-or-move-or-copy-or-delete-files#troubleshooting-reference)

| Issue | Common causes | First steps |
| --- | --- | --- |
| Copy/Move failures | Storage permissions, network connectivity, disk space | Check storage health, verify credentials |
| Sanitization failures | File type not enabled, sanitized version upload issue | Check Scan Instance configuration |
| Performance issues | Multiple destinations, large files, network latency | Review remediation complexity, optimize storage placement |
| Configuration Errors | Invalid storage selections, missing permissions | Validate workflow configuration, test connections |

## [Integration considerations](/docs/mdss/4.4.2/configuration/keep-or-move-or-copy-or-delete-files#integration-considerations)

#### [Storage requirements](/docs/mdss/4.4.2/configuration/keep-or-move-or-copy-or-delete-files#storage-requirements)

- Make sure the destination storages have sufficient capacity (recommend 2x source storage size)
- Verify network bandwidth between source and destination storages

#### [**Security Best Practices**](/docs/mdss/4.4.2/configuration/keep-or-move-or-copy-or-delete-files#security-best-practices)

- Use service accounts with minimum required permissions
- Enable encryption for sensitive file transfers
- Regular security audits of remediation workflows

Next steps after configuring remediation actions:

Test Workflows -> run test scans with sample files to verify remediation behavior

Plan scaling -> consider future storage and performance requirements
