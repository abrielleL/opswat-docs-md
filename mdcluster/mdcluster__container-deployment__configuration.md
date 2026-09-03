<!-- source: https://www.opswat.com/docs/mdcluster/container-deployment/configuration -->

# Configuration

All configuration is supplied through Helm values. This page covers the settings most deployments touch. For the exhaustive list, read the chart's own defaults — every block carries an inline comment:

helm show values ./mdcluster

Only the keys you set are overridden; everything else falls back to the chart default. Put them in your `override-values.yaml` (see [Quick start](/docs/mdcluster/container-deployment/quick-start)) and apply with:

helm upgrade mdcluster ./mdcluster --install -f ./override-values.yaml
## [**Where to configure what**](/docs/mdcluster/container-deployment/configuration#where-to-configure-what)

| To configure | See |
| --- | --- |
| HTTPS for the MetaDefender Cluster Control Center or API Gateway | [Enable HTTPs](/docs/mdcluster/container-deployment/enable-https) |
| CPU, memory and ephemeral storage | [Resource requirements](/docs/mdcluster/container-deployment/resource-requirements) |
