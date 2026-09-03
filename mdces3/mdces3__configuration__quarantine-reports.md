<!-- source: https://www.opswat.com/docs/mdces3/configuration/quarantine-reports -->

# Quarantine Reports

Summarize Page

The Quarantine **Reports** feature allows administrators to schedule, customize, and manage summary reports that are sent to administrators and/or users via email. These reports provide an overview of emails quarantined in **MetaDefender Cloud Email Security ™**.

## [Report List](/docs/mdces3/configuration/quarantine-reports#report-list)

Admins can view and manage existing reports from the **Reports** section under **Settings**.

- **Search bar:** Allows users to filter reports by report name or subject
- **Report columns:**

  - **Report name:** The internal name assigned to the report.
  - **Subject:** The subject line used in the sent email.
  - **Status:** Toggle to activate or deactivate scheduled sending.
- **Report buttons:**

  - **Delete:** Delete icon to permanently remove the report.
  - **Clone:** Clone the report.

## [Creating a New Report](/docs/mdces3/configuration/quarantine-reports#creating-a-new-report)

Click **Add new report** in the top-right corner.

### [Choose Report Type](/docs/mdces3/configuration/quarantine-reports#choose-report-type)

Select report type from the drop down list:

- **Administrator Quarantine Report** – Similar to User Quarantine Reports but includes all quarantined emails for all users:

  - Direct link to the Quarantine portal
  - Summary count
- **User Quarantine Report** – Notifies end users about emails quarantined for them

  - Email details: Sender, subject, date, verdict
  - Optional action links for:

    - Delivering email
    - Requesting rescan

*For other report types, see* [*Scan Reports*](/docs/mdces3/configuration/scan-reports)*.*

## [Report Settings](/docs/mdces3/configuration/quarantine-reports#report-settings)

Each report includes the following configuration options:

- **Active** – Enables or disables the report.
- **Report name** – Internal descriptive name.
- **Report subject** – Subject line of the email.
- **Email sender** – From address for outgoing reports.
- **Select days of the week** – Choose which days the report is sent.
- **Use custom start date** - Choose a custom start date for the first report. If not selected, emails quarantined from the report creation date will be included in the first report.
- **Time / Time zone** – Schedule delivery time.
- **Recipients** – Select users or groups to receive the report.
- **Allowed actions** – Allow users to Deliver, Rescan emails and/or View scan results.
- **Verdicts filter** – Restrict report to specific verdicts (e.g. Malicious, Suspicious, Encrypted content).

## [Editing a Report](/docs/mdces3/configuration/quarantine-reports#editing-a-report)

Clicking on a report opens the **Report Details** page, where you can configure general settings and the email content.

### [Report Settings](/docs/mdces3/configuration/quarantine-reports#report-settings)

- **Report Name**: Internal display name for the report.
- **Report subject**: Subject line used in the report email.
- **Email Sender**: Specifies the sender email address, for example: `noreply@mycompany.com`.

  - The sender field can also include both display name and email address as follows: `"Display name" <noreply@mycompany.com>`.
- **Schedule:** Choose the days of the week and time for delivery.
- **Time zone:** Define the time zone for scheduled delivery.
- **Recipients:** Users or groups to receive the report.

### [Email Content Customization](/docs/mdces3/configuration/quarantine-reports#email-content-customization)

- **HTML Tab**:

  - Provides a rich text editor for formatting email content.
  - Users can insert fields, format text, add tables, and customize the layout.
- **Plain Text Tab**:

  - Used for text-based email clients.

Info

When editing HTML content, the plain text version is automatically updated, based on the content provided.

### [Email Content Preview](/docs/mdces3/configuration/quarantine-reports#email-content-preview)

- Shows a sample report email with placeholders replaced by actual data.

### [Scripting Language](/docs/mdces3/configuration/quarantine-reports#scripting-language)

It is also possible to additionally customize report templates using the **Handlebars** template scripting language. For more information see: <https://handlebarsjs.com/guide/>

### [Custom Fields](/docs/mdces3/configuration/quarantine-reports#custom-fields)

The following field can be inserted into email report templates:

#### [Administrator Quarantine Report](/docs/mdces3/configuration/quarantine-reports#administrator-quarantine-report)

| Name | Description |
| --- | --- |
| **Number of Emails** | Total number of emails quarantined. |
| **Action URL** | Link to **MetaDefender Cloud Email Security ™** Quarantine. |

#### [User Quarantine Report](/docs/mdces3/configuration/quarantine-reports#user-quarantine-report)

| Name | Description |
| --- | --- |
| **Number of Emails** | Total number of emails quarantined for the specific user. |
| **Emails (Array)** | Array of quarantined email details. |
