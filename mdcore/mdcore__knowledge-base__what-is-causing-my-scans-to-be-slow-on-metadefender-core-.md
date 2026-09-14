<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/what-is-causing-my-scans-to-be-slow-on-metadefender-core- -->

# What is causing my Scans to be slow on MetaDefender Core?

Slow scan performance in MetaDefender Core can be caused by several factors:

- **Older MetaDefender Core Version:** It is best practice to upgrade to the latest version since the latest version has the latest bug fixes and performance improvements.
- **MetaDefender Core Configuration**: Settings such as deep scans, heuristic analysis, and archive scanning can impact performance. More thorough scans require more resources and time.

  - Please note that only certain AV engines have Heuristic analysis. The Heuristic scan is a method of detecting potential threats by analyzing the behavior, structure, and characteristics of files rather than relying solely on known malware signatures. This approach allows the AV engine to identify new, unknown, or modified threats that may not yet be included in traditional signature databases.
  - AV engines which have this feature enabled may be slower than others.
- **Number of Engines**: The number of antivirus engines configured can affect performance. While more engines provide better security, they can slow down the scanning process.
- **File Characteristics**: The type and size of files being scanned (for example: executables, archives, multimedia files) can influence performance, as some file types are more complex to process.

  - Examples of file types that can affect the performance of MetaDefender Core during scanning include:

    - **Executables**: These files can be complex to process due to their potential to contain malicious code or embedded resources.
    - **Archives**: These files, such as ZIP may contain multiple nested files, which increases the processing complexity and time required for scanning.
    - **Multimedia files**: These files, like videos or images, can vary significantly in size and complexity, impacting the scanning process depending on their characteristics.
  - **Deep CDR and Proactive DLP**: These features can impact the scanning process in MetaDefender Core. Deep CDR processes files by disarming and reconstructing them, which involves decompression, pixel processing, and reconstruction, potentially adding complexity to the scanning process. Proactive DLP, on the other hand, checks for sensitive data in files and can redact or watermark the data, which also adds processing steps.
- **Concurrent Scans**: The number of simultaneous scans being performed can divide the machine’s resources and impact overall performance.

  - To improve performance when dealing with concurrent scans in MetaDefender Core, you can consider the following steps:

    - **Optimize Background Processes**: Suspend any nonessential background processes and services running on the operating system, as they can consume resources and impact scanning performance.
    - **Adjust Concurrent Scans**: The number of simultaneous scans can divide the machine's resources. Reducing the number of concurrent scans or optimizing the integration method can help improve performance.
    - **Set Power Profile to Performance**: Configure the system's power profile to "Performance" settings to avoid CPU throttling and ensure maximum processing power.
    - **Upgrade Hardware**: If possible, use systems with higher CPU cores (e.g., 32-48 cores) and sufficient memory to handle high workloads efficiently.
    - **Configure Parallel Scans**: Increase the parallel number of scans running per engine using the `parallelcount` setting. This allows better utilization of CPU resources for engines supporting multi-threaded scans.
    - **Increase Queue Size**: If the queue is full of incoming scan requests, increase the maximum queue size using the API call `PUT /admin/config/scan` with the appropriate configuration. Or update the queue by logging in to MD Core UI console > click on Settings > click on General tab
    - **Use the Latest Version**: Always ensure you are using the latest version of MetaDefender Core for optimal performance and to avoid legacy stability issues.
    - **Optimize Network**: For network scanning, ensure a minimum of 1 Gbps network speed, with 5 Gbps recommended, to avoid potential network-related issues.
- **Integration Method**: How MetaDefender Core is integrated into other applications (e.g., via APIs) can also affect performance, especially if the integration is not optimized.

  - An example of how the integration method can affect performance is when MetaDefender Core is integrated into other applications via APIs. If the integration is not optimized, it can lead to inefficiencies in processing, such as increased response times or reduced throughput. For instance, the location of the client application (remote or local) and the use of system caching or engine-level caching can significantly influence performance.
- **Real-Time Protection Systems**: Real-time protection software on the MetaDefender Core server may interfere with scans by deleting or quarantining files, which can disrupt the scanning process.

  - To address this issue navigate to the settings of the real-time protection software.
  - Locate the 'exclusions' or 'exceptions' section in the settings.
  - Add the full installation path of MetaDefender Core to the exclusions list
- **Engine-Specific Factors**: Some engines, like ClamAV, are known to have slower performance due to their design. Adjusting engine-specific settings, such as limiting file size or disabling certain features, can help mitigate this.

It is recommended to review these factors and optimize the configuration to improve scan performance. As stated previously, always ensure you are using the latest version of MetaDefender Core for the best performance and stability.

After confirming that you’ve optimized the configuration to the best that you can and scans are still being processed slowly, please submit a support ticket to OPSWAT Support.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
