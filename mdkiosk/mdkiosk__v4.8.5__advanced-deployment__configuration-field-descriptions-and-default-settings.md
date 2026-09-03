<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/advanced-deployment/configuration-field-descriptions-and-default-settings -->

# Configuration Field Descriptions and Default Settings

The following table provides a brief description and default values for the Kiosk Configuration screen.

## [Basic Configuration](/docs/mdkiosk/v4.8.5/advanced-deployment/configuration-field-descriptions-and-default-settings#basic-configuration)

| **Configuration Setting** | **Description** | **Default Value** | **Range** |
| --- | --- | --- | --- |
| Primary MetaDefender Server | URL of the primary MetaDefender server | (Blank) |  |
| API Key | The API Key of the primary MetaDefender server, if one is set | (Blank) |  |
| Server is a load balancer | Indicates that the primary server is a load balancer for MetaDefender  If checked, the API key is disabled | Unchecked |  |
| Periodically test Core servers every # hours | Periodic interval in which Kiosk will send an EICAR test file to test the Core server detection.  An alert will be logged if no engines detect the EICAR file. | 0 hour | 0 disables the periodic check  Min: 1 hour |
|  |  |  |  |
| Backup Server | Additional MetaDefender servers for the Kiosk to use if the primary is inaccessible (URL & API Key) | Empty |  |
|  |  |  |  |
| MFT Server | MFT servers to be used among different workflows (URL & Admin API key) | Empty |  |
|  |  |  |  |
| Printer Setup | Select the color of the printing output: `Black & White` or `Color` | `Black & White` |  |
| Side margins | Left and right margin length | 3 | 0 or greater  Recommended settings:  3 for a Zebra printer  200 for a Laser Jet |
| Display the MetaDefender URL in the session printout | The URL of the MetaDefender server (Core or MFT) used for a session will be displayed on the printout | Disabled |  |
| Include page numbers | Include the page number on each printed page | Enabled |  |
| Custom introduction message | Add a special header message to the first page of the printout | Disabled |  |
| Display logo | Add a custom logo image to the first page of the printer output. Supported formats: PNG, JPG, BMP, SVG, GIF. | Disabled | Max file size: 2 MB |
|  |  |  |  |
| Session Log > Destination Media | Enables a session text/PDF log to be created at the end of a session on the source media.  *This will not apply to read-only media such as discs or USBs that are not writable.* | Disabled  If enabled, the log will be saved to the root of the source media |  |
| Session Log > Destination Media | Enables a session text/PDF log to be created at the end of a session on the destination media.  *This will not apply to read-only media such as discs or USBs that are not writable.* | Disabled  If enabled, the log will be saved to the root of the destination media |  |
| Session Log > Directory Path | Enables a session text/PDF log to be created at the end of a session in a specified location (local or network share) | Enabled  Logging directory: `<kiosk install dir>\Client\Log` |  |
| Save as Text File / Save as PDF | Specifies whether the session log will be a text or PDF file | Text file |  |
| Display the MetaDefender URL in the session log | The URL of the MetaDefender server (Core or MFT) used for a session will be displayed in the log file | Disabled |  |
| Display logo | Add a custom logo image to the Session Log PDF. Only available when the session log is saved as a PDF (not a text file). If Media Passport is also enabled, the same logo appears on the Media Passport page. Supported formats: PNG, JPG, BMP, SVG, GIF. | Disabled | Max file size: 2 MB |
|  |  |  |  |
| Wipe Method | Specifies which wipe options to display to the user | All wipe methods shown | 0,1,3,7 pass wipe |
|  |  |  |  |
| Exit password | Require password when terminating the Kiosk UI (ALT+S) | Disabled |  |
| Kiosk Administrator's credentials | Require AD Management Console Admin credentials to close the Kiosk UI | Disabled |  |
|  |  |  |  |
| Watchdog | Custom action watchdog that will run when the Kiosk UI is unexpectedly terminated | `Restart Windows` | Options:  `Do nothing`  `Restart MetaDefender Kiosk`  `Log out of Windows`  `Lock Windows`  `Restart Windows` |
|  |  |  |  |
| Export Session History | Enables auto export of session history (in CSV) | Disabled |  |
| Export File History | Enables auto export of files history (in CSV) | Disabled |  |
| Frequency | Interval between history exports | 1 hour | Min: 1 hour  Max: 365 Days |
| Export Path | Directory where the history will be exported to | (Blank - `<kiosk install dir>\Client\Log`) |  |
|  |  |  |  |
| Country of Origin | COO engine detects the country an exe\dll binary originated from and marks the binary as blocked if the country is configured to be forbidden | Disabled |  |
|  |  |  |  |
| Image Media | Enables an image of the inserted media to be taken with the FTK Imager configured | Disabled |  |
| FTK Imager Path | The full path to the FTK Imager executable that handles imaging the media (ftkimager.exe) | (Blank) |  |
| Image Type | The image type FTK will output | RAW/DD |  |
| Fragment Size | The size of chunks the image will be separated into | 1 GB | 0 disables fragmenting the image  Min: 1  Max: 1024  (Min\Max per unit: KB - TB) |
| Compression Level | The compression applied to the image | 0 | Min: 0 (no compression)  Max: 9 (best compression) |
| Encrypt with password | Enables the image to be encrypted with a password.  The password is the name of the user logged in to the session and the id of the session: "<sessionID><username>" | Disabled |  |
| Encryption certificate path | The full path to a X.509 certificate to encrypt the image with.  Supported certificate formats:   - PKCS#12 / PFX (*.p12, *.pfx) - PEM (*.pem) - Stand-alone public key only (*.cer, *.crt, *.der) | (Blank) |  |
| MFT Server | MFT entry to upload the image to | (Blank) |  |
| Directory | Directory to upload the image to | (Blank) |  |

