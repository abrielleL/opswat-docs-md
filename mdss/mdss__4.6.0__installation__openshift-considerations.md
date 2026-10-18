<!-- source: https://www.opswat.com/docs/mdss/4.6.0/installation/openshift-considerations -->

# OpenShift Considerations

## Introduction

This guide explains how to deploy MetaDefender Storage Security (MDSS) on OpenShift using Helm with the required OpenShift-specific configuration.

## Prerequisites

- Access to OpenShift cluster with admin privileges
- Helm 3.x installed
- `oc` command-line tool configured
- Ability to grant privileged SCC permissions

## Deployment Steps

### 1. Login to OpenShift

```bash
oc login --token=<your_token> --server=<cluster_url>
```

### 2. Create Project

```bash
oc new-project mdss
```

### 3. Create Service Account and Grant Permissions

The MDSS components require privileged access to function properly on OpenShift:

```bash
# Create a service account for MDSS
oc create sa mdss -n mdss

# Grant privileged security context constraints to the service account
oc adm policy add-scc-to-user privileged -z mdss -n mdss
```

**Important:** The privileged SCC is necessary because several MDSS components require elevated permissions.

### 4. Add Helm Repository

```bash
helm repo add mdk8s <https://opswat.github.io/metadefender-k8s/>
helm repo update mdk8s
```

### 5. Prepare OpenShift Values File

Create a file named `mdss-openshift.yml` with the OpenShift-specific configuration:

```bash
# Download the OpenShift values file directly from GitHub # Run this command to fetch the file:
curl -O <https://raw.githubusercontent.com/OPSWAT/metadefender-k8s/refs/heads/main/helm_charts/mdss-openshift.yml
```

### 6. Deploy the MDSS Helm Chart

```bash
helm install mdss mdk8s/metadefender_storage_security -f mdss-openshift.yml
```

**Note:** The OpenShift values file configures the SecurityContext to run as user 0 (root), assigns the mdss service account to pods, and adjusts command arguments for compatibility.

### 7. Verify Deployment

```bash
oc get pods -n mdss
oc get services -n mdss
```

Wait until all pods are in Running state. This may take a few minutes as containers initialize.

## Post-Deployment Configuration

### Access MDSS Console

```bash
# Create a route to access the MDSS web interface
oc expose svc/webclient -n mdss
# Get the route URL
oc get route webclient -n mdss
```

Access the web interface using the hostname provided by the route.

## Maintenance

### Upgrading MDSS

```bash
helm repo update mdk8s helm upgrade mdss mdk8s/metadefender_storage_security -f mdss-openshift.yml
```

### Uninstalling MDSS

```bash
helm uninstall mdss oc delete project mdss
```

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
