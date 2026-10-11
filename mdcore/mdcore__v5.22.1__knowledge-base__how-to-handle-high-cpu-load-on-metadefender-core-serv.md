<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/how-to-handle-high-cpu-load-on-metadefender-core-serv -->

# How to handle high CPU load on MetaDefender Core server?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Core V5 releases deployed on Windows or Linux systems.

## [Hardware factor](/docs/mdcore/v5.22.1/knowledge-base/how-to-handle-high-cpu-load-on-metadefender-core-serv#hardware-factor)

When encountering high CPU utilization on your MetaDefender Core server, first verify that the system meets the minimum hardware requirements for your respective engine package:

- [Windows system requirements](/docs/mdcore/v5.22.1/installation/recommended-system-configuration#windows-recommended-system-configuration)
- [Linux system requirements](/docs/mdcore/v5.22.1/installation/recommended-system-configuration#linux-recommended-system-configuration)

As a reference, you can see [Performance and Load Estimation](/docs/mdcore/v5.22.1/installation/performance-and-load-estimation) metrics (throughput, CPU utilization, processing time), to estimate required hardware resource that could meet your throughput and processing time requirements.

## [Software factor](/docs/mdcore/v5.22.1/knowledge-base/how-to-handle-high-cpu-load-on-metadefender-core-serv#software-factor)

If the system meets the requirements, there are other software factors that can affect CPU utilization, as outlined in the [MetaDefender Core Performance Tuning Guide](/docs/mdcore/v5.22.1/configuration/metadefender-core-performance-tuning-guide#software-factors):

- MetaDefender Core version: older versions may not have the best performance optimization.
- Engines and database: processing with more engines and using local PostgreSQL database can increase CPU usage on the server.
- Configuration: more thorough scan settings (such as deep scans, archive scanning) require more hardware resources.
- File characteristics: more complex file types require more resources to scan and process.
- Concurrent scans: higher concurrent scans require more resources.
- Integration method: how MetaDefender Core is integrated into other applications (e.g. via APIs) can influence performance.

Details on these software factors, and software tuning guide to avoid high CPU utilization can be found in the [MetaDefender Core Performance Tuning Guide](/docs/mdcore/v5.22.1/configuration/metadefender-core-performance-tuning-guide#metadefender-core-application-tuning).

Issue Example:

When resource utilization is very high (i.e. 100% CPU utilization) and files contain many archived files.

You can export MetaDefender Core’s [processing history](/docs/mdcore/v5.22.1/operating/processing-history) as CSV format, and analyze which file types are being processed the most, for example:

If you see that there are many archive file types, you may need to adjust [archive handling limits](/docs/mdcore/v5.22.1/configuration/workflow-configuration-template#archive) (max recursive level, max total extracted files, max total size of extracted files) in MetaDefender Core workflow.

- A higher limit means MetaDefender Core needs to dig deeper to process these files, so incrementally reduce the limit and observe CPU utilization.

Hardware limitation:

If all software tuning options have been exhausted and CPU utilization remains high, you might need to consider increasing the hardware resources in order to meet the demanding processing load.

Support:

If you have followed the instructions above but are still encountering **High CPU load on MetaDefender Core server**, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/v5.22.1/troubleshooting/how-to-create-support-package-), before [**creating a support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
