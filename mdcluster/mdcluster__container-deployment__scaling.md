<!-- source: https://www.opswat.com/docs/mdcluster/container-deployment/scaling -->

# Scaling

Two kinds of scaling apply to MetaDefender Cluster, and they work very differently.

**MetaDefender Cluster Workers** scale freely and without downtime. They register themselves with the MetaDefender Cluster Control Center on start and unregister on stop, so adding or removing replicas needs no coordination.

**MetaDefender Cluster File Storage** does not. The MetaDefender Cluster Control Center is given its list of MetaDefender Cluster File Storage endpoints at chart render time, so changing the replica count requires a `helm upgrade` — and a planned downtime window.

MetaDefender Cluster Control Center and MetaDefender Cluster Identity Service are singletons and cannot be scaled.

## [MetaDefender Cluster Workers](/docs/mdcluster/container-deployment/scaling#metadefender-cluster-workers)

Scale each instance type independently, according to which resource is the bottleneck: `ometascan` for scan throughput, `api-gateway` for file submission capacity, `callback-service` for webhook delivery.

helm upgrade mdcluster ./mdcluster --reuse-values \
--set workers.ometascan.replicas=5 \
--set workers.api-gateway.replicas=3 \
--set workers.callback-service.replicas=3
## [MetaDefender Cluster File Storage](/docs/mdcluster/container-deployment/scaling#metadefender-cluster-file-storage)

**Never scale MetaDefender Cluster File Storage in.** Files are distributed across the instances, not copied to all of them, so removing a replica removes the MetaDefender Cluster Control Center's only route to every file that lived there. With the default `FILE_STORAGE_MAX_REPLICA: 1` each file has exactly one copy, so scaling in loses access to a share of your stored files immediately — and the MetaDefender Cluster Control Center reports nothing wrong.

Scaling **out** is safe, but offline: it needs a maintenance window with all MetaDefender Cluster Worker pods stopped. Size MetaDefender Cluster File Storage at install time so you do not need either operation.

Scaling MetaDefender Cluster File Storage requires **downtime**.

### [Procedure](/docs/mdcluster/container-deployment/scaling#procedure)

1. **Scale all MetaDefender Cluster Worker instances to zero.** MetaDefender Cluster File Storage cannot be reconfigured while MetaDefender Cluster workers are running.

   helm upgrade mdcluster ./mdcluster --reuse-values \
   --set workers.ometascan.replicas=0 \
   --set workers.api-gateway.replicas=0 \
   --set workers.callback-service.replicas=0
   # Wait for every worker pod to finish draining
2. **Scale MetaDefender Cluster File Storage:**

   helm upgrade mdcluster ./mdcluster --reuse-values \
   --set file-storage.replicas=5 \
   --set env.FILE_STORAGE_MIN_REPLICA=2 \
   --set env.FILE_STORAGE_MAX_REPLICA=2
3. **Scale instance again:**

   helm upgrade mdcluster ./mdcluster --reuse-values \
   --set workers.ometascan.replicas=5 \
   --set workers.api-gateway.replicas=3 \
   --set workers.callback-service.replicas=3

Finally, confirm on the **Services** page of the console that every MetaDefender Cluster File Storage replica is listed and healthy.

Two settings control how many copies of each file are stored - see [Configuration](/docs/mdcluster/container-deployment/high-availability#configuration).