## [Advanced Configuration](/docs/mdkiosk/v4.8.5/advanced-deployment/configuration-field-descriptions-and-default-settings#advanced-configuration)

| **Configuration Setting** | **Description** | **Default Value** | **Range** |
| --- | --- | --- | --- |
| Max number of parallel scans | Maximum amount of concurrent file processing requests Kiosk will make to a MetaDefender server | 20 | 0 or greater |
| Max number of retries when MetaDefender Core is too busy | Maximum amount of retries that Kiosk will attempt on a file when the Core server notifies that it is too busy to handle new requests. Once the maximum amount of retries is reached for a file, the session will be canceled. | 0 | 0 for infinite  100 or greater |
| Boot sector processing | Allows processing of the first 512 bytes of an input media's partitions\disks.  When enabled, these boot sector files can be selected during browse or are automatically included when 'Process All' is selected.  Boot sector files cannot be included in file handling operations at the end of a session. | Enabled |  |
| Display warning for network errors | Display a warning to the user regarding network issues with the Core server while files are being processed | Enabled |  |
| Allow decryption of encrypted archives | Allows you to input passwords when encrypted archives are detected | Enabled |  |
| The maximum number of password attempts permitted during protected file or archive scanning | 0 (infinite) |  |  |
| The maximum timeout during protected file or archive scanning | 0 (infinite) |  |  |
| Allow user to skip entering a password for McAfee Encrypted USB | In the case that a McAfee encrypted drive is set to unlock via other means instead of a password, a user can skip entering a password | Disabled |  |
| Skip processing locked system files | Enables skipping of system files on media that Core cannot access and will typically result in a failed scan | Disabled |  |
| Skip hidden files and folders | Excludes files and folders marked as hidden from being shown, scanned, or copied. Not recommended unless you're certain hidden content on your media doesn't need to be scanned. | Disabled |  |
| Skip protected operating system files and folders | Excludes Windows-protected system files and folders from being shown, scanned, or copied. Not recommended unless you're certain protected system content on your media doesn't need to be scanned. | Disabled |  |
| Continue processing media with inaccessible content | Action to take when media has deeply nested directories that Kiosk cannot access | Disabled |  |
| Mount and scan Virtual Hard Disks | Allow processing of the contents within an VHD\VHDX file | Disabled |  |
| - Scan original Virtual Hard Disks | Enables sending the entire VHD\VHDX file to MetaDefender after all contents have been processed | Enabled |  |
| Mount and scan Virtual Machines | Allow processing of the contents within a VMDK file  Only VMDK with Windows file systems are currently supported. | Disabled |  |
| - Scan original Virtual Machines | Enables sending the entire VMDK file to MetaDefender after all contents have been processed | Enabled |  |
| Mount and scan Acronis disk backups | Allow processing of the contents within an Acronis disk backup | Disabled |  |
| - Scan original Acronis disk backups | Enables sending the entire Acronis disk backup to MetaDefender after all contents have been processed | Enabled |  |
| Acronis Executable Path | The full path to the Acronis executable that handles mounting the disk backup (acrocmd.exe) | (Blank) |  |
| Mount and scan Clonezilla images | Allow processing of the contents within a Clonezilla folder | Disabled |  |
| Only original Clonezilla image is scanned | Enabled |  |  |
| Heuristic File Type Detection | Kiosk will heuristically group similar file type extensions for reporting | Disabled |  |
| NTFS alternate data stream detection | Kiosk will display a warning in a file's details in both the result UI and reports if alternate data streams are detected in the file.  Alternate data streams will not be scanned - they will be ignored. | Disabled |  |
| Eclypt Management Application Path | The full path to the Eclypt Management Application that handles unlocking the Viasat drives (ema-ui.exe) | (Blank) |  |
| Choose File Scanning Option (***Kiosk 4.7.2 or newer***) | Available options:   - Select files: User can select files for processing - Process all files: User has to process all files in the media - Select or process all files: User can select between ‘Select files’ or ‘Processing all files’ options - Disable file processing: Kiosk does not process files | Select or process all files |  |
| User Interface Timeout | The Kiosk UI will automatically switch back to the idle screen if there is no user action within a specified time on the final screens of the session. | 5 minutes | Min: 60 seconds  Max: 20160 minutes (2 weeks) |
| Display welcome screen | Display the Welcome screen to a user when a new session is started | Enable |  |
| Display disclaimer screen | Display the disclaimer screen to a user when a new session is started | Enabled |  |
| Display scan estimation time | Display the scan estimation time to a user when a scan session is processing | Enabled |  |
| Display Total File Size | Controls whether the Processed Data Size field appears in the session summary and printed/exported scan report. Options: Show, Hide, or Use Global Settings. | Show |  |
| Allow update offline engine | Allow user to offline update engine directly from Kiosk UI | Disable |  |
| Allow user to browse for files | Allow user to select files before processing media | Enabled |  |
| Allow user to process all files | Allow user to select to process the entire media | Enabled |  |
| Alert user if MetaDefender Core license is close to expiration | Alerts you on the Kiosk idle screen if the Core license is close to expiration | Disabled |  |
| Alert user if MetaDefender Kiosk license is close to expiration | Alert you on the Kiosk idle screen if the Kiosk license is close to expiration | Disabled |  |
| Reboot at end of session | Specifies if the system should reboot after a session is completed or canceled. Exiting the Kiosk UI (ALT+S) during the session is not part of this option. | Disabled |  |
| Allow user to select languages | Allow user to select which language the Kiosk UI's text will be displayed as. If this setting is disabled, the default language selected will be locked in. | Enabled |  |
| Available Keyboards | The keyboards allowed for users to select within the on-screen Kiosk keyboard | All keyboards enabled |  |
| Choose Language | The default language to be used for the UI | English |  |
|  |  |  |  |
| Multiple Partitions | Selects the method for processing files on partitions | Process files on all accessible partitions |  |
|  |  |  |  |
| Parallel File Copy Threshold | Enhance performance by maximizing the number of concurrent files copied to the secondary location.  This setting applies to all types of secondary locations including Directory, User media, and MFT Server. | 1  Default value is recommended for copying to MFT. | Min: 1  Max: 100 |
|  |  |  |  |
| Boot Hardening - [Enable] [Disable] | Enables/Disables the process that causes the taskbar on the desktop not to load when Windows is logged in to run Kiosk, thereby disallowing any PC functionality until the Kiosk starts. | Disabled |  |
| Anti-tamper Hardening - [Enable] [Disable] | Enables/Disables security enhancement to prevent escaping the Kiosk UI while running.  Your system needs to be restarted to finish the changes. | Disabled |  |
| Active Keyboard Filter | Configure the keyboard filter to disable access certain key on the keyboard.  Only available if Anti-tamper Hardening is enabled. | Enabled |  |
|  |  |  |  |
| Host | IP or DNS of SMTP server | 127.0.0.1 |  |
| Port | Port of the SMTP server | 25 |  |
| Enable SSL | Enable the use of SSL | Disabled |  |
| Username | Username to authenticate to the SMTP server | (Blank) |  |
| Password | Password to authenticate to the SMTP server | (Blank) |  |
|  |  |  |  |
| Email Template | Template for customizing logos, colors, and font sizes for a workflow's email configuration |  |  |
|  |  |  |  |
| Enable (Pop Up Detection) | Enables Kiosk to detect any windows / pop ups open on the system | Disabled |  |
| Time Open Threshold | Threshold, in minutes, for a pop up to be open to trigger notification | 5 minutes | Min: 1 minute  Max: 60 minutes |
| Notification Action | Action to be taken when a pop up exceeds the time open threshold | Display warning |  |
| Process Allowlist | Ignore pop ups from the processes listed | (Blank) |  |
|  |  |  |  |
| File Integrity Monitor | Enables the File Integrity Monitor, which will shut Kiosk down if any unauthorized changes are made in the Kiosk install directory | Kiosk: disabled |  |
| Server | File Integrity Monitor server location | Kiosk: (blank) |  |
| Port | Port to connect to the File Integrity Monitor server | Kiosk: 0 |  |
| Username | User name to log into File Integrity Monitor server | Kiosk: (blank) |  |
| Password | Password to log into File Integrity Monitor server | Kiosk: (blank) |  |
|  |  |  |  |
| Verify SSL Certificates | Enables verification of SSL certificates when connecting to Core\MFT via HTTPS | Enabled |  |
| Add CA Cert | Add any self-signed or specialized certificates used for Kiosk to successfully verify | (blank) |  |
|  |  |  |  |
| Log Retention - Application Log | Specifies the length that Application Log entries will exist before being automatically deleted. | Never | Never - 12 months |
| Log Retention - Session History | Specifies the length that Session History entries will exist before being automatically deleted.  File history associated with the expired session history will also be deleted. | Never | Never - 12 months |
| Log Retention - Service log file size limit | Specifies the size that Service log file will exists before being automatically deleted. | 500MB | Min: 25MB Max: 500MB |
|  |  |  |  |
| Size Summary - Display | Displays the total files and size of selected files\folders when browsing for files. This is the global default; an individual workflow's Processing settings can override it — see **Display Total File Size** below. | Disabled |  |
| Size Summary - Max size to stop calculating | Kiosk stops calculating the selected files and folders if the accumulated size exceeds this threshold value.  This prevents users from waiting a long time when the total size is large. | 2 MB | Min: 1 MB  Max: 1024 GB |

