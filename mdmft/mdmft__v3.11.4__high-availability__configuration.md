<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/high-availability/configuration -->

# Configuration

Summarize Page    Connect to Cursor Connect to VS Code

To use multiple instances of MetaDefender MFT HA Controller™ in your setup you have to either set up the cluster mode using the HA Configuration Tool™ or edit the `appsettings.json` file focusing on the `Kestrel:Endpoints` and on the `ClusterSettings` sections.

It is recommended that before using the MetaDefender MFT HA Controller™ in a clustered environment, make sure, that the single instance configuration works well. If it does, then continue the configuration with the cluster settings.

Configuring the HA cluster consists of the following steps:

1. Set up the nodes for the MetaDefender® MFT. (See [Initial Setup](/docs/mdmft/v3.11.4/high-availability/initial-setup) section).
2. Test the failover (See [Manually triggered failover](/docs/mdmft/v3.11.4/high-availability/failover-scenarios#manually-triggered-failover) section)
3. Configure the cluster:

   1. by using MetaDefender MFT HA Controller™, see: [Configuration using Configuration Tool](/docs/mdmft/v3.11.4/high-availability/configuration-with-configurator), or
   2. or by editing the appsettings.json, see: [Configuration in appsettings.json](/docs/mdmft/v3.11.4/high-availability/configuration-with-appsettings).
