<!-- source: https://www.opswat.com/docs/mdss/4.4.2/installation/deployment-using-helm -->

# Deployment Using Helm

The Kubernetes deployment for MetaDefender Storage Security can be performed directly using the provided Helm chart, which is available in our public GitHub repository [here](https://github.com/OPSWAT/metadefender-k8s).

Example configuration files for different environments are provided in the `helm_charts` directory within the repository.

## [Using the helm repository](/docs/mdss/4.4.2/installation/deployment-using-helm#using-the-helm-repository)

The GitHub repository can be used directly as a Helm repository:

BashCopyhelm repo add mdk8s https://opswat.github.io/metadefender-k8s/
helm repo update mdk8s
#Example installation command
helm install mdss mdk8s/metadefender_storage_security -f <CUSTOM_VALUES_FILE.yml>

Alternatively, the repository can be cloned locally:

BashCopygit clone https://github.com/OPSWAT/metadefender-k8s.git metadefender
cd metadefender/helm_carts
#Example installation command
helm install mdss ./mdss -f <CUSTOM_VALUES_FILE.yml>
## [Storage](/docs/mdss/4.4.2/installation/deployment-using-helm#storage)

MDSS containers are stateless and do not require persistent storage.

However, if deploying the PostgreSQL database within the cluster, it is recommended to use persistent storage managed by your cloud provider.

An external database can be configured using the following values:

YamlCopymdss-common-environment:
POSTGRESQL_URL: "Host=postgres;Port=5432;Username=user;Password=password;Database=dbName"

When using an external database not deployed via the MDSS chart, the `deploy_with_mdss_db` value must be set to `false` to prevent the chart from deploying an additional database.

## [Exposing MDSS](/docs/mdss/4.4.2/installation/deployment-using-helm#exposing-mdss)

By default, the Helm chart deploys a `ClusterIP` service for the MDSS deployment.

This can be changed to any service type supported by your Kubernetes cluster.

For example, to create a `LoadBalancer` service, overwrite the `service_type` value in the `webclient` component:

YamlCopymdss_components:
webclient:
service_type: LoadBalancer

MDSS can also be exposed using an Ingress:

YamlCopymdss_ingress:
host: <APP_NAMESPACE>-mdss.k8s # Hostname for the publicly accessible ingress, the `<APP_NAMESPACE>` string will be replaced with the namespace where the chart is deployed
enabled: true # Enable or disable the ingress creation
class: nginx # Sets the ingress class depending on the installed ingress controller
## [Flexible deployment](/docs/mdss/4.4.2/installation/deployment-using-helm#flexible-deployment)

By default, the Helm chart deploys MDSS with support for the following storage units: `azureblob`, `amazonsdk`, `googlecloud`, `alibabacloud`, `azurefiles`, and `box`.

For more efficient resource utilization, you can specify only the required storage units by modifying the `ENABLED_MODULES` value.

For instance, to enable support for only Azure, AWS, and GCP:

YamlCopymdss-common-environment:
ENABLED_MODULES: "azureblob,azurefiles,amazonsdk,googlecloud"
## [Supported modules](/docs/mdss/4.4.2/installation/deployment-using-helm#supported-modules)

Currently supported modules include:

- `azureblob`
- `amazonsdk`
- `googlecloud`
- `alibabacloud`
- `azurefiles`
- `smb`
- `box`
- `graph`