## [Overriding File Size Display Per Workflow](/docs/mdkiosk/v4.8.5/advanced-deployment/configuration-field-descriptions-and-default-settings#overriding-file-size-display-per-workflow)

Each Employee and Guest workflow's **Processing** settings include a **Display Total File Size** option that controls whether the selected-files count and total size appear on that workflow's file-selection screen, independent of the global Size Summary setting above:

| Option | Effect |
| --- | --- |
| **Show** | Always displays the selected-files count and total size for this workflow. |
| **Hide** | Never displays the selected-files count and total size for this workflow. |
| **Use Global Settings** | Follows whatever the global Size Summary - Display setting is currently set to. |

This lets you show file size information to one group of users (for example, employees) while hiding it from another (for example, guests), without changing the global setting for everyone.

Note

The global **Size Summary - Max size to stop calculating** threshold continues to apply wherever the total is shown, whether it's shown because of the global setting or because a workflow is set to **Show**.

## [Scanning Engines Configuration](/docs/mdkiosk/v4.8.5/advanced-deployment/configuration-field-descriptions-and-default-settings#scanning-engines-configuration)

The **Scanning Engines** screen lets you enable or disable individual scanning engines and tune performance and workflow-processing behavior.

### [Engines](/docs/mdkiosk/v4.8.5/advanced-deployment/configuration-field-descriptions-and-default-settings#engines)

