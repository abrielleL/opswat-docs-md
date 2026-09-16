<!-- source: https://www.opswat.com/docs/mdcluster/container-deployment/troubleshooting -->

# Troubleshooting

## Inspecting a deployment

### Logs

# Follow a service
kubectl logs -f deploy/control-center
kubectl logs -f deploy/identity-service
# A specific StatefulSet replica
kubectl logs -f file-storage-0
kubectl logs -f ometascan-0
# The previous container, after a crash loop
kubectl logs ometascan-0 --previous
### Configuration actually in effect

kubectl get configmap mdcluster-config -o yaml
kubectl get secret mdcluster-secrets -o jsonpath='{.data}' | jq 'keys' # key names only
helm get values mdcluster

`helm get values` shows what the release really holds, which is not always what your values file says — particularly after an upgrade with `--reuse-values`.

## Collecting information for support

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

Can use [Export](/operating/operating-export) to collect the MetaDefender Cluster logs in full.

Review the files before sharing them — logs and ConfigMap contents may include hostnames and account names from your environment.
