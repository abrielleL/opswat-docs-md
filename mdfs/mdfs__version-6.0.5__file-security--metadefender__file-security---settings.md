<!-- source: https://www.opswat.com/docs/mdfs/version-6.0.5/file-security--metadefender/file-security---settings -->

# File Security - Configuration and Settings

To configure the OPSWAT | MetaDefender for Salesforce application for file uploads, navigate to the application in Salesforce via the app launcher and click on "OPSWAT - Settings" below the search bar on the top of the page.

The table below provides information on each one of the fields you can configure on that page above:

| Field Name | Description |
| --- | --- |
| Scan Server | The default value is MetaDefender Cloud (this field is read only). |
| API Key | You can log into (or register for an account) on the [OPSWAT Portal](https://id.opswat.com/login?redirect=https://my.opswat.com&app=appOCM0001) to view your API Key which you can copy/paste into this field. When your organization makes a purchase of MetaDefender for Salesforce OPSWAT will help provision your API key to the appropriate limits. |
| Paid User | This field presents the API license status. |
| Expiration Date | This is the date your API Key will expire. |
| Multiscanning | When the mode is set to "Enable", files entering your Salesforce environment will be scanned by [OPSWAT's MetaDefender Cloud](https://metadefender.opswat.com/) which consists of 15 industry leading antivirus engines. If this field is set to "Disable", files will not be scanned by MetaDefender Cloud. |
| File Sanitization | When this field is set to "Enable", the app will send the file to MetaDefender Cloud for sanitization using [OPSWAT Deep CDR technology](https://www.opswat.com/technologies/deep-content-disarm-and-reconstruction) |
| Sandbox Scan | When the 'Enable' option is selected for this field, the file will be sent for analysis to assess threat behavior using [OPSWAT Sandbox technology](https://www.opswat.com/products/metadefender/sandbox) |
| File Sanitization Option* | 1. New Version With _sanitized Suffix: This will result in the sanitized file being a new version of the existing file with "_sanitized" Suffix. 2. New Version With Original File Name: This will result in the sanitized file being a new version of the existing file while keeping the original file name without any alteration. 3. Separate File: This will create a separate file for the sanitized version that will be a separate Salesforce record from the original file. 4. Delete Original File: This will delete the original file so that only the sanitized version is retained in Salesforce. |
| Data Loss Prevention | Proactive DLP engine is designed to identify sensitive data within files. You can choose to enable it and the sensitive information within files would be detected, by default the DLP is disabled. |
| Do not scan files with these file extensions (separated by ",") | You can instruct the system to exclude specific file extensions from scanning by entering them in the textbox, (separated by commas ","). If you wish to scan all file extensions, leave the textbox empty. |
| Block the download of files of the given file extension (separated by “,”) | To block specific file extensions from being downloaded, enter the extensions separated by commas (e.g., `exe,zip`). Leave this field empty if you want to allow downloads for all file types. By default, the field is empty, meaning no file types are blocked. |
| Select a ContentVersion field of the file to be skipped for scan. | Specify a field from the Salesforce `ContentVersion` object to act as a flag for bypassing or excluding the associated file from being scanned. |
| Private Scan | If this field is set to "Enable", all files scanned by MetaDefender Cloud will be instantly deleted from the MetaDefender Cloud application upon completing the scan. Scan results will still remain available in MetaDefender Cloud (scan results do not contain any PII). |
| Scan Emails | By checking the checkbox, you activate the email body scanning feature. To avoid scanning the email body, ensure that the checkbox remains unchecked. |
| Block files bigger than 10 MB | Enabling the checkbox activates the functionality to block files larger than 10 MB. |
| Enable Scan Only For Certain Profiles | This feature allows you to only scan files that are uploaded from certain Salesforce profiles (for example if you only want to scan files uploaded by individuals external to your organization). If you select the box, those profiles that you have not selected to have their file uploads scanned will still be able to upload files but will have the file status as "scanning skipped". Note that applies for CDR as well as multiscanning. |
| Rescan Interval | Rescan files when someone download them and the current scan results are older than X days. e.g.: a files was uploaded (scanned) on 1/1/2024, the Rescan Interval is set to 1, if someone download the file on 1/1/2024, the application won't rescan the file. But if they download on 1/2/2024, the application will rescan the file before letting that person downloads it. |

### [Logging Policy Settings](/docs/mdfs/version-6.0.5/file-security--metadefender/file-security---settings#logging-policy-settings)

### [Automatically delete MetaDefender Logs data after a certain time](/docs/mdfs/version-6.0.5/file-security--metadefender/file-security---settings#automatically-delete-metadefender-logs-data-after-a-certain-time)

Based on the verdicts received from the multi-scanning process, you can choose to automatically delete scan logs that are older than a specified period. Available retention options include:

- 1 day
- 1 week
- 4 weeks
- 3 months
- 6 months
- 12 months

The possible scan verdicts are:

- **No Threat Found**
- **Infected**
- **Scanning Skipped**
- **Others**

## [Users Management](/docs/mdfs/version-6.0.5/file-security--metadefender/file-security---settings#users-management)

### [Admin Settings](/docs/mdfs/version-6.0.5/file-security--metadefender/file-security---settings#admin-settings)

You can oversee your users in designated fields tailored to meet your requirements.

- Within the "*Available users*" section, you can view users within your Salesforce Organization. From this group, you can choose users categorized under CSFS Admins. It's important to note that CSFS Admins are a subset of the available users. Your selected Admins will appear under "*Selected users*".
- Within the "*MDFS Admins*" category, you have the option to choose "*Approvers*". Under this section, you will find the list of available users, and you can assign them the role of approving or denying release requests.

All the users which are part of your Salesforce Organization will have *MetaAccess User Access* and *MetaDefender User Access* permission sets assigned automatically, and when a new user is added, there's no need to assign the permissions manually. Also, if the user already exists in the Salesforce Organization, but it is inactive, when it gets activated, the permission sets are assigned automatically as well.

### [Permissions Assignment](/docs/mdfs/version-6.0.5/file-security--metadefender/file-security---settings#permissions-assignment)

**Permissions Assignment Scheduling -** You can configure how often permissions are assigned to users by setting a custom assignment schedule. By default, the system assigns permissions **hourly**. Adjusting the schedule allows you to align permission updates with your organization's specific operational needs. This can be tailored to suit your specific use case as these operations consumes Salesforce Apex limits.

**Configure Permissions for Users Created Before a Specified Number of Days -** This setting allows you to assign permissions only to users whose accounts were created more than **X** days ago. Use this to exclude older created users from automatic permission assignments, if needed. By default, the systems assigns permissions to the users created **1 day ago**. This can be tailored to suit your specific use case as these operations consumes Salesforce Apex limits.

## [Setting Up Scanning for Guest Users](/docs/mdfs/version-6.0.5/file-security--metadefender/file-security---settings#setting-up-scanning-for-guest-users)

To enable file scanning for guest users, there are a few additional steps that should be followed:

- Open the guest user profile used
- Go to Apex Class Accesses -> add access to all CSFS package classes
- Go to Object Settings -> give full access to MetaDefender Configuration, OPSWAT – Setting, OPSWAT – MetaDefender Log objects
- Go to Custom Setting Definitions -> give access to OPSWAT MD Background Process
- *Guest User files will be saved only as a new version.

## [Salesforce Attachment Limitation in Classic mode](/docs/mdfs/version-6.0.5/file-security--metadefender/file-security---settings#salesforce-attachment-limitation-in-classic-mode)

If you are using the Salesforce Classic interface to manage file attachments, it's advisable to activate the setting that uploads files to the Attachments related list as Salesforce Files rather than standard attachments. Doing so converts these files into Salesforce Files, which are then scanned by MetaDefender for Salesforce during both upload and download processes.

To turn on this setting in Salesforce:

- Setup > General Settings > Salesforce Files Settings
- Enable "Files uploaded to the Attachments..."

## [Scan Evaluation Rules](/docs/mdfs/version-6.0.5/file-security--metadefender/file-security---settings#scan-evaluation-rules)

### [Scan rules](/docs/mdfs/version-6.0.5/file-security--metadefender/file-security---settings#scan-rules)

You can reuse old scan results that were created in an interval of maximum 30 days. If files have been scanned within the configured threshold period, the app will skip scanning files already uploaded to avoid duplicate processing, by performing hash lookup.

You can also select to rescan files form a specific interval (days) when users download files. If the results are older than the threshold, the app will rescan the files when users download them, the app doesn't rescan automatically.

### [Scan on demand](/docs/mdfs/version-6.0.5/file-security--metadefender/file-security---settings#scan-on-demand)

You can rescan files based on Scan statuses and Sandbox verdicts.