Under **Scanning Engines > Engines**, you can turn individual engines on or off, including specific antivirus engines, Deep CDR, and Proactive DLP, as well as utility engines such as Archive Extraction.

### [Performance settings](/docs/mdkiosk/v4.8.5/advanced-deployment/configuration-field-descriptions-and-default-settings#performance-settings)

| Configuration Setting | Description | Notes |
| --- | --- | --- |
| Queue size | The number of files Core queues for processing at once. | — |
| Parallel Count | The number of files Core processes in parallel. | Only editable when using a local Core. This field is disabled for a remote Core. |
| 7zip Parallel Count | The number of archive-extraction operations run in parallel. | Only editable when using a local Core. This field is disabled for a remote Core. |

### [Workflow processing options](/docs/mdkiosk/v4.8.5/advanced-deployment/configuration-field-descriptions-and-default-settings#workflow-processing-options)

Within a workflow's processing settings, two options let you tune how thoroughly files are handled:

- **Do not calculate file hashes** — available when a workflow is set to process files without scanning; skips hash calculation for those files.
- **Use existing process results if available** — reuses a file's previous scan result instead of scanning it again, when a matching result already exists.

Note

If your MetaDefender Core is managed by a central policy (through Central Management or vPack), the equivalent settings on this screen appear read-only, since the values are controlled centrally rather than on the individual device.
