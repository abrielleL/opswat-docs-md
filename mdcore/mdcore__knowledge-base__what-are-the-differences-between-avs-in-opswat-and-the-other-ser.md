<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/what-are-the-differences-between-avs-in-opswat-and-the-other-ser -->

# What are the differences between AVs in OPSWAT and the other services?

When comparing antivirus (AV) scanning capabilities, it's essential to understand how configurations and engine versions impact detection performance and reliability. OPSWAT products are specifically designed to protect critical infrastructure, focusing on stability, privacy, and minimizing false positives. This approach differs from other services, which may prioritize higher detection rates at the cost of increased false positives or reduced data privacy. Below, we explore the key differences in configurations and engine versions between OPSWAT and other services.

## [Configurations](/docs/mdcore/knowledge-base/what-are-the-differences-between-avs-in-opswat-and-the-other-ser#configurations)

Some antivirus engines have a cloud scanning feature that is disabled by default in OPSWAT products. Enabling this feature can significantly increase detection capabilities, but it requires sending data to the vendor's servers for processing. This trade-off may have privacy and security implications.

- **Engines with Cloud Scan Features**. OPSWAT disables cloud scanning to prioritize data privacy and local scanning, while other services may enable it to enhance detection.

| Engine | Configuration |
| --- | --- |
| Lionic | Enable Cloud Scan |
| Sophos | Enable Cloud Scan |
| AhnLab | Enable Cloud Scan |

- **Other Configurations**

Additional engine configurations can also improve detection rates but may require adjustments depending on the specific use case.

| Engine | Configuration |
| --- | --- |
| ClamAV | Enable PUP/PUA Detection |
| ESET | Enable Archive Extraction |
| Ikarus | Enable Archive Extraction |
| Huorong | Enable Archive Extraction |
| Crowstrike ML | Change Threshold Detection to lower level |

## [Engine Versions](/docs/mdcore/knowledge-base/what-are-the-differences-between-avs-in-opswat-and-the-other-ser#engine-versions)

OPSWAT typically employs official release versions with selected features tailored for protecting critical infrastructure. This approach minimizes errors and ensures stability. In contrast, other services may use earlier or beta versions to maximize detection rates. While these versions might provide higher detection, they are more prone to false positives and instability.

**Examples of Differences in Engine Behavior**:

1. **Antiy, CrowdStrike Falcon and QuickHeal**

- OPSWAT: Cloud scanning is not used.
- Other services: May enable cloud scanning to improve detection.

2. **McAfee**

- OPSWAT: Artemis detection is excluded. Reference: [Some of my virus detections are called 'Artemis' | McAfee Support](https://www.mcafee.com/support/s/article/000001548?language=en_US#:~:text=When%20your%20McAfee%20app%20quarantines,Threat%20Intelligence%20(GTI)%20system.).
- Other services: May include Artemis detection, increasing detection sensitivity but potentially introducing more false positives.

3. **Webroot SMD**

- OPSWAT: Uses the [SMD version](https://www.webroot.com/us/en/business/threat-intelligence/file/streaming-malware-detection) for scanning.
- Other services: May rely on [File Reputation](https://www.webroot.com/us/en/business/threat-intelligence/file/file-reputation), which could provide broader detection at the cost of stability or accuracy.

By focusing on stability, data privacy, and critical infrastructure protection, OPSWAT's approach differs significantly from other services that may prioritize maximum detection at the expense of reliability or privacy.

Support:

If you have any further questions regarding the differences between AVs in OPSWAT and the other services, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).
