<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/can-metadefender-core-scan-embedded-payloads-or-inline-file-cont -->

# Can MetaDefender Core Scan Embedded Payloads or Inline File Content?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows or Linux systems.

MetaDefender Core does **not** natively scan content that is embedded directly within a payload, such as files included inline in an email body or as raw binary/base64 in an API request.

To scan such content, it must first be programmatically extracted and submitted to MetaDefender Core as a standalone file or data stream via its API.

## [**Supported Scanning Methods**](/docs/mdcore/v5.22.1/knowledge-base/can-metadefender-core-scan-embedded-payloads-or-inline-file-cont#supported-scanning-methods)

There are two two scanning methods that MetaDefender Core supports

### [**1. Remote Scan (HTTP(S) Payload Upload)**](/docs/mdcore/v5.22.1/knowledge-base/can-metadefender-core-scan-embedded-payloads-or-inline-file-cont#1-remote-scan-https-payload-upload)

- File content is included directly in the HTTP(S) request body.
- Core scans the uploaded data as a standalone file.
- Embedded content must be extracted, saved, and then submitted via the API.

### [**2. Local File Path Scan**](/docs/mdcore/v5.22.1/knowledge-base/can-metadefender-core-scan-embedded-payloads-or-inline-file-cont#2-local-file-path-scan)

- Used when the file is already accessible to Core on the local system or network.
- The file path is passed in the request, and Core reads the file directly.
- This method does not process any content embedded in the request payload.

In short:

## [**Steps to Configure**](/docs/mdcore/v5.22.1/knowledge-base/can-metadefender-core-scan-embedded-payloads-or-inline-file-cont#steps-to-configure)

To scan embedded or inline content:

1. **Extract the embedded content** Programmatically extract the embedded file from the email body, base64 blob, or structured payload. This may involve parsing and decoding the content before saving it.
2. **Convert it to a file or stream** Save the extracted content as a temporary file or buffer that can be submitted via HTTP.
3. **Upload the file to MetaDefender Core** Use the `POST /file` API endpoint to submit the file for scanning:

HtmlCopycurl -X POST "http://<core_address>:8008/file" \
-H "apikey: <your_api_key>" \
-F "file=@/path/to/extracted-file"

- The response will contain a `data_id`, which uniquely identifies the scan session:

HtmlCopy{
"data_id": "61dffeaa728844adbf49eb090e4ece0e"
}

4. **Poll for scan results** Use the `GET /file/{data_id}` API to check the scan status:

HtmlCopycurl -X GET "http://<core_address>:8008/file/61dffeaa728844adbf49eb090e4ece0e" \
-H "apikey: <your_api_key>"

- Keep polling until `scan_results.progress_percentage` reaches `100`.

---

## [**Verify the Change**](/docs/mdcore/v5.22.1/knowledge-base/can-metadefender-core-scan-embedded-payloads-or-inline-file-cont#verify-the-change)

To confirm the embedded content was scanned successfully:

1. **Check scan completion**

   - Wait until `progress_percentage` in the `/file/{data_id}` response reaches `100`.
   - Example response field:

HtmlCopy"scan_results": {
"progress_percentage": 100,
...
}

2. **Review the scan results**

   - Once complete, examine the `scan_results` section for detected threats, actions taken, and engine breakdowns.
3. **Search by hash (optional)**

   - You can also retrieve results later using the file's hash (MD5, SHA1, SHA256) with:

HtmlCopyGET /hash/{hash_value}

4. **Use the Core Management Console (optional)**

- Navigate to **History** to view processed files and scan statuses via the GUI.

Support:

If Further Assistance is required, please proceed to [**create a support case or chat with our support engineer**](https://my.opswat.com/support).
