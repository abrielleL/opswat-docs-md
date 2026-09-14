<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/how-to-limit-the-number-of-cpu-cores-used-for-scanning-in-metade -->

# How to Limit the Number of CPU Cores Used for Scanning in MetaDefender Core

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows or Linux systems.

In some environments, administrators may observe that **MetaDefender Core’s scanning processes consume 100% of CPU resources**, even when the number of concurrent scans is below 200. When CPU usage remains at maximum capacity, the **Core API may become unresponsive**, affecting health checks and subsequent file scanning requests.

This article explains how MetaDefender Core manages CPU utilization and provides **tuning recommendations** to maintain system responsiveness.

### [**Can CPU Usage Be Limited Directly?**](/docs/mdcore/knowledge-base/how-to-limit-the-number-of-cpu-cores-used-for-scanning-in-metade#can-cpu-usage-be-limited-directly)

Currently, **MetaDefender Core does not provide an option to directly limit CPU usage** for scanning processes. The scanning engines are designed to utilize available CPU resources as efficiently as possible, while CPU allocation is handled by the **operating system scheduler**.

That said, there are several tuning methods that can help reduce CPU contention and keep the API and queue management processes responsive.

### [**Recommended Tuning Methods**](/docs/mdcore/knowledge-base/how-to-limit-the-number-of-cpu-cores-used-for-scanning-in-metade#recommended-tuning-methods)

#### [**1. Adjust Scanning Concurrency**](/docs/mdcore/knowledge-base/how-to-limit-the-number-of-cpu-cores-used-for-scanning-in-metade#1-adjust-scanning-concurrency)

Modify the `parallelcount` parameter in the engine configuration to control how many threads each engine uses concurrently.

- Lower values reduce CPU load but may also lower scanning throughput.
- The optimal value depends on your system’s hardware and workload characteristics.

> **Example:** Decreasing `parallelcount` from 20 to 15 can significantly lower CPU utilization during high-load periods.

#### [**2. Reduce Workload Complexity**](/docs/mdcore/knowledge-base/how-to-limit-the-number-of-cpu-cores-used-for-scanning-in-metade#2-reduce-workload-complexity)

Simplify scan workloads to reduce CPU consumption:

- Limit **archive extraction depth**.
- Define **maximum file size limits** for scanning.
- Avoid enabling **deep archive scanning** unless absolutely necessary.

#### [**3. Optimize Infrastructure and Configuration**](/docs/mdcore/knowledge-base/how-to-limit-the-number-of-cpu-cores-used-for-scanning-in-metade#3-optimize-infrastructure-and-configuration)

Ensure MetaDefender Core runs on an optimized environment:

- Deploy on hardware with **sufficient CPU cores and memory** beyond the baseline recommendation.
- Enable **high-performance power profiles** and verify that all CPU cores are active.
- Keep MetaDefender Core and all scanning engines **up to date** to take advantage of performance improvements.

Refer to this support article for more detailed information: [MetaDefender Core Performance Tuning Guide](https://www.opswat.com/docs/mdcore/configuration/metadefender-core-performance-tuning-guide)

#### [**4. Scale Horizontally**](/docs/mdcore/knowledge-base/how-to-limit-the-number-of-cpu-cores-used-for-scanning-in-metade#4-scale-horizontally)

In high-load environments, distribute scanning tasks across multiple MetaDefender Core instances to ensure optimal performance and scalability.

This approach reduces per-instance CPU usage and improves overall throughput. You can achieve horizontal scaling by:

- Deploying a **load balancer** or other task distribution mechanism to efficiently route scanning requests across instances.
- Utilizing **MetaDefender Distributed Cluster** for centralized management, job scheduling, and load distribution across multiple Core nodes.

For more detailed configuration guidance, refer to [Using external Load Balance](https://www.opswat.com/docs/mdcore/installation/using-external-load-balancer) and [MetaDefender Distributed Cluster](https://www.opswat.com/blog/introducing-metadefender-distributed-cluster-scalable-distributed-architecture-for-high-volume-file-security) documentation.

### [**Verify the Change**](/docs/mdcore/knowledge-base/how-to-limit-the-number-of-cpu-cores-used-for-scanning-in-metade#verify-the-change)

After applying the tuning recommendations, you can verify the improvements by:

1. **Monitoring CPU utilization** on the MetaDefender Core host via your OS tools (e.g., Task Manager, `top`, `htop`, or system metrics).
2. **Observing API responsiveness** by performing health check requests (`/metadefender/status`) and test file scan submissions.
3. **Observing API responsiveness** by

   1. **Performing health check requests** using `GET /readyz` to verify that the service is up and responding.
   2. **Reviewing the** `nginx.log` file located in your Core log directory. This log records every API request along with its total processing time. Each log entry includes details such as the timestamp, request type, response status, and processing duration.

**Example log entry:**

`[dd/MMM/yyyy:HH:mm:ss +0800] "GET /api/scan HTTP/1.1" 200 512 "-" "Java/17.0.10" 0.245`

In this example, the value `0.245` at the end indicates that the request took **0.245 seconds** to complete.

4. **Comparing throughput and response time** before and after tuning using the same workload.
5. If CPU usage stabilizes and APIs respond consistently, the tuning changes are effective.

### [**Summary**](/docs/mdcore/knowledge-base/how-to-limit-the-number-of-cpu-cores-used-for-scanning-in-metade#summary)

While MetaDefender Core does not support direct CPU throttling for scanning processes, administrators can achieve better performance stability by **tuning concurrency, simplifying workloads, optimizing system configuration, and scaling horizontally**.

Support:

If you continue to experience issue with the upgrade and have followed the instructions above, [**please create a support case or chat with our support engineer for further assistance.**](https://my.opswat.com/portal/support)
