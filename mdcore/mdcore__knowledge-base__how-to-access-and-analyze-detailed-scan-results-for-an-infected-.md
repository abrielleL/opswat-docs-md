<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/how-to-access-and-analyze-detailed-scan-results-for-an-infected- -->

# How to access and analyze detailed scan results for an infected file?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows and Linux systems.

OPSWAT’s MetaDefender Core provides in-depth scan results through both the management console and API, offering crucial insights into detected threats. Each scan result includes:

- **Scanning Engine**: The antivirus or security engine that flagged the file.
- **Threat Name**: The identifier assigned to the detected threat.
- **Metadata**: Additional details such as file hash, scan timestamp.

## [Using the Management Console UI:](/docs/mdcore/knowledge-base/how-to-access-and-analyze-detailed-scan-results-for-an-infected-#using-the-management-console-ui)

- Click the **History** tab on the left, select **Processing** from the drop-down list, and then click the file to view the scan result.

- Navigate to the top right corner and click on the **copy button** to retrieve the file hash. You can choose to export the file hash in SHA1, SHA256, or MD5.
- You can download the result in various formats. To save it as a PDF, click the **Export Result** button.

Or click the arrow button to export the file in your preferred format.

## [Using API Calls:](/docs/mdcore/knowledge-base/how-to-access-and-analyze-detailed-scan-results-for-an-infected-#using-api-calls)

Refer to the API documentation at [MetaDefender Core File Analysis API](/docs/mdcore/metadefender-core#fileanalysispost). Scans are done asynchronously, and each scan request is tracked by a **data ID**. You need to initiate file scans and retrieve the results using two separate API calls.

- **Upload a file to scan**:

  - Use the `POST /file` API endpoint to upload the file.
  - The response will include a `data_id`, which is a unique identifier for the submission. Example response: `{ "data_id": "61dffeaa728844adbf49eb090e4ece0e" }`
- **Fetch the analysis result**:

  - Use the `GET /file/{data_id}` API endpoint with the `data_id` obtained in the previous step.
  - Continue polling this endpoint until the `progress_percentage` in the response reaches 100%. The scan completion can be traced using the `scan_results.progress_percentage` value from the response. Example request:

BashCopycurl --request GET \ --url 'http://localhost:8008/file/{data_id}' \ --header 'apikey: {apikey}'

- **Retrieve the scan results**:

  - Once the scan is complete, you can retrieve the results using the `data_id` or the file's hash (e.g., MD5, SHA1, SHA256).

Scan results can be retrieved in JSON format, enabling further automation and integration with security workflows.

While MetaDefender Core provides high-level detection details, for a more comprehensive analysis, you can cross-reference the reported threat name with the corresponding antivirus vendor’s threat intelligence database. These databases contain detailed descriptions, attack vectors, and mitigation strategies for known malware.

By leveraging both MetaDefender’s scan results and vendor-specific threat intelligence, you can gain a deeper understanding of the nature of the threat and take appropriate remediation actions.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/portal/support).
