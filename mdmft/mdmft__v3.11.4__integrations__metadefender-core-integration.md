<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/integrations/metadefender-core-integration -->

# Integration with MetaDefender Core

Summarize Page    Connect to Cursor Connect to VS Code
## [Configuration](/docs/mdmft/v3.11.4/integrations/metadefender-core-integration#configuration)

1. Go to "Settings" and select "Core Integration."

2. Select "Add MetaDefender Core."

Fill out the required information on the "Configuration" page:

- **REST URL:** used to enable communication between MetaDefender Managed File Transfer™ and MetaDefender Core™. It should point to the machine where Metadefender Core is installed. (i.e., <http://10.1.2.3:8008/metascan_rest>)
- **API Key:** an optional field used to fine-tune the integration and restrict access to the MetaDefender Core installation.
- **Default Workflow**: Select the available workflow (as configured in MetaDefender Core™) from the dropdown list.
- **User Agent:** specify a user agent to filter rules (as configured in MetaDefender Core™).
- **Processing Timeout** Set the timeout for waiting for results from MetaDefender Core™. The timeout can be between 3 and 1,000,000 minutes.

Select actions to take when a file is blocked or when processing with MetaDefender Core™ fails. If you enable "Delete the file", the file will be deleted once it is blocked.

When done, click "Update." MetaDefender Managed File Transfer™ will now process files with MetaDefender Core™.

Info

The list of available workflows is depends on the *User Agent* and *API Key*. If either of these variables is changed, a new list of items will be fetched. For further information, refer to the [MetaDefender Core API documentation](/docs/mdmft).

Info

[You can assign custom MetaDefender Core Workflow for Local Users](/docs/mdmft/v3.11.4/operating/custom-metadefender-core-workflow-rule-for-local-users).

## [Load Balancing and High Availability](/docs/mdmft/v3.11.4/integrations/metadefender-core-integration#load-balancing-and-high-availability)

## [Using the Built-In Round-Robin Algorithm](/docs/mdmft/v3.11.4/integrations/metadefender-core-integration#using-the-built-in-round-robin-algorithm)

MetaDefender Managed File Transfer supports multiple MetaDefender Core servers for load balancing and high availability. To add another server, repeat the steps above.

## [Using an External Layer 7 Load Balancer](/docs/mdmft/v3.11.4/integrations/metadefender-core-integration#using-an-external-layer-7-load-balancer)

Load balancing can also be achieved using an external *Layer 7 load balancer* to manage multiple MetaDefender Core servers. In this configuration, MetaDefender Managed File Transfer communicates directly with the load balancer. The load balancer must support sticky sessions (using cookies) for this setup to work.

For more details, visit the [Using external Load Balancer](/docs/mdmft) page in the MetaDefender Core user guide.
