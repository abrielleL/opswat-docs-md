<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/operating/selecting-a-server-to-process-files -->

# Selecting a Server to Process Files

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [I. File limits](/docs/mdkiosk/v4.8.6/operating/selecting-a-server-to-process-files#i-file-limits)

**Tactics:** Configure specific rules to restrict users from initiating a scan session at pre-processing phase.

**Benefit:** Allow users to optimize and choose data size, file extensions which will be scanned on Kiosk later manually.

If the users select files that exceed applied configured rules, they cannot initiate a scan session. Those rules will be applied to both **Browse** and **Process All** in **Processing options**. The appropriate messages will appear on Kiosk UI and prevent the users from starting the session.

### [**Limited number of files**](/docs/mdkiosk/v4.8.6/operating/selecting-a-server-to-process-files#limited-number-of-files)

Configuring the maximum number of files that the user can select. The minimum value that can be input is 0, max is 100,000,000.

Image: "File count exeeds limit" notification on Kiosk UI

### [**Limited file size**](/docs/mdkiosk/v4.8.6/operating/selecting-a-server-to-process-files#limited-file-size)

Configuring the maximum size of each file, measured in megabytes (MB) or gigabytes (GB). The minimum value that can be input is 0, maximum is 10,000.

Image: "File size exeeds limit" notification on Kiosk UI

### [**Limit of total file size**](/docs/mdkiosk/v4.8.6/operating/selecting-a-server-to-process-files#limit-of-total-file-size)

Configuring the maximum total size of all selected files, measured in megabytes (MB) or gigabytes (GB). The minimum value that can be input is 0, max is 10,000.

Image: "Total file size exeeds limit" notification on Kiosk UI

### [**Blocked file extensions**](/docs/mdkiosk/v4.8.6/operating/selecting-a-server-to-process-files#blocked-file-extensions)

List of blocked extensions that user cannot select to scan. The user needs to input at least one file extension in order to activate this feature. Extension in list is separated by semicolon (`;`).

Image: "Blocking file extensions" option on Kiosk Configuration

**Image:** Blocked file on Kiosk UI (after applying blocking .exe file extension on Management Console)

**Image:** Notification appears on Kiosk UI when selecting folders contain blocked file extensions

Info

**Process All**: A "Limit Exceeded" attention will be displayed if any values surpass their respective threshold.

Image: "Limit Exceeded" notification on Kiosk UI for Process All

Note

Scan limits is not available for Simplified Workflow

II. Processing

### [1. Do not proceed files with a MetaDefender or MFT server](/docs/mdkiosk/v4.8.6/operating/selecting-a-server-to-process-files#1-do-not-proceed-files-with-a-metadefender-or-mft-server)

In the case of no scan requirements, the admin can choose neither MetaDefender nor MFT. With this option, only file handling can be executed.

The hash calculation of files can be disabled with option `Do not calculate file hashes` to speed up the duration of the session.

Image: "Do not proceed files with MetaDefender or MFT Server" option on Kiosk configuration page

Image: "Processing file without scanning" option on Kiosk configuration page

### [2. Use MetaDefender Core server](/docs/mdkiosk/v4.8.6/operating/selecting-a-server-to-process-files#2-use-metadefender-core-server)

MetaDefender Kiosk requires a MetaDefender Core server in order to use the multi-scanning technologies and functionalities. The MetaDefender Core server can be installed on the same system as MetaDefender Kiosk or on another machines. The MetaDefender Core server used is configured in the Primary MetaDefender Server option on the [Configuration settings page](/docs/mdkiosk/v4.8.6/advanced-deployment/configuring-global-kiosk-settings).

Image: "Use MetaDefender Core" option on Kiosk Configuration page

#### [Workflow Rule](/docs/mdkiosk/v4.8.6/operating/selecting-a-server-to-process-files#workflow-rule)

The Workflow Rule drop-down menu determines which MetaDefender Core workflow rule is used to process files from MetaDefender Kiosk.

There are two processing methods to utilize a MetaDefender server:

#### [Files are only processed with the available MetaDefender server chosen at the start of a session](/docs/mdkiosk/v4.8.6/operating/selecting-a-server-to-process-files#files-are-only-processed-with-the-available-metadefender-server-chosen-at-the-start-of-a-session)

The default behavior is an available MetaDefender server will be selected at the beginning of a session. Any errors encountered with the server will cause Kiosk to retry processing the file with the server.

#### [**Include Media Manifest on User Media**](/docs/mdkiosk/v4.8.6/operating/selecting-a-server-to-process-files#include-media-manifest-on-user-media)

When used with MetaDefender Core version 4.8.0+, a media manifest can be added to media processed by MetaDefender Kiosk. This setting enables the creation of a signed Media Manifest that contains the scan results for all files that were scanned as part of the session. This manifest can be validated by other MetaDefender products.

The KIOSK allows choosing the storage location for the manifest.

- **Source and Destination**: By default, the manifest will be saved on both the scanned media and the destination media configured on the [User media](/docs/mdkiosk/v4.8.6/operating/selecting-how-to-handle-processed-files#user-media) page.
- **Only Destination**: The manifest will be exclusively stored on the destination media.

#### [Files are processed with any available MetaDefender server during a session](/docs/mdkiosk/v4.8.6/operating/selecting-a-server-to-process-files#files-are-processed-with-any-available-metadefender-server-during-a-session)

The second processing method allows Kiosk to choose any available server (Primary + Backups) during a session. If any connection failure occurs during the session, Kiosk will re-attempt processing the file on the next available server. With this method selected, the Media Manifest feature cannot be carried out. When viewing files processed under this method in Core's history, they will be displayed individually rather than being grouped into a session entry. All other features are allowed regardless of the processing method selected.

#### [Copy & Go](/docs/mdkiosk/v4.8.6/operating/selecting-a-server-to-process-files#copy--go)

Files to process are copied from the media to the system for processing later. Users are informed to remove their media when the copy has finished. Once the session is finished, all processed files are removed from the system. The system must have enough free space to accommodate all the files to process.

#### [Use file results from media manifest if available](/docs/mdkiosk/v4.8.6/operating/selecting-a-server-to-process-files#use-file-results-from-media-manifest-if-available)

Kiosk can also validate files according to the Media Manifest file that exists on the media to be processed. If a file is found on the media but not found within the manifest, it will be sent to MetaDefender for processing. The certificate with which the manifest is signed by needs to be trusted on the system, else Kiosk cannot trust the manifest and will send files for processing.

#### [Use existing process results if available](/docs/mdkiosk/v4.8.6/operating/selecting-a-server-to-process-files#use-existing-process-results-if-available)

Kiosk can retrieve previously existing results for files by performing a hash lookup instead of uploading a file to MetaDefender for processing. This cannot be used in conjunction with Media Manifest since the manifest always contains the latest results.

#### [File larger than ## [MB/GB] will be not scanned by MetaDefender](/docs/mdkiosk/v4.8.6/operating/selecting-a-server-to-process-files#file-larger-than--mbgb-will-be-not-scanned-by-metadefender)

A maximum file size can be specified for files to be processed by MetaDefender, all files larger than this will still be processed by Kiosk without being processed by MetaDefender. The files that are larger are treated as configured allowed or blocked due to the reason `"Exceeded file size"` .

Image: Choose file size that will be scanned and proceeded by MetaDefender Kiosk

#### [File Integrity Verification](/docs/mdkiosk/v4.8.6/operating/selecting-a-server-to-process-files#file-integrity-verification)

File Integrity Verification (available in Kiosk 4.7.11 or later) is an optional security setting to ensure that files scanned on a Kiosk are not altered, tampered with, or corrupted while being transmitted to MetaDefender Core for processing.

When File Integrity Verification is turned on, Kiosk performs an extra hash-based check around the Core scan:

1. Hash on the Kiosk side: Before sending a file to MetaDefender Core, Kiosk computes the file's SHA‑256 hash.
2. Hash on the Core side: MetaDefender Core also computes the SHA‑256 hash of the file it received and returns it with the scan result.
3. Comparison: Kiosk compares the two hashes:

   - If the hashes match, the file is confirmed to be unchanged in transit. The successful verification is recorded in the session log for audit purposes.
   - If the hashes do not match, Kiosk blocks the file with the reason Integrity Check Failed and records an integrity warning, helping operators detect tampering or transmission errors.

The result of the check is captured in the session history, the session log (text and PDF), the printed receipt, and syslog as:

File Integrity Verification Notes

- **Performance impact:** Because Kiosk must compute a SHA‑256 hash for every file and then validate the value returned by Core, scanning sessions may take longer when this option is enabled.
- **Require processing with Core**: Verification applies only when files are processed by MetaDefender Core. It is not applicable to "Processing file without scanning" or "Use MetaDefender Managed File Transfer" modes.
- **Blocked files:** Files that fail verification are treated like any other blocked file and follow the workflow's configured handling for blocked content (quarantine, delete, copy restrictions, etc.).
## [III. Using MFT Server](/docs/mdkiosk/v4.8.6/operating/selecting-a-server-to-process-files#iii-using-mft-server)

To reduce user time spent at the Kiosk, processing files can be offloaded to a MFT server connected to a MetaDefender Core. Files will be uploaded directly from Kiosk to MFT, once uploading is done, the session will complete and the user may remove their media and proceed. Meanwhile, MFT will send the uploaded files to MetaDefender to process and, based on the configuration, notify the user when the files are ready for retrieval.

- **Workflow:** MD Core workflow rule that MFT will use to proceed the uploaded files
- **MFT Server:** See [6. Configuring with MFT](/docs/mdkiosk/v4.8.6/configuration/configuring-with-metadefender-vault) for instructions and more details
- **Select a MFT account option for file uploads:** Choose a MFT account option in this section

  - **Guest account:** A temporary guest login ID is created and displayed to the Kiosk user both on the scan results screen as well as in the digital and printed logs.
  - **User credentials:** Use the designated user login credentials for logging into the MFT server.
  - **Specific MFT user:** Transmit files directly to a specified user on the MFT system. (This can be useful when custom authentication users do not match users synced with MFT)
- **File Chunk Upload Size:** Size of chunks a file will be broken into for uploading to MFT. The acceptable input range for values is from 0 to 10000 MB/GB.
- **Maximum File Upload Size:** files exceeding the maximum size is not uploaded to MFT server. The acceptable input range for values is from 0 to 10000 MB/GB.
- **Maximum Number Of Upload Files:** upload files until the upload count reaches the maximum. The acceptable input range for values is from 0 to 10000.

Info

If upload authentication fails, files will be uploaded to a MFT guest account
