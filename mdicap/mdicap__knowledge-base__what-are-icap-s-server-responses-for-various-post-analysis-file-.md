<!-- source: https://www.opswat.com/docs/mdicap/knowledge-base/what-are-icap-s-server-responses-for-various-post-analysis-file- -->

# What are ICAP's server responses for various post-analysis file results?

**Applies to**

- MetaDefender ICAP Server / MetaDefender ICAP Cloud
- ICAP clients using REQMOD, RESPMOD, or supported file-scanning workflows
# [Problem](/docs/mdicap/knowledge-base/what-are-icap-s-server-responses-for-various-post-analysis-file-#-problem)

When integrating a custom ICAP client with the OPSWAT ICAP service, what response format should the client expect for different post-analysis results, such as a clean file, an infected file, or an analysis failure / processing error?

# [Solution](/docs/mdicap/knowledge-base/what-are-icap-s-server-responses-for-various-post-analysis-file-#-solution)

MetaDefender ICAP Server follows the ICAP protocol defined in RFC 3507. ICAP responses begin with an ICAP status line such as ICAP/1.0 200 OK, and the status code alone is not enough to determine the final security verdict.

For custom ICAP clients, the correct behavior is to evaluate both of the following:

1. The **ICAP response code**, such as 204, 200, 4xx, or 5xx
2. The **ICAP response headers**, especially OPSWAT-specific headers such as X-Response-Info, X-Blocked-Reason, X-Response-Desc, X-Infection-Found, and X-Violations-Found

**Important:** 200 OK does not mean the file is clean. It only means the ICAP request was processed successfully. The client must inspect the returned headers and, when applicable, the response body.

## [Expected response behavior](/docs/mdicap/knowledge-base/what-are-icap-s-server-responses-for-various-post-analysis-file-#expected-response-behavior)

| Result | ICAP response behavior | Client action |
| --- | --- | --- |
| Clean file, no CDR/DLP processing, client allows 204 | 204 No modification needed | Allow the original file. No response body is returned. |
| Clean file, no CDR/DLP processing, client does not allow 204 | 200 OK with a response body | Allow the file and process the returned body according to the ICAP response. |
| Clean file with CDR/DLP enabled | 200 OK with the processed file in the response body | Allow the file, but use the returned sanitized, redacted, or rebuilt file instead of the original. |
| Infected or policy-blocked file | 200 OK with a block response/body and blocking headers | Block the file. Use response headers to determine the reason. |
| Analysis failed / processing error | Depends on the failure type and configured policy | Do not assume the file is clean. Handle ICAP error codes and error-related headers according to policy. |

## [Clean file behavior](/docs/mdicap/knowledge-base/what-are-icap-s-server-responses-for-various-post-analysis-file-#clean-file-behavior)

When a file is clean and no content transformation is required, MetaDefender ICAP Server may return either 204 or 200, depending on the ICAP client request and the enabled security engines.

### [Case 1: CDR and DLP disabled, and the ICAP client supports 204](/docs/mdicap/knowledge-base/what-are-icap-s-server-responses-for-various-post-analysis-file-#case-1-cdr-and-dlp-disabled-and-the-icap-client-supports-204)

If the ICAP client supports Allow: 204 and the file is clean with no modification required, MetaDefender ICAP Server can return:

ICAP/1.0 204 No modification needed

This means the original content is clean and does not need to be modified. The ICAP client should continue using the original file.

### [Case 2: CDR and DLP disabled, and the ICAP client does not support 204](/docs/mdicap/knowledge-base/what-are-icap-s-server-responses-for-various-post-analysis-file-#case-2-cdr-and-dlp-disabled-and-the-icap-client-does-not-support-204)

If the client does not advertise or support Allow: 204, MetaDefender ICAP Server returns:

ICAP/1.0 200 OK

In this case, the client should parse the ICAP response and handle the returned body accordingly.

### [Case 3: CDR or DLP enabled](/docs/mdicap/knowledge-base/what-are-icap-s-server-responses-for-various-post-analysis-file-#case-3-cdr-or-dlp-enabled)

When CDR or DLP processing is enabled, a clean or allowed file may still be modified. For example, Deep CDR may rebuild the file, or DLP may redact sensitive content.

In this case, MetaDefender ICAP Server returns:

ICAP/1.0 200 OK
X-Response-Info: Allowed

The processed file is returned in the response body. The ICAP client must save and forward the returned file, not the original file.

Some ICAP clients correctly accept the ICAP response but then accidentally discard the returned sanitized or redacted file and continue using the original file. This behavior should be avoided.

## [Infected or blocked file behavior](/docs/mdicap/knowledge-base/what-are-icap-s-server-responses-for-various-post-analysis-file-#infected-or-blocked-file-behavior)

When a file contains malware or violates policy and is blocked by MetaDefender, MetaDefender ICAP Server returns a successful ICAP transaction with blocking headers, for example:

