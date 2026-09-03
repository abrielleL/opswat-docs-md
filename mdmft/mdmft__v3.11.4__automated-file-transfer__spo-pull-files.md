<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/automated-file-transfer/spo-pull-files -->

# SPO – Pull Files

Summarize Page    Connect to Cursor Connect to VS Code Trademark Notice

SharePoint Online™ (referred to as "SPO" in this documentation) is a registered trademark of Microsoft Corporation.

Use this type of job to automatically pull files from an SPO document library to MetaDefender MFT.

## [Configuration](/docs/mdmft/v3.11.4/automated-file-transfer/spo-pull-files#configuration)

**Credential Input Type**

Two types of authentication can be used:

- **Secret**: client ID and client secret
- **Certificate**: client ID and selecting a previously stored certificate (see: [My Credentials](https://app.developerhub.io/mdmft/end-user-guide/my-credentials))

---

**Source SPO Client ID**

This is the unique identifier assigned to the registered MetaDefender® MFT application in Microsoft Entra ID. The Client ID is used to authenticate MetaDefender® MFT when accessing a document library.

It can be found in the "Azure Portal" under the Entra ID "App registrations" section. As it is a GUID, it should look like this: "12345678-90ab-cdef-1234-567890abcdef."

---

**Source SPO Client Secret**

This secret is used to authenticate MetaDefender® MFT when accessing a document library.

It can be found in "Azure Portal" under the Entra ID "App registrations" section.

Info

Note that this refers to the *client secret value,* not the client secret ID.

Info

If you edit or duplicate a previously saved job, the Client Secret must be re-entered.

---

**Select Certificate**

If the "Certificate" credential input type is selected, in addition to providing the Client ID used for authentication with the document library, you should select the appropriate stored certificate for authentication.

---

**Selecting Source SPO**

Choose the SPO integration you wish to use. Files will be pulled from the document library configured in the selected integration. See: [SPO Integration](/docs/mdmft/v3.11.4/integrations/spo-integration).

---

**Providing Source Path(s)**

Specify the paths from which to recursively collect and pull files from the selected SPO document library. Multiple paths can be configured.

Folder Structure

The folder structure beneath the configured source path(s) will be preserved at the destination.

---

**Pulling Files as a Member of the Selected Group**

Select the "Active Directory group" under which you want to upload files. Different groups may have different security settings. This field is available if your account is from AD, you belong to multiple groups, or if the "Allow Users to Upload Files Without Specifying Group Membership" option is disabled.

For more details on security, see [Custom MetaDefender Core Workflow Rule for Groups](/docs/mdmft/v3.11.4/operating/custom-metadefender-core-workflow-rule-for-groups) and [Active Directory Supervisors Setup](/docs/mdmft/v3.11.4/configuration/active-directory-supervisors-setup).

---

### [**Destination Settings**](/docs/mdmft/v3.11.4/automated-file-transfer/spo-pull-files#destination-settings)

Choose how destinations are configured for this pull job. Two modes are available:

- **Use a Single Destination Folder:** All files and subfolders are pushed to one selected destination folder.
- **Map Source Subfolders to Users:** Each source subfolder is mapped to a specific target user and destination folder.

#### [**Use a Single Destination Folder**](/docs/mdmft/v3.11.4/automated-file-transfer/spo-pull-files#use-a-single-destination-folder)

When **Use a Single Destination Folder** is selected (the default), all files pulled from the source will be placed into a single destination in MetaDefender Managed File Transfer. This matches the traditional pull job behavior.

Selecting this mode reveals the **Transfer files to** and **Destination at MFT** fields described below.

- **Transfer files to:** Choose who the pulled files should be delivered to. Three target options are available

  - **My Files** (default): Files are delivered to your own vault. This is the default behavior and maintains backward compatibility with existing jobs.
  - **Specific User:** Files are delivered to a selected user's vault. Search for the user by name or email.
  - **User Group:** Files are delivered to every active member of the selected group. Each group member receives their own copy of the pulled files. Groups can be Custom, Active Directory, or Single Sign-On groups.

Role-Based Access

- **Administrators** can target any user or any group in the system.
- **Automation Coordinators** can only target users and groups that have been explicitly delegated to them by an Administrator. See: Coordinator Group Delegation.

- **Destination at MFT:** Specify the destination path in MetaDefender Managed File Transfer where the files will be pulled. Type a folder name or click **Browse** to select from existing folders.

#### [**Map Source Subfolders to Users**](/docs/mdmft/v3.11.4/automated-file-transfer/spo-pull-files#map-source-subfolders-to-users)

When **Map Source Subfolders to Users** is selected, you can define multiple source-to-user-to-destination mappings using a CSV file. This allows a single job to distribute files from different source sub-folders to different users' vaults.

Download the .csv template, complete the columns, and upload it to map source subfolders to users. Use the same email address in multiple rows to assign multiple folders to a single user.

---

### [**Transfer Method**](/docs/mdmft/v3.11.4/automated-file-transfer/spo-pull-files#transfer-method)

Choose what to do with the original files on the remote file share:

- **Copy Files**: Successfully pulled files will remain intact on the remote file share.
- **Move Files**: Successfully pulled files will be removed from the remote file share.
- **Sync Files:** Keeps a local destination folder identical to a remote source folder.

Move Files

If multiple source paths point to the same file, the file will only be deleted from the remote host if it was successfully pulled from all listed source paths.

For example, if *move* is enabled and there is a file located at `/data/logs/log.txt` with source paths `/data` and `/data/logs` are configured with destination `/pull,` the file will only be removed from the remote file share if both `/pull/logs/log.txt` and `/pull/log.txt` are successfully pulled.

---

### [**Duplicate File Transfer Rule**](/docs/mdmft/v3.11.4/automated-file-transfer/spo-pull-files#duplicate-file-transfer-rule)

Decide how to handle files that already exists in MetaDefender Managed File Transfer™ with the same absolute path:

- **Skip duplicates:** The file on the remote share is not pulled into MFT.
- **Transfer duplicates with unique names:** The existing local file is kept. The new file from the remote share is pulled and saved locally with a unique name.
- **Overwrite existing files:** Pull the file from the remote host and replace the locally existing one.

Overwrite Existing

The **Overwrite existing files** option does not perform any pre-check on the local or remote file; it simply replaces the local file with the remote one, even if they contain the same data. Therefore, if a file does not change on the remote host, it will be pulled repeatedly.

Overwrite behavior with Sanitized Files

The **Overwrite existing files** option will not work for files that have been sanitized by MetaDefender Core and had their filenames changed.

For example, if a file `file.pdf` is sanitized and renamed to `file_sanitized_by_OPSWAT_MetaDefender.pdf` by a Core rule, the overwrite function in MFT will not recognize it as the same file, and a new file will be created instead of overwriting the old one.

To ensure files are overwritten as expected, you can configure the sanitization rules in MetaDefender Core. This will maintain the original filename after sanitization, allowing MFT's overwrite function to work correctly.

---

### [**Sync Behavior for Deleted Files**](/docs/mdmft/v3.11.4/automated-file-transfer/spo-pull-files#sync-behavior-for-deleted-files)

Decide on the course of action if the selected transfer method is **Sync Files**.

- **Delete from destination:** If a file or folder is deleted from the source, it will also be deleted from the destination on the next job run. This ensures the destination remains an exact mirror of the source.
- **Retain on destination:** If a file or folder is deleted from the source, it will **not** be deleted from the destination. This option is useful when you want to use Sync to transfer new and updated files but need to prevent any data from being automatically removed from the destination.

---

### [**Workflow Override**](/docs/mdmft/v3.11.4/automated-file-transfer/spo-pull-files#workflow-override)

If enabled, select which MetaDefender Core™ Workflow Rule should analyze the pulled files.

Info

If Workflow Override is not enabled, the analysis will use the same MetaDefender Core Workflow Rule as for a manually uploaded file.

## [Example](/docs/mdmft/v3.11.4/automated-file-transfer/spo-pull-files#example)

Suppose you want to pull files from your SPO document library into MetaDefender Managed File Transfer™. You only want to pull files from the folder named **"**teodor**"** every monday at 10AM. Your Metadefender MFT application client ID is **"**12345678-90ab-cdef-1234-567890abcdef**"** and the Client Secret is **"**0123456~7890abcdEFGHijklm_nopQRS-TUVWxyz**"**.

Your SPO document library, named **"**Documents,**"** is available at [**https://thiscompany.sharepoint.com/sites/oursite**](https://). You want the files to remain on your SPO document library, and only copy them to the path **"**/pulled/spo**"** on MetaDefender Managed File Transfer. If a file already exists there, overwrite it. You want your MetaDefender Core integration to analyze these files using the workflow rule **"**Pulled from SPO.**"**
