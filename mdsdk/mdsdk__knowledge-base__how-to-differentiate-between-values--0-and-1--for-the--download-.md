<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/how-to-differentiate-between-values--0-and-1--for-the--download- -->

# How to differentiate between values (0 and 1) for the "download" Parameter in the "GetLatestInstaller" Method?

The OPSWAT SDK includes patching capabilities to help ensure third-party applications remain secure and up to date. This document explains the two supported patching methods provided by the SDK, enabling developers and integrators to choose the approach that best fits their environment and update workflow.

## [Patching Methods](/docs/mdsdk/knowledge-base/how-to-differentiate-between-values--0-and-1--for-the--download-#patching-methods)

The patching functionality in the OPSWAT SDK is controlled by the `download` parameter, which determines how update packages are handled.

### [1. `download=0` – Link Only Mode](/docs/mdsdk/knowledge-base/how-to-differentiate-between-values--0-and-1--for-the--download-#1-download0--link-only-mode)

This mode returns the download URL for the installer but does **not** download the file itself.

- **Use Case**: When you want to manually handle the installer download or store the link for later use.
- **Note**: This mode is **not supported for Microsoft Office products**. Attempting to use `download=0` with Office will result in an error response.

*Result returned for non-MS Office product with download=0*

*Error returned for MS Office product with download=0*

### [2. `download=1` – Full Download Mode](/docs/mdsdk/knowledge-base/how-to-differentiate-between-values--0-and-1--for-the--download-#2-download1--full-download-mode)

This mode fully retrieves the installer by downloading it along with any necessary update information.

- **Use Case**: Recommended for most third-party applications where automatic downloading is required.
- **Note**: This mode **is supported** for Microsoft Office products.

By understanding these patching mechanisms, users can efficiently manage third-party application updates through the OPSWAT SDK depending on their usage requirements.
