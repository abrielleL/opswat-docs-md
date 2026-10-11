<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/operating/retrieving-files-from-an-external-source -->

# Retrieving Files from an External Source

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**Purpose:** Enhance diverse workflows for media handling options after users login on Kiosk UI successfully.

**Tactics:** The user can select two options: processing the files on the media or retrieving files on Kiosk UI.

### [Selecting a Retrieval Source](/docs/mdkiosk/v4.8.6/operating/retrieving-files-from-an-external-source#selecting-a-retrieval-source)

If your workflow is configured with more than one place to retrieve files from, Kiosk first asks you to choose which source to use. Only the sources your administrator has enabled for the workflow are listed.

If only one source is enabled, this selection step is skipped and Kiosk takes you directly to the Browse or Retrieve All screen.

Managing Retrieve file options

Starting from version Kisok 4.7.10, administrators can configure to display the BROWSE files option, the DOWNLOAD ALL option, or both.

After selecting to "Retrieve files" option, users can click `BROWSE`files to download specific files or choose `DOWNLOAD ALL` option to download all the files.

**Note:** When both options **" Allow user to browse for files"** and **"Allow user to process all files"** are disabled at Kiosk Interface configuration, the Kiosk will automatically select the "retrieve files options".

If user choose to pick "Guest login" option, an MFT owner ID will be required and there is space for users to flll out information.

Image: "Enter MFT Owner ID" on Kiosk UI

The data and files are available from MFT for downloading when they have "No Threat Detected" scan results and also remarked as "Available" or "Remediated" status. Those files are also marked in black colour in the MFT Files window. Files in other status are neither displayed nor available for downloading.

On Kiosk UI, the Browse view demonstrates that the system allow users to select specific files or data that are Available to download from MFT./

Process encrypted files

Starting from version 4.7.10, Kiosk support processing encrypted files when found. For details, see [Processing Encrypted Archives - MetaDefender Kiosk Windows](https://www.opswat.com/docs/mdkiosk/operating/processing-encrypted-archives)

If there is not enough data storage space on the media to download files, an alert will pop up to notify the amount of required data storage to retrieve the files.

Image: "Cannot proceed" tab pop-up when there is not enough data space on Kiosk
