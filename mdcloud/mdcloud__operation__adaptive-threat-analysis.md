<!-- source: https://www.opswat.com/docs/mdcloud/operation/adaptive-threat-analysis -->

# Sandbox (Adaptive Threat Analysis)

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

Adaptive Sandbox runs files and URLs in an isolated environment and reports what they do: processes started, files written, network connections, registry changes, and indicators of compromise. Use it when signature-based detection is not enough, for example for new or targeted threats.

**Requesting sandbox analysis**

- **From the website.** Select **Adaptive Sandbox** under Custom Scan on the Analyze page, or use a workflow that includes it.
- **From the API.** Send the `sandbox` header with `POST /v4/file`. Any non-empty value other than `false` or `0` requests analysis; `true` or `1` is recommended. Sending `false` or `0` is an explicit opt-out: no sandbox analysis runs, no Sandbox unit is consumed, and the result contains no sandbox section, even when the workflow would otherwise enable the sandbox. The values `windows7` and `windows10` are still accepted for compatibility; they do not select an environment, because Adaptive Sandbox chooses the analysis environment itself.

**Limits and consumption**

- Each file analysed consumes one unit of your Sandbox limit. Within an extracted archive, each extracted file sent to the sandbox consumes one unit as its analysis completes. A request refused with a 4xx error consumes nothing.
- Files above the sandbox file-size limit are not analysed by the sandbox; the rest of the workflow still runs. TO VERIFY (Product): the limit per plan.
- The Aether workflow includes Adaptive Sandbox and consumes one Sandbox unit per file.

**Reading the results**

- Results arrive in stages. Multiscanning, Deep CDR and DLP verdicts are returned as soon as those engines finish; the sandbox section is added when the analysis completes and the overall verdict is recalculated. Progress only moves forward.
- The sandbox verdict is one of No Malicious Behavior, Suspicious (code 26), Likely Malicious (27) or Malicious (28), or Unknown when the analysis was inconclusive. Only Malicious counts as a blocking verdict in the overall result.
- An analysis that could not finish is reported as Aborted with the reason.
- The full report is linked from the result (`sandbox_results.store_at` and `sandbox_results.full_report`). Each link is valid for one day from the moment it is handed out. When you read a result whose link has expired, a new link is issued, so the links can differ between two reads of the same scan. If the report file is no longer stored, the link is omitted.
- Hash lookups return a sandbox summary in `sandbox_scan_details`. For paid accounts, lookups check your private results first and fall back to public data.

**Privacy.** Sandbox results follow your private processing setting: with private processing, only the API key that submitted the file can read its sandbox results.
