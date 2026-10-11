<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/configuration/routing-utilizing-mft-proxy -->

# Routing utilizing MFT Discovery (BETA)

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
## [MFT Discovery](/docs/mdmft/v3.11.5/configuration/routing-utilizing-mft-proxy#mft-discovery)

The MFT Discovery feature enables discovery of MFT instances beyond direct MFT to MFT connections.

Remote MFT instances connected via the MFT to MFT feature to any node in the connected MFT network are automatically discovered and displayed in the user interface.

MFT instances recursively query connected peers to enumerate their links, progressively constructing the network topology.

### [Discovery in restricted networks](/docs/mdmft/v3.11.5/configuration/routing-utilizing-mft-proxy#discovery-in-restricted-networks)

In restricted networks (e.g., with data diodes preventing discovery responses), administrators can still construct the topology manually. The discovery feature lets administrators register remote MFT instances by specifying:

- The known MFT instance through which they are reachable.
- The remote instance’s identifier (deployment id).

## [MFT to MFT connection to a remote instance (Routing)](/docs/mdmft/v3.11.5/configuration/routing-utilizing-mft-proxy#mft-to-mft-connection-to-a-remote-instance-routing)

The **MFT to MFT** feature now allows administrators to select any previously discovered MFT as the destination when setting up a new connection. All intermediate MFTs automatically handle the synchronization process, securely proxying data from the source to the destination.

Although the data may pass through multiple MFTs, the connection is still treated as a **direct link between the source and destination**. This means it fully supports all standard connection features, including **Transfer Policies**, just like a traditional MFT to MFT setup.
