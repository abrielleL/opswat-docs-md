<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/installation/replication---ha-on-k8s -->

# Replication & HA on K8S

When installing MetaDefender ICAP Server in Kubernetes as this technology provide the system with its self-healing feature, it might not be strictly necessary to set it up with at least 2 replicas for each of the pods in case of wanting to have **High Availability,** but it is always a best practice to have 2 replicas of each pod running in different worker nodes. For those components that could not be running within the cluster, we will provide different solutions that are supported by our application.

**3rd Party components**

- `Database` -> Deploy an external service for PostgreSQL with HA or PostgreSQL operator running on K8S cluster

## [HA solutions for PostgreSQL](/docs/mdicap/v5.14.1/installation/replication---ha-on-k8s#ha-solutions-for-postgresql)

For CSPs provided service it has been tested and is supported by the following:

- [Amazon RDS](https://aws.amazon.com/rds/)
- [Azure Database for PostgreSQL](https://azure.microsoft.com/en-us/products/postgresql)
- [Google Cloud SQL](https://cloud.google.com/sql?_gl=1*1aimsvg*_up*MQ..&gclid=EAIaIQobChMI0tue6sSrkgMV3sl5BB3UFx1bEAAYASAAEgI1g_D_BwE&gclsrc=aw.ds&hl=en)

If a highly available database is required inside the k8s cluster, then there are publicly available solutions that can deploy a PostgreSQL Replica Set. For a k8s cluster, Zalando provides an operator for deploying a Replica Set: <https://github.com/zalando/postgres-operator/blob/master/docs/quickstart.md>

## [HA deployment](/docs/mdicap/v5.14.1/installation/replication---ha-on-k8s#ha-deployment)

MetaDefender ICAP Server container can be scaled depending on the availability and performance requirements.

YamlCopyicap_components:
md_icapsrv:
replicas: 1
## [Create environment with HA components](/docs/mdicap/v5.14.1/installation/replication---ha-on-k8s#create-environment-with-ha-components)

For deploying all the components that provide a high availability, OPSWAT have prepared a terraform module to deploy the cluster and the database service for each of the main CSPs

There are 2 ways of using that terraform module

- Applying changes directly using the [terraform project](https://github.com/OPSWAT/metadefender-k8s/tree/main/terraform/aws)
- Using the [metadefenderk8s.sh](https://github.com/OPSWAT/metadefender-k8s/tree/main) to deploy MetaDefender ICAP and MetaDefender Core with it.

## [Automatic replicas using horizontal pod autoscaling (HPA)](/docs/mdicap/v5.14.1/installation/replication---ha-on-k8s#automatic-replicas-using-horizontal-pod-autoscaling-hpa)

The HPA can be enabled from the values:

YamlCopyautoscaling:
enabled: false
minReplicas: 1
maxReplicas: 10
# Can be scaled based on the resource usage of the pods in the scaling target
metrics:
- type: Resource
resource:
name: cpu
target:
type: Utilization
averageUtilization: 60
- type: Resource
resource:
name: memory
target:
type: Utilization
averageUtilization: 60
behavior:
scaleDown:
stabilizationWindowSeconds: 300
policies:
- type: Percent
value: 100
periodSeconds: 15
selectPolicy: Max
scaleUp:
stabilizationWindowSeconds: 60
policies:
- type: Percent
value: 100
periodSeconds: 15
- type: Pods
value: 4
periodSeconds: 15
selectPolicy: Max

In the example above the number of replicas are adjusted within the specified limits depending on the measured CPU usage. For a more granular autoscaling it's needed to manually create a HPA separately from the helm deployment.
