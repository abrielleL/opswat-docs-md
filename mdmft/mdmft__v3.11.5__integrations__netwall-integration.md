<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/integrations/netwall-integration -->

# NetWall Integration

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

To enhance the security and integrity of MFT-to-MFT integrations, you can place a data diode such as MetaDefender NetWall® between systems. This creates a unidirectional network path that streamlines and hardens data flow.

## [MetaDefender Managed File Transfer™ Configuration Example](/docs/mdmft/v3.11.5/integrations/netwall-integration#product_name-configuration-example)

This example shows how to route MFT-to-MFT traffic through a MetaDefender NetWall® Stream so transfers cross the data diode using a diode-facing address. Before you begin, make sure you have the diode-facing IP address (from the Stream configuration) and the destination MFT API key.

Info

Before configuring MetaDefender Managed File Transfer™, consult the MetaDefender NetWall®'s Managed File Transfer Stream [documentation](/docs/mdmft) for guidance.

Configure the remote endpoint so MetaDefender Managed File Transfer™ connects to the diode-facing IP address provided by MetaDefender NetWall®.

1. Enable **MFT to MFT**.
2. Add a destination MFT:

   - **Host/IP**: the diode-facing IP address from MetaDefender NetWall®
   - **API key**: the destination MFT API key
   - **Notes**: Keep this endpoint pointed at the diode-facing address (not the real destination-side address) so all traffic traverses the Stream.

Example network

MFT to MFT settings

Adding a Destination MFT

## [Limitations](/docs/mdmft/v3.11.5/integrations/netwall-integration#limitations)

Warning

When a data diode sits between two MetaDefender Managed File Transfer™ instances, **Enforce Synchronization** cannot be used because it requires bidirectional communication.

If you need synchronization guarantees, use a design that supports return traffic (or validate transfer completion through one-way acknowledgements/log review outside of MetaDefender Managed File Transfer™ synchronization).

Info

MetaDefender NetWall® supports a maximum of 20 TCP connections per Stream. To ensure optimal performance and functionality, configure the source MFT based on the steps below.

### [Configurations](/docs/mdmft/v3.11.5/integrations/netwall-integration#configurations)

In order to have the most effective communication in this setup, and since MetaDefender NetWall® supports a maximum of 20 TCP connections per Stream, cap concurrency on the source MFT should be set to avoid connection exhaustion.

1. Open `opswat.vault.processor.service.exe.config` in the `Services` folder under the installation directory.

- Default path: `C:\Program Files\OPSWAT\MetaDefender Managed File Transfer\Services\`

2. Update these settings (example values shown):

<!-- Keep below the Stream's max of 20 TCP connections -->
<add key="maxConcurrentTransferConnections" value="10" />
<!-- Must be <= maxConcurrentTransferConnections -->
<add key="forwardRequestsThrottle" value="5" />

3. Save the file and restart the relevant MetaDefender Managed File Transfer™ service(s) to apply the changes.

Tip

If you increase `maxConcurrentTransferConnections`, increase `forwardRequestsThrottle` only up to the same value, and keep the total comfortably below 20 to leave headroom for retries and bursts.
