<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/container-deployment/system-requirements -->

# Resources Requirements

### [CPU & RAM Allocation](/docs/mdcore/v5.22.0/container-deployment/system-requirements#cpu--ram-allocation)

See system requirement for CPU and RAM for Linux system defined in [[Linux](/docs/mdcore/v5.22.0/installation/recommended-system-configuration) Recommended System Configuration,linux-recommended-system-configuration] based on License type purchased, multiscanning with 5, 10 or MAX engines. In case of having Deep CDR and Proactive DLP see values recommended for CPU and RAM.

To achieved a desired performance when scanning the files it is recommended to do a load test with the system required resource assigned. There are 3 factors that are important to take into consideration that would mainly affect to the CPU usage.

1. Number of files to scan per minute
2. Average file size
3. File types

Knowing well these 3 factors will help to allocate the proper resources to have best scan time.

### [Sharing Kubernetes Cluster with other applications](/docs/mdcore/v5.22.0/container-deployment/system-requirements#sharing-kubernetes-cluster-with-other-applications)

Helm chart - request only, include notes for limits in case of sharing apps

### [Disk Space Allocation](/docs/mdcore/v5.22.0/container-deployment/system-requirements#disk-space-allocation)

See [Storage Usage Information](/docs/mdcore/v5.22.0/installation/recommended-system-configuration#storage-usage-information) for minimum GB disk space allocation. It will differ depending on the space that is needed to allocate for the temporary files during processing, quarantine and sanitized files.

By default the pod is stateless so it is using the disk space allocated by the worker node where the pod is running on, to request a minimum of storage it is needed to use "ephemeral-storage:" key in the values.yaml file.

In case of wanting to mount a disk for specific files, check the location for those file in [[Linux](/docs/mdcore/v5.22.0/installation/recommended-system-configuration) Installation Details,linux-installation-details].

### [Database Requirements](/docs/mdcore/v5.22.0/container-deployment/system-requirements#database-requirements)

### [How to assign CPU & Memory to pod](/docs/mdcore/v5.22.0/container-deployment/system-requirements#how-to-assign-cpu--memory-to-pod)

To assign resources from the helm chart it is needed to modify the resources component in the values.yaml file

values.yamlCopycore_components:
md-core:
resources:
requests:
memory: "7Gi" # Minimum reserved memory
cpu: "4.0" # Minimum reserved cpu
ephemeral-storage: "60Gi" # Minimum reserved storage
limits:
memory: "8Gi" # Maximum memory limit
cpu: "8.0"
