<!-- source: https://www.opswat.com/docs/filescan/3.2.0/datasheet/additional-scan-steps -->

# Threat Pattern Correlator - Additional Scan Steps Settings

View as Markdown Ask ChatGPT about this page Ask Claude about this page

You will find the Threat Pattern Correlator Settings in the Additional Scan Steps tab among Configurations **Admin Panel > Settings >** [**Configuration**](https://www.filescan.io/admin/settings/config) **> Functionality Extensions > Similarity Search tab**

Info

**Customers are not recommended to interact the following fields as these are mainly for the Admin**

**The Threat Pattern Correlator is disabled by default.**

**If it is enabled, you may find the same values set by default for each field.**

| Field | Description | Values |
| --- | --- | --- |
| *REPORT_SIMILARITY_VERDICT_OVERWRITE* | After the report is completed, it tries to search for similar reports that has been already processed. It will look at the verdict and can modify it.  (e.g. If previous similar reports show `malicious`it will change the verdict to `malicious)` | ON/OFF |
| *REPORT_SIMILARITY_VERDICT_THRESHOLD* | Specifies a threshold value (ranging from 0 to 1) for similarity checks. If the similarity ratio exceeds this threshold, it triggers a specific action or verdict overwrite | Percentage converted to decimal |
| *REPORT_SIMILARITY_VERDICT_FILTER* | Determines the minimal level of similarity verdict that needs to be checked against other samples (e.g., only consider similarities categorized as suspicious or higher) | - no threat - informational - suspicious - likely malicious - malicious |
| *REPORT_SIMILARITY_MALICIOUS_MATCH* | If the ratio of identified malicious similarities exceeds this threshold (0 to 1), the overall verdict for the analyzed sample is changed to "malicious." | Percentage converted to decimal |
| *REPORT_SIMILARITY_LIKELY_MALICIOUS_MATCH* | Similarly, if the ratio of likely malicious similarities surpasses this threshold (0 to 1), the verdict is adjusted to "likely malicious." | Percentage converted to decimal |
| *REPORT_SIMILARITY_SUSPICIOUS_MATCH* | If the ratio of suspicious similarities meets or exceeds this threshold (0 to 1), the verdict is altered to "suspicious." | Percentage converted to decimal |

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
