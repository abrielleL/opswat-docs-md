<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/high-availability/initial-setup -->

# Initial Setup

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

After both nodes and MetaDefender MFT HA Controller™ are installed on their respective hosts, an initial configuration is required to activate MetaDefender MFT HA Controller™.

In order to do that, the following steps needs to be done:

1. Collect the following information on both nodes:

   1. Application Address (e.g. `http://192.168.100.101:8010`)
   2. Node API key: This is located in the following file on the node's host: `<mft-install-dir>\Services\node-manager.appsettings.json`
2. Update the MetaDefender MFT HA Controller™ Configuration

   1. Navigate to the installation directory of the MetaDefender MFT HA Controller™.
   2. Open `appsettings.json` file
   3. Under HighAvailabilitySettings -> Nodes section, populate the following fields using the information collected from each node:

      - ApplicationAddress
      - NodeManagerAddress
      - ApiKey
3. Restart the MetaDefender MFT High Availability Controller™ Service
4. Following a successful installation and startup, the MetaDefender MFT HA Controller™ will be listening on the configured port - port 8100 by default - which is accessible both locally via `http://127.0.0.1:8100` and remotely from external hosts, depending on network configuration and firewall settings.
5. Login into MetaDefender® MFT and navigate to Settings > Security > Trusted Forwarders and configure the freshly installed MetaDefender MFT HA Controller™ as a Trusted Forwarder. Add a new Trusted Forwarder entry with the IP address of the MetaDefender MFT HA Controller™. You can find more information [here](/docs/mdmft/v3.11.5/configuration/trusted-forwarder).

See the [Configuration](/docs/mdmft/v3.11.5/high-availability/controller) page for more configuration details.

## [Example](/docs/mdmft/v3.11.5/high-availability/initial-setup#example)

Let's assume we installed both nodes and the HA controller. We collected the following data from the nodes:

| Node name | Node address | API Key |
| --- | --- | --- |
| Node1 | <http://192.168.100.101:8010> | "your-api-key-1" |
| Node2 | <http://192.168.100.102:8010> | "your-api-key-2" |

Then open the HA Configuration Tool™ , navigate to the Nodes page and propagate the nodes with the collected data (see: [HA Configuration Tool](/docs/mdmft/v3.11.5/high-availability/ha-configuration-tool-manual))

1. Edit or add Node 1:

2. Edit or add Node 2:

3. After clicking OK, the final result:

4. Save changes
5. Restart MetaDefender MFT HA Controller™
