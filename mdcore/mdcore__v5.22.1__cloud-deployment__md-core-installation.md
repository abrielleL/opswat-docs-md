<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/cloud-deployment/md-core-installation -->

# MD Core installation

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Resources for Kubernetes, OpenShift and cloud deployments in general are available on our GitHub repo:

<https://github.com/OPSWAT/metadefender-k8s>

Installation is performed using the provided helm chart for MD Core and an example configuration for OpenShift is provided in the `helm_charts/mdcore-openshift.yml` file.

## [Adding the helm repository](/docs/mdcore/v5.22.1/cloud-deployment/md-core-installation#adding-the-helm-repository)

The GitHub repository can be used directly as a helm repo:

BashCopyhelm repo add mdk8s https://opswat.github.io/metadefender-k8s/
helm repo update mdk8s
#Example installation command
helm install my_mdcore mdk8s/metadefender_core -f mdcore-openshift.yml

Or the repository can be cloned locally:

BashCopygit clone https://github.com/OPSWAT/metadefender-k8s.git metadefender
cd metadefender/helm_carts
#Example installation command
helm install my_mdcore ./mdcore -f mdcore-openshift.yml
## [Cluster requirements](/docs/mdcore/v5.22.1/cloud-deployment/md-core-installation#cluster-requirements)

1. A configured image pull secret for the current OpenShift user for the RedHat docker repo: `registry.redhat.io` . The helm values for OpenShift use the following image from RedHat: `registry.redhat.io/rhel8/postgresql-12` . This is only required if using the database deployment from the Helm chart, a managed external database service can be configured instead if available. The repo credentials ca be configured with the following `oc` commands:

BashCopyoc create secret docker-registry imagepullsecret --docker-server=registry.redhat.io --docker-username=<REDHAT_USER> --docker-password=<REDHAT_PASSWORD> --docker-email=<REDHAT_EMAIL>
oc secrets link <OPENSHIFT_USER> imagepullsecret --for=pull

2. An existing persistent volume or storage class to be used for database persistency. The `helm_charts/mdcore-openshift.yml` values file is configured with an example persistent volume claim using a certain storage class.

## [Storage](/docs/mdcore/v5.22.1/cloud-deployment/md-core-installation#storage)

MD Core containers are stateless and don't require any persistent storage. If the PostgreSQL database is deployed in the cluster, then it's recommended to use persistent storage managed by a cloud provider.

The helm chart can be configured to use a custom storage class or persistent volume by setting the `storage_provisioner` value to custom, adding the Kubernetes yaml for the persistent volume claim in the `storage_configs` value and then using the pvc name in the `storage_name` value to tell the Postgres pod where to save it's files. Here's an example using managed storage in Azure:

Helm ValuesCopystorage_provisioner: custom # Type of storage to use in the pod definition
storage_name: ocstorage # Name of the PVC to use in the pod definition
storage_configs: # Example using a PVC with dynamic provisioning from an existing storage class
pvc-example:
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
name: ocstorage
spec:
accessModes:
- ReadWriteOnce
resources:
requests:
storage: 1Gi
storageClassName: managed-premium

The `managed-premium` storage class is already available in the cluster if provisioned by Azure:

## [Helm chart](/docs/mdcore/v5.22.1/cloud-deployment/md-core-installation#helm-chart)

To deploy the helm chart directly in a RedHat OpenShift cluster we have the `mdcore-openshift.yml` values file. This file can be used as an example of the changes required for OpenShift:

- **PostgreSQL image**: the docker image has been changed to use the RedHat repo: `registry.redhat.io/rhel8/postgresql-12`
- **Storage**: a persistent volume claim has been configured to use an existing storage class since `hostPath` is not supported on an unprivileged container

Example installation when using local helm files and setting the custom values manually:

BashCopyhelm install my_mdcore ./helm_charts/mdcore -f mdcore-openshift.yml \
--set 'db_password=<SET_POSTGRES_PASSWORD>' \
--set 'env.POSTGRESQL_ADMIN_PASSWORD=<SET_POSTGRES_ADMIN_PASSWORD>' \
--set 'storage_configs.pvc-example.spec.storageClassName=<SET_STORAGE_CLASS_NAME>' \
--set 'mdcore_license_key=<SET_LICENSE_KEY>'
## [Exposing MD Core](/docs/mdcore/v5.22.1/cloud-deployment/md-core-installation#exposing-md-core)

After installation MD Core can be exposed in OpenShift by creating a new route in the `Networking -> Routes` section with the following settings:

- Path: `/`
- Service: `md-core`
- Target port: `8008 -> 8008`

An ingress is also created by default and can be disabled by setting the `core_ingress.enabled` value to `false` .
