<!-- source: https://www.opswat.com/docs/mdss/4.5.2/knowledge-base/-k8s--how-to-enable-horizontal-pod-autoscaling-based-on-rabbitmq -->

# [K8s] How to enable Horizontal Pod Autoscaling based on RabbitMQ queue metrics

This guide outlines the process of setting up Horizontal Pod Autoscaling (HPA) for the Scanning service based on RabbitMQ queue size metrics. This configuration automatically scales the number of scanning pods up or down in response to the number of messages in the scan queue.

> **Info**
>
> This documentation provides a general implementation approach that will need to be adapted to your specific environment. The exact commands, configurations, and values presented here should be reviewed and modified according to your organization's specific Kubernetes infrastructure, network architecture, and operational requirements.

## Prerequisites

- Kubernetes cluster with HPA support
- If using an external RabbitMQ instance:
  - RabbitMQ version 3.8.0 or higher
  - RabbitMQ Prometheus plugin must be enabled
  - Port 15692 must be accessible for metrics scraping
  - The RabbitMQ management interface must be available
- Basic understanding of Kubernetes and Prometheus

## 1. Install Prometheus (if not already deployed)

If Prometheus is not already deployed in your cluster, install it using Helm:`

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm install prometheus prometheus-community/prometheus --namespace default
```

## 2. Configure Prometheus to Scrape RabbitMQ Metrics

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

## 3. Install Prometheus Adapter (if not already deployed)

The Prometheus Adapter is required to expose Prometheus metrics to the Kubernetes metrics API:

> **Info**
>
> Please update `prometheus.url` and `prometheus.port` according to your environment

```bash
helm install adapter prometheus-community/prometheus-adapter \
  --set prometheus.url=http://prometheus-server.default.svc \
  --set prometheus.port=80
```

## 4. Configure Prometheus Adapter

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
      metricsQuery: sum(rabbitmq_queue_messages_ready{queue=~"object_ready_for_scan_queue_(Low|Medium|High)"}) by (<<.GroupBy>>)
```

This configuration:

- Queries metrics with name "rabbitmq_queue_messages_ready"
- Associates metrics with Kubernetes namespaces
- Renames the metric to "rabbitmq_scan_queue_messages"
- Filters for scan queues with Low, Medium, and High priorities
- Sums the total number of messages across these queues

After modifying the ConfigMap, restart the adapter:

```bash
kubectl rollout restart deployment adapter-prometheus-adapter
```

## 5. Verify the Custom Metric

Check that the metric is properly exposed to the Kubernetes API:

```bash
kubectl get --raw /apis/custom.metrics.k8s.io/v1beta1/ | jq
```

You should see "rabbitmq_scan_ queue_messages" listed in the output.

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

## 6. Create a Horizontal Pod Autoscaler

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
        value: 5000  # 5000 is the maximum number of messages in the queue set by default in MDSS
```

Apply the HPA:

```bash
$ kubectl apply -f scanningservice-hpa.yaml
```

## 7. Monitor the HPA

Check the status of your HPA:

```bash
kubectl get hpa scanningservice-hpa
kubectl describe hpa scanningservice-hpa
```

## Scaling Behavior

- When the total number of messages in the scan queues exceeds 5000, the HPA will scale up the number of scanning pods (up to the maximum of 10).
- When the number of messages decreases, the HPA will gradually scale down the number of pods.

## Troubleshooting

If the HPA isn't working as expected:

1. Verify Prometheus is collecting RabbitMQ metrics:

```bash
kubectl port-forward svc/prometheus-server 9090:80
```

Then visit [http://localhost:9090](http://localhost:9090/) and query:

`rabbitmq_queue_messages_ready{queue=~"object_ready_for_scan_queue_(Low|Medium|High)"}`

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
