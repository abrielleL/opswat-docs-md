<!-- source: https://www.opswat.com/docs/mdss/4.4.2/knowledge-base/why-is-rabbitmq-consuming-excessive-memory-in-metadefender-secur -->

# Why is RabbitMQ consuming excessive memory in MetaDefender Secure Storage (MDSS) Kubernetes deployment?

This article applies to **MetaDefender Storage Security (MDSS)** deployment on **Kubernetes** environment.

### [Overview](/docs/mdss/4.4.2/knowledge-base/why-is-rabbitmq-consuming-excessive-memory-in-metadefender-secur#overview)

This article addresses a specific memory exhaustion issue affecting RabbitMQ components within MetaDefender Secure Storage (MDSS) Kubernetes deployments. It details the symptoms of the memory leak and provides a configuration change to the Helm Chart to permanently resolve the instability.

### [Issue](/docs/mdss/4.4.2/knowledge-base/why-is-rabbitmq-consuming-excessive-memory-in-metadefender-secur#issue)

RabbitMQ v4.1.0 instances might experience continuous memory growth (memory leaks). This is specifically caused by the improper cleanup of "deleted consumer metrics" within the `rabbitmq:4.1.0-management-alpine` container image.

**Symptoms include:**

- Steadily climbing RAM usage without release.
- High resource consumption attributed to the Management Plugin.
- Potential Out of Memory (OOM) crashes or pod restarts.

### [Solution](/docs/mdss/4.4.2/knowledge-base/why-is-rabbitmq-consuming-excessive-memory-in-metadefender-secur#solution)

To resolve this, you will need to switch the container image to the standard Alpine version, which excludes the Management Plugin.

1. Modify the Configuration

Open the `values.yaml` file used for your MDSS deployment.

**2. Update the Image Tag**

Locate the RabbitMQ image section and remove the `-management` suffix.

**3. Change From:**

`image: rabbitmq:4.1.0-management-alpine`

**Change To:**

`image: rabbitmq:4.1.0-alpine`

**4. Apply the Changes**

Execute the Helm upgrade command to apply the new configuration:

`helm upgrade <release-name> ./<chart-path> -f values.yaml -n <namespace>`

**5. Monitor**

Verify the pod is running the new image and monitor memory usage over the next 24 hours to confirm stability.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
