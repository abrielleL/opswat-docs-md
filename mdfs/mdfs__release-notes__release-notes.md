<!-- source: https://www.opswat.com/docs/mdfs/release-notes/release-notes -->

# Release Notes

|  | **6.1.0 - 5/18/2026** |
| --- | --- |
| New Feature | **Custom Workflows** — Administrators can now connect their MetaDefender Cloud account and select custom workflows to apply to file scans, with region validation and in-app confirmation.  **Selective Reputation Scanning** — The Reputation Service can be scoped to specific objects, and results now link directly back to their source records for easier investigation.  **Enhanced Control & Coverage** — Added Scan Region enforcement for data residency, sanitized file versioning, broader sandbox verdicts, and support for all Salesforce user license types. |
| Fixed | Resolved issues with config storage limits, profile lists, stale workflows, object filtering, package upgrades, permission assignment, and sandbox state errors.  Fixed several internal errors blocking configuration changes. |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04tKf000000Y28N> |

|  | **6.0.5 - 5/18/2026** |
| --- | --- |
| New Feature | Nothing in this version |
| Fixed | - **Security Enhancements** |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04tKf000000Pi62> |

|  | **6.0.1 - 12/30/2025** |
| --- | --- |
| New Feature | Nothing in this version |
| Fixed | - **Resolved issues** found in the package installer |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04tKf000000LSxD&isdtp=p1> |

|  | **6.0 - 12/17/2025** |
| --- | --- |
| New Feature | - **Reputation Service -** We’re pleased to announce that **MetaDefender for Salesforce 6.0** introduces Reputation Service, enabling automated evaluation of **IP addresses**, **domains**, and **URLs** directly within Salesforce. This capability strengthens protection by identifying malicious indicators across records and workflows, extending threat detection well beyond uploaded files. - **UI Enhancements and Feature Segregations -** The user interface has been updated with visual and usability improvements to deliver a cleaner, more intuitive experience. Key features have been reorganized into clearly defined sections, making navigation simpler and helping users locate functionality more efficiently. These changes are designed to improve overall usability, consistency, and ease of interaction across the application. |
| Fixed |  |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04tKf000000gXB6> |

|  | **5.9.2 - 09/17/2025** |
| --- | --- |
| New Feature | **-** |
| Fixed | When a `ContentVersion`is created that contains only a reference to an externally stored file in OpenText, the OPSWAT MetaDefender triggers are bypassing scanning and processing for this record, allowing the insert to succeed without errors. This ensures that Salesforce can maintain a `ContentVersion` pointing to OpenText while still scanning new or unscanned files correctly. |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04tKf000000D8mu> |

|  | **5.9 - 09/12/2025** |
| --- | --- |
| New Feature | - **Workflow for Password Protected files -** Users have now the ability to insert password in case a file is protected - **Cloud Security for Salesforce is now MetaDefender for Salesforce** - **Skip scanning large files for Dynamic Analysis -** You can decide if want to apply Dynamic Analysis for files >10MB, or to skip them from analysis - **Dynamic Analysis capability for files bigger than 10MB -** Dynamic Analysis (Sandbox) available for files bigger than 10MB configurable from OPSWAT Settings. |
| Fixed |  |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04tKf000000Tr6B> |

|  | **5.8 - 05/08/2025** |
| --- | --- |
| New Feature | - **Rescan files on demand based on a selected response:** You can now **rescan uploaded files on demand** based on a selected response — giving you more control when a file is flagged or if you just want to double-check. **Here’s what’s new:**    - 🔍 Select a response action and trigger a **manual file rescan**   - 🖱️ Simple and quick — no need to re-upload   - 🛡️ Ideal for suspicious or previously flagged files      - **You can opt-in for instant alerts for Malicious uploads for the uploader and admins:** Whenever a **malicious or infected file** is uploaded, both **Uploaders and Admins** will now receive **real-time notifications** — via email — with clear warnings. **What you’ll see:**    - 🚨 Immediate alert if a file is flagged as unsafe   - 📩 Email (Uploader and Admins) + in-app notifications for full visibility for Admins   - 👥 Alerts sent to both the uploader and all relevant admins |
| Fixed |  |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04tKf000000TqpH> |

