<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/high-availability/requirements -->

# Requirements

Summarize Page    Connect to Cursor Connect to VS Code
## [Version compatibility](/docs/mdmft/v3.11.4/high-availability/requirements#version-compatibility)

To ensure full compatibility between all MetaDefender® MFT nodes (active, passive) and the MetaDefender MFT HA Controller™, all components must run the same product version. We maintain a unified version across all components: a change in any module triggers a full-version rollout of every component.

## [Database](/docs/mdmft/v3.11.4/high-availability/requirements#database)

Both the active and passive MetaDefender® MFT nodes must have configured with the same database instance. For more information about the supported databases [here](/docs/mdmft/v3.11.4/installation/system-requirements#database).

## [File storage](/docs/mdmft/v3.11.4/high-availability/requirements#file-storage)

The HA cluster requires a [Network Storage](/docs/mdmft/v3.11.4/configuration/storage#adding-a-new-network-storage), [Amazon S3 bucket](/docs/mdmft/v3.11.4/configuration/storage#adding-a-new-cloud-storage-in-amazon-s3) or [S3 Compatible Object Storage](/docs/mdmft/v3.11.4/configuration/storage#adding-s3-compatible-storage) for each storage type. All MetaDefender Managed File Transfer™ nodes must be able to access the storage. For more information about the storage types, click [here](/docs/mdmft/v3.11.4/configuration/storage).

## [HA Controller requirements](/docs/mdmft/v3.11.4/high-availability/requirements#ha-controller-requirements)

The MetaDefender MFT HA Controller™ acts a proxy and must be provisioned with sufficient hardware to forward all expected incoming traffic to the active node without becoming a performance bottleneck. Because the proxy’s job is lighter than the full application server (it does not run background jobs or heavy processing), its resource requirements can be somewhat lower—but it still needs to handle the peak network load.

|  | Minimum | Recommended |
| --- | --- | --- |
| CPU | 4 Cores | 8 Cores |
| RAM | 8 GB | 16 GB |
| Storage | 64 GB | 64 GB |

## [Network setup](/docs/mdmft/v3.11.4/high-availability/requirements#network-setup)

The MetaDefender MFT HA Controller™ and MetaDefender® MFT nodes should be able to access each other through network. In the recommended setup only the MetaDefender MFT HA Controller™ is open to the external/public network, the individual MetaDefender® MFT nodes are not exposed.

## [License](/docs/mdmft/v3.11.4/high-availability/requirements#license)

To operate MetaDefender® MFT in a High Availability cluster with two nodes, a valid license is required for both nodes.
