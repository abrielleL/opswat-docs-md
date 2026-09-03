<!-- source: https://www.opswat.com/docs/mdcluster/container-deployment/kubernetes-components -->

# Kubernetes components

This page describes what the `mdcluster` chart creates and how configuration is shared between them.

## [**Workloads**](/docs/mdcluster/container-deployment/kubernetes-components#workloads)

| Product component | Kubernetes object | Workload | Service and port |
| --- | --- | --- | --- |
| MetaDefender Cluster Control Center | `control-center` | Deployment, always 1 | `NodePort` by default · `8892` |
| MetaDefender Cluster Identity Service | `identity-service` | Deployment, always 1 | `ClusterIP` · `8891` |
| MetaDefender Cluster File Storage | `file-storage` | StatefulSet | Headless · `8890` |
| MetaDefender Cluster Worker running MetaDefender Core | `ometascan` | StatefulSet | Shared headless `worker` · instance `8008` |
| MetaDefender Cluster Worker running the MetaDefender Cluster API Gateway | `api-gateway` | StatefulSet | Shared headless `worker`, plus its own `api-gateway` Service · instance `8899` |
| MetaDefender Cluster Worker running the MetaDefender Cluster Callback Service | `callback-service` | StatefulSet | Shared headless `worker` · instance `8894` |

## [**Architecture**](/docs/mdcluster/container-deployment/kubernetes-components#architecture)

## [**Shared configuration**](/docs/mdcluster/container-deployment/kubernetes-components#shared-configuration)

The chart creates two objects that the Control Center, Identity Service, File Storage and every worker pod mount as environment variables. (The bundled PostgreSQL, Redis and RabbitMQ pods do not get them; they read only the few credential values they need.)

| Object | Rendered from | Contains |
| --- | --- | --- |
| `mdcluster-config` ConfigMap | the `env:` block in your values file | Hostnames, ports, timeouts, file copy settings |
| `mdcluster-secrets` Secret | the `secrets:` block in your values file | Passwords, connection keys, the encryption key, the license key |

Those seven pods pull in both objects wholesale with `envFrom`, so adding a key to `env:` or `secrets:` makes it visible to all of them without touching any template.

The bundled infrastructure works differently. None of the three mounts either object; each pod is given only the individual keys it needs, by reference:

| Pod | Reads from the Secret |
| --- | --- |
| `postgres` | `CONTROL_CENTER_DB_USER`, `CONTROL_CENTER_DB_PASSWORD` — which is why those two also bootstrap its superuser |
| `rabbitmq` | `RABBITMQ_USER`, `RABBITMQ_PASSWORD` |
| `redis` | Nothing. The bundled Redis runs without authentication; `REDIS_USER` / `REDIS_PASSWORD` exist for pointing at an **external** Redis that requires it |
