<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/-k8s--upgrade-of-existing-md-core-stack-to-a-newer-version-by-re -->

# [K8S] Upgrade of existing MD Core stack to a newer version by retaining existing shared database

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [**Overview**](/docs/mdcore/v5.22.1/knowledge-base/-k8s--upgrade-of-existing-md-core-stack-to-a-newer-version-by-re#overview)

This runbook documents the process used to upgrade the local MD Core deployment from `5.19.0` → `5.20.0` while keeping the existing PostgreSQL PVC (`DB_MODE=4`), database structure, and scan-processing history.

The same re-deployment flow can be used to also upgrade to a higher version of the MD Core application. The below article would implement the steps using a local cluster created by Minikube, that hosts 3 pods in total:

| **Item** | **Value** |
| --- | --- |
| Minikube profile | `md-core` |
| Application namespace | `md-core` |
| Helm release | `md-core` |
| PostgreSQL deployment | `postgres-core` |
| Existing PostgreSQL PVC | `postgres-core-20260722195541-60761` |
| Source database | `metadefender_core` |
| New database | `metadefender_core_5_20_0` |
| MD Core endpoints | <http://192.168.59.107:8088/>`(POD1)`<http://192.168.59.107:8089/>`(POD2)` |

## [**Safety Rules**](/docs/mdcore/v5.22.1/knowledge-base/-k8s--upgrade-of-existing-md-core-stack-to-a-newer-version-by-re#safety-rules)

| **Rule** | **Note** |
| --- | --- |
| **Do not delete active PVC** | Do not delete the active PostgreSQL PVC before confirming which claim is mounted by `postgres-core`. |
| **Pin PVC when redeploying** | Do not run a normal app redeploy without pinning the existing PVC. |
| **Avoid concurrent app pods** | Do not run both MD Core application pods while doing a history migration. |

## [**Pre-Checks**](/docs/mdcore/v5.22.1/knowledge-base/-k8s--upgrade-of-existing-md-core-stack-to-a-newer-version-by-re#pre-checks)

Confirm the current context and live resources:

kubectl config current-context
kubectl get deploy,pod,svc,pvc -n md-core -o wide
helm history md-core -n md-core

Identify the active PostgreSQL PVC:

kubectl get deploy postgres-core -n md-core \
-o jsonpath='{range .spec.template.spec.volumes[*]}{.name}{"\t"}{.persistentVolumeClaim.claimName}{"\n"}{end}'

For the current deployment, the active claim is: `postgres-core-20260722195541-60761`

## [**Back Up The Source Database**](/docs/mdcore/v5.22.1/knowledge-base/-k8s--upgrade-of-existing-md-core-stack-to-a-newer-version-by-re#back-up-the-source-database)

#### [**Step 1 - Acquire pod name:**](/docs/mdcore/v5.22.1/knowledge-base/-k8s--upgrade-of-existing-md-core-stack-to-a-newer-version-by-re#step-1---acquire-pod-name)

PGPOD="$(kubectl get pod -n md-core -l app=postgres-core -o jsonpath='{.items[0].metadata.name}')"
#### [**Step 2 - Set backup path of choice:**](/docs/mdcore/v5.22.1/knowledge-base/-k8s--upgrade-of-existing-md-core-stack-to-a-newer-version-by-re#step-2---set-backup-path-of-choice)

BACKUP="/tmp/metadefender_core_pre_prod_5.20.0_history_migration_$(date -u +%Y%m%dT%H%M%SZ).dump"
#### [**Step 3 - Generate the backup:**](/docs/mdcore/v5.22.1/knowledge-base/-k8s--upgrade-of-existing-md-core-stack-to-a-newer-version-by-re#step-3---generate-the-backup)

kubectl exec -n md-core "$PGPOD" -- sh -c 'PGPASSWORD="$POSTGRES_PASSWORD" pg_dump -U "$POSTGRES_USER" -Fc -d metadefender_core' > "$BACKUP"
#### [**Step 4 - Ensure information has been stored:**](/docs/mdcore/v5.22.1/knowledge-base/-k8s--upgrade-of-existing-md-core-stack-to-a-newer-version-by-re#step-4---ensure-information-has-been-stored)

ls -la /tmp/metadefender_core_pre_prod_5.20.0_history_migration_20260729T150523Z.dump
## [**Stop MD Core During Migration**](/docs/mdcore/v5.22.1/knowledge-base/-k8s--upgrade-of-existing-md-core-stack-to-a-newer-version-by-re#stop-md-core-during-migration)

Scale the two application deployments down before running the database migration:

kubectl scale deploy/md-core-8088 deploy/md-core-8089 -n md-core --replicas=0

**PostgreSQL must remain running !**

kubectl rollout status deploy/md-core-8088 -n md-core --timeout=300s || true
kubectl rollout status deploy/md-core-8089 -n md-core --timeout=300s || true
kubectl get pods -n md-core -o wide
## [**Run The 5.20.0 History Migration Pod**](/docs/mdcore/v5.22.1/knowledge-base/-k8s--upgrade-of-existing-md-core-stack-to-a-newer-version-by-re#run-the-5200-history-migration-pod)

Create a temporary migration pod using the `5.20.0` image. This pod reads from `metadefender_core (source database)` and creates the versioned target database `metadefender_core_5_20_0`.

This pod is a one-time migration runner and is sole purpose is to assist with the migration process - **this pod should be removed before the real Helm deployment is started again**.

Deploy the migration pod separately using the below example temporary .YAML file - by adjusting the `image: opswat/metadefendercore-debian:5.20.0`:

The control flow of the migration pod executes the following:

1 - Start a temporary pod based on the `5.20.0` image.
2 - Connect to the PG through the `postgres-core:5432`
3 - Authenticate using the `mdcore-postgres-cred` K8S secret
4 - Read the source database named `metadefender_core`
5 - Create the versioned target database, which becomes `metadefender_core_5_20_0`
6 - Copy/migrate config using the `MDCORE_UPGRADE_FROM_DB_NAME, UPGRADE_DB and MIGRATE_HISTORY` parameters and scan history into the new `metadefender_core_5_20_0`

For more information on the `values.yaml`:

[metadefender-k8s/helm_charts/mdcore/values.yaml at main · OPSWAT/metadefender-k8s](https://github.com/OPSWAT/metadefender-k8s/blob/main/helm_charts/mdcore/values.yaml)

Create the migration pod and apply the YAML:

kubectl apply -n md-core -f md-core-520-prod-history-migration.yaml

md-core-520-prod-history-migration.yaml

apiVersion: v1
kind: Pod
metadata:
name: md-core-520-prod-history-migration
labels:
app: md-core-520-prod-history-migration
spec:
restartPolicy: Never
containers:
- name: md-core
image: opswat/metadefendercore-debian:5.20.0
imagePullPolicy: IfNotPresent
ports:
- containerPort: 18191
name: rest
resources:
requests:
cpu: "2"
memory: 6Gi
ephemeral-storage: 10Gi
limits:
cpu: "6"
memory: 12Gi
ephemeral-storage: 40Gi
env:
- name: DB_MODE
value: "4"
- name: DB_TYPE
value: remote
- name: DB_HOST
value: postgres-core
- name: DB_PORT
value: "5432"
- name: DB_USER
valueFrom:
secretKeyRef:
name: mdcore-postgres-cred
key: user
- name: DB_PWD
valueFrom:
secretKeyRef:
name: mdcore-postgres-cred
key: password
- name: MDCORE_DB_NAME
value: metadefender_core
- name: MDCORE_UPGRADE_FROM_DB_NAME
value: metadefender_core
- name: UPGRADE_DB
value: "true"
- name: MIGRATE_HISTORY
value: "true"
- name: MD_USER
valueFrom:
secretKeyRef:
name: mdcore-cred
key: user
- name: MD_PWD
valueFrom:
secretKeyRef:
name: mdcore-cred
key: password
- name: APIKEY
valueFrom:
secretKeyRef:
name: mdcore-api-key
key: value
- name: LICENSE_KEY
valueFrom:
secretKeyRef:
name: mdcore-license-key
key: value
- name: MD_INSTANCE_NAME
value: md-core-520-prod-history-migration
- name: REST_PORT
value: "18191"
- name: CORE_CONF_JSON
value: '{"global/restaddress": "0.0.0.0"}'

Watch for migration success:

kubectl logs -f -n md-core md-core-520-prod-history-migration

Expected success markers:

Starting Migrate Database
Total migrate time
Total Upgrade schema time
Total Migrate and Upgrade schema time
Run Upgrade Successful
Upgrade successfuly
## [**Verify History Was Preserved**](/docs/mdcore/v5.22.1/knowledge-base/-k8s--upgrade-of-existing-md-core-stack-to-a-newer-version-by-re#verify-history-was-preserved)

Check the source and migrated database counts and confirm the migration of the scan-processing history:

PGPOD="$(kubectl get pod -n md-core -l app=postgres-core -o jsonpath='{.items[0].metadata.name}')"
for db in metadefender_core metadefender_core_5_20_0; do
echo "DB=$db"
kubectl exec -n md-core "$PGPOD" -- sh -c \
"PGPASSWORD=\"\$POSTGRES_PASSWORD\" psql -U \"\$POSTGRES_USER\" -d '$db' -Atc \"
select 'scan.request', count(*) from scan.request
union all select 'scan.scan_result', count(*) from scan.scan_result
union all select 'warehouse.fact_engine_duration_by_rule_2026', count(*) from warehouse.fact_engine_duration_by_rule_2026
union all select 'warehouse.fact_scan_performed_by_user_2026', count(*) from warehouse.fact_scan_performed_by_user_2026
order by 1;
\""
done
## [**Update Runtime Values**](/docs/mdcore/v5.22.1/knowledge-base/-k8s--upgrade-of-existing-md-core-stack-to-a-newer-version-by-re#update-runtime-values)

After migration, normal MD Core runtime should use the migrated database and should not keep upgrade mode enabled.

In `mdcore-minikube-values.yaml`:

storage_provisioner: custom
pvc:
enabled: false
env:
MDCORE_DB_NAME: "metadefender_core_5_20_0"
MDCORE_UPGRADE_FROM_DB_NAME: "metadefender_core"
UPGRADE_DB: "false"
MIGRATE_HISTORY: "false"

The host-networked core components + `init` containers should also use the `5.20.0` image:

#[POD1]
core_components:
md-core-8088:
image: opswat/metadefendercore-debian:5.20.0
initContainers:
- name: check-db-ready
image: opswat/metadefendercore-debian:5.20.0
#[POD2]
core_components:
md-core-8089:
image: opswat/metadefendercore-debian:5.20.0
initContainers:
- name: check-db-ready
image: opswat/metadefendercore-debian:5.20.0
## [**Render And Validate Helm**](/docs/mdcore/v5.22.1/knowledge-base/-k8s--upgrade-of-existing-md-core-stack-to-a-newer-version-by-re#render-and-validate-helm)

Render against the existing PostgreSQL PVC and dry-run to ensure configuration is accepted:

helm lint metadefender-k8s/helm_charts/mdcore -f mdcore-minikube-values.yaml

Then run the template against the `Existing PostgreSQL PVC`:

helm template md-core metadefender-k8s/helm_charts/mdcore \
-n md-core \
-f mdcore-minikube-values.yaml \
--set-string core_components.postgres-core.storage_name=postgres-core-20260722195541-60761 > /tmp/mdcore-520-render.yaml

Dry-run the template and ensure the new variables are set in place:

kubectl apply --dry-run=client -f /tmp/mdcore-520-render.yaml

| **Item** | **Expected** |
| --- | --- |
| image | `opswat/metadefendercore-debian:5.20.0` |
| MDCORE_DB_NAME | `MDCORE_DB_NAME: "metadefender_core_5_20_0"` |
| UPGRADE_DB | `UPGRADE_DB: "false"` |
| MIGRATE_HISTORY | `MIGRATE_HISTORY: "false"` |
| claimName | `claimName: postgres-core-20260722195541-60761` |

## [**Finalize the the Helm Upgrade**](/docs/mdcore/v5.22.1/knowledge-base/-k8s--upgrade-of-existing-md-core-stack-to-a-newer-version-by-re#finalize-the-the-helm-upgrade)

**Delete the temporary migration pod** `md-core-520-prod-history-migration` **before starting the real deployments!**

**Remove the temporary migration pod:**

`kubectl delete pod md-core-520-prod-history-migration -n md-core --ignore-not-found --wait=true`

Upgrade the release while **explicitly keeping the current PostgreSQL PVC**:

helm upgrade --install md-core metadefender-k8s/helm_charts/mdcore \
--namespace md-core \
--history-max 2 \
-f mdcore-minikube-values.yaml \
--set-string core_components.postgres-core.storage_name=postgres-core-20260722195541-60761

Await the uptime on both Core deployments to confirm the success of the upgrade:

kubectl rollout status deploy/md-core-8088 -n md-core
kubectl rollout status deploy/md-core-8089 -n md-core
kubectl get pods -n md-core -o wide

Confirm active PostgreSQL sessions are using the migrated database:

PGPOD="$(kubectl get pod -n md-core -l app=postgres-core -o jsonpath='{.items[0].metadata.name}')"
kubectl exec -n md-core "$PGPOD" -- sh -c '
PGPASSWORD="$POSTGRES_PASSWORD" psql -U "$POSTGRES_USER" -d postgres -Atc "
select datname, count(*)
from pg_stat_activity
where datname like \$\$%metadefender_core\$\$
group by datname
order by datname;
"'

If everything has been set properly in place and there haven’t been no runtime error, the expected active database after upgrade should match: `metadefender_core_5_20_0`

## [**Rollback Sequence**](/docs/mdcore/v5.22.1/knowledge-base/-k8s--upgrade-of-existing-md-core-stack-to-a-newer-version-by-re#rollback-sequence)

**Data Divergence Warning:** Any scan requests, audit records, or processing history generated while `5.20.0` was live exist solely in `metadefender_core_5_20_0`. Rolling back by pointing back to `metadefender_core` will **not** merge post-upgrade records back to the source database.

Because the original `metadefender_core` database remains intact, and assuming no pruning occurred in earlier Helm revisions, you can run a `helm rollback`. There are two options to revert the changes.

Keep the old source database `metadefender_core` until you are certain that the new `5.20.0` version is correct and properly deployed - only then it can be advisable to consider the option of removing any traces of the old one through a PG DROP statement and then removing obsolete not-bound PVCs.

### [**Option 1: Change runtime values back to** `5.20.0 -> 5.19.0` **in the original configuration file**](/docs/mdcore/v5.22.1/knowledge-base/-k8s--upgrade-of-existing-md-core-stack-to-a-newer-version-by-re#option-1-change-runtime-values-back-to-5200---5190-in-the-original-configuration-file)

| **Configuration** | **Value / Details** |
| --- | --- |
| env | `MDCORE_DB_NAME: metadefender_core UPGRADE_DB: "false" MIGRATE_HISTORY: "false"` |
| core_components | `#[POD1]core_components: md-core-8088: image: opswat/metadefendercore-debian:5.19.0  initContainers: - name: check-db-ready image: opswat/metadefendercore-debian:5.19.0 #[POD2] core_components:  md-core-8089: image: opswat/metadefendercore-debian:5.19.0  initContainers: - name: check-db-ready image: opswat/metadefendercore-debian:5.19.0` |

For a normal rollback sequence, `MDCORE_DB_NAME` is the important variable. `MDCORE_UPGRADE_FROM_DB_NAME` matters only during an upgrade; reverting it to `metadefender_core_5_20_0` while rolling back can be misleading and dangerous if someone later sets `UPGRADE_DB=true`.

Since the original PVC would hold the information on both source and destination databases, you should keep it as it is - `postgres-core-20260722195541-60761`

Apply the re-adjustments through Helm:

helm upgrade --install md-core metadefender-k8s/helm_charts/mdcore \
--namespace md-core \
--history-max 2 \
-f mdcore-minikube-values.yaml \
--set-string core_components.postgres-core.storage_name=postgres-core-20260722195541-60761

Verify status:

kubectl rollout status deploy/md-core-8088 -n md-core
kubectl rollout status deploy/md-core-8089 -n md-core

Check if connections are on the original database:

PGPOD="$(kubectl get pod -n md-core -l app=postgres-core -o jsonpath='{.items[0].metadata.name}')"
kubectl exec -n md-core "$PGPOD" -- sh -c '
PGPASSWORD="$POSTGRES_PASSWORD" psql -U "$POSTGRES_USER" -d postgres -Atc "
select datname, count(*)
from pg_stat_activity
where datname like \$\$%metadefender_core\$\$
group by datname
order by datname;
"'

The rollback version `5.19.0` should point back to `metadefender_core`, not `metadefender_core_5_20_0`.

### [**Option 2: Use helm rollback if previous stable revision is present**](/docs/mdcore/v5.22.1/knowledge-base/-k8s--upgrade-of-existing-md-core-stack-to-a-newer-version-by-re#option-2-use-helm-rollback-if-previous-stable-revision-is-present)

Find the last good 5.19.0 revision, for example revision 24:

helm history md-core -n md-core

The `helm rollback` restores the old release values exactly - if that old revision already pointed to the `5.20.0` or to a different PVC, rollback would not return you to `5.19.0` safely, so kindly consider verifying that before running it.

Inspect what that revision would restore:

helm get values md-core -n md-core --revision 24 --all

Confirm that the revision points to:

 image: opswat/metadefendercore-debian:5.19.0
MDCORE_DB_NAME: metadefender_core
PVC: postgres-core-20260722195541-60761

Rollback through Helm:

helm rollback md-core 24 -n md-core --wait --timeout 15m

Verify pods and PG status:

 kubectl rollout status deploy/md-core-8088 -n md-core
kubectl rollout status deploy/md-core-8089 -n md-core
## [**References**](/docs/mdcore/v5.22.1/knowledge-base/-k8s--upgrade-of-existing-md-core-stack-to-a-newer-version-by-re#references)

| **Reference** | **Link** |
| --- | --- |
| OPSWAT MD Core Kubernetes upgrade documentation | <https://www.opswat.com/docs/mdcore/container-deployment/upgrade-metadefender-core-version-on-k8s> |
| OPSWAT MD Core Docker image documentation | <https://www.opswat.com/docs/mdcore/container-deployment/docker-image-published-on-opswat-docker-hub> |

**Support:**

If **further assistance** is required, please log a [**support case or chat with our support engineer**](https://my.opswat.com/support).
