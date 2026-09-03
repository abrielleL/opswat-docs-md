<!-- source: https://www.opswat.com/docs/my/faqs/how-to-submit-files-larger-than-2gb-for-false-positive-analysis- -->

# How to Submit Files Larger Than 2GB for False Positive Analysis?

> **Check Your Version:**
>
> This article applies to all OPSWAT product releases deployed on Windows and Linux systems.

**Issue:** My OPSWAT Portal enforces a 2GB maximum file size for False Detection Reports (FDRs), which prevents customers from submitting larger files (e.g., 9.5GB ISOs) for analysis through the standard portal.

**Resolution:** Customers have two main options for submitting files larger than 2GB for false positive analysis:

**Option 1: Submit Only the Relevant Suspicious Files (Recommended)**

- Extract the specific file(s) flagged as false positives.
- Verify each extracted file is under 2GB.
- Submit these through the standard [False Detection Report portal](https://my.opswat.com/portal/report-false-detection/submit).

**Option 2: Request Manual Processing via Support Case**

- Submit the FDR form as usual.
- After submitting the form, a support case will be automatically created.
- Click the Case No. to access case details
- Upload the complete large file under “Files & CC’s” tab **OR** share a downloadable link in the Comment box.
- Clearly note "File exceeds 2GB limit - requesting manual FDS2 analysis".
- Include detection details (engine name, hash, scan results).

**Workarounds:**

- Split archives using tools like 7-Zip or WinRAR if upload fails at 2GB.

**Prevention:**

- Always check file size before submission.
- Do not upload infected files or any files suspected of containing malware when submitting support cases.
- For ISOs/containers: Extract only the flagged components.
- Include supplemental data: File hashes (SHA-256/MD5), Context about the file's purpose and safety.
- Compress when possible: Use ZIP/7z for smaller uploads.

> **Support:**
>
> If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
