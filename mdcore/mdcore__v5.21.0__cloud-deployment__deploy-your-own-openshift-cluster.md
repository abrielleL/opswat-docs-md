<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/cloud-deployment/deploy-your-own-openshift-cluster -->

# Deploy your Own OpenShift Cluster

RedHat OpenShift is platform agnostic and can be deployed on any compatible hardware. The installation process is covered in detail on their documentation page:

[https://docs.openshift.com/container-platform/4.12/installing/installing_platform_ agnostic/installing-platform-agnostic.html](https://docs.openshift.com/container-platform/4.12/installing/installing_platform_agnostic/installing-platform-agnostic.html)

## [Cluster requirements for MD Core](/docs/mdcore/v5.21.0/cloud-deployment/deploy-your-own-openshift-cluster#cluster-requirements-for-md-core)

- Cluster nodes should still follow the recommended [MD Core system requirements](https://docs.opswat.com/mdcore/installation/recommended-system-configuration#linux-recommended-system-configuration) for the expected load
- Persistent storage is required for the MD Core database (PostgreSQL) while the MD Core containers are stateless and do not require any persistency
- In case of an on-premise cluster, internet access to <hub.docker.com> is required to pull all MD Core related images
