<!-- source: https://www.opswat.com/docs/mdcore/container-deployment/deployment-strategies-kubernetes -->

# Deploying on K8S

Using Kubernetes technology provides us with some features that distinct it from other type of deployments. These are the main features:

- **Service discovery and load balancing.** See [Installing MetaDefender Core in K8S](/docs/mdcore/container-deployment/metadefender-core-in-your-already-created-k8s)
- **Storage orchestration.** Allows you to automatically mount a storage system. See [Storage Configuration on K8S](/docs/mdcore/container-deployment/storage-configuration-on-k8s)
- **Automated rollouts and rollbacks.** See [Upgrade/Deployment Strategy on K8S](/docs/mdcore/container-deployment/upgrade-metadefender-core-version-on-k8s)
- **Automatic bin packing.** You tell Kubernetes how much CPU and memory (RAM) each container needs.
- **Self-healing.** Kubernetes restarts containers that fail, replaces containers, kills containers that don't respond to your user-defined health check, and doesn't advertise them to clients until they are ready to serve. Se **Kubernetes Probes** explained below
- **Secret and configuration management.** Kubernetes lets you store and manage sensitive information. See [Kubernetes Components](/docs/mdcore/container-deployment/kubernetes-components)
- **Horizontal scaling.** Scale your application up and down. See [Scaling K8S Cluster](/docs/mdcore/container-deployment/scaling-k8s-cluster)

There are recommended configuration for each of the features to use by default when deploying MetaDefender Core in a Kubernetes cluster.

### [Kubernetes Probes](/docs/mdcore/container-deployment/deployment-strategies-kubernetes#kubernetes-probes)

The Kubernetes probes are needed to control the correct behavior of the application on this environment. Each probe need to use the health check endpoint [GET - Get health check status](/docs/mdcore/metadefender-core#healthcheck) (/readyz)

- **Readiness Probe** ( Check /readyz endpoint to know if the Health Check is OK )

  - `initialDelaySeconds`= 60
  - `periodSeconds` = 10
  - `successThreshold` = 1
  - `timeoutSeconds` = 10
- **Liveness Probe** ( Check /readyz endpoint to know if the Health Check is OK after Pod is ready)

  - `initialDelaySeconds`= 90
  - `timeoutSeconds` = 10
  - `periodSeconds` = 10
  - `failureThreshold`= 3
