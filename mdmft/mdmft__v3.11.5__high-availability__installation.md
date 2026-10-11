<!-- source: https://www.opswat.com/docs/mdmft/v3.11.5/high-availability/installation -->

# Installation

View as Markdown Summarize this page Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

This guide introduces the components required for setting up HA cluster and outlines the installation flow.

Before beginning the installation, ensure that the [Requirements](/docs/mdmft/v3.11.5/high-availability/requirements) are met.

## [Installation steps](/docs/mdmft/v3.11.5/high-availability/installation#installation-steps)

1. Download both installers from My OPSWAT™ in MetaDefender Managed File Transfer™ section.
2. Install MetaDefender® MFT on two different hosts ([more details](/docs/mdmft/v3.11.5/high-availability/install-mft-nodes)).
3. Install MetaDefender MFT HA Controller™ on the third host ([more details](/docs/mdmft/v3.11.5/high-availability/install-ha-controller)).
4. Configure MetaDefender MFT HA Controller™ ([more details](/docs/mdmft/v3.11.5/high-availability/controller)).

Once the MetaDefender MFT HA Controller™ is configured, verify its connectivity with all nodes to ensure failover capabilities. It's recommended to perform a simulated failover test to validate the high availability setup. Finally, ensure that all components are updated to the latest version to benefit from security patches and improvements.
