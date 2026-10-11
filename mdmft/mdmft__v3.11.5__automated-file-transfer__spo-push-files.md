<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/automated-file-transfer/spo-push-files -->

# SPO – Push Files

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool Trademark Notice

SharePoint Online™ (referred to as "SPO" in this documentation) is a registered trademark of Microsoft Corporation.

Use this type of job to automatically push files to an SPO document library.

Info

During automated file transfers, only files in the "Available" and "Sanitized" states within the source folders will be transferred.

## [Configuration](/docs/mdmft/v3.11.5/automated-file-transfer/spo-push-files#configuration)

**Credential Input Type**

Two types of authentication can be used:

- **Secret**: client ID and client secret
- **Certificate**: client ID and selecting a previously stored certificate (see: [My Credentials](https://app.developerhub.io/mdmft/end-user-guide/my-credentials))

---

**Target SPO Client ID**

This is the unique identifier assigned to the registered MetaDefender MFT application in Microsoft Entra ID. The Client ID is used to authenticate MetaDefender MFT when accesing a document library.

It can be found in the "Azure Portal" under the Entra ID "App registrations" section. As it is a GUID, it should look like this: "12345678-90ab-cdef-1234-567890abcdef."

---

**Target SPO Client Secret**

This secret is used to authenticate MetaDefender MFT when accessing a document library.

It can be found in the "Azure Portal" under the Entra ID "App registrations" section.

Info

Please note that this refers to the *client secret value*, not the client secret ID.

Info

If you edit or duplicate a previously saved job, the Client Secret must be re-entered.

---

**Select Certificate**

If the Certificate credential input type was selected, beside adding the Client ID, which used to authenticate to the document library, you should select the proper stored certificate to authenticate.

---

**Selecting Target SPO**

Choose the SPO integration you want to use. Files will be pushed to the document library configured in the selected integration. See: [SPO Integration](/docs/mdmft/v3.11.5/integrations/spo-integration).

---

**Providing Source Path(s)**

Specfify the paths from which files should be recursively collected and pushed from MetaDefender Managed File Transfer. Multiple paths can be configured. If no path is added, the root ('/') will be the default source path.

---

**Destination at Target SPO**

Specify the destination path in the SPO document library. If the path does not exist, it will be created automatically.

---

**Transfer Method**

Choose what to do with the original files on MetaDefender Managed File Transfer.

- **Copy Files**: Files that are successfully pushed will remain intact on MetaDefender Managed File Transfer.
- **Move Files**: Files that are successfully pushed will be removed from MetaDefender Managed File Transfer.
- **Sync Files:** Keeps a remote destination folder identical to a local source folder.

Move Files

If multiple source paths point to the same file, the file will only be deleted from the local instance if it was successfully pushed from all listed source paths.

For example, if *move* is enabled and there is a file `/data/logs/log.txt` with source paths `/data` and `/data/logs` are configured with the destination `/push`, the file will only be removed from the local instance if pushing was successful for both `/push/logs/log.txt` and `/push/log.txt`.

---

**Duplicate File Transfer Rule**

Decide how to handle files that already exists in the SPO document library with the same absolute path:

- **Skip duplicates:** The file from MetaDefender MFT is not pushed to the destination.
- **Transfer duplicates with unique names:** The existing destination file is kept. The new file from MetaDefender MFT is pushed and saved at the destination with a unique name.
- **Overwrite existing files:** Push the file to the remote host, overwriting the existing one.

Overwrite Existing

- When overwriting a file on SPO, all previous versions will remain intact and can be accessed in the file's version history.
- Only the files that have changed either in MetaDefender MFT or in the SPO document library since the last job run will be pushed to SPO. Identical files will not be pushed.

---

**Sync Behavior for Deleted Files**

Decide on the course of action if the selected transfer method is **Sync Files.**

- **Delete from destination:** If a file or folder is deleted from the source, it will also be deleted from the destination on the next job run. This ensures the destination remains an exact mirror of the source.
- **Retain on destination:** If a file or folder is deleted from the source, it will **not** be deleted from the destination. This option is useful when you want to use Sync to transfer new and updated files but need to prevent any data from being automatically removed from the destination.

## [Example](/docs/mdmft/v3.11.5/automated-file-transfer/spo-push-files#example)

Suppose you want to push files from MetaDefender Managed File Transfer to your SPO document library. You only want to push files from the folder named **"**teodor,**"** located in the root folder, every 30 minutes. Your Metadefender MFT application client ID is **"**12345678-90ab-cdef-1234-567890abcdef,**"** and the Client Secret is **"**0123456~7890abcdEFGHijklm_nopQRS-TUVWxyz**"**.

Your SPO document library, named **"**Documents,**"** is available at "[https://thiscompany.sharepoint.com/sites/oursite](https:)**"**. You want the files to be copied to the folder **"**/teodor/from_mft**"** in your SPO document library. If a file already exists there, overwrite it if it has been changed since the last job run, while keeping the previous versions intact.
