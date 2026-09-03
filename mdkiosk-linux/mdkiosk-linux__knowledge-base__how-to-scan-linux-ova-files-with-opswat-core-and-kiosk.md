<!-- source: https://www.opswat.com/docs/mdkiosk-linux/knowledge-base/how-to-scan-linux-ova-files-with-opswat-core-and-kiosk -->

# How to Scan Linux OVA Files with OPSWAT Core and Kiosk

**Summary**

A user attempted to scan a Linux VM .ova file using OPSWAT Core and Kiosk but received an error indicating that the file could not be processed. This case aims to clarify whether Linux-based .ova VM template files are supported for scanning and what steps should be taken to resolve the issue.

**Issue**

The user is trying to scan a Linux VM .ova file (for VMware) via OPSWAT Core and Kiosk. Both systems return an error stating they cannot process the file. The question is whether Linux-based .ova templates are supported for scanning and, if so, why this error is occurring.

**Resolution**

According to the release notes for the File Type Engine version v7.3.1, .ova files are supported. OPSWAT Support has recommended the following steps to troubleshoot and resolve the issue:

✔️ **Key Points:**

- ✅ **File Type Engine Version:** Ensure the engine on the Core machine is updated to version **7.3.1** or higher.
- ✅ **Supported Format:** .ova files are supported as of the latest engine release.
- ✅ **Diagnostic Request:** Provide the specific scan result or error message for analysis.
- ✅ **Customer Context:** Share the name of the end customer for internal tracking.
- ✅ **Re-Scan Suggested:** After verifying the engine version, attempt to scan the file again and report if the issue persists.

**Example Scenario**

- Attempted scan: Linux .ova file using OPSWAT Core and Kiosk
- Error: File cannot be processed
- File Type Engine version: Unknown (needs confirmation)
- Expected behavior: .ova file should scan successfully under version **7.3.1**

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
