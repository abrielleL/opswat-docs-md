<!-- source: https://www.opswat.com/docs/mdcluster/container-deployment/upgrade -->

# Upgrade

MetaDefender Cluster upgrades are Helm upgrades. A `helm upgrade` covers the core services and the workers together — or, by pinning individual `version` keys, one component at a time.

## [**Step 1 — Clone the new version**](/docs/mdcluster/container-deployment/upgrade#step-1--clone-the-new-version)

# Clone new
git clone https://github.com/OPSWAT/metadefender-k8s.git metadefender
# Or pull
git pull -r
cd metadefender/helm_charts/mdcluster
## [**Step 2 — Upgrade**](/docs/mdcluster/container-deployment/upgrade#step-2--upgrade)

**Option 1: Upgrade everything**

helm upgrade mdcluster ./mdcluster --reuse-values \
--set MDCLS_VERSION=<new_version>

**Option 2: Upgrade one component**

# component = control-center | file-storage | identity-service
helm upgrade mdcluster ./mdcluster --reuse-values \
--set <component>.version=<new_version># instance_type = ometascan | api-gateway | callback-service
helm upgrade mdcluster ./mdcluster --reuse-values \
--set workers.<instance_type>.version=<new_version>
