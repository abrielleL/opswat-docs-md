<!-- source: https://www.opswat.com/docs/mdcluster/container-deployment/troubleshooting -->

# Troubleshooting

Use this guide when a MetaDefender (MD) Cluster service does not start, keeps restarting, or is not working as expected. Start with the quick checks below, then collect the relevant logs and configuration if you need help from OPSWAT Support.

## [Start with a quick health check](/docs/mdcluster/container-deployment/troubleshooting#start-with-a-quick-health-check)

Check the status of all pods and review recent Kubernetes events:

kubectl get pods -o wide

Look for pods that are not `Running` or `Ready`, frequent restarts, scheduling failures, storage problems, or failed health checks.

For more information about a specific pod, run:

kubectl describe pod <pod-name>

The **Events** section at the end of the output often explains why the pod cannot start or become ready.

### [Common pod states](/docs/mdcluster/container-deployment/troubleshooting#common-pod-states)

| Pod status | What to check |
| --- | --- |
| `Pending` | Run `kubectl describe pod <pod-name>` and check for insufficient CPU or memory, unbound volumes, or scheduling restrictions. |
| `CrashLoopBackOff` | Check both the current and previous container logs. The previous logs usually contain the error that caused the last restart. |
| `ImagePullBackOff` | Check the image name, registry access, image pull secret, and network connectivity to the registry. |
| `Running` but not `Ready` | Review the pod events and logs for failed readiness checks or unavailable dependencies. |

## [Review service logs](/docs/mdcluster/container-deployment/troubleshooting#review-service-logs)

Follow the logs for a Deployment:

kubectl logs -f deploy/control-center
kubectl logs -f deploy/identity-service

Follow the logs for a specific StatefulSet pod:

kubectl logs -f file-storage-<pod_index>
kubectl logs -f ometascan-<pod_index>

If a container has restarted, view the logs from its previous run:

kubectl logs <pod-name> --previous

For pods with more than one container, include logs from every container:

kubectl logs <pod-name> --all-containers

Press **Ctrl+C** to stop following live logs.

## [Check the active configuration](/docs/mdcluster/container-deployment/troubleshooting#check-the-active-configuration)

Review the configuration currently used by the deployment:

kubectl get configmap mdcluster-config -o yaml
kubectl get secret mdcluster-secrets -o jsonpath='{.data}' | jq 'keys'
helm list
helm get values <release-name> --all

The Secret command displays key names only; it does not decode or print their values.

`helm get values` shows the values stored in the Helm release. These values may differ from your local values file, especially after an upgrade performed with `--reuse-values`.

## [Collect information for OPSWAT Support](/docs/mdcluster/container-deployment/troubleshooting#collect-information-for-opswat-support)

The easiest way to collect complete MD Cluster logs is to use [Export](/docs/mdcluster/operating/operating-export) in MD Cluster Control Center.

If MD Cluster Control Center is unavailable, you can collect Kubernetes diagnostics manually. The following commands save the output in your current directory:

# Workload and storage status
kubectl get all,pvc -o wide > cluster-state.txt
# Pod details and recent events
kubectl describe pods > pod-details.txt
kubectl get events --sort-by=.metadata.creationTimestamp > cluster-events.txt
# Active configuration (Secret values are not included)
kubectl get configmap mdcluster-config -o yaml > config.yaml
helm get values <release-name> --all > values-<release-name>.yaml
# The latest 5,000 log lines from every pod and container
for p in $(kubectl get pods -o name); do
kubectl logs "$p" --all-containers --tail=5000 \
> "logs-${p#pod/}.txt" 2>&1
done

If an affected pod has restarted, also collect its previous logs:

kubectl logs <pod-name> --all-containers --previous > logs-<pod-name>-previous.txt 2>&1

Include the following details in your support request:

- MD Cluster version (`MDCLS_VERSION`)
- Kubernetes version (`kubectl version`)
- Helm release names (`helm list`)
- Whether PostgreSQL, Redis, RabbitMQ, and MD Cluster File Storage are bundled or externally managed
- Name of the affected service or pod
- Approximate time of the issue, including the time zone
- Steps to reproduce the issue, if known
- Any configuration, upgrade, or infrastructure changes made before the issue started
