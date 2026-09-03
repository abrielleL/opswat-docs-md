<!-- source: https://www.opswat.com/docs/mdmft/automated-file-transfer/mft---pull-filesw8h -->

# MFT - Push Files

Summarize Page    Connect to Cursor Connect to VS Code

Use this type of job to automatically push files to a remote MetaDefender Managed File Transfer™ instance.

Difference from MFT to MFT

Unlike the system-level MFT to MFT mirroring functionality, the MFT - Push Files job only transfers files from configured sources for users who have specifically defined these jobs.

## [Configuration](/docs/mdmft/automated-file-transfer/mft---pull-filesw8h#configuration)

**Target MFT Username**

The username to authenticate with on the remote MetaDefender Managed File Transfer instance.

---

**Target MFT Password**

The password to authenticate with on the remote MetaDefender Managed File Transfer instance.

Info

In case of editing or duplicating a previously saved job, the password needs to be re-entered.

---

**Select MFT API Key**

If the **MFT API Key** input type is selected. You should select a stored API key to authenticate with the remote MetaDefender Managed File Transfer instance. This is required when multi-factor authentication (MFA) is enabled on the remote server. See: [MFT Keys](/docs/mdmft/end-user-guide/my-credentials#mft-keys)

---

**Select Target MFT**

The MetaDefender Managed File Transfer integration to which files will be pushed. See: [MFT Integration](/docs/mdmft/integrations/mft-integrations).

---

**Source Folders**

Provide paths to recursively collect and push files to the selected MetaDefender Managed File Transfer instance via HTTP(S). Any number of paths can be configured; if no path is added, the root ('/') will be used as the source path.

Folder Structure

The folder structure under the configured source paths will be preserved at the destination.

---

**Push Files as a Member of the Selected Group**

Enter the Active Directory group you want to use for uploading files. Different groups may have different security settings. This field is required when uploading files to an Active Directory user on the target MFT.

For further information, see [Custom MetaDefender Core Workflow Rule for Groups](/docs/mdmft/operating/custom-metadefender-core-workflow-rule-for-groups) and [Active Directory Supervisors Setup](/docs/mdmft/configuration/active-directory-supervisors-setup).

---

**Destination at Target MFT**

The destination path on the remote MetaDefender Managed File Transfer instance where the files will be pushed. If the path does not exist, it will be created automatically.

---

**Transfer Method**

Decide what to do with the original files on the local instance.

- **Copy Files**: Files successfully pushed will remain intact on the local instance.
- **Move Files**: Files successfully pushed will be removed from the local instance.
- **Sync Files:** Keeps a remote destination folder identical to a local source folder.

Move Files

If multiple source paths point to the same file, the file will only be deleted from the local instance if it was successfully pushed from all listed source paths.

For example, if *move* is enabled and there is a file located at `/data/logs/log.txt` and the source paths `/data` and `/data/logs` are both configured with the destination `/pull,` it will only be removed from the local instance if pushing is successful for both `/pull/logs/log.txt` and `/pull/log.txt`.

---

**Duplicate File Transfer Rule**

Decide what to do if a file with the same path already exists on the remote MetaDefender Managed File Transfer instance:

- **Skip duplicates:** The file from MetaDefender MFT is not pushed to the destination.
- **Transfer duplicates with unique names:** The existing destination file is kept. The new file from MetaDefender MFT is pushed and saved at the destination with a unique name.
- **Overwrite existing files:** Push the file to the remote host, overwriting the existing one.

Overwrite Existing

The **Overwrite existing files** option doesn't do any pre-check on the local or the remote file, it is just simply overwriting the remote file with the local one even if they contain the same data. This means if a file does not change on the local instance, the same file will be pushed repeatedly.

---

**Sync Behavior for Deleted Files**

Decide on the course of action if the selected transfer method is **Sync Files.**

- **Delete from destination:** If a file or folder is deleted from the source, it will also be deleted from the destination on the next job run. This ensures the destination remains an exact mirror of the source.
- **Retain on destination:** If a file or folder is deleted from the source, it will **not** be deleted from the destination. This option is useful when you want to use Sync to transfer new and updated files but need to prevent any data from being automatically removed from the destination.

---

## [Example](/docs/mdmft/automated-file-transfer/mft---pull-filesw8h#example)

I want to push files to my remote MetaDefender Managed File Transfer™ instance from my local instance. . I only want to push files that are under the paths */work/share* and */tools*, and I want this to be done every Tuesday at 10 AM and on Fridays at 4 PM. My username is *teodor* and my password is *pass%123!* on the remote instance.

My remote instance can be reached via the FQDN *mft.remote.io*. I want my files to remain on my local instance and just copy them to my user folder under */pushed/mft* on the remote instance. If a file already exists on the remote instance, I don't want to overwrite it.
