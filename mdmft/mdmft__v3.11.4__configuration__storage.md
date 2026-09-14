<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/configuration/storage -->

# File Storage

Summarize Page    Connect to Cursor Connect to VS Code

MetaDefender Managed File Transfer™ supports various types of storage (local, network, Amazon S3) for different purposes (temporary, processed, permanent, archived). Configure these storage types by navigating to the "Settings" → "File Storage" page.

Storage types:

|  | Type | Description |
| --- | --- | --- |
| 1 | Local | A storage represented by a local directory on the disk. |
| 2 | Network storage | A storage represented by a network location. |
| 3 | Amazon S3 storage | A bucket or a directory inside a bucket on Amazon S3 for saving files in the cloud. |
| 4 | S3 Compatible Storage | A bucket or a directory inside a bucket on S3 compatible storage for saving files in the cloud. |

Storage Purposes:

|  | Purpose | Description |
| --- | --- | --- |
| 1 | Temporary | Used to save files before processing and for files scheduled for reprocessing |
| 2 | Processed | Used to save files sanitized by MetaDefender Core™ |
| 3 | Permanent | Used to save fully processed files available for download |
| 4 | Archive | Used to save files no longer needed but kept for audit purposes |

### [Adding a New Local Storage](/docs/mdmft/v3.11.4/configuration/storage#adding-a-new-local-storage)

Add a new local storage:

1. Go to "Settings" → "File Storage"
2. Choose the purpose (Permanent, Processed, Temporary, Archive) and click "Add New Storage"
3. Fill out the required information

4. Click "Add New Storage"

### [Adding a New Network Storage](/docs/mdmft/v3.11.4/configuration/storage#adding-a-new-network-storage)

MetaDefender Managed File Transfer™ supports connecting to Network Storage via the SMB (Server Message Block) protocol. This allows files to be read from or written to a shared network path, such as a NAS or Windows file share.

Info

Samba is supported from protocol version SMB2_10.

| Input Field | Description | Required |
| --- | --- | --- |
| Path | The full UNC (Universal Naming Convention) path to the network share. Example: `\\server-name\share-name`. | Yes |
| Domain | The domain of the user account used to access the share. If your environment uses domain-based authentication (such as Active Directory), provide the domain name here. | No |
| Username | The username for accessing the share. Required if the share is not publicly accessible or requires specific credentials. | No |
| Password | The password corresponding to the provided username. Only required when a username is specified. | No |

Info

If the network share allows guest or anonymous access, the username, password, and domain fields can be left empty.

Add a new network storage:

1. Go to "Settings" → "File Storage"
2. Choose the purpose (Permanent, Processed, Temporary, Archive) and click "Add New Storage"
3. Fill out the required information

4. Click "Add New Storage"

### [Adding a New Cloud Storage in Amazon S3](/docs/mdmft/v3.11.4/configuration/storage#adding-a-new-cloud-storage-in-amazon-s3)

Add a new cloud storage:

1. Go to "Settings" → "File Storage"
2. Choose the purpose (Permanent, Processed, Temporary, Archive) and click "Add New Storage"
3. Fill out the required information

4. Click "Add New Storage"

### [Adding S3 Compatible Storage](/docs/mdmft/v3.11.4/configuration/storage#adding-s3-compatible-storage)

Add a new S3 compatible storage:

1. Go to "Settings" → "Storage"
2. Choose the purpose (Permanent, Processed, Temporary, Archive) and click "Add New Storage"
3. Fill out the required information (input values are case sensitive)

4. Click "Add New Storage"

### [Storage history](/docs/mdmft/v3.11.4/configuration/storage#storage-history)

After a new storage was added, the previously used storage becomes inactive. The information about the previously used storages - individually of each purpose - can be reached by clicking on the "View history":

On the detailed storage history page you can check the ground information for the inactive storage(s):

By clicking on the three dot action button you can choose from different actions:

- **Move to Active Storage**: move the files from the inactive storage to the currently used active storage. The process may take a long time depending on the number and size of the files, but it can be followed on the appearing process corner modal. Please note that the closing of the process modal won't cancel the moving process.
- **Reactivate storage**: set the selected inactive storage as the active one (the active will be inactivated)
- **Delete storage:** Deletes the inactive storage if it is no longer needed

Info

Move to Active Storage action is not available for Temporary Storages.
