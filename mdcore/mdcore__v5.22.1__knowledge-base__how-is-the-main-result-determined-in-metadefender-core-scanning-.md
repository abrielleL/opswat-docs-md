<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/how-is-the-main-result-determined-in-metadefender-core-scanning- -->

# How is the Main Result Determined in MetaDefender Core Scanning?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**Check Your Version:**

This article applies to all MetaDefender Core releases deployed on Windows and Linux systems.

MetaDefender Core scanning involves multiple sequential checks to determine the security status of a file.

Each step in the process contributes to the final decision, but the **main result** displayed is based on the earliest decisive action in the scanning flow.

## [**Scanning Flow**](/docs/mdcore/v5.22.1/knowledge-base/how-is-the-main-result-determined-in-metadefender-core-scanning-#scanning-flow)

The scanning process follows this order:

1. **Archive Extraction**
2. **File Type Analysis**
3. **Blocklist / Allowlist Check**
4. **Country of Origin**
5. **Reputation**
6. **Cloud Hash Lookup**
7. **Vulnerability Assessment**
8. **YARA Rules**
9. **Metascan (+ External Scan)**
10. **Proactive DLP**
11. **Deep CDR (Content Disarm & Reconstruction)**
12. **Adaptive Sandbox**
13. **Software Bill of Materials**
14. **Post Action**

## [**Main Result Logic**](/docs/mdcore/v5.22.1/knowledge-base/how-is-the-main-result-determined-in-metadefender-core-scanning-#main-result-logic)

If a file is blocked for multiple reasons during the scanning process, the **main result** will reflect the **highest-priority decisive reason** based on the scanning flow.

For example:

- If a file is:

  - **Known Bad** (due to **Reputation**),
  - flagged as **Potentially Vulnerable** (by **Vulnerability Assessment**),
  - and **infected** (detected by **Metascan**),

  The **main result** will display **Known Bad**, because **Reputation** is evaluated earlier in the flow and takes precedence.
- Other block reasons (e.g., Vulnerability Assessment, Metascan infection) will **not appear in the main result** but can be viewed by clicking the **three dots (…)** in the scan report for detailed information.

**Support:**

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
