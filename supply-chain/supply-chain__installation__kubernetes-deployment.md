<!-- source: https://www.opswat.com/docs/supply-chain/installation/kubernetes-deployment -->

# Kubernetes deployment

## Install using the Helm chart

The MDSSC k8s deployment can be performed directly using the provided helm chart in our public GitHub repo [here](https://github.com/OPSWAT/metadefender-k8s) and example configuration files for different environments are provided in the `helm_charts` directory.

For system requirements and sizing considerations, please refer to the [Sizing Guide | Kubernetes Deplyoment](https://www.opswat.com/docs/supply-chain/sizing-guide/kubernetes-deployment).

### Using the helm repository

The GitHub repository can be used directly as a helm repo:

```bash
helm repo add mdk8s https://opswat.github.io/metadefender-k8s/
helm repo update mdk8s

#Example installation command
helm install mdssc mdk8s/metadefender_software_supply_chain -f <CUSTOM_VALUES_FILE.yml>
```

Or the repository can be cloned locally:

```bash
git clone https://github.com/OPSWAT/metadefender-k8s.git metadefender
cd metadefender/helm_charts

#Example installation command
helm install mdssc ./mdssc -f <CUSTOM_VALUES_FILE.yml>
```

### Storage

MDSSC containers are stateless and don't require any persistent storage. If the PostgreSQL database is deployed in the cluster, then it's recommended to use persistent storage managed by a cloud provider. The external database can be configured from the values:

```yaml
mdss-common-environment:
  POSTGRESQL_URL: "Host=postgres;Port=5432;Username=user;Password=password;Database=dbName"
```

When using an external database that is not deployed from the MDSSC chart, the `deploy_with_mdssc_db` value has to be set to `false` in order to not deploy an additional database from the chart.

### Exposing MDSSC

By default, the helm chart deploys a `ClusterIP` service for MD Core and this can be changed to any service type supported by the Kubernetes cluster. For example, a `LoadBalancer`service type can be created by overwriting the `service_type` value in the `webclient`component:

```yaml
mdssc_components:
  frontend:
    service_type: LoadBalancer
```

MDSSC can also be exposed using an ingress:

```yaml
mdssc_ingress:
  host: <APP_NAMESPACE>-mdssc.k8s  # Hostname for the publicly accessible ingress, the `<APP_NAMESPACE>` string will be replaced with the namespace where the chart is deployed
  enabled: true                     # Enable or disable the ingress creation
  class: nginx                      # Sets the ingress class depending on the installed ingress controller
```

> When the ingress terminates TLS, set [ALLOWED_ORIGINS](https://www.opswat.com/docs/supply-chain/configuration/custom-configuration#allowed-origins) in the `helm_charts/mdssc` chart values to the ingress URL.

##

---

[All pages in this documentation](https://www.opswat.com/docs/supply-chain/llms.txt)
