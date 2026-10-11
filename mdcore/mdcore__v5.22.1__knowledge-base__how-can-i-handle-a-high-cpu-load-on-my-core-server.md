<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/how-can-i-handle-a-high-cpu-load-on-my-core-server -->

# How can I handle a high CPU load on my Core server

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**Overview** This article outlines steps and best practices to troubleshoot and resolve high CPU load issues on your OPSWAT Core server. A high CPU load can lead to decreased file processing performance and can affect the overall system throughput. By following these guidelines, you can optimize your server’s performance and ensure efficient scanning operations.

To effectively troubleshoot and resolve high CPU load issues on your OPSWAT MetaDefender Core server, please follow the steps and best practices outlined below. High CPU load can lead to decreased file processing performance and affect overall system throughput. By adhering to these guidelines, you can optimize your server's performance and ensure efficient scanning operations.

**Symptoms**

- Noticeable slowdown in file scanning and processing
- Increased average processing time per object
- Elevated CPU utilization consistently exceeding recommended thresholds

**Potential Causes**

- **Configuration Settings**: Overly aggressive parallel scan counts or a high queue size can stress the CPU.
- **Engine Issues**: Outdated or misconfigured scanning engines (e.g., FileType engine issues) may consume excessive CPU resources.
- **System Resources**: Inadequate hardware (e.g., insufficient CPU cores or suboptimal system settings) can lead to high CPU usage.
- **System Tuning**: Power plans, BIOS settings, or operating system configurations that are not optimized for performance can also contribute to high CPU load.

**Troubleshooting Steps**

1. **Review System Requirements**

Before proceeding, ensure that your server meets the [Recommended System Configuration](/docs/mdcore/v5.22.1/installation/recommended-system-configuration) for MetaDefender Core. Inadequate hardware specifications can lead to high CPU usage and degraded performance.

2. **Monitor System Resources**

   1. Use system monitoring tools to assess CPU, memory, and disk I/O usage.
   2. Identify if CPU usage spikes coincide with specific scanning activities.
3. **Review MetaDefender Core Configuration**

   1. Verify that the engine parallel count and maximum queue size settings match your workload. Adjust these settings if necessary.
   2. Check for any misconfigurations in the MetaDefender Core settings that might be triggering unnecessary load.
4. **Update Scanning Engines**

   1. Ensure that all scanning engines, especially the FileType engine, are updated to the latest versions to mitigate known issues that may cause high CPU usage.
5. **System and Hardware Optimization**

   1. Confirm that your server hardware meets the recommended specifications. For instance, using a high-performance power plan and ensuring BIOS settings are optimized (e.g., enabling Turbo Boost on CPUs).
   2. Consider increasing CPU cores if the current hardware is consistently overburdened.
6. **Review Logs and System Health**

   1. Examine MetaDefender Core logs to detect any error messages or alerts related to CPU load.
   2. Use the built-in health check features to determine if the high CPU load is affecting other system components.
7. **Restart the MetaDefender Core Service**

   1. After applying configuration changes, restart the service to ensure the changes take effect.

**Recommendations**

- **Adjust Configuration Settings**: Tweak engine parallel counts and queue sizes based on your typical workload to avoid overloading the CPU.
- **Regular Updates**: Maintain the latest version of all scanning engines and MetaDefender Core software to benefit from performance improvements and bug fixes.
- **Optimize Hardware**: If performance issues persist, evaluate whether a hardware upgrade (such as adding more CPU cores or faster memory) is required.
- **Follow Best Practices**: Refer to the [Performance Optimization and Fine-Tuning Guide](https://www.opswat.com/products/metadefender/core/performance-optimization-and-fine-tuning) for in-depth recommendations on system tuning and optimal configurations.

**Additional Resources**

- **Performance Optimization and Fine-Tuning Guide**: Learn how to maximize overall performance through system and application tuning. [Read more](https://www.opswat.com/products/metadefender/core/performance-optimization-and-fine-tuning)
- **How to Increase Parallel Count and Max Queue Size**: Detailed steps for adjusting these settings in your MetaDefender Core configuration. [Read more](/docs/mdcore/v5.22.1/knowledge-base/how-can-i-increase-parallel-count-and-max-queue-size)
- **Troubleshooting MetaDefender Core**: A comprehensive guide to diagnosing and resolving common issues. [Read more](/docs/mdcore/v5.22.1/troubleshooting/troubleshooting-metadefender-core)

By following these guidelines and recommendations, you can effectively manage high CPU loads on your OPSWAT MetaDefender Core server and ensure smooth, efficient operation. If issues persist, consider reaching out to OPSWAT Support for further assistance.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
