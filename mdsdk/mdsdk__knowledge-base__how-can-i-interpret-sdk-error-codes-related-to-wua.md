<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/how-can-i-interpret-sdk-error-codes-related-to-wua -->

# How can I interpret SDK error codes related to Windows Update Agent?

`GetMissingPatches`, `InstallMissingPatches` and `GetInstalledPatches` do not rely on the `wuo.dat` file. Therefore, the presence or absence of `wuo.dat` does not impact their results.

## [**Overview**](/docs/mdsdk/knowledge-base/how-can-i-interpret-sdk-error-codes-related-to-wua#overview)

When using the Windows Update Agent (WUA) to execute `GetMissingPatches`, `GetInstalledPatches`, or `InstallMissingPatches`, it can be challenging to determine the cause of failure if these operations do not succeed. This article explains how to interpret the behavior and return codes of these methods.

## [Understanding the Interaction Between Windows Update Agent and SDK](/docs/mdsdk/knowledge-base/how-can-i-interpret-sdk-error-codes-related-to-wua#understanding-the-interaction-between-windows-update-agent-and-sdk)

The `GetMissingPatches`, `GetInstalledPatches`, and `InstallMissingPatches` methods act as wrappers around native Windows Update operations and are primarily used in compliance verification workflows. When a patch is passed to one of these methods, the system follows the standard behavior defined by Microsoft Windows Update.

To function correctly, the following conditions must be met:

- Windows Update must be **enabled** and **allowed by system policy**
- The Windows Update service **must be running.**
- Internet connectivity **must be available**.

The table below outlines common failure scenarios and their corresponding error codes:

| Code | **Description** |
| --- | --- |
| -24 (`WAAPI_ERROR_NOT_RUNNING`) | The Windows Update service is not running. |
| -17 (`WAAPI_ERROR_NO_CONNECTION`) | Unable to reach the Windows Update service. |
| -22 (`WAAPI_ERROR_ACCESS_DENIED`) | Insufficient permissions to access required Windows resources. |
| -25 (`WAAPI_ERROR_COM`) | Failure in API communication. |

If the Windows Update Agent is configured correctly, the following conditions may still lead to different behavior:

- Windows Update service startup type is set to **Disabled**: Returns error code **-24** (`WAAPI_ERROR_NOT_RUNNING`).
- No internet connection available: Returns error code **-17** (`WAAPI_ERROR_NO_CONNECTION`).
- Windows Update service is set to `Manual`**,** `Automatic`**,** `Boot`**,** or `System`, and internet connection is available: Returns the list of missing patches successfully.

Support

If further assistance is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
