<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/windefend-service-prerequisite-for-patching-windows-defender -->

# WinDefend Service Prerequisite for Patching Microsoft Defender Antivirus

This article applies to OESIS Framework version **4.3.6077.0** and later releases on **Windows** with **Microsoft Defender Antivirus** Integration.

## [Overview](/docs/mdsdk/knowledge-base/windefend-service-prerequisite-for-patching-windows-defender#overview)

A prerequisite for OESIS Framework patching Microsoft Defender Antivirus (referred as Windows Defender, signature **477**) is that its service (`WinDefend`) is running. When invoking `InstallFromFiles` (method **50301**), our SDK validates the service state and, if necessary, attempts to start it automatically **before** performing the installation.

This article describes that validation behavior, including the checks our SDK performs, the conditions it evaluates, and the error codes it may return if patching cannot proceed.

## [Microsoft Defender Antivirus Operating Modes](/docs/mdsdk/knowledge-base/windefend-service-prerequisite-for-patching-windows-defender#microsoft-defender-antivirus-operating-modes)

Microsoft Defender Antivirus operates in one of three modes. The current mode determines whether Windows Defender patching can be applied:

| Mode | Description | Patching Supported? |
| --- | --- | --- |
| **Active** | Windows Defender is the primary antivirus on the device. All protection features are running normally. | ✅ Yes |
| **Passive** | Another third-party antivirus is installed and active. Windows Defender runs in a reduced-functionality compatibility mode, but its service remains running. | ✅ Yes |
| **Disabled** | Defender has been turned off, either by a third-party antivirus, by Group Policy, or by MDM/Intune configuration. `WinDefend` service is not running. | ❌ No |

Key takeaway

Patching requires the `WinDefend` service to be **running**. Both Active and Passive modes satisfy this requirement. Disabled mode does not.

## [How the SDK Validates Readiness](/docs/mdsdk/knowledge-base/windefend-service-prerequisite-for-patching-windows-defender#how-the-sdk-validates-readiness)

Before installing any Windows Defender patch, OESIS Framework executes the following prerequisite validation:

1. Confirms the calling process has **administrator (elevated) rights**. If not → return `WAAPI_ERROR_ACCESS_DENIED`.
2. Detects whether **another antivirus supersedes Defender**. If Defender is superseded and cannot operate → return `WAAPI_ERROR_PRODUCT_SUPERSEDED_BY_ANOTHER_PRODUCT`.
3. Reads policy (e.g., via Group Policy or MDM) and service configuration to determine if **WinDefend can start**. If not → return `WAAPI_ERROR_PRODUCT_DISABLED`.
4. **Final service start** before patching: If WinDefend fails to start for another reason → return `WAAPI_ERROR_FAILED_TO_START_SERVICE`.

If all checks pass, the SDK proceeds with loading the patch database and applying updates.

## [Prerequisite Error Codes Reference](/docs/mdsdk/knowledge-base/windefend-service-prerequisite-for-patching-windows-defender#prerequisite-error-codes-reference)

When a prerequisite check fails, our SDK returns one of the following error codes:

### [**WAAPI_ERROR_ACCESS_DENIED** *(code -22)*](/docs/mdsdk/knowledge-base/windefend-service-prerequisite-for-patching-windows-defender#waapi_error_access_denied-code--22)

**Meaning**

The SDK is not running in an elevated (administrator) session. Windows requires elevated privileges to query and control the `WinDefend` service and update Microsoft Defender Antivirus.

**Common Cause**

The host application launched the SDK process without requesting administrator rights.

**Resolution**

Ensure the integrating application runs with administrator or elevated privileges.

### [**WAAPI_ERROR_PRODUCT_SUPERSEDED_BY_ANOTHER_PRODUCT** *(code -98)*](/docs/mdsdk/knowledge-base/windefend-service-prerequisite-for-patching-windows-defender#waapi_error_product_superseded_by_another_product-code--98)

**Meaning**

Another active antivirus product has been detected on the device and has fully superseded Microsoft Defender, preventing it from running even in Passive mode.

**Common Cause**

A third-party antivirus application is installed and configured in a way that completely disables Defender rather than allowing it to coexist.

**Resolution**

Either uninstall the third-party antivirus, or configure it to allow Microsoft Defender to run alongside it in Passive mode. Refer to the third-party vendor's documentation for coexistence settings.

### [**WAAPI_ERROR_PRODUCT_DISABLED** *(code -97)*](/docs/mdsdk/knowledge-base/windefend-service-prerequisite-for-patching-windows-defender#waapi_error_product_disabled-code--97)

**Meaning**

Microsoft Defender Antivirus is disabled at the system level. The `WinDefend` service startup type is set to Disabled and cannot be changed by the SDK.

**Common Cause**

A Group Policy Object (GPO), MDM/Intune policy, or the `DisableAntiSpyware` registry value has explicitly disabled Defender.

**Resolution**

Review and adjust the applicable policy: check Group Policy, MDM/Intune endpoint protection profiles, or the registry key `HKLM\SOFTWARE\Policies\Microsoft\Windows Defender\DisableAntiSpyware`.

### [**WAAPI_ERROR_FAILED_TO_START_SERVICE** *(code -99)*](/docs/mdsdk/knowledge-base/windefend-service-prerequisite-for-patching-windows-defender#waapi_error_failed_to_start_service-code--99)

**Meaning**

The SDK attempted to start the `WinDefend` service but the operation failed for an undetermined reason.

**Common Cause**

Service dependencies are missing, the service binary is corrupted, or another system-level condition is preventing the service from starting.

**Resolution**

Inspect the Windows Event Log for related error entries. Consider enable OESIS debug logging and contact the OESIS support team for further analysis.

## [Additional Resources](/docs/mdsdk/knowledge-base/windefend-service-prerequisite-for-patching-windows-defender#additional-resources)

- [**Microsoft: Troubleshoot Microsoft Defender Antivirus settings**](https://learn.microsoft.com/en-us/defender-endpoint/troubleshoot-settings)
- [**Microsoft: Microsoft Defender Antivirus compatibility with other security products**](https://learn.microsoft.com/en-us/defender-endpoint/microsoft-defender-antivirus-compatibility)
- [**Microsoft: Use Group Policy to manage Microsoft Defender Antivirus**](https://learn.microsoft.com/en-us/defender-endpoint/use-group-policy-microsoft-defender-antivirus)

Support

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
