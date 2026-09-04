<!-- source: https://www.opswat.com/docs/mdces3/operating/quarantine -->

# Quarantine

Summarize Page

The **Quarantine** page provides information of blocked and modified emails, including some basic metadata. Each entry is linked to an Event (See [Events](/docs/mdces3/operating/events)).

# [Search and Filtering Options](/docs/mdces3/operating/quarantine#search-and-filtering-options)

- **Search Bar**: Allows users to search for specific quarantine based on keywords.
- **Time Range**: Narrows down entries by time range.
- **Filters:** Use the panel to narrow the list of entries using one or more search criteria. It includes:

  - **Status:** Filters entries by their current processing status (for example, Quarantined).
  - **Verdict:** Filters events by the final processing verdict.
  - **Message ID:** Searches for a specific email message using its unique Message ID.
  - **Quarantine ID:** Filters entries by its unique Quarantine ID.
  - **Subject:** Filters entries by the email subject.
  - **SMTP Sender:** Filters entries by the SMTP envelope sender address.
  - **From Address:** Filters entries by the email sender shown in the **From** header.
  - **Recipient:** Filters entries by the recipient email address.
  - **Policy Name:** Filters entries processed by a specific policy.
  - **Attachment Name:** Filters entries containing attachments with a specified file name.

- **Column visibility:** Configure columns to display in list. Available are:

  - **Select (Fixed Column):** Allows for batch operations.
  - **Quarantine ID (Fixed Column):** Unique ID automatically assigned to each entry.
  - **Actions (Fixed Column):** Provides quarantine actions, like Release or Delete.
  - **Policy:** Shows the policy that was applied during email processing.
  - **Verdict:** Displays the final security verdict assigned to the event.
  - **Status:** Shows the current processing status of the event (for example, Delivered or Quarantined).
  - **Time of Event:** Displays the date and time the event occurred. This column is fixed and cannot be hidden.

# [Quarantine List (Blocked & Sanitized Originals)](/docs/mdces3/operating/quarantine#quarantine-list-blocked--sanitized-originals)

Each row in the list represents an event with the following details:

- **Time of Event**: Timestamp indicating when the event occurred.
- **Quarantine ID**: Unique identifier assigned to each security event.
- **Status**: The current status of the event, for example, Quarantined.
- **Policy**: Indicates the Policy that applied for the the content.
- **Verdict**: See [Verdicts](/docs/mdces3/configuration/verdicts).

## [Viewing Details](/docs/mdces3/operating/quarantine#viewing-details)

Clicking the arrow next to a **Quarantine ID** expands detailed metadata about the quarantined email, including:

- **Item type:** Type of content.
- - **View headers**: View the email header for analysis.
- **Affected User**: The user(s) affected by the event.
- **Sent at**: Timestamp of when the email was sent.
- **Received at**: Timestamp of when the email was received.
- **Message ID**: Unique email message identifier.
- **Subject**: The subject of the email.
- **Sender & Recipients**: Sender's email address and SMTP server details.
- **From, To & Cc:** Identify the sender and recipients listed in the email header.
- **Received from**: Endpoint from where email was received.
- **Size**: Email content size.

## [Actions](/docs/mdces3/operating/quarantine#actions)

To the right of each quarantined email are action icons:

- **View Event**: Opens the associated event for detailed threat analysis. See [Viewing Event details](/docs/mdces3/operating/events#viewing-event-details).
- **Delete**: Permanently removes the email from the system
- **Release**: Delivers the email to the intended recipient if deemed safe
- **Download:** Download the email.

These actions can help administrators quickly manage threat resolution or allow legitimate emails that were flagged in error.
