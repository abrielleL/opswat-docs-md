<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/operating/managing-notification-emails -->

# Managing notification emails

Summarize Page    Connect to Cursor Connect to VS Code

Administrators and Helpdesk Administrators can specify dedicated email addresses to receive system notifications on behalf of users. If configured, these notification email addresses take precedence over the users’ default email addresses when notifications are sent.

## [Adding notification emails](/docs/mdmft/v3.11.4/operating/managing-notification-emails#adding-notification-emails)

There are two ways to add a notification email for a user.

The first method is through a bulk CSV update. By uploading a CSV file containing at least two columns — **Username** (or **UserName** or **User**) and **Notification Email** (or **NotificationEmail** or **Notification_Email**) — the system will update existing users listed in the file with the corresponding notification email specified in the same row. Note that the column names must be in English.

Info

By default, existing notification email addresses will not be overwritten during the CSV upload. Only if the "Overwrite Existing Notification Emails" switch is turned on.

Example for a valid CSV format

Info

Ensure that the CSV file contains plain text only and does not include any formatting. Spreadsheet applications such as Microsoft Excel may automatically apply formatting to e-mail addresses (for example, underlining or hyperlink styling), which is not supported by the application. Verify that all e-mail address fields are unformatted before uploading the file.

"Update Notification Emails" button appears on the upper right corner. "Notification Email Address" column can also be displayed for users next to "Email Address" column.

After clicking the "Update Notification Emails" button, a modal appears where the CSV file can be uploaded either by clicking the "Upload" button or drag-and-dropping the file.

The selected file appears after uploading. It can be cleared by clicking the "x" next to it.

After a successful update a confirmation modal will appear and the modal can be closed.

After an unsuccessful update an error modal will appear informing the user about the problem.

Info

If the upload is unsuccessful, please verify the format of the CSV file and its records. Ensure that all email addresses are in a valid format and that the usernames match those registered in the application.

The second method for adding a notification email is by editing the user.

> In this way, the notification email can also be modified or removed as needed.

Notification email can be added, modified or cleared through editing the user.
