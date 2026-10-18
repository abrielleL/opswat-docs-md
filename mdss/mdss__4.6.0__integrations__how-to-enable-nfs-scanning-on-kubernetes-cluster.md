<!-- source: https://www.opswat.com/docs/mdss/4.6.0/integrations/how-to-enable-nfs-scanning-on-kubernetes-cluster -->

# How to Enable NFS scanning on a Kubernetes Cluster

In order to scan an NFS share when having MDSS deployed in a Kubernetes cluster, the share location has to be mounted in the `nfsservice` container as a directory in the following path: `/opt/mdss/nfs/` . For example, the following values file can be applied when deploying MDSS using the helm chart.

```yaml
mdss_components:
  nfsservice:
    extraVolumes:
      nfsTest:
        name: nfs-storage-unit
        nfs:
          server: <NFS_SERVER_IP>
          path: <PATH_EXPORTED_ON_SERVER>
          readOnly: no
    extraVolumeMounts:
      - name: nfs-storage-unit
        mountPath: /opt/mdss/nfs/<MOUNT_DIRECTORY>
        subPath: <SUBPATH_TO_SCAN>
```

This example file can also be found on our GitHub repo for k8s deployments [here](https://github.com/OPSWAT/metadefender-k8s/blob/main/helm_charts/mdss-nfs-example.yml)

After replacing the placeholders, these values can be applied when deploying MDSS:

```bash
helm install mdss <PATH_TO_HELM_CHART> -f mdss-nfs-example.yml
```

#### Notes:

- Any storage unit that can be mounted as a Persistent Volume in the container can also have it's contents scanned using the NFS module
- Make sure that the share is mounted with the appropriate permissions, for example, whenever remediations or CDR are configured write permissions are also required

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
