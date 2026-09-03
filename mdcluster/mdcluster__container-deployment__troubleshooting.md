<!-- source: https://www.opswat.com/docs/mdcluster/container-deployment/troubleshooting -->

# Troubleshooting

## [Inspecting a deployment](/docs/mdcluster/container-deployment/troubleshooting#inspecting-a-deployment)

### [Pod status](/docs/mdcluster/container-deployment/troubleshooting#pod-status)

kubectl get pods
kubectl get pods -l component=worker # all worker instances
kubectl describe pod <pod> # events, probe failures, scheduling problems

The `Events` section at the end of `describe` is usually where the answer is: image pull failures, unschedulable resource requests, and probe failures all appear there.

### [Logs](/docs/mdcluster/container-deployment/troubleshooting#logs)

# Follow a service
kubectl logs -f deploy/control-center
kubectl logs -f deploy/identity-service
# A specific StatefulSet replica
kubectl logs -f file-storage-0
kubectl logs -f ometascan-0
# The previous container, after a crash loop
kubectl logs ometascan-0 --previous
### [Run a health check by hand](/docs/mdcluster/container-deployment/troubleshooting#run-a-health-check-by-hand)

Every container carries the same health check script that its probes use. Running it directly shows you *why* a probe is failing:

kubectl exec ometascan-0 -- sh -c '${WORK_DIR}/healthcheck.sh readiness'
kubectl exec ometascan-0 -- sh -c '${WORK_DIR}/healthcheck.sh liveness'
kubectl exec deploy/control-center -- sh -c '${WORK_DIR}/healthcheck.sh readiness'
### [Readiness detail](/docs/mdcluster/container-deployment/troubleshooting#readiness-detail)

The MetaDefender Cluster Control Center reports per-component readiness:

kubectl port-forward deploy/control-center 8892:8892
curl -s 'http://127.0.0.1:8892/readyz?verbose=true' | jq

This names the component that is not ready — database, cache, broker or MetaDefender Cluster Identity Service — which is faster than reading the log. Use `https://` if you enabled HTTPS on the Control Center.

### [Configuration actually in effect](/docs/mdcluster/container-deployment/troubleshooting#configuration-actually-in-effect)

kubectl get configmap mdcluster-config -o yaml
kubectl get secret mdcluster-secrets -o jsonpath='{.data}' | jq 'keys' # key names only
helm get values mdcluster

`helm get values` shows what the release really holds, which is not always what your values file says — particularly after an upgrade with `--reuse-values`.

## [Diagnosing specific areas](/docs/mdcluster/container-deployment/troubleshooting#diagnosing-specific-areas)

### [Database connectivity](/docs/mdcluster/container-deployment/troubleshooting#database-connectivity)

The MetaDefender Cluster Control Center creates four databases on first start. Confirm they exist:

kubectl exec deploy/postgres -- psql -U <db-user> -d postgres -c '\l'

Expect `md_cluster_control_center`, `md_cluster_datalake`, `md_cluster_datawarehouse` and `md_cluster_identity_service`.

If they are missing, the database role most likely cannot create databases. With the bundled PostgreSQL this happens when the four credential pairs in `secrets:` disagree — the bundled instance takes its superuser credentials from `CONTROL_CENTER_DB_USER` and `CONTROL_CENTER_DB_PASSWORD`, so the MetaDefender Cluster Identity, datalake and warehouse users must match. With an external database, the role needs `createdb`.

Check connection exhaustion when running many replicas:

kubectl exec deploy/postgres -- psql -U <db-user> -d postgres -c \
'SELECT count(*), setting FROM pg_stat_activity, pg_settings WHERE name = $$max_connections$$ GROUP BY setting;'

Raise `postgres.maxConnections` if you are near the limit.

### [Service discovery](/docs/mdcluster/container-deployment/troubleshooting#service-discovery)

Verify a name resolves from inside a pod:

kubectl exec deploy/control-center -- getent hosts identity-service
kubectl exec deploy/control-center -- getent hosts file-storage-0.file-storage

If components live in different namespaces, endpoints must be fully qualified as `<service>.<namespace>.svc.cluster.local`.

### [Storage](/docs/mdcluster/container-deployment/troubleshooting#storage)

kubectl get pvc
kubectl exec file-storage-0 -- df -h /app/storage
kubectl exec deploy/postgres -- df -h /var/lib/postgresql/data

Permission errors writing to `/app/storage` normally mean the volume does not honour the pod's `fsGroup`. This is the expected failure mode with NFS, which is not supported — see [Storage configuration](/docs/mdcluster/container-deployment/storage-configuration).

## [Collecting information for support](/docs/mdcluster/container-deployment/troubleshooting#collecting-information-for-support)

# Everything in the namespace
kubectl get all -o wide > cluster-state.txt
kubectl describe pods > pod-details.txt
# Effective configuration (Secret values are not included)
kubectl get configmap mdcluster-config -o yaml > config.yaml
helm get values mdcluster > values-mdcluster.yaml
# Logs
for p in $(kubectl get pods -o name); do
kubectl logs "$p" --all-containers --tail=5000 > "logs-${p#pod/}.txt"
done

Include your MetaDefender Cluster version (`MDCLS_VERSION`), your Kubernetes version (`kubectl version`), and whether you use the bundled or external infrastructure.

Can use [Export](/docs/mdcluster/operating/operating-export) to collect the MetaDefender Cluster logs in full.

Review the files before sharing them — logs and ConfigMap contents may include hostnames and account names from your environment.
