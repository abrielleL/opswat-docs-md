<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/cloud-deployment/recommended-architectures-in-azure -->

# Recommended Architectures

These pages explain what are the architecture recommended for running MetaDefender Core in an Azure VM or Azure AKS (Kubernetes)

## [Infrastructure Options for MetaDefender Core in Azure VM](/docs/mdcore/v5.22.0/cloud-deployment/recommended-architectures-in-azure#infrastructure-options-for-metadefender-core-in-azure-vm)

The possible infrastructure vary depending on what are the number of VMs where MetaDefender Core will be installed

Options:

1. Single Azure VM

## [Infrastructure Options for MetaDefender Core in Azure AKS](/docs/mdcore/v5.22.0/cloud-deployment/recommended-architectures-in-azure#infrastructure-options-for-metadefender-core-in-azure-aks)

The possible infrastructure options in Azure AKS vary depending on how the PostgreSQL database is provisioned.

Options:

1. Azure Vm + Azure PostgreSQL
2. Azure Vm + PostgreSQL Pod

Above options are explained at [AKS Cluster Architecture](/docs/mdcore/v5.22.0/cloud-deployment/aks-cluster-architecture)

We offer a provisioning script that depending on the selection, we automatically provision the cluster for you and install the K8S components needed for MD Core service. See [AKS Cluster Deployment](/docs/mdcore/v5.22.0/cloud-deployment/aks-cluster-provision)
