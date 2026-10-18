<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/how-do-i-recover-metadefender-core-pods-failing-with-http-403--- -->

# How do I recover MetaDefender Core pods failing with HTTP 403 “Access denied” because of an API key mismatch?

View as Markdown Ask ChatGPT about this page Ask Claude about this page
### [**Check your version**](/docs/mdcore/knowledge-base/how-do-i-recover-metadefender-core-pods-failing-with-http-403---#check-your-version)

This article applies to MetaDefender Core deployed on Kubernetes using the `mdcore-api-key` Secret. Before proceeding, confirm that your deployment uses this Secret and that the pod logs show repeated HTTP 403 “Access denied” errors as described below.

# [**When to use this**](/docs/mdcore/knowledge-base/how-do-i-recover-metadefender-core-pods-failing-with-http-403---#when-to-use-this)

Use this KB when:

- MetaDefender Core is deployed on Kubernetes and the pods were previously running normally.
- The issue started after a recent change, such as an upgrade, restore, redeployment, Secret rotation, Helm/GitOps sync, or database/PVC reuse.
- Pod logs show repeated `403 Access denied` errors.
- You want to recover the existing deployment safely without recreating MetaDefender Core, PostgreSQL, or persistent volumes.

Common log messages include:

- `Warning: Setup proxy failed. Response (403): {"err":"Access denied"}`
- `Warning: License activation failed. Response (403): {"err":"Access denied"}`
- `Info: The license failed to deactivate via the Core service (403): {"err":"Access denied"}`

The proxy warning appears only if a proxy is configured.

# [**What this means**](/docs/mdcore/knowledge-base/how-do-i-recover-metadefender-core-pods-failing-with-http-403---#what-this-means)

This usually means the API key inside Kubernetes does not match the API key stored in the MetaDefender Core database.

In short:

- The pod starts with the API key from the `mdcore-api-key` Secret.
- MetaDefender Core checks that key against the key stored in its database.
- If they do not match, Core returns HTTP 403.
- The pod may fail health checks and restart before you can fix it.

# [**Quick recovery steps**](/docs/mdcore/knowledge-base/how-do-i-recover-metadefender-core-pods-failing-with-http-403---#quick-recovery-steps)

1. Confirm the pod logs show `403 Access denied`.
2. Temporarily remove only the `livenessProbe` and `startupProbe` so the pod stays running while you repair it. Save each probe definition before removing it so you can add the probes back later.
3. Port-forward to the pod and log in to the MetaDefender Core web interface.
4. Choose one of the two repair options:

   - **Option A:** First read the API key value from the Kubernetes `mdcore-api-key` Secret. Then go to the MDCore web console and update the administrator API key there to match the Secret value.
   - **Option B:** If Option A does not work, log in to the MDCore web console, create a new API key there, then patch the Kubernetes Secret with the new key.
5. After completing Option A or Option B, run the non-interactive `kubectl exec` verification command to confirm the right API key now exists in the database.
6. If verification succeeds, restart the rollout and wait for the pods to come online.
7. If Option A verification fails, use Option B, verify again, restart the rollout, confirm the pods are healthy, add the probes back, and restart the deployment if required.

# [**Step-by-step**](/docs/mdcore/knowledge-base/how-do-i-recover-metadefender-core-pods-failing-with-http-403---#step-by-step)

## [**1. Confirm the error**](/docs/mdcore/knowledge-base/how-do-i-recover-metadefender-core-pods-failing-with-http-403---#1-confirm-the-error)

Check pod status:

kubectl get pods -n <namespace>

Check logs:

kubectl logs -n <namespace> deployment/md-core --since=30m

If you see repeated `Response (403): {"err":"Access denied"}`, continue with this procedure.

If the logs show connection refused, DNS, timeout, or PostgreSQL authentication errors instead, this KB is not the right fix.

## [**2. Temporarily disable restart probes**](/docs/mdcore/knowledge-base/how-do-i-recover-metadefender-core-pods-failing-with-http-403---#2-temporarily-disable-restart-probes)

