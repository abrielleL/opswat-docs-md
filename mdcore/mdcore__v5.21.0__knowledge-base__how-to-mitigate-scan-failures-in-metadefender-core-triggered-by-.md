<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/how-to-mitigate-scan-failures-in-metadefender-core-triggered-by- -->

# How to Mitigate Scan Failures in MetaDefender Core Triggered by Real-Time Protection Systems?

This article applies to all MetaDefender Core V5 releases deployed on Windows systems.

### [Summary:](/docs/mdcore/v5.21.0/knowledge-base/how-to-mitigate-scan-failures-in-metadefender-core-triggered-by-#summary)

This article provides insights and solutions to a prevalent issue in MetaDefender Core where scans may fail due to disruptions from real-time protection systems. The problem often manifests without generating explicit error messages, complicating diagnosis. This guide will walk you through the steps to identify and rectify this situation.

### [Problem Description:](/docs/mdcore/v5.21.0/knowledge-base/how-to-mitigate-scan-failures-in-metadefender-core-triggered-by-#problem-description)

Users of MetaDefender Core may experience scan failures that do not return specific error messages. A successful scan should typically display "No available scan result" in the Metascan details, and the corresponding report should state "Not Scanned."

### [Primary Cause:](/docs/mdcore/v5.21.0/knowledge-base/how-to-mitigate-scan-failures-in-metadefender-core-triggered-by-#primary-cause)

In most cases, real-time protection systems like antivirus software delete or quarantine files uploaded to MetaDefender Core, perceiving them as potential threats. This action inhibits MetaDefender Core's ability to process these files, leading to scan failures. Notably, these failures may also show errors from engines indicating the file does not exist.

### [Solution:](/docs/mdcore/v5.21.0/knowledge-base/how-to-mitigate-scan-failures-in-metadefender-core-triggered-by-#solution)

To resolve this issue and ensure effective scanning, follow these steps:

1. Identify the real-time protection (RTP) software operational on the MetaDefender Core server.
2. Navigate to the settings of the identified RTP software.
3. Look for the “Exclusions” or “Exceptions” section in the settings.
4. Add the full installation path of MetaDefender Core, and the temporary upload path used by MetaDefender Core, to the exclusions list.
5. **Important Note:**   If Windows Defender is used *both* as the local antivirus **and** as an AV engine inside MetaDefender Core, **do not exclude** `engineprocess.exe` from the real-time protection exclusion list. In that scenario, excluding the engine process may interfere with the integrated AV engine functionality.
6. In other cases (for example, when Windows Defender is used only as the local AV, not as the AV engine for MetaDefender Core), you may exclude `engineprocess.exe` along with other processes like `ometascan.exe`, `postgres.exe`, and `nginx.exe` to prevent interference by the real-time protection system.
7. Save your changes and exit the settings.
8. Conduct a test scan to confirm the resolution of the problem. For detailed instructions on adding exclusions or exceptions to your AV software, refer to the user manual or documentation provided by the software vendor.

### [Conclusion:](/docs/mdcore/v5.21.0/knowledge-base/how-to-mitigate-scan-failures-in-metadefender-core-triggered-by-#conclusion)

By following the provided steps and adjusting your real-time protection software settings, you should be able to address MetaDefender Core scan failures. This process ensures that files you upload for scanning are not wrongly removed by real-time protection systems, enabling successful MetaDefender Core scans. As a result, you should observe "No available scan result" in the Metascan details and "Not Scanned" in the exported report, as expected.

Support:

If the problem persists despite following the outlined steps, please open a [**Support Case**](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [**OPSWAT Expert Forum**](https://go2.opswat.com/s).
