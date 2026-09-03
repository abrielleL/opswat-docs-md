<!-- source: https://www.opswat.com/docs/mdces3/configuration/email-notifications -->

# Email Notifications

Summarize Page

The **Email Notification Templates** feature allows administrators to create, customize, and manage email notifications sent to users when actions are taken on their emails.

## [Template list](/docs/mdces3/configuration/email-notifications#template-list)

- **Search Bar**: Allows users to find specific templates by name or subject.
- **Template Columns**:

  - **Template Name**: The name assigned to the notification template.
  - **Subject**: The notification email subject.
- **Template Buttons**:

  - **Clone**: Clone the selected template.
  - **Delete**: Delete the selected template.
- **Pagination Controls**: Users can navigate through multiple pages of templates.

## [Editing an Email Notification Template](/docs/mdces3/configuration/email-notifications#editing-an-email-notification-template)

Clicking on a template from the list opens the **Template Details** page, where users can configure email notification content.

### [Template Settings](/docs/mdces3/configuration/email-notifications#template-settings)

- **Email Template Name**: The display name of the template.
- **Email Subject**: The notification email subject.
- **Email Sender**: Specifies the sender email address, for example: `noreply@mycompany.com`.

  - The sender field can also include both display name and email address as follows: `"Display name" <noreply@mycompany.com>`.

### [Email Content Customization](/docs/mdces3/configuration/email-notifications#email-content-customization)

- **HTML Tab**:

  - Provides a rich text editor for formatting email content.
  - Users can insert fields, format text, add tables, and customize the layout.
  - Example content: "Your email was blocked due to a security issue."
- **Plain Text Tab**:

  - Used for text-based email clients.

Info

When editing HTML content, the plain text version is automatically updated, based on the content provided.

### [Email Content Preview](/docs/mdces3/configuration/email-notifications#email-content-preview)

- Shows a sample notification email with placeholders replaced by actual data.

### [Scripting Language](/docs/mdces3/configuration/email-notifications#scripting-language)

It is also possible to additionally customize templates using the **Handlebars** template scripting language. For more information see: <https://handlebarsjs.com/guide/>

### [Custom Fields](/docs/mdces3/configuration/email-notifications#custom-fields)

The following field can be inserted into email notification templates:

| Name | Description |
| --- | --- |
| First Name | Affected user's first name |
| Subject | Affected email subject |
| From | Affected email From: address |
| To | Affected email To: address |
| Date | Affected email date/time |
| Verdict | Policy verdict |
| Engines | Number of MetaScan™ Multiscanning engines used to scan content |
| Detected engines | Number of MetaScan™ Multiscanning engines that triggered the policy verdict |
| Action URL | Link to end-user actions wizard |
