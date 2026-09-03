<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/how-to-understand-opswat-s-multiscanning-av-detection-difference -->

# How to Understand OPSWAT's Multiscanning AV Detection Differences Compared to Other Scanners?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows or Linux systems.

There are times when OPSWAT Multiscanning antivirus detection presents results that differ from those provided by other scanner providers. This variance might lead to some questions and concerns, but it's imperative to understand that there are specific and logical explanations for these differences. In this page, we'll explore these reasons.

## [Keeping security and false positives in balance](/docs/mdcore/v5.21.0/knowledge-base/how-to-understand-opswat-s-multiscanning-av-detection-difference#keeping-security-and-false-positives-in-balance)

One of the primary factors contributing to the difference in detection results is the configuration of OPSWAT's AV engines. We carefully choose our configurations to provide robust security while minimizing the possibility of harmless files being incorrectly flagged. Maintaining this balance is crucial to maintaining both the integrity of the system and the trust of the users.

If OPSWAT Mulitscanning engine doesn't detect a file that other scanner providers do, it's possible that adjusting the engine configurations could resolve this issue.

| Engine | Configuration |
| --- | --- |
| AegisLab | Cloud Scan - On |
| ClamAV | Detect PUP/PUA - On |
| ESET | Extract Archive - On |
| Ikarus | Extract Archive - On |
| Huorong | Extract Archive - On |
| Sophos | Cloud scan - On |
| Symantec | Insight Scan - On |
| Crowstrike ML | Change Threshold Detection to lower level |

## [Cloud Features and Enterprise Suitability](/docs/mdcore/v5.21.0/knowledge-base/how-to-understand-opswat-s-multiscanning-av-detection-difference#cloud-features-and-enterprise-suitability)

Another significant point of differentiation is OPSWAT's approach to cloud features. The AV engines we employ are designed with enterprises in mind, focusing on robust, on-premises solutions. This approach contrasts with many other services that rely heavily on cloud-based features. While cloud-based AV solutions are popular and effective for some users, they might not always be the best fit for enterprise environments where control, privacy, and security are paramount.

Listing Known Detection Differences

Here is you can find a list of known differences in detections between OPSWAT and other scanner services. These differences can stem from a variety of factors such as licensing agreements, efforts to reduce high false positives, the use of remote servers, or choosing to utilize a different product from the same company. Each of these elements contributes to the unique way OPSWAT approaches and implements its antivirus detection strategies. Here is a list of the known differences:

| Engine | Difference |
| --- | --- |
| Antiy | OPSWAT products don’t use their cloud service. |
| BitDefender Theta | According to the vendor, this is not a standard version, it is a machine-learning engine version, they don’t sell it to anyone, they only put it in VT to collect data and use it to update the standard version. |
| CrowdStrike Falcon | OPSWAT products don’t use their cloud feature. This feature will send the customer data to CrowdStrike server to analyze more, the detection comes from the cloud server. OPSWAT product is for enterprise customers, we do not allow sending the customer’s data to outside the organization, therefore the detection is just based on the local database and can’t detect the file. In general, the vendor will review the cloud detection and add it to the local database if needed, it just takes time, we don’t know when. |
| McAfee | The comparable version in VT is Trellix ENS not the McAfee Scanner.  OPSWAT products don’t use Artemis detection.  The Artemis detection comes from Trellix GTI Cloud detection, this detection will or won’t be moved to the traditional/local database, it depends on the prevalence. |
| Webroot | OPSWAT products use [SMD](https://www.webroot.com/us/en/business/threat-intelligence/file/streaming-malware-detection), Some providers use [File Reputation](https://www.webroot.com/us/en/business/threat-intelligence/file/file-reputation). |

Support:

If you need help learning more information about **OPSWAT's Multiscanning AV Detection Differences Compared to Other Scanners** feel free to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).
