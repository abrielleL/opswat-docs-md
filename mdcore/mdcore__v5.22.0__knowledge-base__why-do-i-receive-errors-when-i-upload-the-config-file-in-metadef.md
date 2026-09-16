<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/why-do-i-receive-errors-when-i-upload-the-config-file-in-metadef -->

# Why do I receive errors when I upload the Config file in MetaDefender Core?

**Summary**

Uploading a Configuration File in MetaDefender Core (MD Core) may result in errors if there are mismatches between versions or platforms, or if file paths do not align with the current environment. This article outlines common causes and provides steps for resolution.

**Issue**

Users may encounter errors when attempting to upload a Configuration File to MD Core. Usually, the most common error message is related to an invalid pickupfolder path.

**Cause**

There are several potential reasons for these upload errors:

1. **Version Mismatch:** The Configuration File may not be compatible across different versions of MD Core. Changes in core functionality and configuration structure between versions can prevent successful file import.
2. **Platform Mismatch:** Configuration Files generated on one platform (e.g., Windows) may not be compatible with another (e.g., Linux). Attempting to upload a configuration from a Windows instance to a Linux-based MD Core can lead to incompatibility errors.
3. **Incorrect File Paths:** One of the most frequent errors involves the pickupfolder path. This error typically occurs when the path in the Configuration File does not match the installation directory of the target MD Core system.

**Resolution**

1. **Ensure Version Compatibility:**

- Confirm that both the source and target MD Core instances are running the same version.
- If upgrading/downgrading the Configuration File manually, review version-specific documentation to adjust settings accordingly.

2. **Match Platforms:**

- Only use Configuration Files on MD Core instances with the same underlying operating system (e.g., Linux-to-Linux, Windows-to-Windows).
- Avoid cross-platform transfers to prevent compatibility issues.

3. **Correct the Pickupfolder Paths:**

- Open the Configuration File in a text editor.
- Locate the pickupfolder entry.
- Update the path to reflect the actual directory used by your MD Core installation.

  - Example: Change e:\MD Core\pickup to C:\Program Files\MD

**Additional Notes**

- Always back up your current configuration before making any modifications.
- Use caution when editing configuration files manually to avoid syntax errors or misconfigurations.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
