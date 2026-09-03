<!-- source: https://www.opswat.com/docs/cm/product-management/operating-system-for-windows-only -->

# Operating System for Windows Only

My OPSWAT Central Management enables administrators to conduct checks on Windows devices, ensuring they maintain up-to-date operating system versions and its updates.

## Monitoring device without an approved operating system version

Administrators can configure My OPSWAT Central Management policy to verify if device runs an "approved" specific version of the operating system.

To set this up, administrators need to:

- Navigate to **Policies > Endpoint Security > Select Policy > Deep Compliance > Operating System**
- Check off **Device is not running an approved operating system version**.
- The operating system conditional will appear. **There must be at least one condition for the policy to save with this requirement enabled.**
- Using this condition to set the scope of the approved release version(s). Release versions might be defined differently than the OS name. For example, release version of Windows 7 is **6.1**, and release version of macOS High Sierra is 10.12. Please find release information from the vendor website or contact the OS vendor directly to find that information.
  - For Windows, Administrators are able to add more advanced customization to their conditional by using the (+) . This allows the administrator to filter by edition and exclude specific builds.
- **Save** the policy when all changes are completed.

> **Warning**
>
> Please be aware that My OPSWAT Central Management prioritizes approved versions in sequential order. If a device satisfies one of the listed conditions, it will be recognized as an approved version, and subsequent conditions will not be evaluated.

Detected operating system is not supported by manufacturer (EOL)

This setting will notify administrators of an operating system that is at end-of-life (EOL) deemed by the manufacturer. Ex: Windows XP and Windows Vista are versions of Windows that are no longer supported by Microsoft. They are labeled as EOL.  If enabled, My OPSWAT Central Management will consider an EOL device as an issue.

## Update(s) have been available for X day(s) or more

My OPSWAT Central Management will check client device's current Windows version and will compare it to versions that are available for updating from Microsoft. If there are updates that are available for the device and have been available past the threshold set, My OPSWAT Central Management will consider this to be an issue.

This will let end users know it is time to run Windows Update to retrieve the latest update.

> **Example**
>
> With a precondition, the device runs Windows 11 22H2 with OS build 22621.2134, which can be verified in 'System > About'. It should be associated with a policy set to flag issues when updates have been available for 14 days or more."
>
> **How My OPSWAT Central Management Process to Determine OS Update Issue:**
>
> 1. Checking the Next Recent Build: My OPSWAT Central Management begins by referencing the Windows release history provided by Microsoft for Windows 11. It checks for the next-recent build based on the device's current build. For example, if the device is on OS build 22621.2134, the next-recent build might be 22621.2215, released on 2023-08-22.
> 2. Date Comparison: My OPSWAT Central Management then compares the current date (e.g., 2023-09-20) to the available date (e.g., 2023-08-22) to determine if it exceeds the configured policy period (e.g., 14 days).
> 3. Exceeding Policy Period: In this case, the current date exceeds the configured period (14 days). If this condition is not met, the device is considered good. Otherwise, My OPSWAT Central Management proceeds to further checks.
> 4. Check for Compliant Builds: Based on the policy configuration (14 days) and Windows release history, My OPSWAT Central Management identifies compliant builds (e.g., 22621.2283 or 22621.2215).
> 5. Check for Available Builds: My OPSWAT Central Management checks if the available OS patches reported by the Windows Update Agent match any of the compliant builds. If the device has any of these builds available for installation but not yet installed, My OPSWAT Central Management flags the device as having an issue with OS Update (indicating that it can be updated to a compliant build, but the end-user has not installed it).

## Device has not been rebooted in over X day(s)

My OPSWAT Central Management will check to see the last time the client device was rebooted. If it surpasses this threshold, My OPSWAT Central Management will consider it an issue.
