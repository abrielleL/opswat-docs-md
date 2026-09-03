<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/metadefender-core-on-k8s--persisting-quarantine--dlp--and-cdr-ou -->

# MetaDefender Core on K8s: Persisting Quarantine, DLP, and CDR Output Across Pod Restarts

This article applies to MetaDefender Core All MetaDefender Core releases deployed on Linux.

## [Problem Summary](/docs/mdcore/v5.21.0/knowledge-base/metadefender-core-on-k8s--persisting-quarantine--dlp--and-cdr-ou#problem-summary)

When MetaDefender Core runs on Kubernetes without persisting output directories, files produced by quarantine, DLP, and Content Disarm and Reconstruction (CDR) are lost after pod restarts, reschedules, or scale-in/out events. This occurs because ephemeral container filesystems do not survive lifecycle changes.

## [What Not to Do](/docs/mdcore/v5.21.0/knowledge-base/metadefender-core-on-k8s--persisting-quarantine--dlp--and-cdr-ou#what-not-to-do)

Avoid manually mounting internal Core application paths such as `/opt/ometascan/core_data/var/lib/ometascan/`. While it may appear to work initially, it can cause instability, misconfiguration, and operational issues over time. Do not rely on the `DATA_DIR` variable; it is not supported for this purpose and will be removed in the future.

## [Recommended Approach](/docs/mdcore/v5.21.0/knowledge-base/metadefender-core-on-k8s--persisting-quarantine--dlp--and-cdr-ou#recommended-approach)

Use a dedicated, persistent storage path exposed to the pod via a PersistentVolumeClaim (PVC), and instruct MetaDefender Core to place its output there using a new environment variable `STORAGE_PATH`. This cleanly separates app internals from persistent data and works reliably across pod restarts.

### [Design Overview](/docs/mdcore/v5.21.0/knowledge-base/metadefender-core-on-k8s--persisting-quarantine--dlp--and-cdr-ou#design-overview)

- Create or reference a PVC sized for your expected workload (quarantine, DLP artifacts, sanitized output, SBOMs).
- Mount the PVC into the MetaDefender Core pod at a path reserved for outputs (example: `/home/metascan/`).
- Set the environment variable `STORAGE_PATH` to the same path (example: `/home/metascan/`).
- Core organizes data by pod instance under this directory, ensuring all output persists beyond pod lifecycle events.

### [Benefits](/docs/mdcore/v5.21.0/knowledge-base/metadefender-core-on-k8s--persisting-quarantine--dlp--and-cdr-ou#benefits)

- Prevents loss of quarantine, DLP, sanitized, and SBOM files after pod restarts.
- Avoids brittle mounts into internal app paths.
- Simplifies troubleshooting and auditing by keeping pod-specific subfolders.

## [High-Level Implementation Steps](/docs/mdcore/v5.21.0/knowledge-base/metadefender-core-on-k8s--persisting-quarantine--dlp--and-cdr-ou#high-level-implementation-steps)

### [1) Plan Capacity and Retention](/docs/mdcore/v5.21.0/knowledge-base/metadefender-core-on-k8s--persisting-quarantine--dlp--and-cdr-ou#1-plan-capacity-and-retention)

- Estimate daily volume of quarantined, DLP, sanitized, and SBOM artifacts.
- Align PVC size and storage class performance (IOPS/throughput) to SLA and retention goals.
- Plan a rotation/cleanup policy.

### [2) Create or Select a PersistentVolumeClaim](/docs/mdcore/v5.21.0/knowledge-base/metadefender-core-on-k8s--persisting-quarantine--dlp--and-cdr-ou#2-create-or-select-a-persistentvolumeclaim)

Provision a PVC using your Kubernetes platform’s standard process. At minimum define:

- Storage class (backed by your CSI driver)
- Requested capacity
- Access mode compatible with your deployment pattern (e.g., ReadWriteOnce or ReadWriteMany as your storage supports)

Details vary by platform; use your provider’s documentation for PVC creation and binding.

### [3) Mount the PVC in the Pod and Set STORAGE_PATH](/docs/mdcore/v5.21.0/knowledge-base/metadefender-core-on-k8s--persisting-quarantine--dlp--and-cdr-ou#3-mount-the-pvc-in-the-pod-and-set-storage_path)

In your deployment (YAML/Helm/Operator), add:

- A volume sourced from your PVC
- A persistentDir and storage_name `/home/metascan/` (examples) under core components
- An environment variable `STORAGE_PATH=/home/metascan/`

pvc:
- name: opswat-mdcore-volume # The name of the PVC.
enabled: true
labels:
app: mdcore-opswat # Key-value pairs for categorizing and selecting resources.
annotations:
accessModes: # Specifies the desired access modes for the volume. (Common modes ReadWriteOnce, ReadOnlyMany and ReadWriteMany)
- ReadWriteOnce
resources:
requests: # The amount of storage requested.
storage: 100Gi
storageClassName: local-path # The name of the StorageClass to use for dynamic provisioning. If omitted, the default StorageClass is used.
volumeMode: Filesystem # Defines whether the volume is presented as a filesystem (Filesystem) or a raw block device (Block).
core_components:
md-core:
name: md-core
env:
- name: STORAGE_PATH
value: /home/metascan # A path inside MDCore pod
persistentDir: /home/metascan
storage_name: opswat-mdcore-volume

Notes:

- Provided sample values in the above. Use values that are valid for your current system.
- Do not mount to internal app directories; use a clean path like `/home/metascan/`.

## [What You Should See After Startup](/docs/mdcore/v5.21.0/knowledge-base/metadefender-core-on-k8s--persisting-quarantine--dlp--and-cdr-ou#what-you-should-see-after-startup)

When the pod is running with this PVC attached, the `STORAGE_PATH` directory will include subdirectories for each pod instance name as well as shared artifacts. For example (the following are ls commands run from inside a running pod):

root@md-core-6554dc5f5c-6cmlg:/# ls /home/metascan/
docker_upgrade_db.log md-core-6554dc5f5c-6cmlg md-core-6554dc5f5c-8vnkb md-core-6554dc5f5c-ww26l sharedb
root@md-core-6554dc5f5c-6cmlg:/# ls /home/metascan/md-core-6554dc5f5c-6cmlg/
dlp quarantine sanitized sbom_report
root@md-core-6554dc5f5c-6cmlg:/# ls /home/metascan/md-core-6554dc5f5c-6cmlg/sanitized/a8/4b/a84bcc759e6bfac668b9aa7b46d70b243c26f2561cdfd0d474a78653633d4982
/home/metascan/md-core-6554dc5f5c-6cmlg/sanitized/a8/4b/a84bcc759e6bfac668b9aa7b46d70b243c26f2561cdfd0d474a78653633d4982
root@md-core-6554dc5f5c-6cmlg:/#

This reflects:

- Per-pod folders for running and previously deleted pods—data persists across restarts.
- Directories for DLP output, quarantine, sanitized files, and SBOM reports under each pod’s folder.

Summary:

Use `STORAGE_PATH` to direct Core’s output to a PVC-backed directory (e.g., `/home/metascan/`). Do not mount internal app directories or use the `DATA_DIR` variable. This approach ensures quarantine, DLP, sanitized, and SBOM files persist across pod restarts.

Support:

If Further Assistance is required, please proceed to [log a support case or chatting with our support engineer](https://my.opswat.com/support)
