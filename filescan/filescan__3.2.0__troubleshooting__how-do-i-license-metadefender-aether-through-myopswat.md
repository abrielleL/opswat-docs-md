<!-- source: https://www.opswat.com/docs/filescan/3.2.0/troubleshooting/how-do-i-license-metadefender-aether-through-myopswat -->

# How do I license MetaDefender Aether through MyOpswat

View as Markdown Ask ChatGPT about this page Ask Claude about this page

In order to license a managed MetaDefender Aether instance through our On-Prem OCM V10 instance the following steps are necessary:

- Navigate to the OCM console (OCM console\License\MetaDefender Aether tab)

- Type in the activation key/ upload YML file that has MetaDefender Aether license slots available

You can add/update licenses two ways:

-Online Activation — Only requires the license key. Enter it on the License page, and OCM v10 validates it with the Activation Server, then pushes it to enrolled instances automatically via the heartbeat mechanism.

-Offline Activation — For air-gapped environments. You'll need to obtain a license file from the MyOPSWAT Portal and upload it.

- The enrolled instances periodically send heartbeat calls. When a license command is pending, the instance fetches and activates it automatically.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