Save only the current probe definitions, then remove the probes temporarily. This avoids restoring a stale full Deployment manifest later.

kubectl get deployment md-core -n <namespace> -o jsonpath='{.spec.template.spec.containers[0].livenessProbe}' > liveness.json
kubectl get deployment md-core -n <namespace> -o jsonpath='{.spec.template.spec.containers[0].startupProbe}' > startup.json

Then remove only the `livenessProbe` and `startupProbe` manually. The liveness probe can restart the pod, and removing the startup probe gives you time to complete the repair before Kubernetes starts enforcing the liveness check.

Check that both probes are defined before you remove them. If either output is empty, do not run the corresponding remove command.

kubectl get deployment md-core -n <namespace> -o jsonpath='{.spec.template.spec.containers[0].livenessProbe}{"\n"}{.spec.template.spec.containers[0].startupProbe}{"\n"}'
kubectl patch deployment md-core -n <namespace> --type=json -p='[{"op":"remove","path":"/spec/template/spec/containers/0/livenessProbe"}]'
kubectl patch deployment md-core -n <namespace> --type=json -p='[{"op":"remove","path":"/spec/template/spec/containers/0/startupProbe"}]'

Wait for the rollout:

kubectl rollout status deployment/md-core -n <namespace>

Only leave the probes disabled long enough to recover the deployment. Re-enable them after the Secret is fixed.

## [**3. Connect to the pod**](/docs/mdcore/knowledge-base/how-do-i-recover-metadefender-core-pods-failing-with-http-403---#3-connect-to-the-pod)

Find the new pod:

kubectl get pods -n <namespace>

Port-forward to it:

kubectl port-forward -n <namespace> pod/<mdcore-pod-name> 8008:8008

Then open one of these in your browser:

- `http://127.0.0.1:8008`
- `https://127.0.0.1:8008` if TLS is enabled

## [**4. Choose the repair option**](/docs/mdcore/knowledge-base/how-do-i-recover-metadefender-core-pods-failing-with-http-403---#4-choose-the-repair-option)

There are two repair options. Start with **Option A**: use the API key value that is already stored in Kubernetes and update MDCore to match it. Use **Option B** only if Option A does not work.

### [**Option A: Update MDCore with the API key from the Kubernetes Secret**](/docs/mdcore/knowledge-base/how-do-i-recover-metadefender-core-pods-failing-with-http-403---#option-a-update-mdcore-with-the-api-key-from-the-kubernetes-secret)

Use this option first. The goal is to take the API key value currently stored in the Kubernetes Secret and update the MDCore administrator API key in the web console so MDCore and Kubernetes match. If this verification fails because the Kubernetes Secret contains an invalid API key, continue with Option B.

1. Get the current API key value from the Kubernetes `mdcore-api-key` Secret.
2. Log in to the MetaDefender Core web interface with an administrator account.
3. Go to **User management** → **Users**, open the administrator user, and update the API key so it matches the value from the Kubernetes Secret. MetaDefender Core API keys are 36 characters long.
4. Log in to the MDCore pod and verify the API key with `curl` using the command below.
5. If the `curl` verification returns `200`, continue to Step 5.

# Get the current API key from the mdcore-api-key Secret first.
MDCORE_API_KEY="$(kubectl get secret mdcore-api-key -n <namespace> -o jsonpath='{.data.value}' | base64 -d)"
printf 'Kubernetes Secret API key: %s\n' "${MDCORE_API_KEY}"
# Find the MDCore pod and verify the key with a non-interactive exec.
MDCORE_POD=$(kubectl get pod -n <namespace> -l app=md-core -o jsonpath='{.items[0].metadata.name}')
kubectl exec -n <namespace> "$MDCORE_POD" -- \
curl -s -o /dev/null -w '%{http_code}\n' -H "apikey: $MDCORE_API_KEY" http://localhost:8008/stat/nodes

