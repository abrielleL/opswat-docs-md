<!-- source: https://www.opswat.com/docs/mdcore/cloud-deployment/vm-scale-set -->

# VM Scale Set

The multi instance deployment is recommended for medium or large environments that need high availability. This deployment consist of a VMSS with as many virtual machines as needed depending on the number of files to scan.

## [Diagram](/docs/mdcore/cloud-deployment/vm-scale-set#diagram)

## [Resources Inventory](/docs/mdcore/cloud-deployment/vm-scale-set#resources-inventory)

### [Resource Management](/docs/mdcore/cloud-deployment/vm-scale-set#resource-management)

| Service Type | Resource Name | Description |
| --- | --- | --- |
| Resource Group | metadefender-rg | Azure Resource group for grouping all the resources needed for MetaDefender Core |

### [Networking](/docs/mdcore/cloud-deployment/vm-scale-set#networking)

| Service Type | Resource Name | Description |
| --- | --- | --- |
| Security Group | MetaDefenderSecurityGroup | Generated security group to allow traffic to MetaDefender REST API. |
| Vnet | metadefender-core-vnet | Desired Virtual Private Cloud |
| SubNet | metadefender-core-subnet |  |

### [Compute](/docs/mdcore/cloud-deployment/vm-scale-set#compute)

| Service Type | Resource Name | Description |
| --- | --- | --- |
| Azure VMSS | metadefender-core-<vmss> | Azure VMSS Instance to run multiple instances |

### [Storage](/docs/mdcore/cloud-deployment/vm-scale-set#storage)

| Service Type | Resource Name | Description |
| --- | --- | --- |
| Azure Managed Disk | metadefender-core-data1-disk | Azure Disk for use cases where is needed additional storage |
