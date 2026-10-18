<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/advanced-deployment/configuring-global-kiosk-settings -->

# Configuring Global Kiosk Settings

View as Markdown Ask ChatGPT about this page Ask Claude about this page

The Configuration page lets you configure global settings for MetaDefender Kiosk.

## Protect closing the Kiosk

It is highly recommended to set exit credentials to protect the Kiosk scanning User Interface from being closed by users.

Two options exist to protect exiting the Kiosk UI:

### Exit password

Select this options to require users to enter a password when exiting the Kiosk. After selecting this checkbox, two fields appear: **New password** and **Confirm password**.

### Kiosk Administrator's credentials

Select this option to allow AD users, that are assigned as administrative users of the Management Console, to close the Kiosk UI. Upon attempting to close the UI, a prompt will be displayed to enter AD credentials.

## Configuring session log files

You can save session log files as a text or PDF file, and choose to save log files to a specific location on the system or to the processed media. By default, MetaDefender Kiosk saves session log files to the Log folder in the MetaDefender Kiosk installation directory.

To save session log files:

1. Select the **Save as Text File** or **Save as PDF** radio button, depending on the output type of the session log files you prefer.
2. Select the destination to save the session logs

   1. By default, Kiosk will automatically save the session logs to the local Kiosk's log folder. The admin can change to a different location by providing **Directory Path**
   2. In addition, the admin can also configure to save session logs to **Source Media** and **Destination Media**
3. **Display the MetaDefender URL used in the session log** allows for the MetaDefender URL, that was used for the session, to be displayed in the log file. This is useful when configuring a backup Core server and determining which server was used for a particular session.
4. **Export separate logs for archive files > ISO File.** When enabled, MetaDefender Kiosk generates a separate, detailed log specifically for ISO files. Instead of a single result for the whole ISO, the detailed log lists every file and folder inside the ISO individually, each with its own scan result and SHA-256 hash — making it easier to identify exactly which file inside a disk image was flagged or failed to process. If the ISO contains another ISO nested inside it, the detailed log automatically includes the contents of the nested ISO as well.

**Note:** The save options are independent from each other. You can save session logs locally and/or save it to the processed media or disable session log files altogether.

> **Note:** Converting a very large session log to PDF can take a long time — potentially several minutes or more — during which the end-of-session screen shows no progress indicator. This is most likely with workflows that scan a large amount of data in one session, such as a full scan of a large virtual disk image. If you expect a workflow to regularly produce very large session logs, choosing the **Text file** format avoids this delay. If a PDF session log appears to be taking a long time to generate, allow it to finish rather than restarting the session.

> **Note:** The detailed ISO log follows the same format (text or PDF) and destination settings (default location, custom directory, source/destination media, or email) configured above for session logs. This option is off by default and can also be configured centrally through Central Management.

## Auto Export Logs

The session and/or file history can be configured to be automatically exported to a specified directory path in CSV format. By default, the history will be exported to the Kiosk's log directory. The frequency dictates how often the automatic export will run.

## Setting advanced configuration options

You can set advanced configuration options by expanding the Advanced Configuration section of the Configuration page.

**Allow preloading of passwords for encrypted files**

This allows users to provide passwords of encrypted archives before scanning. The Kiosk application detects encrypted files and asks users to provide passwords in advance so that the scanning can proceed without waiting for user input.

**Maximum password attempts**

This allows administrators to configure the maximum number of password attempts permitted during protected file or archive scanning. This setting helps prevent repeated brute‑force attempts and ensures better control over scanning workflows involving encrypted content.

**Timeout for encrypted file unlock**

This allows administrators to configure a timeout limit for unlocking encrypted files. When a password is required, a countdown is shown to the user while Kiosk waits. If the user does not provide a password within the configured time, the unlock attempt is stopped and the file is automatically marked as blocked, and processing continues with the next file. This helps prevent stalled workflows and ensures that scanning continues smoothly without being blocked by unattended password prompts.

The timeout applies separately to each encrypted file — if a session includes more than one encrypted file, each one gets its own full countdown. If an encrypted file is nested inside an archive and its unlock attempt times out, the containing archive is blocked as well.

Note

Set the timeout to `0` to disable it (the default), which restores the previous behavior of waiting indefinitely for a password.

## Email Settings

The admin can configure SMTP server to support for email sending at session termination. It's advised to use SMTP mail server, not relay. The username and password are authenticated to login to mail server. Any sender configured to appear as a From field in the email header must be an email address that the username has permission to send as. See [Email Session Report](/operating/email-session-report) or [Visitor Management](/metadefender-kiosk-windows/v4.5.7/advanced-deployment/visitor-management) for email header settings

