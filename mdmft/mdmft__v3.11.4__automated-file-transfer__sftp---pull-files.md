<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/automated-file-transfer/sftp---pull-files -->

# SFTP - Pull Files

Summarize Page    Connect to Cursor Connect to VS Code

Use this type of job to automatically pull files from a remote host using SFTP.

## [Configuration](/docs/mdmft/v3.11.4/automated-file-transfer/sftp---pull-files#configuration)

SFTP Pull configuration viewed as an user

**Credential Input Type**

Two types of authentication can be used:

- **Manual**: username and password
- **SSH Key**: username and selecting previously stored private SSH key (see: [My Credentials](/docs/mdmft/v3.11.4/end-user-guide/my-credentials))

---

**Source SFTP Username**

The username used to authenticate via SFTP on the selected host.

---

**Source SFTP Password**

The password used to authenticate via SFTP on the selected host. It is possible to provide an empty password.

Info

In case of editing or duplicating a previously saved job, the password needs to be re-entered.

---

**Select SSH Key**

If the SSH Key credential input type was selected, beside adding the username which used to authenticate on the SFTP server, you should select the proper stored private SSH key to authenticate.

---

**Select Source SFTP**

Select the SFTP integration to use. Files will be pulled from the selected host. See: [SFTP Integration](/docs/mdmft/v3.11.4/integrations/sftp)

---

**Provide Source Paths**

Provide paths to recursively collect and pull files from the selected host through SFTP. You can configure any number of paths; if no path is added, the root ('/') will be the default source path.

Folder Structure

The folder structure under the configured source paths will be preserved under the destination.

---

**Pull Files as a Member of the Selected Group**

Select the "Active Directory" group under which you want to upload files. Different groups may have different security settings. This field is available if your account belongs to Active Directory and you are part of multiple groups, or if the "Allow Users to Upload Files Without Specifying Group Membership" option is disabled.

For further information about the security aspects, read [Custom MetaDefender Core Workflow Rule for Groups](/docs/mdmft/v3.11.4/operating/custom-metadefender-core-workflow-rule-for-groups) and [Active Directory Supervisors Setup](/docs/mdmft/v3.11.4/configuration/active-directory-supervisors-setup).

---

### [**Destination Settings**](/docs/mdmft/v3.11.4/automated-file-transfer/sftp---pull-files#destination-settings)

Choose how destinations are configured for this pull job. Two modes are available:

- **Use a Single Destination Folder:** All files and subfolders are pushed to one selected destination folder.
- **Map Source Subfolders to Users:** Each source subfolder is mapped to a specific target user and destination folder.

#### [**Use a Single Destination Folder**](/docs/mdmft/v3.11.4/automated-file-transfer/sftp---pull-files#use-a-single-destination-folder)

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

#### [**Map Source Subfolders to Users**](/docs/mdmft/v3.11.4/automated-file-transfer/sftp---pull-files#map-source-subfolders-to-users)

When **Map Source Subfolders to Users** is selected, you can define multiple source-to-user-to-destination mappings using a CSV file. This allows a single job to distribute files from different source sub-folders to different users' vaults.

Download the .csv template, complete the columns, and upload it to map source subfolders to users. Use the same email address in multiple rows to assign multiple folders to a single user.

---

### [**Transfer Method**](/docs/mdmft/v3.11.4/automated-file-transfer/sftp---pull-files#transfer-method)

Decide what to do with the original files on the remote host:

- **Copy Files**: Files successfully pulled will remain on the remote host.
- **Move Files**: Files successfully pulled will be removed from the remote host.
- **Sync Files:** Keeps a local destination folder identical to a remote source folder.

Move Files

If multiple source paths point to the same file, the file will only be deleted on the remote host if it was successfully pulled from all listed source paths.

For example, if *move* is enabled and there is a file `/data/logs/log.txt` and source paths `/data` and `/data/logs` are configured with the destination `/pull,` the file will only be removed from the remote host if pulling was successful for both `/pull/logs/log.txt` and `/pull/log.txt`.

---

### [**Duplicate File Transfer Rule**](/docs/mdmft/v3.11.4/automated-file-transfer/sftp---pull-files#duplicate-file-transfer-rule)

Decide what to do if a file with the same absolute path already exists in MetaDefender Managed File Transfer:

- **Skip duplicates:** The file on the remote share is not pulled into MFT.
- **Transfer duplicates with unique names:** The existing local file is kept. The new file from the remote share is pulled and saved locally with a unique name.
- **Overwrite existing files:** Pull the file from the remote host and replace the locally existing one.

Overwrite Existing

The **Overwrite existing files** option does not perform any pre-check on the local or remote file; it simply overwrites the local file with the remote one, even if they contain the same data. This means if a file does not change on the remote host, the same file will be pulled repeatedly.

Overwrite behavior with Sanitized Files

The **Overwrite existing files** option will not work for files that have been sanitized by MetaDefender Core and had their filenames changed.

For example, if a file `file.pdf` is sanitized and renamed to `file_sanitized_by_OPSWAT_MetaDefender.pdf` by a Core rule, the overwrite function in MFT will not recognize it as the same file, and a new file will be created instead of overwriting the old one.

To ensure files are overwritten as expected, you can configure the sanitization rules in MetaDefender Core. This will maintain the original filename after sanitization, allowing MFT's overwrite function to work correctly.

---

### [**Sync Behavior for Deleted Files**](/docs/mdmft/v3.11.4/automated-file-transfer/sftp---pull-files#sync-behavior-for-deleted-files)

Decide on the course of action if the selected transfer method is **Sync Files**.

- **Delete from destination:** If a file or folder is deleted from the source, it will also be deleted from the destination on the next job run. This ensures the destination remains an exact mirror of the source.
- **Retain on destination:** If a file or folder is deleted from the source, it will **not** be deleted from the destination. This option is useful when you want to use Sync to transfer new and updated files but need to prevent any data from being automatically removed from the destination.

---

### [**Workflow Override**](/docs/mdmft/v3.11.4/automated-file-transfer/sftp---pull-files#workflow-override)

If enabled, select which MetaDefender Core Workflow Rule should analyze the files being pulled.

Info

If Workflow Override is not enabled, the analysis will use the same MetaDefender Core Workflow Rule as it would for a manually uploaded file.

## [Example](/docs/mdmft/v3.11.4/automated-file-transfer/sftp---pull-files#example)

I want to pull files from my remote Ubuntu 20.04 host into MetaDefender Managed File Transfer. I only want to pull files located in my home folder, and I want this to occur every Monday at 10 AM. My username is *teodor* and my password is *pass%123!*.

My Ubuntu host is accessible through the FQDN *lnx.home.io*, where the SSH server is running on port 22. I want to keep the files on my Linux host, while copying them for my user under the path `/pulled/lnx` in MetaDefender Managed File Transfer. If a file already exists at this destination, I want it to be overwritten. For these files, I want my MetaDefender Core integration to analyze them with the Workflow Rule named "Pulled From Linux."
