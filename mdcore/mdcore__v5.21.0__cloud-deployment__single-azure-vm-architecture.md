<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/cloud-deployment/single-azure-vm-architecture -->

# Single Azure VM

The single instance deployment is only recommended for small or test environments that do not need high availability. This deployment consist of a single VM instance using the MetaDefender Core image published in the Azure marketplace that includes a Standalone MetaDefender Core where the PostgreSQL database is deployed in the same instance than MetaDefender Core.

## [Diagram](/docs/mdcore/v5.21.0/cloud-deployment/single-azure-vm-architecture#diagram)

## [Resources Inventory](/docs/mdcore/v5.21.0/cloud-deployment/single-azure-vm-architecture#resources-inventory)

### [Resource Management](/docs/mdcore/v5.21.0/cloud-deployment/single-azure-vm-architecture#resource-management)

| Service Type | Resource Name | Description |
| --- | --- | --- |
| Resource Group | metadefender-rg | Azure Resource group for grouping all the resources needed for MetaDefender Core |

### [Networking](/docs/mdcore/v5.21.0/cloud-deployment/single-azure-vm-architecture#networking)

| Service Type | Resource Name | Description |
| --- | --- | --- |
| Security Group | MetaDefenderSecurityGroup | Generated security group to allow traffic to MetaDefender REST API. |
| Vnet | metadefender-core-vnet | Desired Virtual Private Cloud |
| SubNet | metadefender-core-subnet |  |

### [Compute](/docs/mdcore/v5.21.0/cloud-deployment/single-azure-vm-architecture#compute)

| Service Type | Resource Name | Description |
| --- | --- | --- |
| Azure VM | metadefender-core-<os> | Azure VM Instance to run Windows MetaDefender Core AMI |

### [Storage](/docs/mdcore/v5.21.0/cloud-deployment/single-azure-vm-architecture#storage)

| Service Type | Resource Name | Description |
| --- | --- | --- |
| Azure Managed Disk | metadefender-core-data1-disk | Azure Disk for use cases where is needed additional storage |
