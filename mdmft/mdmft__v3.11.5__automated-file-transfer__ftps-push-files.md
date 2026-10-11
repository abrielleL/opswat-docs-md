<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/automated-file-transfer/ftps-push-files -->

# FTPS – Push Files

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

Use this type of job to automatically push files to a file share on a remote host using the FTPS protocol.

Info

During the automated file transfer, only files with *Available* and *Sanitized* states in the source folders will be transferred.

## [Configuration](/docs/mdmft/v3.11.5/automated-file-transfer/ftps-push-files#configuration)

**Target FTPS Username**

The username used to authenticate via the FTPS protocol on the selected host.

---

**Target FTPS Password**

The password used to authenticate via the FTPS protocol on the selected host.

---

**Server Certificate**

Select how the server certificate should be validated. Two options are available:

- **All certificates are accepted**: The MFT will accept any certificate presented by the FTP server (useful for self-signed certificates).
- **Certificate**: Choose a specific, previously stored certificate associated with your Client ID (see: [My Credentials](/docs/mdmft/v3.11.5/end-user-guide/my-credentials))

---

**Connection Mode**

Select the mode used for data connections. Two modes are supported:

- **Active:** The client opens a port and waits for the server to connect. (Note: You must specify a valid port range).
- **Passive:** The server opens a port and waits for the client to connect.

---

**Select Target FTPS**

Select the FTPS integration to use. Files will be pushed to the selected file share. See: [FTPS Integration](/docs/mdmft/v3.11.5/integrations/ftps-integration).

---

**Provide Source Path(s)**

Provide paths to recursively collect and push files from MetaDefender Managed File Transfer. Any number of paths can be configured. If no path is defined, the root ('/') will be the default source path.

---

**Destination at Target FTPS**

The destination path on the remote file share. If the path does not exist, it will be created automatically.

---

**Transfer Method**

Decide what to do with the original files on MetaDefender Managed File Transfer:

- **Copy Files**: Files successfully pushed will remain on MetaDefender Managed File Transfer.
- **Move Files**: Files successfully pushed will be removed from MetaDefender Managed File Transfer.
- **Sync Files:** Keeps a remote destination folder identical to a local source folder.

Move Files

If multiple source paths point to the same file, the file will only be deleted from the local instance if it is successfully pushed from all listed source paths.

For example, if *move* is enabled and there is a file located at `/data/logs/log.txt` and source paths `/data` and `/data/logs` are configured with the destination `\push,` it will only be removed from the local instance if pushing is successful for both `\push\logs\log.txt` and `\push\log.txt`.

---

**Duplicate File Transfer Rule**

Decide what to do if a file with the same absolute path exists in the remote file share.

- **Skip duplicates:** The file from MetaDefender MFT is not pushed to the destination.
- **Transfer duplicates with unique names:** The existing destination file is kept. The new file from MetaDefender MFT is pushed and saved at the destination with a unique name.
- **Overwrite existing files:** Push the file to the remote host, overwriting the existing one.

Overwrite Existing

The **Overwrite existing files** option does not perform any pre-check on the local or remote file; it simply overwrites the remote file with the local one, even if they contain the same data. This means if a file does not change on the local instance, the same file will be pushed repeatedly.

---

**Sync Behavior for Deleted Files**

Decide on the course of action if the selected transfer method is **Sync Files.**

- **Delete from destination:** If a file or folder is deleted from the source, it will also be deleted from the destination on the next job run. This ensures the destination remains an exact mirror of the source.
- **Retain on destination:** If a file or folder is deleted from the source, it will **not** be deleted from the destination. This option is useful when you want to use Sync to transfer new and updated files but need to prevent any data from being automatically removed from the destination.

## [Example](/docs/mdmft/v3.11.5/automated-file-transfer/ftps-push-files#example)

I want to push files to my remote FTP server from MetaDefender Managed File Transfer. I only want to push files located in the 'share' folder of my root directory, and I want this to be done every 30 minutes. My username is 'teodor' and my password is 'pass%123!' on the remote host.

The FTP server is reachable via the FQDN 'planet.jupiter.io' on port 21. I want my files to be copied from my local folder to the directory '/teodor/from_mft' on the FTP server. If a file already exists at the destination, I want to overwrite it
