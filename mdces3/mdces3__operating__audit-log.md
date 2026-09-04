<!-- source: https://www.opswat.com/docs/mdces3/operating/audit-log -->

# Audit Log

Summarize Page

The **Audit Log** provides a comprehensive record of key user actions and system events within the platform. It helps administrators track changes, ensure security, and maintain compliance.

## [Search and Filtering Options](/docs/mdces3/operating/audit-log#search-and-filtering-options)

- **Time Range**: Narrows down events by time range.
- **Search Bar**: Enter keywords to filter by event content.
- **Filters:** Use the panel to narrow the list of entries using one or more search criteria. It includes:

  - **Event Type**: Select a specific event type to filter results (e.g., only *Configuration* updates).
- **Column visibility:** Configure columns to display in list. Available are:

  - **User (Fixed Column):** Displays the user who performed the action. This column is fixed and cannot be hidden.
  - **Event Type:** Shows the category of the recorded audit event.
  - **Operation:** Displays the action performed (for example, Create, Update, Delete, or Login).
  - **Event Details:** Shows additional information about the audited action.
  - **Time of Event:** Displays the date and time the audit event occurred.

## [Audit Events List](/docs/mdces3/operating/audit-log#audit-events-list)

Each row in the quarantine list represents an email with the following details:

- **User:** User that performed the operation.
- **Event type:** Possible types include:

  - **Authentication** – Authentication related events.
  - **Configuration** – Activity related to system configuration (create/update/delete).
- **Operation:** Type of operation performed, for example:

  - **Create:** A new item was created.
  - **Delete:** An existing item was deleted.
  - **Update:** An existing item was updated.
- **Event details:** Human readable description of the event, including links to the affected item (when applicable).
- **Time of Event**: When the entry was recorded.
