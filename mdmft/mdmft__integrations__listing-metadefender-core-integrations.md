<!-- source: https://www.opswat.com/docs/mdmft/integrations/listing-metadefender-core-integrations -->

# Listing MetaDefender Core Integrations

Summarize Page    Connect to Cursor Connect to VS Code
## [Overview](/docs/mdmft/integrations/listing-metadefender-core-integrations#overview)

The MetaDefender Core™ Integrations page provides a data table that lists all configured integrations. This table allows users to view integration details and perform various actions such as adding a new integration, editing, disabling, testing, and deleting an integration.

Manage integration actions

## [Load Balancing](/docs/mdmft/integrations/listing-metadefender-core-integrations#load-balancing)

The **“Load Balancing”** button is only displayed when at least two cores are set up.

- **Round Robin (default)**: Distributes files evenly across all MetaDefender Cores in a rotating sequence
- **Core Health:** Routes files to the least loaded MetaDefender Core based on current usage.

## [Workflows and modules](/docs/mdmft/integrations/listing-metadefender-core-integrations#workflows-and-modules)

When clicking on a connected integration's address its workflows and modules show up with details. Users can view the workflows and modules used by the integration with details such as technologies used by a workflow, versions of a module etc.

Warning

Detailed information will be displayed only if an API key for MetaDefender Core™ has been saved for the selected integration.

Workflows used by an integration

Modules used by an integration

Integration details without saved API key

Click the Metascan™ or the Utilities engines card to access detailed information about the selected engines.

Utility engines details

## [Table Columns](/docs/mdmft/integrations/listing-metadefender-core-integrations#table-columns)

The integrations table contains the following columns:

1. **Address**

   - Displays the URL or IP address of the MetaDefender Core™ instance.
2. **Connection Status**

   - Indicates the current connection state of the integration.
   - Possible values: `Connected`, `Disconnected`, `NotFound`.
3. **File Processing**

   - Shows whether file processing is enabled for the integration.
   - Possible values: `Enabled`, `Disabled`.
4. **API Key**

   - Displays the API key used to authenticate requests.
5. **Processing Timeout**

   - Indicates the maximum allowed processing time for each file.
   - Value is displayed in minutes.
6. **Actions**

   - Provides a set of action buttons for managing the integration:

     - **Edit**: Modify the integration settings.
     - **Disable**: Temporarily disable the integration without removing it.
     - **Test Connection**: Check the connection status of the integration.
     - **Delete**: Remove the integration from the system.

## [Managing Integrations](/docs/mdmft/integrations/listing-metadefender-core-integrations#managing-integrations)

Users can perform the following actions from the integrations table:

- **Editing an Integration:** Click the **Edit** button to modify the integration details such as address, API key, and processing timeout.
- **Disabling an Integration:** Click the **Disable** button to temporarily deactivate the integration. A disabled integration can be re-enabled at any time.
- **Testing the Connection:** Click the **Test Connection** button to verify the connection status of the integration in real-time.
- **Deleting an Integration:** Click the **Delete** button to permanently remove the integration from the system. A confirmation prompt will appear before deletion.
- **Clicking on an Integration:** Click the integration's **address** to show its workflows and modules with details.
