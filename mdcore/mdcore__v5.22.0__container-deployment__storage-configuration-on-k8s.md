<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/container-deployment/storage-configuration-on-k8s -->

# Storage Configuration on K8S

MD Core containers are stateless and don't require any persistent storage by default. However, there are some cases where it is needed to attach a volume to the app container or database container.

### [Configure Database Storage](/docs/mdcore/v5.22.0/container-deployment/storage-configuration-on-k8s#configure-database-storage)

If the PostgreSQL database is deployed in the cluster, then it's recommended to use persistent storage managed by a cloud provider.

When using an external database that is not deployed from the MD Core chart, the `deploy_with_core_db` value has to be set to `false` in order to not deploy an additional database from the chart.

The helm chart can be configured to use a custom storage class or persistent volume by setting the `storage_provisioner` value to custom.

Available storage providers:

- **hostPath**: doesn't use any PVCs in the pod definitions and just mounts a path on the host starting with the hostPathPrefix
- **custom**: mounts from the PVC named as the storage_name value and uses component name as the subpath

Adding the Kubernetes yaml for the persistent volume claim in the `storage_configs` value and then using the pvc name in the `storage_name` value to tell the container where to mount to volume. Here's an example using managed storage in Azure:

YamlCopystorage_configs: # Example using a PVC with dynamic provisioning from an existing storage class
pvc-example:
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
name: md-core-store-data-pvc
spec:
accessModes:
- ReadWriteOnce
resources:
requests:
storage: 1Gi
storageClassName: managed-premium
core_components:
md-core:
extraVolumeMounts:
- name: md-core-store-data
mountPath: /var/lib/ometascan
extraVolumes:
configStore:
name: md-core-store-data
persistentVolumeClaim:
claimName: md-core-store-data-pvc
