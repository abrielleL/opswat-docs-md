<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/understanding-force-install-input-in-installfromfile -->

# Understanding the force_install input in the InstallFromFile method

### [Overview](/docs/mdsdk/knowledge-base/understanding-force-install-input-in-installfromfile#overview)

`force_install` | **Type:** boolean | **Platform:** Windows only | **Optional:** True

The `force_install` option tells the SDK to **preprocess and install the product even if the installer does not comply with certain Windows security mechanisms**.

- When `force_install = false` (default): The SDK validates the installer against Windows security mechanisms. If any issues are detected, **the installation fails with an error**, and no action is applied.
- When `force_install = true`: The SDK attempts to **bypass two Windows security mechanisms** by preprocessing the installer: **Mark of the Web (MOTW)** and **low integrity level**. Use this option **only if you fully trust the installer** and accept that the SDK may modify it during preprocessing.

| Installation status | SDK's modification |
| --- | --- |
| MOTW | Remove this hidden security tag |
| Low integrity level | Increase to medium level |

Note

The `force_install` function only bypasses Windows security mechanisms (MOTW and integrity level). It does not impact other SDK validations, such as digital signature checks and hash checks, etc.

### [Windows Security Mechanisms Involved](/docs/mdsdk/knowledge-base/understanding-force-install-input-in-installfromfile#windows-security-mechanisms-involved)

#### [Mark of the Web (MOTW)](/docs/mdsdk/knowledge-base/understanding-force-install-input-in-installfromfile#mark-of-the-web-motw)

- MOTW is a hidden security tag added to files downloaded from the internet.
- It indicates an **untrusted origin**, causing Windows to:

  - Show warnings (e.g., Protected View in Microsoft Office)
  - Trigger SmartScreen prompts for executables
- This helps prevent automatic execution of potentially malicious files.
- In some cases, attackers may attempt to bypass MOTW by using specific file types (e.g., compressed archives).

**References**

- <https://support.microsoft.com/en-us/windows/download-files-from-the-web-abb92c09-af3a-bd99-d279-a89848b54b0b>
- <https://windowsforum.com/threads/windows-11-preview-pane-now-blocks-internet-marked-files-motw.386415/>

**How to simulate a MOTW file**

Download the installer directly from the internet (browser) or use PowerShell:

PowershellCopySet-Content -Path '.\filename.ext' -Stream Zone.Identifier -Value '[ZoneTransfer]','ZoneId=3'
#### [Integrity Level (Windows Mandatory Integrity Control)](/docs/mdsdk/knowledge-base/understanding-force-install-input-in-installfromfile#integrity-level-windows-mandatory-integrity-control)

- Every process and many objects (files, registry keys, etc.) in Windows have an integrity level, such as:

  - Low
  - Medium (default for standard users)
  - High (typical for administrators)
  - System
- A lower‑integrity process cannot modify higher‑integrity objects.
- This prevents untrusted or low‑privileged processes from changing critical files or system resources.
- You can view or modify integrity levels using tools like:

  - Process Explorer (procexp)
  - The icacls command

Both MOTW and low integrity level are designed to mitigate risks from untrusted files and protect the system from potentially malicious installers.

**References**

- <https://learn.microsoft.com/en-us/windows/win32/secauthz/mandatory-integrity-control>
- <https://learn.microsoft.com/en-us/windows/security/book/application-security-application-isolation>

**How to simulate low integrity level**

Using `icacls`:

BashCopyicacls "path\to\your\file" /setintegritylevel L
### [Use Cases and Error Scenarios](/docs/mdsdk/knowledge-base/understanding-force-install-input-in-installfromfile#use-cases-and-error-scenarios)

#### [When `force_install = false`](/docs/mdsdk/knowledge-base/understanding-force-install-input-in-installfromfile#when-force_install--false)

In this mode, the SDK strictly enforces Windows security mechanisms. If the installer violates certain conditions, the SDK fails with one of the following errors, and **no preprocessing or installation is performed**:

| Error | Description |
| --- | --- |
| `WAAPI_ERROR_FILE_MARKED_MOTW` | The installer file is marked with **Mark of the Web (MOTW)**, indicating it originates from an untrusted source. |
| `WAAPI_ERROR_LOW_INTEGRITY_LEVEL` | The installer has a **low integrity level**, which is considered unsafe for installation. |

#### [When `force_install = true`](/docs/mdsdk/knowledge-base/understanding-force-install-input-in-installfromfile#when-force_install--true)

When `force_install` is enabled, the SDK attempts to preprocess the installer to make it acceptable for installation, even if Windows security mechanisms would normally block it.

During preprocessing, the SDK tries to:

- Remove the Mark of the Web (MOTW) from the installer.
- Increase the integrity level of the installer if it is too low.

If the SDK fails to complete these preprocessing steps, it returns the following error, and the installation **does not proceed**:

| Error | Description |
| --- | --- |
| `WAAPI_ERROR_FAILED_TO_PREPROCESS_INSTALLER` | The SDK encountered an error during preprocessing, such as:   - Failed to remove MOTW - Failed to change the integrity level |
