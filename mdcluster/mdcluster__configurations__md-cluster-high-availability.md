<!-- source: https://www.opswat.com/docs/mdcluster/configurations/md-cluster-high-availability -->

# High Availability

## [Overview](/docs/mdcluster/configurations/md-cluster-high-availability#overview)

In MetaDefender Cluster (MD Cluster), critical components for its continuous operation include RabbitMQ, Redis, Postgres, and MD Cluster File Storage. Any disruption of these components will lead to an interruption in the scanning processes and result in a failed verdict for the processed files. To prevent the interruption, high-availability solutions must be implemented on the components.

A strategy for achieving high availability is the replication and redundancy of essential components. The key concept is that if a single component fails, the redundant system takes over seamlessly, avoiding any interruption in service. Following are guidelines to set up the high availability solution on individual components and apply them in MetaDefender Cluster.

- [High availability support for MD Cluster File Storage.](/docs/mdcluster/configurations/file-storage-ha)
- [High availability support for RabbitMQ.](/docs/mdcluster/configurations/rabbitmq-ha)
- [High availability support for Redis.](/docs/mdcluster/configurations/redis-ha)
- [High availability support for Data lake.](/docs/mdcluster/configurations/data-lake-ha)
