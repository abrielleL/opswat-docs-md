<!-- source: https://www.opswat.com/docs/filescan/datasheet/verdict -->

# Report Verdict

The table provided below offers a high-level overview of submission classifications based on their potential threat levels and a summarized overview within your report verdicts.

Info

From MetaDefender Sandbox 2.5.0, the displayed verdicts will use the new, **human-friendly** variants from the table below. The old, **risk score based** verdicts can still be enabled through the Admin Panel, see the Configuration options under [General Settings](/docs/filescan/configuration/general).

The final verdict is an aggregate of the detected threat indicators based on our proprietary verdict calculation logic, which is tuned to mitigate the occurrence of both false negative and false positive results, ensuring a more accurate and reliable assessment of potential threats.

The `threatLevel` field contains a numeric representation that corresponds to a given verdict. For some verdicts, the `threatLevel` is a range, not a single value. See the exact values below.

| **Human Friendly Verdict (New)** | **Risk Score Based Verdict (Old)** | **Description** | **Action** | Threat Level Values |
| --- | --- | --- | --- | --- |
| Trusted | Benign | The file has been whitelisted based on a hash match with the National Software Reference Library (NSRL), custom whitelists, or valid certificates from reputable software vendors. | No Action | -1 |
| Undetermined | Unknown | The file is unsupported, contains insufficient data, or the analysis is inconclusive. | Malware Analysis | 0 |
| No Threat Detected | No Threat | Although the file is supported, its reputation data and threat indicators do not indicate any known capability typically associated with malware. | No Action | 0.1-0.25 |
| Low Risk | Suspicious | The file contains some threat indicators commonly found in malware. To address this, please ensure that the [MD Cloud Reputation](https://docs.opswat.com/filescan/integrations/reputation-api-integration) service is enabled and perform an AV engine scan with [MetaDefender Multiscanning.](https://docs.opswat.com/filescan/integrations/metadefender-multiscanning) | Perform AV engine/reputation check | 0.5 |
| High Risk | Likely Malicious | The file exhibits numerous threat indicators commonly associated with malware, and there is no compelling evidence from the AV engine or reputation services to suggest otherwise.  **Note**: Behaviors often associated with malware—such as code injection, process manipulation, or network communication—can also occur in legitimate applications, making definitive conclusions challenging. In air-gapped environments, where certificate-based whitelisting and external reputation lookups are unavailable, legitimate application presenting such capabilities may be classified as "High Risk". See how [Adaptive Threat Context](https://www.opswat.com/docs/filescan/3.1.1/datasheet/adaptive-threat-context) helps to mitigate these false positives. | Block file | 0.75 |
| Confirmed Threat | Malicious | The file provides clear evidence of being malware, either due to a critical mass of threat indicators, a true positive indicator, or validation from a first-tier AV engine or reputable source. | Block File | 1 |
| System Error | N/A | The verdict could not be determined due to an internal malfunction (e.g., engine crash). | Retry or Report Issue | N/A |

### [**Verdict Visualization**](/docs/filescan/datasheet/verdict#verdict-visualization)

### [Verdict Representation in the API Scan Results](/docs/filescan/datasheet/verdict#verdict-representation-in-the-api-scan-results)

If the **human-friendly** verdicts are enabled, then the API returns scan results in the following format: the `finalVerdict` object contains the `verdict` field that matches **risk score based** verdicts from the table above, and the `verdictLabel` field matches the **human-friendly** verdicts.

Info

For all API integrations, please use the `threatLevel` field contains a stable numeric representation that corresponds to a given verdict. The text representation of a verdict might change in future versions, but the `threatLevel` will have the same value.

JsonCopy"finalVerdict": {
"verdict": "SUSPICIOUS",
"threatLevel": 0.5,
"confidence": 1.0,
"verdictLabel": "low_risk"
}

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