|  | **5.7 - 04/17/2025** |
| --- | --- |
| New Feature | - **Assigning User Permissions based on the User Profile:** The system now supports assigning user permissions based on user profile, this functionality fully integrated into the user interface within OPSWAT Settings tab: |
| Fixed |  |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04tKf000000TqkL> |

|  | **5.6 - 03/17/2025** |
| --- | --- |
| New Feature | - **OPSWAT Settings tab:** In the user interface, users can now specify the time interval for running the permission assignment job, with options such as daily, twice a day, or at a specific hour. - **OPSWAT Settings tab:** Additionally, users can choose whether to assign permissions to users created or existing for more than a specified number of days. |
| Fixed | - **Improvements to the Assign User Permissions job:** Enhancements have been made to the **Assign User Permissions** job within Cloud Security for Salesforce to optimize performance and reduce the consumption of Salesforce governor limits |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04t6g000008o346> |

|  | **5.4 - 02/03/2025** |
| --- | --- |
| New Feature | - **Duplicate File handling across the system:** this prevents duplicate file uploads across system, improving efficiency and reducing unnecessary processing. You can reuse old scan results that where created in an interval of time - You can input the number of days in the Settings page. |
| Fixed | - Fixed issues on the Admin side to not be able to download file if the file has been marked as a threat - Fixed issue to display correct message on the Release Request page - Fixed issue on the uploading a new version file trigger on sanitized files. |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04t6g000008o2yv> |

|  | **5.3 - 12/11/2024** |
| --- | --- |
| New Feature | - **Delete Files on Downloading**: A new checkbox has been added to the user interface, allowing you to enable the option to delete files immediately after they are downloaded. - **Block Files for All Profiles**: A new checkbox has been introduced in the user interface, enabling you to apply file-blocking settings (based on specific file type extensions) across all user profiles. - **Private Scanning for Paying Customers**: The Private Scanning feature is now exclusively available for paying customers. |
| Fixed | - Fixed issues on the MetaDefender Logs page for the message in case prevention limits are consumed. - Fixed issue on the MetaDefender Logs page to not have additional failed record when user click a file which doesn't have a log. - Fixed issue on Release Request feature to have a single email sent to the requesters, instead of multiple ones. - Fixed issue on Custom Notification for Guest Users. |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04t6g000008o2u4> |

|  | **5.2 - 10/17/2024** |
| --- | --- |
| New Feature | - **Infected File Detection Notifications for Admins** Salesforce CSFS Approvers will now receive notifications whenever an infected file is detected within their Salesforce organization. - **New IP/Domain/URL Reputation Check for Email-to-Case** A new feature has been introduced to enhance the email-to-case functionality. This feature checks the reputation of IP addresses, domains, and URLs in the body of incoming emails. - **Data Loss Prevention (DLP) Capabilities in Cloud Security for Salesforce** Cloud Security for Salesforce now includes Data Loss Prevention (DLP) capabilities. When DLP is enabled, the DLP Status will indicate whether sensitive data was found ("Sensitive Data Found") or not ("No Sensitive Data Found"). |
| Fixed | - Fixed issues on the Dashboard page |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04t6g000008o2nb> |

|  | **5.1.1 - 9/23/2024** |
| --- | --- |
| New Feature | - Nothing in this version |
| Fixed | - Resolved issue on the number of *opswat_secrev Async Apex Jobs* |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04t6g000008WwfM> |

