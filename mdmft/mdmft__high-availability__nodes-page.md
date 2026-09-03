<!-- source: https://www.opswat.com/docs/mdmft/high-availability/nodes-page -->

# Nodes Page

Summarize Page    Connect to Cursor Connect to VS Code

The Nodes page manages the MetaDefender® MFT servers monitored by the MetaDefender MFT HA Controller™. A minimum of **1** and maximum of **2** nodes are supported.

After a new installation the nodes are pre-filled with placeholder data. In this case setting up the nodes can be done by editing the prefilled nodes.

### [Viewing Nodes](/docs/mdmft/high-availability/nodes-page#viewing-nodes)

Each node is displayed as a card showing:

| Field | Description |
| --- | --- |
| Node name | Display name of the Node (e.g., "Node: MFT1") |
| Application URL | The public-facing MetaDefender® MFT URL |
| Node Manager URL | The internal API endpoint used for health checks. |
| Node Key | Always masked (shown as `••••••••••`) for security. |

### [Editing a Node](/docs/mdmft/high-availability/nodes-page#editing-a-node)

1. Click the **Edit** button on the node card.
2. A dialog appears pre-populated with the node's current values:

| Field | Description |
| --- | --- |
| Node name | Display name of the Node (e.g., "Node: MFT1") |
| Application URL | The public-facing MetaDefender® MFT URL |
| Node Manager URL | The internal API endpoint used for health checks. This is typically the same as the Application URL followed by `"/node_manager/".`  *Example:*   - Application URL: "[http://192.168.100.101:8010"](http://192.168.100.101:8010%22) - Node manager URL: "[http://192.168.100.101:8010/node_manager/"](http://192.168.100.101:8010/node_manager/%22) |
| Node Key | This value can be copied from the `node-manager.appsettings.json` file on the node where MetaDefender® MFT is installed. The file is located in the `Services` subfolder of the installation directory. Minimum 10 alphanumeric characters. |

3. Click OK to apply the changes or Cancel to discard

### [Adding a Node](/docs/mdmft/high-availability/nodes-page#adding-a-node)

If there is not already two nodes present on the page, you can add nodes with the **+ Add Node** button.

1. Click the **+ Add Node** button in the upper-right corner.
2. The same dialog opens with empty values.
3. Fill all fields and click **OK** to apply changes.

The **+ Add Node** button is disabled when 2 nodes already exist.

### [Removing a Node](/docs/mdmft/high-availability/nodes-page#removing-a-node)

1. Click the **Remove** button on the node card.
2. The node is removed from the list immediately.

The **Remove** button is disabled when only 1 node exists (minimum of 1 is required).
