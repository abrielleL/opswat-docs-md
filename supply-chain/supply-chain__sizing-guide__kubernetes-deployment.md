<!-- source: https://www.opswat.com/docs/supply-chain/sizing-guide/kubernetes-deployment -->

# Kubernetes Deployment

An existing cluster is the primary requirement for installing the MDSSC Helm chart.  Provisioning a Kubernetes cluster from scratch is complex task but in general, for production use cases, users choose managed Kubernetes. The differences between them are:

- **Managed Kubernetes Services**: These services abstract away much of the complexity of managing a Kubernetes cluster, but they may be more expensive.
- **Self-Managed Kubernetes**: Gives you more control over your cluster's configuration and may be cheaper, but requires more setup and maintenance.

## Installing Supply Chain on Kubernetes (k8s)

MDSSC for Kubernetes comes packaged as a Helm chart and it’s available on GitHub here: [metadefender-k8s](https://github.com/OPSWAT/metadefender-k8s/tree/main)

Additionally, it’s recommended to have MD Core installed on the same cluster for best performance and flexibility. Similarly to MD Software Supply Chain, MD Core can be installed using it’s own helm chart: [https://docs.opswat.com/mdcore/cloud-deployment/md-core-installation#helm-chart](https://docs.opswat.com/mdcore/cloud-deployment/md-core-installation#helm-chart)

For a detailed, step-by-step installation guide, please refer to the **Installation Guide: **[**Kubernetes deployment**](https://www.opswat.com/docs/supply-chain/installation/kubernetes-deployment)**.**

![](https://uploads.developerhub.io/prod/jdK6/aozb9hnuztimcjuka2tw4iy85laflbvji237feinqdjlo1a4ytjgp5jui51upray.jpeg)
