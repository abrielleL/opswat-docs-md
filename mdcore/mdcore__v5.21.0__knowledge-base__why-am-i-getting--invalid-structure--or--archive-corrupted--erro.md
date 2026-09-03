<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/why-am-i-getting--invalid-structure--or--archive-corrupted--erro -->

# Why am I getting "invalid structure" or "archive corrupted" errors when extracting archives in Core?

This article is applied to Core releases deployed on Windows and Linux systems.

**Issue:** Core encounters errors such as "invalid structure" or "archive corrupted" during archive extraction.

**Resolution:** The issue might stem from the archive file itself being corrupted, rather than a problem with Core's extraction engine. To verify this, follow the steps below.

**Steps to Diagnose:**

- Test the archive using the standalone 7Zip application on a Windows system.
- Attempt to extract the archive using 7Zip.
- If 7Zip also fails to extract the file and reports similar errors, the archive is likely corrupted.

**Example of 7Zip extraction issue message:**

**Conclusion:** If 7Zip reports errors, the problem lies within the archive file and not with Core. You will need to obtain a valid, uncorrupted archive.

Support:

If 7Zip reports errors, the problem lies within the archive file and not with Core. You will need to obtain a valid, uncorrupted archive.