|  | **5.1 - 9/5/2024** |
| --- | --- |
| New Feature | - Starting with 5.1 version, You will have the power to decide which files to be scanned, and which ones to be skipped for scan. This will help you to save your limits and to consume limits only on the files you would like to be processed |
| Fixed | - Resolved issue on Developer Script exception issue - Resolved issue on CSFS to automatically assign necessary permission set for the community users. - Resolved issue on Release Request feature. |
| Installation link | [https://login.salesforce.com/packaging/installPackage.apexp?p0=04t6g000008o1X0](https://login.salesforce.com/packaging/installPackage.apexp?p0=04t6g000008o1X0&isdtp=p1) |

|  | **5.0.5 - 8/27/2024** |
| --- | --- |
| New Feature | - Nothing in this version |
| Fixed | - Resolved Apex limit: opswat_secrev:Too many query rows: 50001 issue - Resolved Apex limit: opswat_secrev:Too many SOQL queries: 101 issue |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04t6g000008WtmM> |

|  | **5.0.4 - 8/22/2024** |
| --- | --- |
| New Feature | - Nothing in this version |
| Fixed | - Resolved Apex limit: opswat_secrev:Too many query rows: 50001 issue |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04t6g000008Wtm2> |

|  | **5.0.3 - 8/14/2024** |
| --- | --- |
| New Feature | - Nothing in this version |
| Fixed | - Fixed issues for _*Developer script exception error messages 'opswat_secrev.SandboxScanner'* |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04t6g000008WtlT> |

|  | **5.0.2 - 8/8/2024** |
| --- | --- |
| New Feature | - Nothing in this version |
| Fixed | - Fixed issues for *EmailMessage_HeaderVerificationTest* method |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04t6g000008WthB> |

|  | **5.0.1 - 8/2/2024** |
| --- | --- |
| New Feature | - Nothing in this version |
| Fixed | - Fixed issues for CANNOT_INSERT_UPDATE_ACTIVATE_ENTITY and FIELD_CUSTOM_VALIDATION_EXCEPTION |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04t6g000008Wtgw> |

|  | **5.0 - 7/24/2024** |
| --- | --- |
| New Feature | - Starting with CSFS version 5.0, you can now scan files larger than 10MB by following a few simple steps to enable this feature. For more details, please refer to the File Security page. *File Security (MetaDefender) - File Security - Large File Support.* |
| Fixed | - Nothing in this version |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04t6g000008o1WC> |

|  | **4.14.1 - 7/18/2024** |
| --- | --- |
| New Feature | - Nothing in this version |
| Fixed | - 'Scan Emails' functionality - Skip creating files for users who don't have access to create files, and in case it fails to be created. |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04t6g000008o1Rf> |

|  | **4.14 - 7/5/2024** |
| --- | --- |
| New Feature | - From now on you will have the ability to block an infected file without letting it to be uploaded to your system, based on specific selection - check the *File Security - Options on Upload/Download* - UI enhancements for the text displayed when a file is being blocked on download action - *Block the download of files of the given file extension (separated by ",")* - A new label has been added for Block on upload action - *Delete blocked files when uploading*, with the following description: *Blocked files will be removed right after the uploading process* - A new value has been added in MetaDefender Logs *Status* field when the file is deleted due to current configuration - *Deleted due to current configurations.* |
| Fixed | - Resolved issues with file scanning on Community zone on Salesforce. |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04t6g000008o1R6> |

|  | **4.13 - 5/28/2024** |
| --- | --- |
| New Feature | - OPSWAT - Settings page is now being Deprecated, please use OPSWAT Settings tab in order to update your application configuration. - From now on you have the ability to **delete the logs automatically after a certain amount of time,** together with the possibility to choose which logs to be deleted (No threat detected, Infected, Scanning skipped, others). To enable this feature, navigate to the OPSWAT Settings tab and select the options that best suit your needs. - UI enhancements for blocked files messages. |
| Fixed | - Resolved issues on saving the configuration page without an API Key. - Resolved issues on trigger exception - Resolved issue to not have the files automatically scanned after the fresh install of application - Resolved issue on file download error when log record was being deleted - Resolved issues on Block file feature |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04t6g000008o1Lg> |

|  | **4.12 - 4/15/2024** |
| --- | --- |
| New Feature | - Now you have the possibility to block the file based on the extension - Attachment and documents can be now sanitized. |
| Fixed | - Resolved issues on User object used to assign permissions to new and active users. |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04t6g000008o1GG> |

|  | **4.11 - 3/13/2024** |
| --- | --- |
| New Feature | - Now you have visibility on the consumption and remaining limits on the Dashboard page - New functionality was added to have the possibility to block a file if it is infected. Only enable “Block infected files” if Sanitization is enabled, otherwise the box is greyed out. |
| Fixed | - Resolved small issues on the texts and descriptions - Resolved issue on Sandbox to not remain in "Scanning" when limit is reached - Resolved issue for the external users to be able to see the scanning page or request to release page - Resolved issue with the files which are still being scanned even the scan status is "Scanning skipped" |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04t6g000008o1BZ> |

|  | **4.10.2 - 2/21/2024** |
| --- | --- |
| Fixed | - Resolved security challenges. - System Log improved to show error details about Omniscript. |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04t6g000008wItd&isdtp=p1> |

|  | **4.10.1 - 1/31/2024** |
| --- | --- |
| New Feature | - Improvements have been made to the Scan Details pick list statuses. To refresh the information, simply visit the OPSWAT Settings page. - A new OPSWAT System Logs feature has been implemented to log errors occurring during the installation process. |
| Fixed | - Resolved challenges with flex queue overflow for smoother operation. - Addressed the issue to ensure files are promptly scanned upon upload in classic mode. |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04t6g000008wIbJ&isdtp=p1> |

|  | **4.9 - 12/19/2023** |
| --- | --- |
| New Feature | Excluding file extension is applied for the Attachment type |
| Fixed | Can't download files in some cases |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04t6g000008o10P> |

|  | **4.8 - 12/11/2023** |
| --- | --- |
| New Feature | - A configuration to define what file extensions (based on the file name) can be skipped |
| Fixed | - Files are blocked when the sandbox is enabled. - Behavior when downloading the sanitized files. |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04t6g000008o10F&isdtp=p1> |

|  | **4.7.1 - 11/17/2023** |
| --- | --- |
| Fixed | - Configuration issues when users upgrade from 4.6 to 4.7 |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04t6g000008fHkn> |

|  | **4.7 - 11/7/2023** |
| --- | --- |
| New Feature | - A new sanitization option to keep the original file name |
| Fixed | - Approver permission - License info is shown incorrectly in the Setting page |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04t6g000008o0zb> |

|  | **4.6 - 10/10/2023** |
| --- | --- |
| New Feature | - Improve Sandbox scan result - Release blocked files through UI |
| Fixed | - Can't release blocked files bigger than 10MB |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04t6g000008o0uk&isdtp=p1> |

|  | **4.5 - 9/26/2023** |
| --- | --- |
| New Feature | - Enhance CSFS Admin search function |
| Fixed | - Rescan button doesn't show when upgrading from an old version to 4.4 |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04t6g000008fkoD&isdtp=p1> |

|  | **4.4 - 9/21/2023** |
| --- | --- |
| New Feature | - A configuration to allow or block if a file is bigger than 10MB - Ability to rescan a file |
| Fixed | - Fix SOQL issue |
| Installation link | [https://login.salesforce.com/packaging/installPackage.apexp?p0=04t6g000008fknj](https://login.salesforce.com/packaging/installPackage.apexp?p0=04t6g000008fknj&isdtp=p1) |

|  | **4.3 - 9/11/2023** |
| --- | --- |
| New Feature | - Permission set for users who can access to the Setting and Logs page. - Capability to define who should receive the release request email |
| Fixed | - In some cases, files are scanned even they are not in the selected profiles (Email-to-case, OmniStudio,...) |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04t6g000008fknA> |

|  | **4.2 - 8/22/2023** |
| --- | --- |
| Fixed | - Selected profiles are applied to old files |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04t6g000008fkm2> |

|  | **4.1 - 8/16/ 2023** |
| --- | --- |
| New Feature | - Added possibility to scan the incoming email body. - Added a possibility to select a list of admin users for CSFS logic. - The maximum file scan size is increased from 6 MB to 10 MB and files won't be blocked if exeeded 10MB. |
| Fixed | - Release/Request logic fix. |
| Installation link | <https://login.salesforce.com/packaging/installPackage.apexp?p0=04t6g000008fkh1> |

|  | **May 2023** |
| --- | --- |
| New Feature | - A new configuration to set how the sanitized file version will be stored |
| Fixed | - Fixed issue with file uploading after the Salesforce release. |

|  | **January 2023** |
| --- | --- |
| New Feature | - Enhanced configuration options for sanitized files - Ability to only scan files from specific Salesforce profiles |

|  | **August 2022** |
| --- | --- |
| New Feature | - Support for guest user type (those with guest user type can have files scanned with multiscanning) |
| Fixed | - Resolved issue with partner user type - Resolved issue preventing download for documents generated within Salesforce |

|  | **April 2022** |
| --- | --- |
| New Feature |  |
| Fixed | - Installation issue resolved - Updated documentation |
