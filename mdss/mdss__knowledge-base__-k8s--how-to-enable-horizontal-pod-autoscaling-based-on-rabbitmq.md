<!-- source: https://www.opswat.com/docs/mdss/knowledge-base/-k8s--how-to-enable-horizontal-pod-autoscaling-based-on-rabbitmq -->

# [K8s] How to enable Horizontal Pod Autoscaling based on RabbitMQ queue metrics

This guide explains how to scale the MDSS processing services (Scanning, Discovery and Remediations) with the number of messages waiting in RabbitMQ, so the number of pods grows when a backlog builds up and shrinks when the work is done.

CPU is a poor signal for these services: they spend most of their time waiting on the storages and on MetaDefender Core, so a large backlog can build up while CPU usage stays low. The services exchange work through RabbitMQ queues, which makes the queue length the direct measure of pending work.

Two ways to do it are described here:

| Option | Best for | Effort |
| ---- | ---- | ---- |
| **A. KEDA** (recommended) | Any cluster where KEDA can be installed. Built into the MDSS Helm chart. | Install KEDA, then set `keda.enabled: true`. No Prometheus needed. |
| **B. Prometheus + Prometheus Adapter** | Clusters that already run Prometheus and cannot run KEDA. | Manual setup of scraping, adapter rules and an HPA per service. |

> **Info**
>
> This documentation provides a general implementation approach that will need to be adapted to your specific environment. The exact commands, configurations, and values presented here should be reviewed and modified according to your organization's specific Kubernetes infrastructure, network architecture, and operational requirements.

> **Warning**
>
> Use one autoscaling mechanism per service. Two autoscalers on the same Deployment fight each other. When KEDA is enabled the chart skips the CPU based HPA (`hpa.enabled`) for the services KEDA manages, and a manually created HPA (Option B) must not target a service that KEDA manages.

## Prerequisites

