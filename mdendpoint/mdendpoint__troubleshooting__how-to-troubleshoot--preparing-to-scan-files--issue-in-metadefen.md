<!-- source: https://www.opswat.com/docs/mdendpoint/troubleshooting/how-to-troubleshoot--preparing-to-scan-files--issue-in-metadefen -->

# How to Troubleshoot "Preparing to Scan Files" Issue in MetaDefender Endpoint?

> **Check Your Version:**
>
> This article applies to all MetaDefender Endpoint releases deployed on Windows , Linux and Mac systems.

An endpoint running MetaDefender Endpoint remains stuck at the **"Preparing to scan files"** stage. The following symptoms were observed:

- A large number of files including OS-level system files are being scanned.
- Many files (e.g., pagefile.sys, swap files) return "access denied" or "can't access this file" errors.
- The malware scan logs contain numerous errors and unusual data entries.
- The configured MetaDefender MetaDefender Core appears to be unreachable or invalid.
- There is confusion about the scan type (e.g., full system, memory scan, removable media).
- It is unclear whether MetaDefender Endpoint has sufficient privileges or if files are being correctly routed through the MetaDefender Core workflow.

### **Root Cause:**

The issue appears to be caused by a combination of:

- Insufficient permissions for the MetaDefender Endpoint agent, preventing it from accessing protected system files.
- Connectivity issues between the endpoint and the MetaDefender MetaDefender Core server, resulting in failure to submit or process scan jobs.
- Excessive scan scope, including unnecessary system files, which delays scan initialization and increases error rates.

### **Resolution Steps:**

Follow these steps to troubleshoot and resolve the issue:

1. **Verify the Scan Type**
   - Confirm whether the scan is a full system scan, memory scan, or targeted scan (e.g., USB, ISO).
   - Reduce the scan scope if full system or memory scans are not required, especially on production machines.
2. **Run MetaDefender Endpoint with Administrative Privileges**
   - Ensure MetaDefender Endpoint is installed and executed with administrator rights.
   - Reinstall MetaDefender Endpoint if necessary, making sure to run the installer as an administrator.
3. **Check MetaDefender Core Server Connectivity**
   - Confirm the MetaDefender MetaDefender Core server URL is correct and accessible:
     - Open a web browser on the affected endpoint.
     - Navigate to the MetaDefender Core UI using the URL.
     - If unreachable, check firewall rules, DNS, routing, or replace with a reachable MetaDefender Core instance.
4. **Validate File Processing via MetaDefender Core UI**
   - Log in to the MetaDefender Core console and manually upload a sample file.
   - Confirm that the file is scanned successfully to validate MetaDefender Core processing functionality.
5. **Review MetaDefender Core Workflow Configuration**
   - In OPSWAT Central Management (OCM), go to the Endpoint section.
   - Check if the default “File Scan” workflow or a custom workflow is assigned.
   - Ensure the workflow includes appropriate steps for file scanning and returning results.
6. **Exclude Unnecessary System Files (Windows Only)**
   - Update scan policy to exclude OS-critical files such as:
     - `C:\pagefile.sys`
     - `C:\hiberfil.sys`
     - Swap files, system restore points, etc.
   - This can significantly reduce scan time and avoid permission errors.
7. **Review Logs for Additional Errors**
   - Review logs on both the endpoint and the MetaDefender MetaDefender Core server.
   - Look for:
     - File access errors
     - Timeout messages
     - Workflow or policy misconfigurations

### **Additional Recommendation:**

If the issue persists after performing the above checks, consider updating the MetaDefender Endpoint and MetaDefender Core versions to the latest releases, as performance improvements and bug fixes may resolve similar issues.

> **Support:**
>
> If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
