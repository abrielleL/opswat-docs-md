<!-- source: https://www.opswat.com/docs/mdmft/automated-file-transfer/mft---pull-files -->

# MFT - Pull Files

Summarize Page    Connect to Cursor Connect to VS Code

Use this type of job to automatically retrieve files from a remote MetaDefender Managed File Transfer™ instance.

To securely transfer files from a low-security network, it is often more secure for the high-security network to initiate the transfer. Once initiated, the files will be pushed from the low-security network.

Difference from MFT to MFT

Unlike the system-level *MFT to MFT mirroring* functionality, using the *MFT - Pull Files* job will only pull files from the configured sources for the users who have defined such jobs.

## [Configuration](/docs/mdmft/automated-file-transfer/mft---pull-files#configuration)

MFT Pull configuration viewed as an user

**Source MFT Username**

The username to authenticate with on the remote MetaDefender Managed File Transfer instance.

---

**Source MFT Password**

The password to authenticate with on the remote MetaDefender Managed File Transfer instance.

Info

In case of editing or duplicating a previously saved job, the password needs to be re-entered.

---

**Select MFT API Key**

If the **MFT API Key** input type is selected. You should select a stored API key to authenticate with the remote MetaDefender Managed File Transfer instance. This is required when multi-factor authentication (MFA) is enabled on the remote server. See: [MFT Keys](/docs/mdmft/end-user-guide/my-credentials#mft-keys)

---

**Select MFT Source**

Select the MetaDefender Managed File Transfer integration to use. Files will be pulled from the selected instance. See: [MFT Integration](/docs/mdmft/integrations/mft-integrations).

---

**Provide Source Paths**

Specify the paths to recursively collect and pull files from the remote MetaDefender Managed File Transfer™ instance through HTTP(S). You can configure any number of paths; if no path is added, the root ("/") will be the default source path.

Folder Structure

The folder structure under the configured source paths will be preserved under the destination.

---

**Pull Files as a Member of the Selected Group**

Select the "Active Directory group" you want to upload files to. Different groups may have different security settings. This field is available if your account is from Active Directory and you belong to multiple groups, or if the "Allow Users to Upload Files Without Specifying Group Membership" option is disabled.

For further information, see [Custom MetaDefender Core Workflow Rule for Groups](/docs/mdmft/operating/custom-metadefender-core-workflow-rule-for-groups) and [Active Directory Supervisors Setup](/docs/mdmft/configuration/active-directory-supervisors-setup).

---

### [**Destination Settings**](/docs/mdmft/automated-file-transfer/mft---pull-files#destination-settings)

Choose how destinations are configured for this pull job. Two modes are available:

- **Use a Single Destination Folder:** All files and subfolders are pushed to one selected destination folder.
- **Map Source Subfolders to Users:** Each source subfolder is mapped to a specific target user and destination folder.

#### [**Use a Single Destination Folder**](/docs/mdmft/automated-file-transfer/mft---pull-files#use-a-single-destination-folder)

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

#### [**Map Source Subfolders to Users**](/docs/mdmft/automated-file-transfer/mft---pull-files#map-source-subfolders-to-users)

When **Map Source Subfolders to Users** is selected, you can define multiple source-to-user-to-destination mappings using a CSV file. This allows a single job to distribute files from different source sub-folders to different users' vaults.

Download the .csv template, complete the columns, and upload it to map source subfolders to users. Use the same email address in multiple rows to assign multiple folders to a single user.

---

### [**Transfer Method**](/docs/mdmft/automated-file-transfer/mft---pull-files#transfer-method)

Decide what to do with the original files on the remote instance:

- **Copy Files**: Files successfully pulled will remain on the remote instance.
- **Move Files**: Files successfully pulled will be removed from the remote instance.
- **Sync Files:** Keeps a local destination folder identical to a remote source folder.

Move Files

If multiple source paths point to the same file, the file will only be deleted on the remote instance if it was successfully pulled from all listed source paths.

For example, if *move* is enabled and there is a file located at `/data/logs/log.txt` and the source paths `/data` and `/data/logs` are configured with the destination `/pull,` the file will only be removed from the remote instance if the pull was successful for both `/pull/logs/log.txt` and `/pull/log.txt`.

---

### [**Duplicate File Transfer Rule**](/docs/mdmft/automated-file-transfer/mft---pull-files#duplicate-file-transfer-rule)

Decide what to do if a file with the same path already exists in the local MetaDefender Managed File Transfer instance:

- **Skip duplicates:** The file on the remote share is not pulled into MFT.
- **Transfer duplicates with unique names:** The existing local file is kept. The new file from the remote share is pulled and saved locally with a unique name.
- **Overwrite existing files:** Pull the file from the remote host and replace the locally existing one.

Overwrite Existing

The **Overwrite existing files** option does not perform any pre-check on the local or remote file, it simply overwrites the local file with the remote one, even if both files contain the same data. This means if a file does not change on the remote instance, the same file will be pulled repeatedly.

Overwrite behavior with Sanitized Files

The **Overwrite existing files** option will not work for files that have been sanitized by MetaDefender Core and had their filenames changed.

For example, if a file `file.pdf` is sanitized and renamed to `file_sanitized_by_OPSWAT_MetaDefender.pdf` by a Core rule, the overwrite function in MFT will not recognize it as the same file, and a new file will be created instead of overwriting the old one.

To ensure files are overwritten as expected, you can configure the sanitization rules in MetaDefender Core. This will maintain the original filename after sanitization, allowing MFT's overwrite function to work correctly.

---

### [**Sync Behavior for Deleted Files**](/docs/mdmft/automated-file-transfer/mft---pull-files#sync-behavior-for-deleted-files)

Decide on the course of action if the selected transfer method is **Sync Files**.

- **Delete from destination:** If a file or folder is deleted from the source, it will also be deleted from the destination on the next job run. This ensures the destination remains an exact mirror of the source.
- **Retain on destination:** If a file or folder is deleted from the source, it will **not** be deleted from the destination. This option is useful when you want to use Sync to transfer new and updated files but need to prevent any data from being automatically removed from the destination.

---

### [**Flatten folder structure on destination**](/docs/mdmft/automated-file-transfer/mft---pull-files#flatten-folder-structure-on-destination)

When enabled, all files pulled to the destination will be placed directly into the destination folder without preserving their original folder structure.

---

### [**Workflow Override**](/docs/mdmft/automated-file-transfer/mft---pull-files#workflow-override)

If enabled, select which MetaDefender Core Workflow Rule will analyze the files being pulled.

Info

If Workflow Override is not enabled, the analysis will follow the same MetaDefender Core Workflow Rule as for a manually uploaded file.

## [Example](/docs/mdmft/automated-file-transfer/mft---pull-files#example)

I want to pull files from my remote MetaDefender Managed File Transfer instance into my local instance. I only want to pull files that are under the path */work/share* and */tools*, I want this process to occur on Tuesdays at 10 AM and on Fridays at 4 PM. My username is *teodor* and my password is *pass%123!*.

My remote instance can be accessed at the FQDN *mft.remote.io*. I want my files to remain on my remote instance, just copy them to my user under the path **/pulled/mft** on the local instance. If a file exists locally then *keep it, do not overwrite it*. I want my MetaDefender Core integration to analyze such files by the workflow rule "Pulled From Remote MFT."

Pull MFT configuration with Configured Times

Rest of Pull MFT configuration