ICAP/1.0 200 OK
X-Response-Info: Blocked
X-Blocked-Reason: Infected
X-Response-Desc: Infected
X-Virus-ID: <threat name>
X-Infection-Found: Type=0; Resolution=0; Threat=<threat name>;

The response body may contain a block message rather than the original file.

The client should not interpret 200 OK as a clean result. In ICAP, 200 OK means the request was processed successfully. The actual verdict must be determined from the ICAP response headers and body.

### [Relevant OPSWAT headers](/docs/mdicap/knowledge-base/what-are-icap-s-server-responses-for-various-post-analysis-file-#relevant-opswat-headers)

| Header | Meaning |
| --- | --- |
| X-Response-Info | One-word action applied by the ICAP server, such as Allowed, Blocked, or Options. Available in all ICAP server responses. |
| X-Blocked-Reason | Blocking reason, such as Infected. Present only when scanned content has violations. |
| X-Response-Desc | Description of the blocking reason. Available in blocked responses. |
| X-Virus-ID | Short description of the detected threat. |
| X-Infection-Found | Threat details, including type, resolution, and threat name. |
| X-Violations-Found | Detailed list of violations, including archive-contained files when applicable. |

## [Analysis failed or processing-error behavior](/docs/mdicap/knowledge-base/what-are-icap-s-server-responses-for-various-post-analysis-file-#analysis-failed-or-processing-error-behavior)

There is no single universal ICAP response form for analysis failures. The response depends on the failure type and the configured workflow or security policy.

Examples of failure or exceptional conditions include:

- Multipart parsing error
- Core busy
- File size limit exceeded
- Scan timeout
- MetaDefender Core server error
- Unsupported content encoding
- Decoding error

MetaDefender ICAP Server policies can be configured to block, allow, or process certain error scenarios differently. For example, scan timeouts and Core server errors may be configured to allow requests, while unsupported encoding and decoding errors may be configured with actions such as block, scan without decoding, or allow.

For multipart batch submissions, if a file fails during submission to MetaDefender Core, the ICAP Server triggers batch scan cancellation for that scenario.

## [Recommended client decision logic](/docs/mdicap/knowledge-base/what-are-icap-s-server-responses-for-various-post-analysis-file-#recommended-client-decision-logic)

1. If the ICAP response code is 204, treat the file as clean with no modification needed.
2. If the ICAP response code is 200, check X-Response-Info.

   - If X-Response-Info is Allowed, accept the response. If a response body is present, use the returned body.
   - If X-Response-Info is Blocked, block the file and read headers such as X-Blocked-Reason, X-Response-Desc, X-Infection-Found, and X-Violations-Found.
3. If the ICAP response code is 4xx or 5xx, treat it as an ICAP, server, or request error and follow the organization’s fail-open or fail-closed policy.
4. If response headers indicate timeout, server error, parsing error, or another processing failure, do not assume the file is clean. Apply the configured security policy.

## [Important implementation guidance for custom ICAP clients](/docs/mdicap/knowledge-base/what-are-icap-s-server-responses-for-various-post-analysis-file-#important-implementation-guidance-for-custom-icap-clients)

- Do not rely only on the ICAP status code.
- 204 means the file is clean and no modification is needed.
- 200 means the ICAP request was processed, but the client must inspect the headers and response body.
- 200 can represent an allowed file, a sanitized or redacted file, or a blocked response.
- When CDR or DLP is enabled, the response body may contain a newly created, sanitized, or redacted file.
- The client must forward the returned file when a modified body is provided.
- The client should not discard the processed file and continue with the original file.
- For blocked files, use X-Response-Info, X-Blocked-Reason, X-Response-Desc, X-Infection-Found, and X-Violations-Found to determine the reason.

## [Example decision table for custom ICAP client logic](/docs/mdicap/knowledge-base/what-are-icap-s-server-responses-for-various-post-analysis-file-#example-decision-table-for-custom-icap-client-logic)

| ICAP code | Header/body condition | Recommended client behavior |
| --- | --- | --- |
| 204 | No modification needed | Allow original file |
| 200 | X-Response-Info: Allowed, no modified body required | Allow file |
| 200 | X-Response-Info: Allowed, modified body returned | Allow and use returned body |
| 200 | X-Response-Info: Blocked | Block file |
| 200 | X-Infection-Found or X-Violations-Found present | Block or handle according to policy |
| 4xx | Bad request, invalid ICAP request, missing headers, or similar request-side issues | Treat as integration or request error |
| 5xx | Server-side error or unavailable service | Apply fail-open or fail-closed policy |

**Key takeaway:** A custom ICAP client should never treat 200 OK alone as a clean verdict. It must parse the response headers and, when CDR or DLP is enabled, must use the returned file from the ICAP response body instead of continuing with the original file.

If **Further Assistance** is required, please proceed to log a [support case or chat with one of our support engineers](https://my.opswat.com/support).
