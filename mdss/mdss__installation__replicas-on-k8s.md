<!-- source: https://www.opswat.com/docs/mdss/installation/replicas-on-k8s -->

# Replication & High Availability on K8S

When installing MetaDefender Storage Security in Kubernetes as this technology provide the system with its self-healing feature, it might not be strictly necessary to set it up with at least 2 replicas for each of the pods in case of wanting to have **High Availability,** but it is always a best practice to have 2 replicas of each pod running in different worker nodes. For those components that could not be running within the cluster, we will provide different solutions that are supported by our application.

However, there are a few components that may incur in high load in some situations, so for those components it is recommended to have more than 1 replica. These components are the following.

**MDSS services**

- `Web Client` -> to provide high availability to outside requests
- `API Gateway` -> to provide high availability to outside requests
- `Scanning Service` -> to provide high availability when having to handle big number of files to scan

**3rd Party components**

- `Database` -> Deploy an external service for PostgreSQL with HA or PostgreSQL operator running on K8S cluster
- `RabbitMQ` -> Use external service for RabbitMQ with HA
- `Redis Cache` -> Use external service for Redis cache with HA

## [HA solutions for PostgreSQL](/docs/mdss/installation/replicas-on-k8s#ha-solutions-for-postgresql)

For CSPs provided service it has been tested and is supported by the following:

- [Amazon RDS](https://aws.amazon.com/rds/)
- [Azure Database for PostgreSQL](https://azure.microsoft.com/en-us/products/postgresql)

If a highly available database is required inside the k8s cluster, then there are publicly available solutions that can deploy a PostgreSQL Replica Set. For a k8s cluster, Zalando provides an operator for deploying a Replica Set: <https://github.com/zalando/postgres-operator/blob/master/docs/quickstart.md>

## [HA Solution for Redis Cache](/docs/mdss/installation/replicas-on-k8s#ha-solution-for-redis-cache)

OPSWAT have tested the following services to provided HA to a redis service.

- [AWS ElasticCache for Redis](https://docs.aws.amazon.com/es_es/AmazonElastiCache/latest/red-ug/GettingStarted.html)
- [Azure Cache for Redis](https://azure.microsoft.com/es-es/products/cache#overview)

## [HA Solution for RabbitMQ](/docs/mdss/installation/replicas-on-k8s#ha-solution-for-rabbitmq)

OPSWAT have tested the following services to provided high availability to a RabbitMQ service.

- [Amazon MQ for RabbitMQ](https://docs.aws.amazon.com/amazon-mq/latest/developer-guide/working-with-rabbitmq.html)
- [Bitnami package for RabbitMQ in Azure MP](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/bitnami.rabbitmq?tab=overview)

#### [RabbitMQ Cluster Operator](/docs/mdss/installation/replicas-on-k8s#rabbitmq-cluster-operator)

1. Install Cert-Manager (required for operator webhooks)

BashCopykubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.13.3/cert-manager.yaml

2. Install RabbitMQ Cluster Operator:

You can download the file using this link: [RabbitMQ Cluster Operator](https://github.com/rabbitmq/cluster-operator/releases)

BashCopykubectl apply -f <path-to-cluster-operator.yml>

3. Install RabbitMQ Messaging Topology Operator:

You can download the file using this link: [RabbitMQ Messaging Topology Operator](https://github.com/rabbitmq/messaging-topology-operator/releases)

BashCopykubectl apply -f <path-to-messaging-topology-operator-with-certmanager.yaml>

Update your Helm values to enable the operator:

YamlCopyrabbitmq-cluster-operator:
enabled: true
replicas: 3
resources:
requests:
cpu: "250m"
memory: "512Mi"

The operator will automatically create a 3-node RabbitMQ cluster with quorum-based HA. During node failures, the cluster continues operating and services automatically reconnect to healthy nodes.

## [HA deployment for MDSS](/docs/mdss/installation/replicas-on-k8s#ha-deployment-for-mdss)

MDSS containers can be scaled independently depending on the availability and performance requirements. For example, just the `webclient`and `apigateway` pods can be replicated to provide high availability to outside requests and for the web interface.

YamlCopymdss_components:
webclient:
replicas: 3
apigateway:
replicas: 3

The `mongomigrations`service is used to migrate the data from older versions of MDSS at startup if required and provides no benefits if replicated .

## [Create environment with HA components](/docs/mdss/installation/replicas-on-k8s#create-environment-with-ha-components)

For deploying all the components that provide a high availability, OPSWAT have prepared a terraform module to deploy all the 3rd parties applications (Redis, RabbitMQ & PostgreSQL DB).

There are 2 ways of using that terraform module

- Applying changes directly using the [terraform project](https://github.com/OPSWAT/metadefender-k8s/tree/main/terraform/aws)
- Using the [metadefenderk8s.sh](https://github.com/OPSWAT/metadefender-k8s/tree/main) to deploy MDSS with it.

## [Automatic replicas using horizontal pod autoscaling (HPA)](/docs/mdss/installation/replicas-on-k8s#automatic-replicas-using-horizontal-pod-autoscaling-hpa)

The HPA can be enabled on all MDSS services from the values:

YamlCopyhpa:
enabled: true
minReplicas: 2
maxReplicas: 3
cpuTargetUtilization: 85

In the example above the number of replicas are adjusted within the specified limits depending on the measured CPU usage. The HPA is applied for all MDSS services, for a more granular autoscaling it's recommended to manually create a HPA separately from the helm deployment just for the desired services.
