<!-- source: https://www.opswat.com/docs/mdtransferguard/configuration/metadefender-core -->

# MetaDefender Core

The MetaDefender Diode X can be configured to integrate with an instance of the MetaDefender Core Advanced Threat Prevention Solution, installed on Diode X BLUE server. MD Core stops file-borne threats, including ransomware, zero-day exploits, and embedded malware, before they reach users or systems. It integrates seamlessly into existing infrastructure, securing uploads, downloads, email attachments, and file transfers without disrupting workflows. Diode X supports up to 10 AV engines. MD Core must be purchased separately from the Diode X.

Once configured, **all** files transferred using MetaDefender Diode X will be scanned for malicious activity by MetaDefender Core. The scan is performed prior to file transfer from BLUE to RED. For more details on MetaDefender Core management and operation, go to <https://docs.opswat.com/mdcore>

Info

The MetaDefender Diode X/ MetaDefender Core integration is supported on the BLUE side only.

A security dongle must be inserted in the BLUE side to change configuration.

## API Key

An API key is required in order to enable API integration with Diode X.

### Generating an API Key

Important

Before accessing the MetaDefender Core UI, the management IP needs to be changed from the default 10.10.10.10 address. Subnet 10.10.10.0/24 is an internal subnet used by MetaDefender Core and causes conflict when trying to access.

On MetaDefender Diode X BLUE, go to **http://<management IP>:8008** to access MetaDefender Core UI and login.

1. From the sidebar menu go to **User Management.**
2. Click on **Admin** user.
3. Copy the API key (generate one if the box is empty). It will be used to configure the Diode X BLUE side integration with MetaDefender Core.

Copy/Generate API Key

## Diode X BLUE

This section describes configuration of the Diode X BLUE to communicate with MD Core.

### Initial Setup

On Diode X BLUE navigate to **MetaDefender Core -> Connection**. Select **Edit** and fill in the following fields:

1. **URL:** URL of the MD Core instance used to scan files.
2. **API Key:** API Key for authorized access to MD Core. Paste the API Key copied in the previous Generating API key step.
3. **Timeout**: the maximum duration Diode X maintains an idle TCP connection in its state table before closing it. Default = 60.
4. **Block Empty Files:** Block zero byte files
5. **Enabled:** Click check box to enable communication with MD Core.
6. **Core Version:** Version of MD Core installed.
7. **Submit:** Press Submit to save configuration.

Initial Setup - BLUE

### Configure Workflow and Logging

Navigate to **MetaDefender Core -> Configuration**. Select **Edit** and fill in the following fields:

1. **Default Workflow:** Choose a default workflow. The values from this selector (other than system default) are retrieved from MetaDefender Core. There must be a successful connection to retrieve workflows.
2. **Log Level:** Level of logging. Default: Info
3. **Syslog:** Switch on logging to a remote ('protocol://<hostname>:<port>') syslog server. Multiple syslog servers can be specified separated with a comma).
4. **CEF:** Select checkbox to enable Common Event Formatting.
5. **Syslog Level:** Level of Syslog logging. Optional.

Configure Workflow and Logging

## Maintenance

On daily basis MetaDefender Core performs data base maintenance operations, freeing database space and generating database log files. Once generated, users can download and/or delete the files in the Maintenance tab.

Navigate to **MetaDefender Core -> Maintenance**. Download or delete MD Core maintenance files.

MetaDefender Core Maintenance File

## History Data

Diode X will keep records of files transferred from BLUE to RED. To review File Transfer History Data, click on the **History** tab within the File Transfer section.

Info

File Transfer Historical Data is not stored in backups.

History Data

History data can be filtered in several ways.

- **Undelivered:** Shows undelivered transfers. File has not been received by the RED side.
- **Time Filters:** Daily, weekly, monthly or date range filters can be applied.
- **Search Box:** Search for specific files by typing text.

File Transfer History

History information can be viewed on both the BLUE and RED sides.

## File Scan Results

When a file is blocked, the MetaDefender Core Scan Result report can be reviewed by clicking on the word **blocked** in the corresponding file.

File Transfer Status

Blocked File Report
