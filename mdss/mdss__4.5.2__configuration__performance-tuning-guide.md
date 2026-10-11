<!-- source: https://www.opswat.com/docs/mdss/4.5.2/configuration/performance-tuning-guide -->

# Performance Tuning Guide

## About This Guide

This guide is designed to assist you in fine-tuning various configuration settings to achieve desired throughput and performance levels. By default, MetaDefender Storage Security operates in a balanced mode, optimizing both speed and functionality for maximum value. However, in scenarios where certain features may be unnecessary and system throughput is paramount, this guide will provide you with the necessary steps to adjust your settings for optimal performance outcomes.

## Scanning Performance

The throughput of the system largely depends on the speed of the scan instance. If you are using MetaDefender Cloud, our SaaS offering,  you are automatically benefiting from optimal performance. For users of MetaDefender Core, we recommend visiting the [MetaDefender Core Performance Tuning Guide](https://www.opswat.com/docs/mdcore/configuration/metadefender-core-performance-tuning-guide#performance-tuning)  to explore ways to reduce the response time of your scan instance.

### Increasing the number of concurrent file scans

A critical configuration parameter in MetaDefender Storage Security that significantly affects throughput is the number of concurrent scan requests sent to the scan instance. By default, the system processes 20 files simultaneously. As each file completes scanning, another is promptly queued. If your scan instance has additional capacity, we recommend gradually increasing this count to optimize throughput until you reach the desired performance level.

> **IMPORTANT**
>
> When adjusting the number of parallel scan requests, it's important to monitor the scan instance queue closely. An excessive number of messages in the queue indicates that the setting is too high, which can lead to performance degradation due to overloading the scan instance. Please adjust accordingly to maintain optimal performance.

To adjust this setting please modify the **`RABBITMQ_SCANNING_PREFETCH_COUNT`**environment variable as described in: [Custom Configuration | Increase the number of concurrent scans](https://www.opswat.com/docs/mdss/configuration/custom-configuration#increase-the-number-of-concurrent-scans).

## Discovery Performance

### Discovery Throttling

In scenarios where system load is exceptionally high, you may encounter a notification that discovery has been temporarily throttled. This measure halts the discovery of new files when the queue already contains a large volume of pending files. It is designed to optimize system resources and prevent excessive RAM usage. By setting this limit, we ensure efficient processing and reduce the risk of an endlessly growing queue, which can occur if the rate of file discovery exceeds the scanning capacity.

The threshold for maximum pending files is controlled by two environment variables:

- `DISCOVERY_THROTTLER_MAX_PENDING_FILES` , which defaults to 5000 for workflows with scanning
- `DISCOVERY_THROTTLER_NOT_SCANNED_MAX_PENDING_FILES` , which default to 50000 for discovery-only workflows

These values can be adjusted up or down based on your system's specifications to optimize memory usage.

When the system is throttled, it does not stop indefinitely -  it waits a moment, then checks whether it is ready to continue. Two settings let you control how long it keeps trying before moving on:

- `DISCOVERY_THROTTLER_MAX_RETRY_ATTEMPTS` - the number of times the system will check before resuming discovery. Defaults to `10`.
- `DISCOVERY_THROTTLER_MAX_DELAY_MINUTES` - the maximum wait time between each check, in minutes. Defaults to `10`.

You can raise these values if you want the system to wait longer during periods of high load, or lower them if you prefer it to resume sooner.

## Performance Mode

Several configuration options are available that can accelerate system performance while slightly reducing functionality. When certain features are not required, enabling **Performance Mode** can be an effective way to enhance speed.

To activate Performance Mode, modify the environment variable `PERFORMANCE_MODE`as outlined in [Custom configuration](https://www.opswat.com/docs/mdss/configuration/custom-configuration) and set the value to `PERFORMANCE_MODE=true` .

### Functionality Impacted with Performance Mode Activated

Before enabling Performance Mode, please review the table below, which details all areas that will be impacted. This information will help you make an informed decision about whether the trade-offs in functionality are acceptable for your needs.

| Functionality | Details |
| ---- | ---- |
| Amazon S3 | Tags are not being retrieved automatically for all files which means they are not available on the response of `/api/file/{fileId}` and `/api/file/{scanId}/{startIndex}/{count}` APIs. |
| Core max file size validation | The WorkflowRules Job which updates cache with the max file size configured on each Core Instance will not run, and files which are bigger than this limit will be sent for scanning and fail |

## Rabbitmq configuration

One of the key ways to adjust MetaDefender Storage Security performance is by changing default configuration of Rabbitmq. The following are three environment variables that can help increase performance

`RABBITMQ_CONSUMER_MULTIPLIER`

Controls how many RabbitMQ consumers are created per standard (non-RPC) subscribe queue. The value is applied per priority tier with built-in multipliers:

- Low = N
- Medium = N × 3
- High = N × 6

When to increase:

When a service's standard queues show growing message backlogs and the service has spare CPU headroom. Each additional consumer adds a concurrent message-processing goroutine per priority channel.

Recommended values (16 CPU / 32 GB RAM VM): 1–3.

Valid range: 1–10. Default: 1.

`RABBITMQ_RPC_CONSUMER_MULTIPLIER`

Controls how many RabbitMQ consumers are created per RPC (request/reply) subscribe queue. RPC consumers handle synchronous-style calls from the API Gateway and other services, so they typically need higher concurrency than fire-and-forget consumers.

Valid range: 1–50. Default: 10.

Recommended values (16 CPU / 32 GB RAM VM): 10–20.

When to increase:

When RPC calls time out under load due to all consumers being busy, not because of slow downstream processing. Check RabbitMQ management for consumer utilization on RPC queues before raising this

`RABBITMQ_CONNECTION_CONSUMER_CONCURRENCY`

Sets **ConsumerDispatchConcurrency** on the RabbitMQ connection, which controls the maximum number of messages the client dispatches concurrently to consume callbacks on a single connection. This is a connection-level cap — it limits the total in-flight message processing across ALL channels and consumers on the connection.

Default: 50.

When to increase:

When the service has many queues/consumers (especially after raising ConsumerMultiplier or RpcConsumerMultiplier) and you observe that throughput plateaus while CPU is not used at full capacity. A low concurrency cap starves consumers even when there are messages ready.

Recommended values (16 CPU / 32 GB RAM VM): 50–100.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