Expected result: `200`. If the command returns `200`, continue to Step 5. If it returns `403` or another failure because the Secret value is invalid, use Option B to create a new MDCore API key and patch the Kubernetes Secret.

### [**Option B: Create a new MDCore API key and patch the Kubernetes Secret**](/docs/mdcore/knowledge-base/how-do-i-recover-metadefender-core-pods-failing-with-http-403---#option-b-create-a-new-mdcore-api-key-and-patch-the-kubernetes-secret)

Use this option only if Option A does not work. In this path, create a new API key in the MDCore web console, then update Kubernetes so the Secret contains the same new key.

1. Log in to the MetaDefender Core web interface with an administrator account.
2. Go to **User management** → **Users**, open the administrator user, and generate or reset the API key.
3. Copy the new 36-character API key.
4. Patch the existing `mdcore-api-key` Kubernetes Secret with the new key.
5. Log in to the MDCore pod and verify the API key with `curl` using the command below.
6. If the `curl` verification returns `200`, continue to Step 5.

read -rsp "New MetaDefender Core API key: " MDCORE_API_KEY
echo
MDCORE_API_KEY_B64="$(printf '%s' "${MDCORE_API_KEY}" | base64 | tr -d '\n')"
kubectl patch secret mdcore-api-key -n <namespace> --type=merge -p "{\"data\":{\"value\":\"${MDCORE_API_KEY_B64}\"}}"
# Find the MDCore pod and verify the key with a non-interactive exec.
MDCORE_POD=$(kubectl get pod -n <namespace> -l app=md-core -o jsonpath='{.items[0].metadata.name}')
kubectl exec -n <namespace> "$MDCORE_POD" -- \
curl -s -o /dev/null -w '%{http_code}\n' -H "apikey: $MDCORE_API_KEY" http://localhost:8008/stat/nodes

Expected result: `200`. If the command returns `200`, continue to Step 5.

Do not paste API keys into tickets, screenshots, or shared notes. Base64 is not encryption.

If the `mdcore-cred` Secret was rotated too, UI login may also fail. Fix administrator login first, then continue with the API key repair.

After completing Option A or Option B, test the `curl` command internally from the MDCore pod. This verifies that the right API key now exists in the database. If the request returns the expected successful response, proceed with restoring the Deployment, restarting the rollout, waiting for pods to come online, and re-enabling health checks.

## [**5. Restart the pod so it reads the repaired key**](/docs/mdcore/knowledge-base/how-do-i-recover-metadefender-core-pods-failing-with-http-403---#5-restart-the-pod-so-it-reads-the-repaired-key)

After completing Option A or Option B, restart the deployment so the pod reads the updated Secret:

kubectl rollout restart deployment/md-core -n <namespace>
kubectl rollout status deployment/md-core -n <namespace>

If your environment is managed by Argo CD, Flux, or an external secret manager, make sure the same valid API key is also updated in the source of truth. Otherwise the managed value may be put back automatically.

## [**6. Restore the original probes**](/docs/mdcore/knowledge-base/how-do-i-recover-metadefender-core-pods-failing-with-http-403---#6-restore-the-original-probes)

Add the saved probe definitions back to the Deployment. Do not use `kubectl rollout undo` here: the restart in Step 5 creates a new revision, so undo would roll back only to the probe-less revision instead of the original probe configuration.

Run:

kubectl patch deployment md-core -n <namespace> --type=json \
-p="[{\"op\":\"add\",\"path\":\"/spec/template/spec/containers/0/livenessProbe\",\"value\":$(cat liveness.json)}]"
kubectl patch deployment md-core -n <namespace> --type=json \
-p="[{\"op\":\"add\",\"path\":\"/spec/template/spec/containers/0/startupProbe\",\"value\":$(cat startup.json)}]"
kubectl rollout status deployment/md-core -n <namespace>

**Support:**

If you need further assistance, please contact OPSWAT Support through the [OPSWAT Portal](https://my.opswat.com/) or your assigned support representative.
