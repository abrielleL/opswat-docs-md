<!-- source: https://www.opswat.com/docs/mdss/installation/openshift-considerations -->

# OpenShift Considerations

## [Introduction](/docs/mdss/installation/openshift-considerations#introduction)

This guide explains how to deploy MetaDefender Storage Security (MDSS) on OpenShift using Helm with the required OpenShift-specific configuration.

## [Prerequisites](/docs/mdss/installation/openshift-considerations#prerequisites)

- Access to OpenShift cluster with admin privileges
- Helm 3.x installed
- `oc` command-line tool configured
- Ability to grant privileged SCC permissions

## [Deployment Steps](/docs/mdss/installation/openshift-considerations#deployment-steps)

### [1. Login to OpenShift](/docs/mdss/installation/openshift-considerations#1-login-to-openshift)

BashCopyoc login --token=<your_token> --server=<cluster_url>
### [2. Create Project](/docs/mdss/installation/openshift-considerations#2-create-project)

BashCopyoc new-project mdss
### [3. Create Service Account and Grant Permissions](/docs/mdss/installation/openshift-considerations#3-create-service-account-and-grant-permissions)

The MDSS components require privileged access to function properly on OpenShift:

BashCopy# Create a service account for MDSS
oc create sa mdss -n mdss
# Grant privileged security context constraints to the service account
oc adm policy add-scc-to-user privileged -z mdss -n mdss

**Important:** The privileged SCC is necessary because several MDSS components require elevated permissions.

### [4. Add Helm Repository](/docs/mdss/installation/openshift-considerations#4-add-helm-repository)

BashCopyhelm repo add mdk8s <https://opswat.github.io/metadefender-k8s/>
helm repo update mdk8s
### [5. Prepare OpenShift Values File](/docs/mdss/installation/openshift-considerations#5-prepare-openshift-values-file)

Create a file named `mdss-openshift.yml` with the OpenShift-specific configuration:

BashCopy# Download the OpenShift values file directly from GitHub # Run this command to fetch the file:
curl -O <https://raw.githubusercontent.com/OPSWAT/metadefender-k8s/refs/heads/main/helm_charts/mdss-openshift.yml
### [6. Deploy the MDSS Helm Chart](/docs/mdss/installation/openshift-considerations#6-deploy-the-mdss-helm-chart)

BashCopyhelm install mdss mdk8s/metadefender_storage_security -f mdss-openshift.yml

**Note:** The OpenShift values file configures the SecurityContext to run as user 0 (root), assigns the mdss service account to pods, and adjusts command arguments for compatibility.

### [7. Verify Deployment](/docs/mdss/installation/openshift-considerations#7-verify-deployment)

BashCopyoc get pods -n mdss
oc get services -n mdss

Wait until all pods are in Running state. This may take a few minutes as containers initialize.

## [Post-Deployment Configuration](/docs/mdss/installation/openshift-considerations#post-deployment-configuration)

### [Access MDSS Console](/docs/mdss/installation/openshift-considerations#access-mdss-console)

BashCopy# Create a route to access the MDSS web interface
oc expose svc/webclient -n mdss
# Get the route URL
oc get route webclient -n mdss

Access the web interface using the hostname provided by the route.

## [Maintenance](/docs/mdss/installation/openshift-considerations#maintenance)

### [Upgrading MDSS](/docs/mdss/installation/openshift-considerations#upgrading-mdss)

BashCopyhelm repo update mdk8s helm upgrade mdss mdk8s/metadefender_storage_security -f mdss-openshift.yml
### [Uninstalling MDSS](/docs/mdss/installation/openshift-considerations#uninstalling-mdss)

BashCopyhelm uninstall mdss oc delete project mdss
