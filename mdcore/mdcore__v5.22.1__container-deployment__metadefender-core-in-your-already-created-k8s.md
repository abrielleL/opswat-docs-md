<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/container-deployment/metadefender-core-in-your-already-created-k8s -->

# Installing MetaDefender Core in K8S

View as Markdown Ask ChatGPT about this page Ask Claude about this page

This guide explains how to use the provisioning script for generating all the Kubernetes components needed to run MetaDefender Core in you already created K8S cluster that depending on some configuration options chosen it will adapt the helm chart values for configuring it properly.

Also includes the details needed to understand how to install MetaDefender Core using directly the Helm chart.

## [Install using the Helm chart](/docs/mdcore/v5.22.1/container-deployment/metadefender-core-in-your-already-created-k8s#install-using-the-helm-chart)

The MD Core k8s deployment can be performed directly using the provided helm chart in our public GitHub repo [here](https://github.com/OPSWAT/metadefender-k8s) and example configuration files for different environments are provided in the `helm_charts` directory.

### [Using the helm repository](/docs/mdcore/v5.22.1/container-deployment/metadefender-core-in-your-already-created-k8s#using-the-helm-repository)

The GitHub repository can be used directly as a helm repo:

BashCopyhelm repo add mdk8s https://opswat.github.io/metadefender-k8s/
helm repo update mdk8s
#Example installation command
helm install mdcore mdk8s/metadefender_core -f <CUSTOM_VALUES_FILE.yml>

Or the repository can be cloned locally:

BashCopygit clone https://github.com/OPSWAT/metadefender-k8s.git metadefender
cd metadefender/helm_charts
#Example installation command
helm install mdcore ./mdcore -f <CUSTOM_VALUES_FILE.yml>
### [Exposing MetaDefender Core Service](/docs/mdcore/v5.22.1/container-deployment/metadefender-core-in-your-already-created-k8s#exposing-metadefender-core-service)

By default, the helm chart deploys a `ClusterIP` service for MD Core and this can be changed to any service type supported by the Kubernetes cluster. For example, a `LoadBalancer`service type can be created by overwriting the `service_type` value in the `md-core` component:

YamlCopycore_components:
md-core:
service_type: LoadBalancer

MD Core can also be exposed using an ingress:

YamlCopycore_ingress:
host: <APP_NAMESPACE>-mdcore.k8s # Hostname for the publicly accessible ingress, the `<APP_NAMESPACE>` string will be replaced with the namespace where the chart is deployed
enabled: true # Enable or disable the ingress creation
class: nginx # Sets the ingress class depending on the installed ingress controller
### [Scaling MD Core](/docs/mdcore/v5.22.1/container-deployment/metadefender-core-in-your-already-created-k8s#scaling-md-core)

Multiple MD Core pods can be deployed by setting the `replicas`value in the`md-core` component:

YamlCopycore_components:
md-core:
replicas: 3
### [TLS Configuration](/docs/mdcore/v5.22.1/container-deployment/metadefender-core-in-your-already-created-k8s#tls-configuration)

In case we want to use a self-signed certificate, we need to create the secrets with the crt and key

BashCopymkdir ~/cert
openssl req -new -newkey rsa:4096 -days 36500 -nodes -x509 -keyout ~/cert/mdcore.key -out ~/cert/mdcore.crt
# Needed to replace <user>. kubectl do not accept "~"
kubectl create secret generic mdcore-tls-cert --from-file=/home/<user>/cert/mdcore.crt -n default
kubectl create secret generic mdcore-tls-cert-key --from-file=/home/<user>/cert/mdcore.key -n default

We can set up the configuration parameters in the values.yaml file

YamlCopy# From Values.yaml
tls:
enabled: false
certSecret: mdcore-tls-cert
certSecretSubPath: mdcore.crt
certKeySecret: mdcore-tls-cert-key
certKeySecretSubPath: mdcore.key
ReadinessProbe:
httpGet:
scheme: HTTPS
livenessProbe:
httpGet:
scheme: HTTPS
### [Ingress Configuration By CSP](/docs/mdcore/v5.22.1/container-deployment/metadefender-core-in-your-already-created-k8s#ingress-configuration-by-csp)

1. In case we want to use a self-signed certificate, we need to create the tls secret with the crt and key

BashCopymkdir ~/cert
openssl req -new -newkey rsa:4096 -days 36500 -nodes -x509 -keyout ~/cert/mdcore.key -out ~/cert/mdcore.crt
# Needed to replace <user>. kubectl do not accept "~". Also change <namespace>
kubectl create secret tls mdcore-tls --key="/home/<user>/cert/mdcore.key" --cert="/home/<user>/cert/mdcore.crt" -n <namespace>

2. Set up the following configuration parameters in the values.yaml file

YamlCopy# Ingress setting for md core (md core setting are ignored if deploy_with_core is false)
core_ingress:
host: <APP_NAMESPACE>-mdcore.k8s # Hostname for the publicly accessible ingress, the `<APP_NAMESPACE>` string will be replaced with the namespace where the chart is deployed
service: md-core # Service name where the ingress should route to, this should be left unchanged
port: 8008 # Port where the ingress should route to
enabled: true # Enable or disable the ingress creation
spec_className: true # true -> for adding class as spec || false -> for adding class as annotation. false for GKE as it needs to be as annotation.
class: nginx # Sets the ingress class
tls: true # Flag for set up tls section in ingress
secret: mdcore-tls # SecretName of the tls secret created to be used for ingress
ingress_annotations:
nginx.ingress.kubernetes.io/affinity: cookie # To set affinity when having more than one pod running behind the ingress

3. Install MetaDefender Core using Helm
4. Install [Nginx Ingress Controller](https://github.com/kubernetes/ingress-nginx)

   1. For Azure see example below
   2. For AWS you need to install AWS LB Controller and set up the ingress with the annotations indicated
   3. GCP install it automatically, see below configuration needed

AzureAWSGCPBashCopyhelm upgrade --install mdcore-ingress ingress-nginx/ingress-nginx --debug \
--create-namespace \
--namespace nginx-ingress \
--version 4.6.1 \
--set controller.replicaCount=2 \
--set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-internal"=false \ #Change to true if you want to have an internal load balancer
--set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-health-probe-request-path"=/healthzyamlCopycore_ingress:
host: <APP_NAMESPACE>-mdcore.k8s
enabled: true
spec_className: true
ingress_annotations:
alb.ingress.kubernetes.io/scheme: internet-facing
alb.ingress.kubernetes.io/target-type: ipvalues.ymlCopycore_ingress:
spec_className: false
core_components:
md-core:
service_type: NodePort
### [Proxy Configuration](/docs/mdcore/v5.22.1/container-deployment/metadefender-core-in-your-already-created-k8s#proxy-configuration)

To enable Proxy, the following criteria must be met

- The proxy server should be already deployed and reachable from the MetaDefender Core pod.
- Add env vars needed

values.yamlCopyenv:
# MD Core proxy settings
PROXY: false # Enable the proxy settings in MD Core
PROXY_HOST: "" # Proxy server host address
PROXY_PORT: 8080 # Proxy server port
PROXY_USER: "" # (optional) Username for proxy authentication
PROXY_PWD: "" # (optional) Password for proxy authentication
PROXY_EXCLUSION: "" # Not use the proxy server for the addresses starting with the following entries, separated by comma
## [Flowchart for MetaDefender K8S Script](/docs/mdcore/v5.22.1/container-deployment/metadefender-core-in-your-already-created-k8s#flowchart-for-metadefender-k8s-script)

The following flow chart represents how the MetaDefenderK8S script will configure the environment based on the options selected for installing MetaDefender products in an already created cluster.

### [Summary options to be selected](/docs/mdcore/v5.22.1/container-deployment/metadefender-core-in-your-already-created-k8s#summary-options-to-be-selected)

1. Select your cluster context where you want to install the MetaDefender products
2. Access to the K8S cluster. Generate **Ingress** or provide **own** access.

   1. **An Ingress** will be create per each product flag added as parameter to the script
   2. **Own Access**, you decide how to access to the cluster so it won't generate any ingress for accessing
3. Have your **own database** or create **new database**

   1. **Own database,** will be asked if you want either

      1. the script to set up the credentials and database host url for you
      2. the script will just indicate the secrets to edit, later on by you, for connecting the MetaDefender Core with your database.
   2. Create new **DB in K8S.** It will generate a postgreSQL pod inside the cluster

### [How to run script](/docs/mdcore/v5.22.1/container-deployment/metadefender-core-in-your-already-created-k8s#how-to-run-script)

Only MD CoreMD Core + MDSSCopy./metadefenderk8s.sh install --mdcore --name <k8s-cluster-name>./metadefenderk8s.sh install --mdcore --name <k8s-cluster-name> --mdss
### [Script Parameters](/docs/mdcore/v5.22.1/container-deployment/metadefender-core-in-your-already-created-k8s#script-parameters)

| Parameter | Flags | Options | Default | Description | Required/Optional |
| --- | --- | --- | --- | --- | --- |
| **Cluster Name** | --name |  | md-k8s | Name of the cluster that will be used for naming all the resources | **Required** |
| **MetaDefender Flag Installation** | Combination of   - --mdcore - --mdss - --icap |  |  | Install MD Core in the cluster provisioned | **Required** |
| **Image Version** | --image | latest 5.0.1 | latest | MD Core image version to install | Optional |
| **Region** | --region | [AWS Regions](AWS Regions) | eu-central-1 | AWS region where all the resources will be provisioned | Optional |
| **Number of Replicas** | --replicas | [0-9]* | 1 | Number of replicas for MD Core service | Optional |
| **Namespace** | --namespace | [A-Za-z]{1,10} |  | Namespace where MetaDefender products will be installed in the K8S Cluster | Optional Max Characters: 10 |
