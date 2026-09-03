<!-- source: https://www.opswat.com/docs/mdss/4.4.2/integrations/configuring-error-handling-and-retry-mechanisms-for-sharepoint-o -->

# Configuring Error Handling and Retry Mechanisms for SharePoint On-Premise

This guide is for administrators and users managing the MetaDefender Storage Security integration with SharePoint On-Prem. It details crucial environment variables that control error handling, request retries, connection management, and batch processing. Properly tuning these settings is essential for maximizing your deployment's performance and reliability. Fine-tuning helps prevent SharePoint server throttling, which can occur under heavy load, ensuring smoother operations and minimizing disruptions.

## [Key Configuration Settings (Environment Variables)](/docs/mdss/4.4.2/integrations/configuring-error-handling-and-retry-mechanisms-for-sharepoint-o#key-configuration-settings-environment-variables)

Below are the environment variables you can configure to optimize communication with your SharePoint On-Prem server.

**SHAREPOINT_ON_PREM_MAX_CONNECTIONS** sets the maximum number of simultaneous connections to SharePoint On-Prem that can be held in the connection pool. Requests exceeding this limit will wait for an existing connection to become available.

Impact

- Higher Value

  - Can lead to faster processing of requests to the same site and better performance during high-demand periods by allowing more concurrent operations.
  - Increases the risk of hitting the SharePoint server's own simultaneous connection limits, potentially causing throttling, slower responses, and service disruptions.
- Lower Value

  - Enhances connection reusability, leading to more reliable and stable request management.
  - May reduce processing speed, as fewer simultaneous connections can lead to longer wait times for requests, especially during peak usage.
- Default is set to 5 maximum connections for every pool
- Units measured in number of connections

`SHAREPOINT`*ON* `PREM_MAX_QUERY_RETRIES` controls how many times a failed SharePoint On-Prem query will be automatically retried. Retries use an exponential backoff strategy (increasing delays between attempts) to avoid overwhelming a struggling server

Impact

- Higher Value

  - Increases the chance of a query succeeding during temporary server issues.
  - Can lead to longer overall operation times if failures are frequent or persistent.
- Lower Value

  - Reduces time spent retrying, leading to quicker finalization of operations (either success or failure)
  - May result in a higher rate of failed operations if transient issues are common, as the system gives up sooner.
- Default is set to 5 retries per query
- Configurable Range goes from 0 to 8 (MetaDefender Storage Security enforces a hard upper limit of 8 retries)
- Units measured in number of retries

**SHAREPOINT_ON_PREM_CIRCUIT_BREAKER_THRESHOLD** defines the number of consecutive connection failures to SharePoint that must occur before the circuit breaker "opens." Once open, connection attempts are temporarily halted to prevent overwhelming an unhealthy SharePoint server.

Impact

- Higher Value

  - Makes the system more tolerant of repeated transient issues before halting requests
  - Risks overwhelming an unhealthy SharePoint server for a longer duration, potentially worsening performance issues and recovery times.
- Lower Value

  - Reacts more quickly to potential SharePoint server issues, helping to prevent server overload and allowing for faster recovery.
  - May lead to more frequent (though temporary) interruptions in service if transient issues are common.
- Default is set to 5 consecutive failed requests
- Units measured in number of failures

**SHAREPOINT_ON_PREM_CIRCUIT_BREAKER_DURATION_SECS** specifies how long (in seconds) the circuit breaker remains open after tripping. During this "cooldown" period, all requests to SharePoint are automatically rejected. After the duration, the circuit enters a "half-open" state to test if the SharePoint server has recovered.

Impact

- Higher Value

  - Provides a longer recovery window for a significantly troubled SharePoint server before new connection attempts are made
  - Results in a longer period of unavailability for users trying to access SharePoint resources.
- Lower Value

  - Reduces downtime by attempting to reconnect to SharePoint sooner.
  - Risks repeatedly tripping the circuit breaker if the server hasn't fully recovered, potentially increasing load on an unstable server.
- Default is set to 30 seconds

**SHAREPOINT_``MAX``_CONCURRENT_REQUESTS** controls the maximum number of SharePoint requests that MetaDefender Storage Security will process simultaneously. This helps prevent overwhelming the SharePoint server.

Impact

- Higher Value

  - Allows more requests to be processed at once, potentially improving throughput and performance during high demand.
  - Increases the risk of overwhelming the SharePoint server, which can lead to throttling or degraded performance.
- Lower Value

  - Helps prevent server overload and ensures more stable performance, especially during peak usage.
  - May result in slower overall processing times and longer wait times for users, as requests are queued.
- Default is set to 5 concurrent requests
- Units: Number of concurrent requests

`SHAREPOINT_BATCH_SIZE` specifies the maximum number of SharePoint requests to be processed in a single batch operation. Batching optimizes performance by reducing round-trips but needs to be balanced against server resource capacity

Impact

- Higher Value

  - Can improve efficiency and performance by processing more requests in each interaction with SharePoint.
  - Larger batches consume more resources and increase the risk of overwhelming the SharePoint server, potentially leading to throttling.
- Lower Value

  - Helps maintain stability and prevent resource saturation on the SharePoint server.
  - May lead to increased overall processing times due to a higher number of smaller batch operations.
- Default is set to 10 requests per batch.

**SHAREPOINT_BATCH_INTERVAL_MS** defines the time interval in milliseconds between the processing of SharePoint request batches. This determines how frequently the system checks for and processes queued requests.

Impact

- Higher Value

  - Reduces the frequency of batch processing, which can lessen the load on the SharePoint server, especially during peak times.
  - May lead to increased wait times for users as requests are queued for longer before being processed.
- Lower Value

  - Improves responsiveness and user experience by processing queued requests more frequently.
  - Increases the load on the SharePoint server due to more frequent processing cycles, potentially leading to resource saturation or throttling if the interval is too short.
- Default is set to 1000 milliseconds (1 second)
