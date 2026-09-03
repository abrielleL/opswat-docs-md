<!-- source: https://www.opswat.com/docs/mdces3/configuration/integrations -->

# Integrations

Summarize Page

Set up integrations to seamlessly connect your email infrastructure with **MetaDefender Cloud Email Security ™** for enhanced threat protection and policy enforcement. Refer to the sub-sections for detailed guidance on each integration type available.

## [Integration List](/docs/mdces3/configuration/integrations#integration-list)

- **Search Bar**: Allows users to find specific integrations by name.
- **Integration Columns**:

  - **Integration Name:** The name assigned to the integration.
  - **Service**: The integration service type.
  - **User count**: The number of users/groups available through the integration.
  - **Status**: The integration status. Any of the following statuses are possible

    - **Disconnected**: The integration is disconnected and needs attention.
    - **Monitoring**: The integration is active in monitoring mode.
    - **Protected**: The integration is active in protection mode.
  - **Integration Buttons**:

    - **Delete**: Remove the selected integration. See [Removing an Integration](/docs/mdces3/configuration/integrations#removing-an-integration)
- **Pagination Controls**: Users can navigate through multiple pages of integrations.

## [Viewing an Integration](/docs/mdces3/configuration/integrations#viewing-an-integration)

Clicking on an integration from the list opens the **Integration Details** page, where users can view the integration details.

### [Integration Details](/docs/mdces3/configuration/integrations#integration-details)

- **Integration Name**: The name assigned to the integration.
- **Status**: The integration status. Any of the following statuses are possible

  - **Disconnected**: The integration is disconnected.
  - **Monitoring**: The integration is active in monitoring mode.
  - **Protected**: The integration is active in protection mode.
- **Direction:** Traffic direction(s) protected.
- **Service**: The integration service type.
- **Protection mode**: Inline or monitoring mode.

#### [Routing](/docs/mdces3/configuration/integrations#routing)

Use the **Edit Routing** dialog to configure/change where emails for each domain should be delivered.

- **Domain:** Displays the domains currently configured for routing (e.g., `opswat.com`).
- **Destination hosts:** Lists the mail servers that will receive emails for the selected domain.
- **Add a destination host**

  1. Enter the mail server address (e.g., `mail.example.com`) in the **Add destination host** field.
  2. Click **Add host** to include it in the list.
- **Remove a destination host**

  - Click **Delete** next to the host you want to remove.
- Click **Save** to apply your updates.

Info

An integration with 'Disconnected' status will need manual attention and re-authorization by clicking the 'Reauthorize' button.

#### [Users & Groups](/docs/mdces3/configuration/integrations#users--groups)

List of users and groups available for this integration.

- **Search Bar**: Find specific users and/or groups by name or email address.
- **Columns**:

  - **Name:** The user/group name.
  - **Email Address**: The user/group email address.
- **Pagination Controls**: Users can navigate through multiple pages of users/groups.

## [Removing an Integration](/docs/mdces3/configuration/integrations#removing-an-integration)

To remove an integration, click the 'Remove integration' button. Any associated users & groups will be removed from the system.

Warning

Any objects created in Microsoft 365 must be removed manually when removing the integration. Please refer to [Integration Details (In-line protection mode)](/docs/mdces3/configuration/microsoft-exchange-online#integration-details-in-line-protection-mode) or [Integration Details (Monitoring mode)](/docs/mdces3/configuration/microsoft-exchange-online#integration-details-monitoring-mode) for details on objects created by **MetaDefender Cloud Email Security ™**.
