<!-- source: https://www.opswat.com/docs/mdicap/installation/installing-using-helm -->

# Installing using Helm

The Kubernetes deployment for MetaDefender ICAP Server can be performed directly using the provided Helm chart, which is available in our public GitHub repository [here](https://github.com/OPSWAT/metadefender-k8s).

Example configuration files for different environments are provided in the `helm_charts` directory within the repository. As for the demand of customizing the installation of our MetaDefender ICAP Server product in a K8S cluster, we have published the helm chart on GitHub: <https://github.com/OPSWAT/metadefender-k8s/tree/main/helm_charts/icap>

## [How to Install MetaDefender ICAP Server using Helm](https://docs.opswat.com/mdcore/kubernetes-configuration/metadefender-core-in-your-already-created-k8s#how-to-install-metadefender-core-using-helm)

This chart is configured based on the variables listed in the values.yaml, minimum variables to setup to have the application running

- ACCEPT_EULA
- mdicapsrv__license__key

gitCopygit clone https://github.com/OPSWAT/metadefender-k8s.git
cd metadefender/helm_carts/icap
helm install md-icapsrv ./icap .
#You put the variables in the values.yaml file or use --set mdicapsrv_license_key=<license_key>
### Configuration Options

For configuration using helm please check [Configuration on K8S](/installation/configuration-on-k8s)
