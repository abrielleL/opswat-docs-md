<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/container-deployment/troubleshooting -->

# Troubleshooting

To perform load testing, we recommend using the Gatling tool which you can find on <https://github.com/OPSWAT>

## [How to check the logs with Kubectl](/docs/mdcore/v5.22.0/container-deployment/troubleshooting#how-to-check-the-logs-with-kubectl)

- We can check the logs of the different containers running for the MetaDefender Core pod.

  - For init container "check-db" run `kubectl logs [-n <namespace> ] <pod-name> -c check-db-ready`
  - For app container "md-core" run `kubectl logs [-n <namespace> ] <pod-name>` (No container needed to be indicated)
- To describe the pod and see all the configurations of it.

  - `kubectl describe [ -n <namespace> ] <pod-name>`

## [How to collect logs generating a support package](/docs/mdcore/v5.22.0/container-deployment/troubleshooting#how-to-collect-logs-generating-a-support-package)

For generating and exporting the logs we need to run the following commands

kubectlCopy# Generate support package, it will log the support package name at the last line (<sp_file_name>)
kubectl exec <mdcore_pod_name> -n <namespace> -- bash -c "cd /opt/ometascan/core_data/var/lib/ometascan && /opt/ometascan/usr/bin/ometascan-collect-support-data.sh"
#export support package, replace <namespace>, <mdcore_pod_name> & <sp_file_name>
kubectl cp -n <namespace> <mdcore_pod_name>:opt/ometascan/core_data/var/lib/ometascan/<sp_file_name>.tar.gz <sp_file_name>.tar.gz
## [Installation Script is failing](/docs/mdcore/v5.22.0/container-deployment/troubleshooting#installation-script-is-failing)

- Follow pre-install requirements in [Installing MetaDefender Core in K8S](/docs/mdcore/v5.22.0/container-deployment/metadefender-core-in-your-already-created-k8s)
- Message Error "INSTALLATION FAILED: found in Chart.yaml, but missing in charts/ directory: aws-load-balancer-controller".

  - Run `helm dependency update`

## [Nginx Ingress Issues](/docs/mdcore/v5.22.0/container-deployment/troubleshooting#nginx-ingress-issues)

Problems found:

1. Tls is not enabled for ingress
2. Controller is not picking up the changes of the services

### [**TLS not enabled**](/docs/mdcore/v5.22.0/container-deployment/troubleshooting#tls-not-enabled)

***How to debug***

- Check ingress rule deployed and name of the tls secret that contains the certificate and key

***Solution Proposed***

