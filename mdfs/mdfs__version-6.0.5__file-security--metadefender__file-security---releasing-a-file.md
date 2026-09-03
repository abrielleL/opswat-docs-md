<!-- source: https://www.opswat.com/docs/mdfs/version-6.0.5/file-security--metadefender/file-security---releasing-a-file -->

# File Security - Accepting & Denying Release Requests

There may be instances where a user believes that a file is safe despite the system flagging it as malicious.

A request release notification should be sent to administrators. An SFDC administrator can decline/accept the request based on his judge. After a file is released, the user can access the original file.

### [Accepting Release Requests](/docs/mdfs/version-6.0.5/file-security--metadefender/file-security---releasing-a-file#accepting-release-requests)

Administrators can approve release requests either through the email notification they receive or in the OPSWAT app on Salesforce

#### [Accepting Release Requests via Email](/docs/mdfs/version-6.0.5/file-security--metadefender/file-security---releasing-a-file#accepting-release-requests-via-email)

Administrators receive an email when the user submits a request to release a file. They can click on “Accept” in the email to accept the release request (see screenshot below).

After the administrator releases a file through the email, the popup below will display.

## [Accepting Release Requests via the App](/docs/mdfs/version-6.0.5/file-security--metadefender/file-security---releasing-a-file#accepting-release-requests-via-the-app)

1. The account administrator must log into Salesforce
2. From there, they can select the OPSWAT | Cloud Security for Salesforce application and navigate to the “Files requested to release” section (as shown above).

   1. To get to the "Files requested to release" section, the administrator can either click on the widget on the home page of the OPSWAT application (see first screenshot below) or find the "Files requested to release" report in the Reports application of Salesforce (see second screenshot below)

Files can be released via the "Files requested to be released" section on the home page of the OPSWAT app

Files can also be released via the "Files requested to be released" report in the reports application

Administrators can then click on the "MetaDefender Log: Log ID" of the file they wish to release and set the Release Status to "Released" as shown in the screenshot below:

### [Declining Release Requests](/docs/mdfs/version-6.0.5/file-security--metadefender/file-security---releasing-a-file#declining-release-requests)

Administrators can decline release requests either through the email notification they receive or in the OPSWAT app on Salesforce

#### [Declining Release Requests via Email](/docs/mdfs/version-6.0.5/file-security--metadefender/file-security---releasing-a-file#declining-release-requests-via-email)

Administrators receive an email when the user submits a request to release a file. They can click on "Decline" in the email to decline the release request (see screenshot above).

Administrators will have the opportunity to send a message to the requestor as to why they are declining their release request

After the administrator types the message and clicks "Decline Release Request" below the message box, they will receive a confirmation as shown below:

The requestor will receive an email stating their request has been declined

Declining Release Requests via the App

1. The account administrator must log into Salesforce
2. From there, they can select the OPSWAT | Cloud Security for Salesforce application and navigate to the “Files requested to release” section (as shown above).

   1. To get to the "Files requested to release" section, the administrator can either click on the widget on the home page of the OPSWAT application (see first screenshot below) or find the "Files requested to release" report in the Reports application of Salesforce (see second screenshot below)

Requests can be declined via the "Files requested to be released" section on the home page of the OPSWAT app

Requests can also be declined via the "Files requested to be released" report in the reports application

Administrators can then click on the "MetaDefender Log: Log ID" of the file they wish to decline and set the Release Status to "Declined" as shown in the screenshot below. After setting the Release Status to "Declined", admins can click the dark blue save button at the bottom of the page
