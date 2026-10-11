<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/advanced-deployment/visitor-management -->

# Visitor Management

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Visitor Management enables a formal check-in process for guests that visit your organization. The settings for Visitor Management are available for all Guest workflows. The Kiosk admin can configure Visitor Management for individual Guest workflow through the Guest workflow editor.

## [Visitor questions](/docs/mdkiosk/v4.8.6/advanced-deployment/visitor-management#visitor-questions)

When a guest logs in with a Visitor-enabled guest workflow, he is routed through the check-in process. He will be initially presented with check-in questions to gather further information of the visitor. The email answer in the visitor [Questions] will be used to receive check-in summary and session report (if configured) attachment.

## [Prompt user for media processing](/docs/mdkiosk/v4.8.6/advanced-deployment/visitor-management#prompt-user-for-media-processing)

This setting allows for visitors to bring files into your organization. After logging in and answering the check-in questions, the user will be asked if files are being brought in. If so, the user will be routed through the Guest workflow for processing the files. However, even with [Prompt user for media processing] enabled, if nothing enabled in the workflow [User Questions], then the guest will be navigated directly to the workflow for processing the files without any promt windows. User should insert their media into the Kiosk for scanning. If he does not scan anything and decides to [Cancel] or [Exit&Eject], then the check-in is considered incomplete, as a result no check-in summary emails are sent.

## [Email](/docs/mdkiosk/v4.8.6/advanced-deployment/visitor-management#email)

Automated emails are sent contacts and management and the guest himself to notify the necessary parties when he has arrived and successfully checked-in. The SMTP settings must be set on the [Configuration](/docs/mdkiosk/v4.8.6/advanced-deployment/configuring-global-kiosk-settings) page to ensure emails are sent.

The session log is always attached to the email.

**Management Email Address**

Address to send a notification email containing the guest login information and PDF attachment of all the signed agreements for your organization's records.

**Send Notification As**

This is a mandatory input. It appears as a From field in the email header.

**Backup Contact Email**

When a guest user checks in, they are required to identify their contact person in the organization. This primary contact will be notified via email that their guest has arrived and completed check-in. If the primary contact's email cannot be found, the backup contact is notified of the guest's arrival along with the login information.

**Session report attachment for visitor emails**

When a guest finishes his checkin procedure with file processing or retrieval activity, the session report file can be attached in the Management or Contact/Backup email. The admin can configure to attach it or not in the emails.

**Custom logo**

Logo to include in the PDF document of the agreements signed by the visiting guest.

---

## [Badge Printer](/docs/mdkiosk/v4.8.6/advanced-deployment/visitor-management#badge-printer)

Print user information to a badge that the guest can wear. User information:

- Name
- Company
- Contact Name
- Date
- MFT Guest ID (if files were uploaded to MFT)
- MFT URL (url to retrieve uploaded files from)

**Configured Printer**

Specific printer to be used for printing the guest badge.

**Printers**

List of printers connected to the system to allow selection of the one to print the guest badge.

## [Contacts](/docs/mdkiosk/v4.8.6/advanced-deployment/visitor-management#contacts)

During check-in, a guest will be prompted to input their contact's name. While entering the name, filtered results from the Available Contacts will display on the screen to allow for easy selection for the guest.

**Available Contacts**

List of users that a guest can select when specifying their contacts during check-in. The Contact list is built from Active Directory server. Once AD is configured, the Contacts area will load and display users fetched from AD server. Not all users will be loaded but if the admin scrolls the slider down to the bottom, more contacts will be fetched and displayed. Only users with email address are available to add as Contacts. The Kiosk admin can add users or groups of users as Contact.

The admin can specify a displayName (an attribute in AD server) to search through the AD. This is different from the search in [[Properties & Membership]](/docs/mdkiosk/v4.8.6/metadefender-kiosk-windows/v4.5.7/operating/properties---membership) in creating a workflow, where the search accepts sAccountName.

Info

The [Import all AD Contacts] is not available from version 4.5.7. For any previous versions with [Import all AD Contacts] enabled, the upgrade to to 4.5.7+ will not automatically add all users to Contacts but the admin must manually add who as contact as he wants.

## [Agreements](/docs/mdkiosk/v4.8.6/advanced-deployment/visitor-management#agreements)

Specify any agreements to be acknowledged and signed by all visitors. A copy of all the signed agreements will be generated and sent in the management notification email and accessible via the [Visitor Log](/docs/mdkiosk/v4.8.6/advanced-deployment/visitor-logs) in the management console.

Variables from the guest login can be utilized in the text box of the agreement:

- - the guest's full name
- - guest's company
