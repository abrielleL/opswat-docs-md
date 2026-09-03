<!-- source: https://www.opswat.com/docs/mdces3/configuration/scan-reports -->

# Scan Reports

Summarize Page

The **Scan** **Reports** feature allows administrators to schedule, customize, and manage summary reports that are sent via email. These reports provide an overview of scan activity, threats detected, policy enforcement, and other metrics for each tenant.

## [Report List](/docs/mdces3/configuration/scan-reports#report-list)

Admins can view and manage existing reports from the **Reports** section under **Settings**.

- **Search bar:** Allows users to filter reports by report name or subject
- **Report columns:**

  - **Report name:** The internal name assigned to the report.
  - **Subject:** The subject line used in the sent email.
  - **Status:** Toggle to activate or deactivate scheduled sending.
- **Report buttons:**

  - **Delete:** Delete icon to permanently remove the report.
  - **Clone:** Clone the report.

## [Creating a New Report](/docs/mdces3/configuration/scan-reports#creating-a-new-report)

Click **Add new report** in the top-right corner.

### [Choose Report Type](/docs/mdces3/configuration/scan-reports#choose-report-type)

Select **Scan Report**.

*For other report types, see* [*Quarantine Reports*](/docs/mdces3/configuration/quarantine-reports)*.*

## [Report Settings](/docs/mdces3/configuration/scan-reports#report-settings)

Each report includes the following configuration options:

- **Active** – Enables or disables the report.
- **Report name** – Internal descriptive name.
- **Report subject** – Subject line of the email.
- **Email sender** – From address for outgoing reports.
- **Select days of the week** – Choose which days the report is sent.
- **Use custom start date** - Choose a custom start date for the first report. If not selected, emails processed from the report creation date will be included in the first report.
- **Time / Time zone** – Schedule delivery time.
- **Recipients** – Select users or groups to receive the report.

## [Editing a Report](/docs/mdces3/configuration/scan-reports#editing-a-report)

Clicking on a report opens the **Report Details** page, where you can configure general settings and the email content.

### [Report Settings](/docs/mdces3/configuration/scan-reports#report-settings)

- **Report Name**: Internal display name for the report.
- **Report subject**: Subject line used in the report email.
- **Email Sender**: Specifies the sender email address, for example: `noreply@mycompany.com`.

  - The sender field can also include both display name and email address as follows: `"Display name" <noreply@mycompany.com>`.
- **Schedule:** Choose the days of the week and time for delivery.
- **Time zone:** Define the time zone for scheduled delivery.
- **Recipients:** Users or groups to receive the report.

### [Email Content Customization](/docs/mdces3/configuration/scan-reports#email-content-customization)

- **HTML Tab**:

  - Provides a rich text editor for formatting email content.
  - Users can insert fields, format text, add tables, and customize the layout.
- **Plain Text Tab**:

  - Used for text-based email clients.

Info

When editing HTML content, the plain text version is automatically updated, based on the content provided.

### [Email Content Preview](/docs/mdces3/configuration/scan-reports#email-content-preview)

- Shows a sample report email with placeholders replaced by actual data.

### [Scripting Language](/docs/mdces3/configuration/scan-reports#scripting-language)

It is also possible to additionally customize report templates using the **Handlebars** template scripting language. For more information see: <https://handlebarsjs.com/guide/>

### [Custom Fields](/docs/mdces3/configuration/scan-reports#custom-fields)

The following field can be inserted into email report templates:

| Name | Description |
| --- | --- |
| **Created At** | Timestamp when the report was generated. Useful for showing when the data snapshot was taken. |
| **Sanitization Rate** | Percentage of emails sanitized vs total emails processed. Calculated as: `sanitized / scanned`. |
| **Emails Scanned** | Total number of emails scanned during the report period (via multiscanning). |
| **Scan Rate** | Rate of scanning (emails per minute/hour depending on system config). Useful for performance trends. |
| **Emails Blocked** | Number of emails blocked by policies (Threats, encrypted content etc.) |
| **Block Rate** | Percentage of scanned emails that were blocked. |
| **Emails Sanitized** | Number of emails that passed through Deep CDR for content sanitization. |
| **Deep CDR Sanitization Rate** | Percentage of sanitized emails vs total emails sanitized by Deep CDR. |
| **Deep CDR Sanitization Rate** | Number of emails sanitized by Deep CDR. |
| **Threats Prevented** | Number of threats removed by Multiscanning. |
| **Total Events** | Total number of events logged during the report window (including all verdicts). |
| **Quarantined Events** | Number of emails placed in quarantine due to policy rules or detected threats. |
| **Sanitized Events** | Number of emails marked as sanitized. |
| **Released Events** | Number of emails that were released from quarantine (via admin/user action). |
| **Deleted Events** | Number of emails that were permanently deleted from quarantine. |
| **Closed Events** | Number of events that reached a final state 'Closed without action'. |
| **Blocked File Types (Array)** | List of file types that were blocked during the report period. |
| **Blocked Senders (Array)** | List of sender addresses that were blocked during the period. |
| **Blocked Recipients (Array)** | List of recipient addresses whose emails were blocked. |
