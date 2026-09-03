<!-- source: https://www.opswat.com/docs/filescan/3.1.1/datasheet/offline-url-reputation -->

# URL Reputation Predictor Overview

MetaDefender Aether [formerly known as MetaDefender Sandbox] on-premise / standalone integrates an Offline URL detector ML model.

Info

URL offline reputation will now auto-apply in air-gapped / offline environments (in case of lack of internet connection), but be disabled by default

## [Introduction](/docs/filescan/3.1.1/datasheet/offline-url-reputation#introduction)

The offline URL detection ML model enhances security by effectively identifying suspicious URLs. Unlike traditional methods, it utilizes machine learning on a dataset of labelled URLs to accurately detect threats without relying on web rendering or code analysis. **Meaning malicious URL detection can still be carried out in air-gapped sandbox environment.**

Key differences

- **Real-time vs. Offline Analysis:** Online reputation depends on real-time data and active web interactions, whereas offline URL reputation relies on pre-existing datasets and machine learning models to evaluate URLs without needing live access.
- **Resource Intensity:** Online reputation methods can be resource-intensive due to the need for real-time rendering and analysis. Offline URL reputation is less resource-demanding, as it uses pre-trained models to make assessments.
- **Adaptability:** Offline URL detection is more adaptable in environments with limited or no internet access, providing a consistent layer of security regardless of connectivity.

## [Operations](/docs/filescan/3.1.1/datasheet/offline-url-reputation#operations)

The model performs a comprehensive analysis of key attributes from a new URL to assess its safety. It then generates a probability score indicating the likelihood of the URL being malicious or benign

## [Example](/docs/filescan/3.1.1/datasheet/offline-url-reputation#example)

Its adaptability to offline environments makes it versatile for various security scenarios, such as preventing malware from exfiltrating data through disguised URLs or thwarting phishing attempts by flagging fraudulent links in emails.

## [Data](/docs/filescan/3.1.1/datasheet/offline-url-reputation#data)

The Suspicious URL detector Machine Learning model was trained on close to 1 million URLs from various sources, including reputation vendors and feeds.

## [Report](/docs/filescan/3.1.1/datasheet/offline-url-reputation#report)

Offline Reputation result will be displayed under **OSINT Lookups** in the scan report.

#### [The item details](/docs/filescan/3.1.1/datasheet/offline-url-reputation#the-item-details)

|  |  |
| --- | --- |
| **Resource** | Identifies the certain URL being analyzed |
| **Type** | Specifies the nature of the entity |
| **Origin** | Methods to assess the reputation of the URL (e.g. **VBA Emulation**: In this example, VBA emulation helps in identifying if the code performs any malicious activities, such as downloading malware or manipulating system files, which could impact the reputation of the associated URL..) |
| **Provider** | Indicates the dataset providers: OPSWAT (Online) Reputation or OfflineURLReputation. |
| **Verdict** | The trained model is then applied to the extracted features, enabling it to predict whether the URL is benign or suspicious |

Please find the Showcase Report [here.](/docs/filescan/3.1.1/datasheet/web---phishing)

## [Configuration](/docs/filescan/3.1.1/datasheet/offline-url-reputation#configuration)

Info

The following setting is only required to manually enable the URL model in online mode. However, the feature is enabled automatically in offline mode.

The URL model can only provide an assessment of whether a URL is suspicious, without offering a more definitive judgment. To enable the model the following line has to be added to the appropriate configuration:

transform.cfgCopyenableUrlReputationPredictor=true

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