- Create tls secret if not created and add the secret name matching the tls secret created. See [TLS configuration](https://docs.opswat.com/mdcore/kubernetes-configuration/metadefender-core-in-your-already-created-k8s#tls-configuration)

### [**Ingress Controller not picking up the changes**](/docs/mdcore/v5.22.0/container-deployment/troubleshooting#ingress-controller-not-picking-up-the-changes)

***How to debug***

- Check the logs of the ingress controller pod. Search for any error or warning that could point to the root cause

***Solution Proposed***

- If error is not clear try to find in the ingress controller user guide to review the configuration.

## [Errors Connecting to Database](/docs/mdcore/v5.22.0/container-deployment/troubleshooting#errors-connecting-to-database)

Problems found

1. MetaDefender Core cannot connect to database
2. PostgreSQL extenstion is not installed

### [**Cannot connect to database**](/docs/mdcore/v5.22.0/container-deployment/troubleshooting#cannot-connect-to-database)

***How to debug***

- MetaDefender Core init container is not finishing. Check logs of check-db init container to see if the database if reachable.
- If MetaDefender Core init container is terminated means that the database could be reached with the configuration provided. In this case it is needed to check the MetaDefender Core app container and search for 'connection error'

***Solutions Proposed***

- Check **DB_HOST** in ***mdcore-env*** configmap
- Check user and password values in ***mdcore-postgres-cred*** secret

### [**PostgreSQL extension not installed**](/docs/mdcore/v5.22.0/container-deployment/troubleshooting#postgresql-extension-not-installed)

***How to debug***

- Check logs of MetaDefender Core pod and search for éxtension missing' message.

***Solutions Proposed***

- There are some extensions that are needed to be installed, sometimes they are installed by the admin user that MetaDefender Core use for connecting to the database but other times there are some database services in the CSPs that does not allow this kind of actions and the extensions have to be installed from the CSP console.

## [Error Activating MetaDefender Core license](/docs/mdcore/v5.22.0/container-deployment/troubleshooting#error-activating-metadefender-core-license)

**Problems found**

1. MetaDefender Core pod does not get activated

### [**MetaDefender Core does not get activated**](/docs/mdcore/v5.22.0/container-deployment/troubleshooting#metadefender-core-does-not-get-activated)

***How to debug***

- MetaDefender Core pod is restarting as it does not get activated because of the livenessprobe is failing. By default the health check endpoint /readyz is checking if the pod is activated, so if this fails the pod will get restarted.
- It is needed to review the MetaDefender Core pod logs to see what is the specific error, it could be things like

  - Not enough activations left
  - Activation Key expired

***Solutions Proposed***

1. Each activation key has a number of slots/Core that can be activated and generate a deployment id, if your reach the limit could be because either any of the deployments was not deactivated properly or because you need to get more Core licensed in your activation key

   1. Check the sidecar container *activation-manager* logs to see if there is any error on deactivation
   2. Contact support if there is any error in the logs, or you need to extend the number of slots/Core
2. In case it is saying that the activation key is expired, please contact Sales to extend your license

## [Activate license key failed even though the import zip config file was successful](/docs/mdcore/v5.22.0/container-deployment/troubleshooting#activate-license-key-failed-even-though-the-import-zip-config-file-was-successful)

**Problems found**

1. Discrepancy between the **APIKEY** environment variable on K8S and the **API key** stored in the zip config file

### [Discrepancy between APIKEYs](/docs/mdcore/v5.22.0/container-deployment/troubleshooting#discrepancy-between-apikeys)

**How to Debug**

- Check if the API Key is protected (Feature available from version 5.9.0, For more details see [link](https://docs.opswat.com/mdcore/v5.9.0/release-notes/release-notes))

**Solution Proposed**

- Case 1: If user does not enable **API key protection**

  - Step 1: Remove the current helm chart and re-deploy it again with the correct APIKEY env var (**plain text** **API key** stored in the zip config file)
- Case 2: If user enabled **API key protection** and user does not remember **plain text** **API key**

  - Step 1: Ignore Health Checks (livenessProbe, readinessProbe) for md-core deployment via kubectl command

BashCopykubectl patch deployment md-core --type json -p='[{"op": "remove", "path": "/spec/template/spec/containers/0/livenessProbe"}]'
kubectl patch deployment md-core --type json -p='[{"op": "remove", "path": "/spec/template/spec/containers/0/readinessProbe"}]'

- Step 2: Login to the Core UI, adjust settings that users want (workflow, user, other settings, etc), then generate a **new apikey** and export **new zip config file** - Step 3: Copy the **new zip config file** from the client to the NFS share folder - Step 4: Re-deploy helm chart again with correct APIKEY environment variable (newly generated API key in the Core UI) - Step 5: Restart K8S md-core deployment via kubectl command

BashCopykubectl rollout restart deploy md-core
## [MetaDefender Core Engines Errors](/docs/mdcore/v5.22.0/container-deployment/troubleshooting#metadefender-core-engines-errors)

**Problems found**

1. Engines does not get activated

### [**Engines does not get activated**](/docs/mdcore/v5.22.0/container-deployment/troubleshooting#engines-does-not-get-activated)

***How to debug***

- Check, in the MetaDefender Core console, the configuration under Inventory > Modules > Metascan. There would be an error indicating that the engines are failing to be activated or installed.
- Check the logs of the MetaDefender Core pod and search for errors when installing the engines. "Waiting for init message timeout, no response from engine"

***Solutions Proposed***

- Review the resources allocated to the MetaDefender Core pod. The limit resources settings in K8S must meet the recommended system in the documentation (for more details: [link](https://docs.opswat.com/mdcore/installation))

## [IKARUS engine](/docs/mdcore/v5.22.0/container-deployment/troubleshooting#ikarus-engine)

For IKARUS, `--shm-size=1gb` should be added when starting the docker.

If you're using K8S, the section below should be also specified in the yaml file:

YamlCopyspec:
volumes:
- name: dshm
emptyDir:
medium: Memory
containers:
- volumeMounts:
- mountPath: /dev/shm
name: dshm
## [Xcitium engine](/docs/mdcore/v5.22.0/container-deployment/troubleshooting#xcitium-engine)

For Xcitium, `--shm-size=300m` should be added when starting the docker.

If you're using K8S, the section below should be also specified in the yaml file:

YamlCopyspec:
volumes:
- name: dshm
emptyDir:
medium: Memory
containers:
- volumeMounts:
- mountPath: /dev/shm
name: dshmNotice

If you are using both IKARUS and Xcitium, please use `--shm-size=1300m` to satisfy the requirements of both engines.
