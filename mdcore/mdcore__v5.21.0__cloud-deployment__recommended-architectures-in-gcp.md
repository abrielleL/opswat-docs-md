<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/cloud-deployment/recommended-architectures-in-gcp -->

# Recommended Architectures

These pages explain what are the architecture recommended for running MetaDefender Core in GCP GKE (Kubernetes)

## [Infrastructure Options for MetaDefender Core in GCP GKE](/docs/mdcore/v5.21.0/cloud-deployment/recommended-architectures-in-gcp#infrastructure-options-for-metadefender-core-in-gcp-gke)

The possible infrastructure options in Azure AKS vary depending on how the PostgreSQL database is provisioned.

Options:

1. GCP GKE + GCP Cloud SQL
2. GCP GKE + PostgreSQL Pod

Above options are explained at [GKE Architecture](/docs/mdcore/v5.21.0/cloud-deployment/gke-cluster-architecture)

We offer a provisioning script that depending on the selection, we automatically provision the cluster for you and install the K8S components needed for MD Core service. See [GKE Deployment](/docs/mdcore/v5.21.0/cloud-deployment/gke-cluster-deployment)
