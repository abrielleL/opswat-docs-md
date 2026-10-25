<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/installation/upgrade-strategy-on-k8s -->

# Upgrade Strategy on K8S

View as Markdown Ask ChatGPT about this page Ask Claude about this page

For upgrading MetaDefender ICAP Server the container of the application contains the automation to upgrade the database schema and migrate the configuration data. The strategy recommended to use is

- Rolling Update ( Easy deployment where functionality test with new version is based on Kubernetes Probes )

As indicated in , the Kubernetes probes like Readiness and Liveness probes help the application to control the expected behavior, not to have a downtime, when doing an upgrade.

## [Rolling Update Strategy](/docs/mdicap/v5.15.0/installation/upgrade-strategy-on-k8s#rolling-update-strategy)

When using the Rolling Update strategy provided by Kubernetes technology, these are the main points to consider

- Traffic wont be sent to new pods until readiness probe is successful
- Old version pods won’t be terminated until new version pods are ready to serve traffic
- Rolling Update is the default strategy for deployment

### [Step by step using kubectl](/docs/mdicap/v5.15.0/installation/upgrade-strategy-on-k8s#step-by-step-using-kubectl)

- Set new image version on the MetaDefender ICAP Server deployment

BashCopykubectl set image -n <namespace> deployments/md_icapsrv icap_components.md_icapsrv.image=opswat/metadefendericapsrv-debian:<NEW_IMAGE_TAG>
#### [Step by step using helm](/docs/mdicap/v5.15.0/installation/upgrade-strategy-on-k8s#step-by-step-using-helm)

- Set new image version in values.yaml helm file

values.yamlCopyicap_components:
md_icapsrv:
image: opswat/metadefendercore-debian:<NEW_IMAGE_TAG>

- Run helm upgrade command with the environment variables desired if not indicated in values.yaml file when first deployment

BashCopyhelm upgrade md-icapsrv <chart> -n <namespace>
#### [Rollout Failed Update](/docs/mdicap/v5.15.0/installation/upgrade-strategy-on-k8s#rollout-failed-update)

Info

MetaDefender ICAP run the upgrade over the same database. So to rollout it is needed to change the database using the backup created before upgrading. Once the database contains the previous version the deployment can be rollout