- Kubernetes cluster with HPA support (Kubernetes 1.23 or higher for `autoscaling/v2`)
- MDSS deployed with the Helm chart (the KEDA integration is available from chart version 4.6.0)
- The RabbitMQ instance used by MDSS (in-cluster or external) must be reachable from the cluster
- Option A (KEDA):
  - [KEDA](https://keda.sh) installed in the cluster (on OpenShift: the *Custom Metrics Autoscaler* operator from OperatorHub)
  - KEDA must be able to reach RabbitMQ over AMQP (port 5672). The RabbitMQ management plugin and the Prometheus plugin are **not** required
- Option B (Prometheus):
  - If using an external RabbitMQ instance: version 3.8.0 or higher, the RabbitMQ Prometheus plugin enabled, port 15692 accessible for metrics scraping and the management interface available
  - Basic understanding of Kubernetes and Prometheus

## Option A: Autoscaling with KEDA

### Step 1. Install KEDA (if not already deployed)

```bash
helm repo add kedacore https://kedacore.github.io/charts
helm repo update
helm install keda kedacore/keda --namespace keda --create-namespace
```

Check that the operator is running and the CRDs are registered:

```bash
kubectl get pods -n keda
kubectl get crd scaledobjects.keda.sh triggerauthentications.keda.sh
```

On OpenShift, install the *Custom Metrics Autoscaler* operator from OperatorHub and create its `KedaController` instance instead.

### Step 2. Enable KEDA in the MDSS Helm values

Add the following to your values file (or pass the same keys with `--set`):

```yaml
keda:
  enabled: true
  minReplicaCount: 1
  maxReplicaCount: 5
  queueLength: 100      # target number of ready messages per replica, evaluated per queue
  cooldownPeriod: 300   # seconds to wait before scaling back to minReplicaCount
  behavior: {}          # optional autoscaling/v2 behavior block for the HPA KEDA creates
```

Then install or upgrade the release:

```bash
helm upgrade --install mdss <path-to-mdss-chart> --namespace <namespace> --reuse-values -f keda-values.yaml
```

The chart creates, in the release namespace:

- one `ScaledObject` for each service that has queues configured (`scanningservice`, `discoveryservice`, `remediationsservice`),
- one `TriggerAuthentication` (`mdss-rabbitmq`),
- one Secret (`mdss-keda-rabbitmq`) with the AMQP connection string, built from `RABBITMQ_HOST`, `RABBITMQ_PORT`, `RABBITMQ_DEFAULT_USER` and `RABBITMQ_DEFAULT_PASS`.

To use your own Secret instead, create one containing the full `amqp://user:password@host:5672/` URI under the key `host` and set `keda.existingSecret` to its name. An external RabbitMQ needs no other change, as long as `RABBITMQ_HOST` points to it.

A service managed by KEDA is created without a fixed `replicas` value, so a later `helm upgrade` does not reset the replica count chosen by the autoscaler.

### Step 3. Which queues are monitored

Every work queue exists in three priorities (`_High`, `_Medium`, `_Low`). Each one is a separate trigger, and the service is scaled to whatever the busiest queue requires.

| Service | Queues (each with `_High`, `_Medium`, `_Low`) |
| ---- | ---- |
| scanningservice | `scanning.object_ready_for_scan.v2_queue`, `object_ready_for_scan_queue`, `object_scan_instance_result_queue` |
| discoveryservice | `start_discovery_queue`, `request_object_download_queue`, `event_based_discovery_queue`, `folder_discovery_queue` |
| remediationsservice | `object_scanned_queue`, `object_not_scanned_queue` |

### Step 4. Verify

```bash
kubectl get scaledobject
kubectl get hpa
kubectl describe scaledobject scanningservice
```

Each `ScaledObject` should report `READY=True`. KEDA creates and manages an HPA for it, named `keda-hpa-<service>` (for example `keda-hpa-scanningservice`).

To see the queue depth that drives the scaling:

```bash
kubectl exec deploy/rabbitmq -- rabbitmqctl list_queues name messages consumers
```

### Step 5. Tune the scaling

Every setting can be overridden per service, which is also how you change the thresholds for a single service:

```yaml
mdss_components:
  scanningservice:
    keda:
      maxReplicaCount: 10
      queueLength: 200
```

- `queueLength` is the number of ready messages one replica is expected to handle, evaluated for each queue separately. A lower value scales up earlier.
- `minReplicaCount` / `maxReplicaCount` bound the number of pods.
- `cooldownPeriod` is how long the queues must stay empty before the service scales back to `minReplicaCount`. Scale-down between those limits follows the standard HPA stabilization window; use `behavior` to change it.

> **Info**
>
> Scanning throughput is ultimately bound by the MetaDefender Core instances behind it. Scaling the Scanning service beyond what Core can absorb only moves the backlog, so scale MetaDefender Core as well (see the MetaDefender Core Helm chart).

### Scaling behavior with KEDA

- When the number of ready messages in any monitored queue exceeds `queueLength` per replica, KEDA scales the service up, up to `maxReplicaCount`.
- When the queues drain, the HPA scales the service down gradually; after `cooldownPeriod` seconds with empty queues it returns to `minReplicaCount`.

### Troubleshooting KEDA

1. `kubectl describe scaledobject <service>` shows the conditions and events. A `READY=False` status usually means KEDA cannot reach RabbitMQ.
2. Check the KEDA operator logs: `kubectl logs -n keda -l app=keda-operator`
3. The AMQP connection string is stored in the `mdss-keda-rabbitmq` Secret (key `host`). KEDA runs in its own namespace, so a short in-cluster host such as `rabbitmq` is qualified automatically with the release namespace; use a fully qualified host name for an external broker.
4. If the service does not scale, compare `queueLength` with the real queue depth (`rabbitmqctl list_queues`).

## Option B: Autoscaling with Prometheus and the Prometheus Adapter

Use this option when KEDA is not available. It scales the Scanning service on the total number of messages in its scan queues, using a manually created HPA. Set `hpa.enabled: false` for the service in the Helm values (it is disabled by default) so the chart does not create a CPU based HPA for the same Deployment, and do not enable `keda` for it.

### Step 1. Install Prometheus (if not already deployed)

If Prometheus is not already deployed in your cluster, install it using Helm:

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm install prometheus prometheus-community/prometheus --namespace default
```

### Step 2. Configure Prometheus to Scrape RabbitMQ Metrics

Add the following scrape configuration to your Prometheus ConfigMap to collect metrics from RabbitMQ:

```yaml
- job_name: rabbitmq
  kubernetes_sd_configs:
  - role: service
    namespaces:
      names:
        - default
  relabel_configs:
  - action: keep
    source_labels: [__meta_kubernetes_service_name]
    regex: rabbitmq
  - action: keep
    source_labels: [__meta_kubernetes_service_port_name]
    regex: 15692
  - action: labelmap
    regex: __meta_kubernetes_service_label_(.+)
  - source_labels: [__meta_kubernetes_namespace]
    target_label: kubernetes_namespace
  - source_labels: [__meta_kubernetes_service_name]
    target_label: kubernetes_service_name
  metrics_path: /metrics
```

Apply the updated ConfigMap and restart Prometheus to apply the changes.

> **Info**
>
> **Note for External RabbitMQ**: If using an external RabbitMQ instance, you'll need to modify the scrape configuration to target your external instance instead of using Kubernetes service discovery.

### Step 3. Install Prometheus Adapter (if not already deployed)

The Prometheus Adapter is required to expose Prometheus metrics to the Kubernetes metrics API:

> **Info**
>
> Please update `prometheus.url` and `prometheus.port` according to your environment

```bash
helm install adapter prometheus-community/prometheus-adapter \
  --set prometheus.url=http://prometheus-server.default.svc \
  --set prometheus.port=80
```

### Step 4. Configure Prometheus Adapter

Update the Prometheus Adapter ConfigMap to expose the RabbitMQ queue metric:

```yaml
data:
  config.yaml: |
    rules:
    - seriesQuery: '{__name__="rabbitmq_queue_messages_ready",kubernetes_namespace!=""}'
      seriesFilters: []
      resources:
        overrides:
          kubernetes_namespace: {resource: "namespace"}
      name:
        matches: "rabbitmq_queue_messages_ready"
        as: "rabbitmq_scan_queue_messages"
      metricsQuery: sum(rabbitmq_queue_messages_ready{queue=~"(scanning\\.object_ready_for_scan\\.v2_queue|object_ready_for_scan_queue)_(Low|Medium|High)"}) by (<<.GroupBy>>)
```

This configuration:

- Queries metrics with name "rabbitmq_queue_messages_ready"
- Associates metrics with Kubernetes namespaces
- Renames the metric to "rabbitmq_scan_queue_messages"
- Filters for the scan queues (both the `scanning.object_ready_for_scan.v2_queue` and `object_ready_for_scan_queue` queues) with Low, Medium, and High priorities
- Sums the total number of messages across these queues

After modifying the ConfigMap, restart the adapter:

```bash
kubectl rollout restart deployment adapter-prometheus-adapter
```

### Step 5. Verify the Custom Metric

Check that the metric is properly exposed to the Kubernetes API:

```bash
kubectl get --raw /apis/custom.metrics.k8s.io/v1beta1/ | jq
```

You should see "rabbitmq_scan_queue_messages" listed in the output.

```bash
$ kubectl get --raw /apis/custom.metrics.k8s.io/v1beta1/ | jq
{
  "kind": "APIResourceList",
  "apiVersion": "v1",
  "groupVersion": "custom.metrics.k8s.io/v1beta1",
  "resources": [
    {
      "name": "namespaces/rabbitmq_scan_queue_messages",
      "singularName": "",
      "namespaced": false,
      "kind": "MetricValueList",
      "verbs": [
        "get"
      ]
    }
  ]
}
```

To get the metric value:

```bash
$ kubectl get --raw /apis/custom.metrics.k8s.io/v1beta1/namespaces/default/metrics/rabbitmq_scan_queue_messages | jq
```

You should see the actual value of the queue size:

```bash
$ kubectl get --raw /apis/custom.metrics.k8s.io/v1beta1/namespaces/default/metrics/rabbitmq_scan_queue_messages | jq
{
  "kind": "MetricValueList",
  "apiVersion": "custom.metrics.k8s.io/v1beta1",
  "metadata": {},
  "items": [
    {
      "describedObject": {
        "kind": "Namespace",
        "name": "default",
        "apiVersion": "/v1"
      },
      "metricName": "rabbitmq_scan_queue_messages",
      "timestamp": "2025-03-28T11:37:19Z",
      "value": "4994",
      "selector": null
    }
  ]
}
```

### Step 6. Create a Horizontal Pod Autoscaler

Create an HPA resource that uses the custom metric to scale the Scanning service:

```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: scanningservice-hpa
  namespace: default  # Change if your deployment is in a different namespace
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: scanningservice
  minReplicas: 1  # Minimum number of pods
  maxReplicas: 10  # Maximum number of pods
  metrics:
  - type: Object
    object:
      metric:
        name: rabbitmq_scan_queue_messages
      describedObject:
        apiVersion: v1
        kind: Namespace
        name: default  # Or the namespace where your RabbitMQ is running
      target:
        type: Value
        value: 5000  # Total ready messages that trigger scale-up; tune it to your workload
```

Apply the HPA:

```bash
$ kubectl apply -f scanningservice-hpa.yaml
```

### Step 7. Monitor the HPA

Check the status of your HPA:

```bash
kubectl get hpa scanningservice-hpa
kubectl describe hpa scanningservice-hpa
```

## Scaling Behavior (Option B)

- When the total number of messages in the scan queues exceeds the configured target (5000 in the example), the HPA scales up the number of scanning pods, up to the maximum of 10.
- When the number of messages decreases, the HPA will gradually scale down the number of pods.

## Troubleshooting (Option B)

If the HPA isn't working as expected:

1. Verify Prometheus is collecting RabbitMQ metrics:

```bash
kubectl port-forward svc/prometheus-server 9090:80
```

Then visit [http://localhost:9090](http://localhost:9090/) and query:

`rabbitmq_queue_messages_ready{queue=~"(scanning\\.object_ready_for_scan\\.v2_queue|object_ready_for_scan_queue)_(Low|Medium|High)"}`

2. Check that the Prometheus Adapter can access the metrics:

```bash
kubectl logs -l app.kubernetes.io/name=prometheus-adapter
```

3. Verify the custom metric is available:

```bash
kubectl get --raw /apis/custom.metrics.k8s.io/v1beta1/namespaces/default/metrics/rabbitmq_scan_queue_messages
```

4. Ensure the HPA is targeting the correct deployment and namespace.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
