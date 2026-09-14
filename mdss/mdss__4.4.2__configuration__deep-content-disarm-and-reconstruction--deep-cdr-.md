<!-- source: https://www.opswat.com/docs/mdss/4.4.2/configuration/deep-content-disarm-and-reconstruction--deep-cdr- -->

# Deep Content Disarm and Reconstruction (Deep CDR)

Enabling the File Sanitization feature creates a secure version of a file by removing potentially harmful content. This process utilizes OPSWAT's Deep Content Disarm and Reconstruction (Deep CDR) technology.

For detailed configuration instructions, refer to the [Deep CDR user guide](https://www.opswat.com/docs/mdcore/deep-cdr).

Learn more about OPSWAT's Deep CDR technology: <https://www.opswat.com/technologies/data-sanitization>

## [Enabling Deep CDR](/docs/mdss/4.4.2/configuration/deep-content-disarm-and-reconstruction--deep-cdr-#enabling-deep-cdr)

Dependency

In order to be able to use the Deep CDR functionality, Deep CDR must be active in MetaDefender Core instance or Metadefender Cloud.

1. Navigate to **Workflows** from the left-side navigation menu.
2. Select the workflow for which you want to enable Deep CDR.
3. In the **Workflow Diagram**, click on the "**Deep CDR**" node
4. In the modal window that's opened, select the **Deep CDR** tab and toggle **Active** to enable File Sanitization

Info

Enabling Deep CDR, also enables the configuration nodes for sanitized files that were allowed or blocked, which define what will happen with the sanitized file. Disabling Deep CDR disables the two nodes.

## [Replace Original Files with Sanitized Versions](/docs/mdss/4.4.2/configuration/deep-content-disarm-and-reconstruction--deep-cdr-#replace-original-files-with-sanitized-versions)

Info

This is currently only supported for **OneDrive** and **SharePoint** storage types.

### [Overview](/docs/mdss/4.4.2/configuration/deep-content-disarm-and-reconstruction--deep-cdr-#overview)

This feature enables **true in-place replacement** of original files with their sanitized counterparts produced by Deep CDR.

Previously, when Deep CDR was configured to *keep the sanitized version* and *delete the original*, the system performed these actions as two separate steps:

- A **new sanitized file** was uploaded
- The **original file** was deleted

With Replace Original Files enabled, the original file is **replaced directly** with the sanitized content, preserving file continuity by creating a new version of the same file rather than a new file.

### [How to Enable](/docs/mdss/4.4.2/configuration/deep-content-disarm-and-reconstruction--deep-cdr-#how-to-enable)

1. Enable Deep CDR in the MetaDefender Storage Security Workflow
2. Check **“Replace Original Files with Sanitized Versions”**
3. Click Save Changes

When Replace Original Files with Sanitized Versions is enabled, all other **file remediation options are disabled and locked**.

### [File Version Cleanup (Optional)](/docs/mdss/4.4.2/configuration/deep-content-disarm-and-reconstruction--deep-cdr-#file-version-cleanup-optional)

By default, previous file versions are **retained** after replacement.

To automatically delete older file versions after replacement, set the following environment variable:

envCopyDELETE_FILE_VERSIONS_AFTER_REPLACE=1
