<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/why-are-pdf-documents-being-flagged-as-false-positives-by-virusb -->

# Why are PDF documents being flagged as false positives by VirusBlokAda?

View as Markdown Ask ChatGPT about this page Ask Claude about this page
#### [Issue:](/docs/mdcore/v5.22.1/knowledge-base/why-are-pdf-documents-being-flagged-as-false-positives-by-virusb#issue)

PDF files, including official letters or documents with standard formatting, are sometimes flagged as suspicious by the VirusBlokAda engine

#### [Cause:](/docs/mdcore/v5.22.1/knowledge-base/why-are-pdf-documents-being-flagged-as-false-positives-by-virusb#cause)

The issue is often related to the **Heuristic Scan** feature, which can mistakenly classify normal PDF structures as threats. **Resolution / Workaround:**

1. Verify that the flagged PDF is from a trusted source.
2. If confirmed safe, adjust the VirusBlokAda settings:

- Disable **Heuristic Scan**, or
- Set **Heuristic Scan Level** to **Level 1** to reduce unwanted detections.

**Note**: Disabling or lowering heuristic scanning may reduce detection sensitivity, so only adjust this setting if false positives are persistent.

Support:

If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