To configure oAuth email authentication with Microsoft 365 (Graph API), please refer to [this guide](https://www.opswat.com/docs/mdkiosk/advanced-deployment/configuring-global-kiosk-settings#email-settings).

The admin can verify if the email configuration is correct by providing existing email addresses as [From Address] and [To Address] and proceeding SEND. [From Address] must be an email that the username has permission to send as.

## Email Template

The email template allows Kiosk admin to prepare common email content in HTML format. It will apply for email part in the workflow creation. This template aims to email signature with a company logo. The logo attached in the template should be a low resolution not exceeding 100KB and only one.

The email template does not apply for testing email.

## Disk Image Files

The administrator can configure Kiosk to scan 4 types of disk images:

1. Virtual Hard Disks refer .VHD or .VHDX files
2. Virtual Machines refer .VMDK files
3. Arcronis Disk backups refers to .TIB or .TIBX files. The path of the Acronis executable is necessary. For example: C:\Program Files\Acronis\CommandLineTool\acrocmd.exe
4. Clonezilla image. The files and folders must meet the required structure. Please see this KB for more details [link](https://www.opswat.com/docs/mdkiosk/knowledge-base/how-to-scan-clonezilla-images-with-kiosk).

**Acronis Disk backups**

Contents within a disk backup created by Acronis can be processed when Acronis backup software is installed on the system. When enabling Kiosk to process the contents in a backup, the path to the Acronis command line executable must be provided (e.g. `C:\Program Files\Acronis\CommandLineTool\acrocmd.exe`). This will allow the disk backup to be mounted to the system for Kiosk to access. The disk backup will be unmounted once the Kiosk session is finished.

**Clonezilla Images**

The contains of a Clonezilla folder must follow the structure:

- It contains clonezilla-img, disk, parts, and Info-img-id.txt.
- The disk file has one line with the disk name (e.g., sda, sdb).
- The parts file lists partition names (e.g., sdb1 sdb2 sdb4).
- Required files exist for that disk: DISKNAME-pt.parted, DISKNAME-mbr, DISKNAME-gpt-1st, DISKNAME-gpt-2nd.
- Partition data files follow the format: PARTITION.FILESYSTEM-ptcl-img. (e.g., sdb1.xfs-ptcl-img.gz.aa).

See [Configuration Field Descriptions and Default Settings](https://www.opswat.com/docs/mdkiosk/advanced-deployment/configuration-field-descriptions-and-default-settings) for more details about the options.

**LVM Disk Image**

Kiosk 4.7.11 adds support for scanning LVM (Logical Volume Manager) disk images, allowing users to perform full security analysis on files and directories stored inside LVM volumes without converting the disk to another format.

The disk image must use the .lvm file extension for Kiosk to recognize and mount it.

## Multiple Partitions

| Option | Single Windows Partition | Only Windows Partitions | Mixed Windows and Non Windows Partitions | Only Mac / Linux Partitions |
| --- | --- | --- | --- | --- |
| Block all media with multiple partitions | SCAN ONE | BLOCKED | BLOCKED | BLOCKED |
| Process files on all accessible partitions | SCAN ALL | SCAN ALL | SCAN ALL | SCAN ALL |

The SCAN ALL action will mount every partition it can successfully mount. All partitions will be scanned by "Process All." The file browser will have the ability to select files on any partition.

## Managing the display language

You can also change the default language displayed in MetaDefender Kiosk from the Choose Language drop-down menu. Options include English, Arabic, Hebrew, Korean, Vietnamese, German, Japanese, Spanish and French . If you wish to add a language to the MetaDefender Kiosk UI or edit the translations of any of the existing languages, click **View and edit languages** .

## Pop Up Detection

Enabling pop up detection will allow Kiosk to detect any windows/pop ups open on the underlying desktop and notify the user. Any pop up that triggers the detection will be logged to the Application Log on the WebMC, along with the process that owns it. *Time Open Threshold* indicates how long a pop should be open until Kiosk notifies that a pop up needs attention. *Process Allowlist* specifies any process whose pop ups will be ignored from triggering the detection. *Notification Action* indicates what action Kiosk will take to notify the user:

- *Display warning* - a warning will be displayed indicating that there is a pop up that requires attention
- *Display warning and disable Kiosk* - warning displayed with the addition of canceling any running session and disallowing any new session to be started until the Administrator attends to the pop up. This requires closing the UI, handling the pop up and starting Kiosk again.

## Screensaver

Kiosk screensaver helps protect the LCD lifetime or to play company introduction video or ads. Kiosk disables Windows system screensaver and support an alternative in the settings. By default, a built-in screensaver is selected. The admin can select desired video or image from an URL or local sources.

To change the screensaver settings, navigate to **Configuration**, select **Kiosk U**I, expand **Customize Theme**. Select the source of the screensaver video or image

- **Browse file**: Click on the clip icon to select and upload a local media file to use as screensaver

- **Use URL:** Provide the URL links to the media files. Kiosk must have permissions to access and play the media file.

- **Disable screensaver while processing files:** When enabled, Kiosk will not play screensaver at the file scanning and scan result screens.

Info

- Supported media types:

  - **Video**: MP4, 3GP, MKV, MOV, MPEG-4, WebM
  - **Image**: JPG, PNG, ICO, GIF, SVG, WEBP
- This list is fully supported when uploading with Google Chrome browser, other browsers can make some of the media types cannot be previewed.
- If the video or URL is invalid, the default will be played instead.
Self Scan and Screen saver

If Self Scan is triggered while the screen saver is active, the screen saver remains running.
